# **Architecture Decision Records (ADR) v4.0**

📂 Location: docs/adr/

📌 Status: Accepted set for MVP v4.0 (Data-led, Agent-ready)

📅 Date: September 2025

---

## **ADR-001: Database Support Matrix (15/16 Supported; 13/14 Best-Effort Demo Only)**

- **Status:** Accepted
- **Context:** We need predictable behavior across data platforms while minimizing test complexity and maintaining clear support boundaries.
- **Decision:**
  - **Fully support:** Postgres 15/16 (all cloud variants: RDS, Aurora, Azure Database, GCP Cloud SQL).
  - **Demo/pilot only:** Postgres 13/14 ("best-effort"): smoke tests, documented gaps, not production-supported.
  - **Data warehouse anchoring:** Snowflake QUERY_HISTORY, Databricks Delta commits, BigQuery job metadata.
  - `clyra doctor` exits non-zero on enforcement unless `--allow-best-effort`.
- **Consequences:** Reliable performance, smaller test matrix, clear customer guidance; older clusters demo-capable but must upgrade for production.
- **15-Factor Compliance:** Backing services treated as attached resources with clear version boundaries.
- **Repo Impact:**
  - `docs/compatibility/database_matrix.md`
  - `cmd/clyra/doctor/*` version checks & exit codes
  - `internal/warehouse/anchors/*` platform-specific implementations

---

## **ADR-002: Evidence Format Architecture (DEF v0 + PEF v0 Unified)**

- **Status:** Accepted
- **Context:** Need unified evidence format supporting both data platform changes and automation/agent actions with independent verification.
- **Decision:**
  - **DEF v0** (Data Evidence Format): dbt runs, schema changes, activation syncs, warehouse operations.
  - **PEF v0** (Portable Evidence Format): automation, agents, RPA, microservices.
  - **Unified structure:** Same bundle format (`manifest.json`, `journal.jsonl`, `artifacts/`), same verifiers.
  - **Canonical JSON:** UTF-8 NFC, sorted keys, RFC3339 UTC, fixed numeric formats.
  - **Merkle roots:** Tamper-evident integrity with cryptographic hash chains.
- **Consequences:** Single verification pipeline, format portability, auditor-friendly structure.
- **15-Factor Compliance:** Build/release separation with immutable artifacts, logs as event streams.
- **Repo Impact:**
  - `spec/def/schemas/*` (data evidence format)
  - `spec/pef/schemas/*` (portable evidence format)
  - `spec/common/schemas/*` (shared structures)
  - Unified Go/TS verifiers support both formats

---

## **ADR-003: Snapshot Strategy (Metadata-Only with Warehouse Anchoring)**

- **Status:** Accepted
- **Context:** Need lineage proof without heavy data capture, compatible with customer backup strategies and warehouse-native operations.
- **Decision:**
  - **Metadata-only snapshots:** Row counts, checksums, schema fingerprints, no full data capture.
  - **Warehouse anchoring:**
    - Postgres: WAL LSN under REPEATABLE READ
    - Snowflake: QUERY_HISTORY refs, session tags
    - Databricks: Delta Lake commit versions, Unity Catalog lineage
  - **dbt integration:** Model metadata, test results, semantic delta hashes.
  - **Performance target:** ≤50ms for ≤100 tables, ≤2s for dbt hook execution.
- **Consequences:** Lightweight operations, customer RPO/RTO preserved, deterministic replay foundation.
- **15-Factor Compliance:** Processes are stateless, disposable with fast startup/shutdown.
- **Repo Impact:**
  - `spec/def/schemas/snapshot_metadata.json`
  - `internal/warehouse/anchors/*` platform implementations
  - `internal/dbt/hooks/*` model metadata capture

---

## **ADR-004: Replay Isolation (Scratch Schema + Network Deny)**

- **Status:** Accepted
- **Context:** Forensic replay must be safe, deterministic, and independently verifiable without production impact.
- **Decision:**
  - **Scratch schema isolation:** All replays in `clyra_replay_<run_id>` namespace.
  - **Network denylist:** Block RFC1918, metadata endpoints (169.254.x.x), production systems.
  - **Data replay support:** Recreate dbt runs, schema changes in isolated warehouse environments.
  - **Replay Certificate:** Signed status {success|partial|failed} with detailed failure codes.
  - **Deterministic outcomes:** ≤2× baseline performance, identical results across runs.
- **Consequences:** Safe forensics, auditable outcomes, zero production risk.
- **15-Factor Compliance:** Disposability with clean teardown, port binding for service isolation.
- **Repo Impact:**
  - `spec/common/schemas/replay_certificate.json`
  - `internal/replay/isolation.go` network controls
  - `internal/replay/data/*` warehouse replay engines

---

## **ADR-005: Enhanced Enforcement Primitives (BEC-Grade Security)**

- **Status:** Accepted
- **Context:** GenAI security threats (deepfakes, BEC, prompt injection) require advanced enforcement beyond basic validation.
- **Decision:**
  - **BEC-grade approval certificates:** SSO binding (`approver_sso_sub`, `idp_domain`, `challenge_nonce`), payload hash binding (RFC 8785).
  - **Idempotency keys:** HMAC fingerprints, TTL-bound, tenant-scoped, single-use default.
  - **Velocity guards:** Sliding window rate limits, per-actor/tenant/route, burst protection.
  - **Tenant fences:** Cross-tenant write prevention, DSN hash namespacing, header consistency.
  - **SQL safety:** Advisory blocks on mass UPDATE/DELETE, rows_affected limits, allowlist exceptions.
  - **Prompt delta tracking:** Sanitized hash changes for injection drift detection.
- **Consequences:** Comprehensive GenAI threat protection, enterprise-grade access control.
- **15-Factor Compliance:** Config-driven enforcement, authentication with identity binding.
- **Repo Impact:**
  - `spec/common/schemas/bec_approval_cert.json`
  - `internal/enforcement/primitives/*`
  - `internal/genai/security/*` threat detection

---

## **ADR-006: Data Platform Integration Architecture**

- **Status:** Accepted
- **Context:** Need deep dbt/warehouse integration for data-led market entry while maintaining universal automation support.
- **Decision:**
  - **dbt hooks:** `on_run_start`/`on_run_end` with DEF bundle emission, CI gate integration.
  - **SQL safety macros:** `clyra_guard.merge_with_cert()`, approval token validation.
  - **Warehouse-native guards:**
    - Snowflake: Session tags, stored procedures, QUERY_HISTORY anchoring
    - Databricks: Delta commits, Unity Catalog integration, macro helpers
  - **Activation gateway:** HTTP proxy for reverse-ETL with full enforcement primitives.
  - **CI/CD integration:** GitHub Actions, policy violation blocking, evidence verification.
- **Consequences:** Natural data team workflow integration, minimal friction adoption.
- **15-Factor Compliance:** API-first design, config externalization, telemetry integration.
- **Repo Impact:**
  - `sdk/python/dbt/*` hooks and macros
  - `internal/warehouse/guards/*` platform-specific implementations
  - `internal/activation/gateway.go` reverse-ETL proxy

---

## **ADR-007: GenAI Security Framework (Threat Detection + Response)**

- **Status:** Accepted
- **Context:** 62% of organizations hit by deepfake attacks, 32% by prompt injection - need comprehensive GenAI security layer.
- **Decision:**
  - **Built-in detectors:** Prompt injection heuristics (regex/JSONPath), reflex/loop detection.
  - **External detector integration:** Vendor-agnostic HTTP API for deepfake/BEC services.
  - **Shadow mode default:** New detectors start logging-only to avoid false positive disruption.
  - **Kill-switch enhancement:** Multi-trigger (prompt injection spikes, deepfake campaigns, error bursts).
  - **Threat classification:** OWASP LLM codes + MITRE ATT&CK mapping where applicable.
  - **Voice/conversation support:** Session tracking, disclaimer compliance, barge-in windows.
- **Consequences:** Market-leading GenAI security, proactive threat response, comprehensive audit trails.
- **15-Factor Compliance:** Telemetry with security metrics, backing services for external detectors.
- **Repo Impact:**
  - `internal/genai/detectors/*` built-in and external detector framework
  - `internal/genai/threats/*` classification and response
  - `internal/voice/*` conversation compliance tracking

---

## **ADR-008: Policy Engine Architecture (Unified policy.yaml)**

- **Status:** Accepted
- **Context:** Need single policy surface covering data platform, automation, and GenAI security with clear promotion paths.
- **Decision:**
  - **Unified schema:** Single `policy.yaml` with sections for data_platform, genai_security, enforcement, compliance.
  - **Policy hash embedding:** Cryptographic binding in all evidence artifacts.
  - **Shadow mode promotion:** Test new policies without enforcement impact.
  - **Data platform sections:**
    ```yaml
    data_platform:
      dbt_hooks: {enabled, test_failures_block}
      warehouse_guards: {sql_safety, approval_tokens}
      activation_enforcement: {idempotency, rate_limits}
    ```
  - **GenAI security sections:**
    ```yaml
    genai_security:
      prompt_injection: {detectors, shadow_mode}
      bec_defenses: {approval_grade, sso_binding}
      deepfake_integration: {external_detectors}
    ```
- **Consequences:** Single source of truth, testable policy changes, comprehensive coverage.
- **15-Factor Compliance:** Config externalization, admin processes for policy management.
- **Repo Impact:**
  - `spec/policy/schemas/policy_v4.schema.json`
  - `internal/policy/loader.go` unified parsing
  - `cmd/clyra/policy/*` management commands

---

## **ADR-009: Attestation Framework (Multi-Framework Support)**

- **Status:** Accepted
- **Context:** Need to support SOX ITGC, PCI DSS, HIPAA compliance plus EU AI Act/NIST overlays with single pipeline.
- **Decision:**
  - **Signed JSON primary:** Source of truth with canonical structure and cryptographic signatures.
  - **PDF secondary:** Human-readable report referencing JSON digest for integrity.
  - **Framework support:**
    - **SOX ITGC:** Change control, segregation of duties, approval tracking for data changes.
    - **PCI DSS:** Daily review automation, access control evidence, change logging.
    - **HIPAA:** Audit controls, integrity safeguards, voice session privacy.
    - **EU AI Act/NIST:** Overlay labels and mappings (not pass/fail enforcement).
  - **Evidence correlation:** Bundle references, replay certificates, governance metadata.
- **Consequences:** Single attestation pipeline, multi-framework compliance, auditor-ready artifacts.
- **15-Factor Compliance:** Logs as event streams with structured output formats.
- **Repo Impact:**
  - `spec/attestation/schemas/*` framework-specific overlays
  - `cmd/clyra/attest.go` multi-framework generation
  - `docs/compliance/*` mapping documentation

---

## **ADR-010: Voice/Conversation Compliance (TCPA + Session Correlation)**

- **Status:** Accepted
- **Context:** Voice AI agents require specialized compliance (TCPA disclaimers, barge-in rights, session correlation).
- **Decision:**
  - **Session tracking:** Unique `voice_session_id` per interaction with metadata-only capture.
  - **Compliance fields:** `disclaimer_played`, `disclaimer_acknowledged`, `barge_in_available`.
  - **Partner correlation:** UCaaS integration (Teams, Zoom, Twilio) for audit trail linking.
  - **TCPA compliance:** Automated disclaimer enforcement, consent tracking, opt-out mechanisms.
  - **Privacy preservation:** Session metadata only, no audio storage, hashed correlation IDs.
- **Consequences:** Voice AI compliance readiness, comprehensive audit trails, privacy protection.
- **15-Factor Compliance:** Backing services for UCaaS integration, logs for session events.
- **Repo Impact:**
  - `internal/voice/*` session management and compliance
  - `internal/voice/correlation/*` partner system integration
  - `spec/voice/schemas/*` session and compliance schemas

---

## **ADR-011: Two-SKU Model (Review vs Gate)**

- **Status**: Accepted
- **Context**: Enterprises fear breaking production with enforcement. Need progressive adoption path.
- **Decision**:
  - Split product into two SKUs:
    - **Clyra Review**: Detection-only, listen-only mode, attestation, ServiceNow/Jira export
    - **Clyra Gate**: Full enforcement with policy gates, idempotency, velocity controls
  - Review mode starts with webhook/log ingestion (agentless)
  - Gate mode enables inline proxy and enforcement primitives
  - Clear upgrade path from Review to Gate
- **Consequences**:
  - Easier initial adoption (listen-only safe)
  - Natural upsell path as trust builds
  - Requires clear feature boundaries
  - Must maintain backward compatibility
- **15-Factor Compliance**: API-first allows smooth SKU transitions
- **Repo Impact**:
  - `internal/review/*` listen-only components
  - `internal/gate/*` enforcement components
  - `cmd/clyra/review/*` and `cmd/clyra/gate/*` commands

---

## **ADR-012: ServiceNow/Jira as Primary Integration**

- **Status**: Accepted
- **Context**: Enterprises consume compliance evidence through ITSM tools, not new dashboards.
- **Decision**:
  - Build native ServiceNow/Jira exporters as OSS stubs
  - One-way sync (Clyra → ITSM) for simplicity
  - Attested Change Tickets include:
    - Evidence bundle hash
    - Verification command
    - SOX/PCI/HIPAA compliance status
    - Direct link to badge/verification
  - JSON/CSV export with lightweight REST API scripts
- **Consequences**:
  - Immediate enterprise credibility
  - Fits existing workflows
  - One-way sync simpler than bidirectional
  - Must handle ticket format variations
- **15-Factor Compliance**: API-first design for ITSM integration
- **Repo Impact**:
  - `bridges/servicenow/*` ServiceNow integration
  - `bridges/jira/*` Jira integration
  - `examples/itsm-integration/*` setup guides

---

## **ADR-013: Badge Program for Viral Adoption**

- **Status**: Accepted
- **Context**: Need organic growth in dbt community without heavy sales investment.
- **Decision**:
  - Issue cryptographically signed compliance badges for dbt projects
  - Badge format: JWT with Ed25519 signature
  - Badge criteria:
    - SOX: All tests pass + schema reviewed + tickets created
    - PCI: Daily reviews + sensitive data tagged
    - HIPAA: PHI marked + encryption verified
  - Public verification endpoint at clyra.io/verify/{badge_id}
  - README.md integration with badge images
  - 90-day expiration to drive re-certification
- **Consequences**:
  - Visual proof of compliance
  - Viral growth through README visibility
  - Must prevent badge forgery
  - Creates badge service maintenance burden
- **15-Factor Compliance**: Stateless badge service with CDN caching
- **Repo Impact**:
  - `badge/service/*` issuance and verification
  - `badge/registry/*` project tracking
  - `badge/templates/*` SVG generation

---

## **ADR-014: Listen-Only via Webhooks**

- **Status**: Accepted
- **Context**: Installing proxies/agents creates high friction for enterprise adoption.
- **Decision**:
  - Support webhook/log-based ingestion for zero-touch onboarding
  - Primary integration: dbt Cloud webhooks
  - Secondary: log tailing, API polling
  - Generate full evidence bundles from webhook data
  - Graceful degradation when data incomplete
  - Progressive enhancement path to inline proxy
- **Consequences**:
  - Dramatically lower adoption friction
  - May miss some data without inline proxy
  - Requires robust webhook parsing
  - Must handle delivery failures gracefully
- **15-Factor Compliance**: Backing services for webhook processing
- **Repo Impact**:
  - `internal/review/listeners/*` webhook parsers
  - `internal/review/enrichment/*` data completion
  - `examples/webhook-setup/*` configuration guides

---

## **ADR-015: CI/CD Enforcement (Code Change Control)**

- **Status:** Accepted
- **Context:** Need comprehensive change control for code, infrastructure, and configuration changes with SOX compliance.
- **Decision:**
  - **GitHub Actions integration:** Evidence bundle verification, policy gate enforcement.
  - **Commit SHA binding:** Approval certificates tied to specific commit hashes.
  - **Deploy rate limiting:** Prevent runaway automation, enforce approval workflows.
  - **SOX ITGC tracking:** "Who/what/when" for all changes with segregation of duties.
  - **Badge generation:** "Evidence Verified" artifacts for README display.
  - **Policy gates:** Block merges violating Clyra policies with actionable feedback.
- **Consequences:** Automated change control, compliance-ready development workflows.
- **15-Factor Compliance:** Build/release/run separation, admin processes for deployments.
- **Repo Impact:**
  - `.github/actions/clyra-verify/*` composite actions
  - `internal/cicd/*` change control enforcement
  - `cmd/clyra/cicd.go` integration commands

---

## **ADR-016: Evidence Bundle Cryptography (Enhanced Integrity)**

- **Status:** Accepted
- **Context:** Need cryptographic integrity with multiple signature algorithms and KMS integration for enterprise deployment.
- **Decision:**
  - **Primary algorithm:** Ed25519 for speed and security.
  - **Alternative support:** ECDSA P-256, RSA-2048 for enterprise compatibility.
  - **KMS integration:** AWS KMS, Azure Key Vault, HashiCorp Vault for key management.
  - **Signature structure:** `{algo, key_id, signature, seq_no, event_count, digest}`.
  - **Hash chaining:** Per-run chains prevent insertion/reordering attacks.
  - **Canonical signing:** RFC 8785 (JCS) for payload hash binding in approval certificates.
- **Consequences:** Cryptographic integrity, enterprise key management, tamper evidence.
- **15-Factor Compliance:** Authentication with cryptographic verification.
- **Repo Impact:**
  - `internal/crypto/*` signature and verification engines
  - `internal/crypto/kms/*` key management integrations
  - `spec/crypto/schemas/*` signature format specifications

---

## **ADR-017: Performance and Reliability SLAs**

- **Status:** Accepted
- **Context:** Need strict performance guarantees for production data pipelines while supporting comprehensive enforcement.
- **Decision:**
  - **Data platform SLAs:**
    - dbt hook execution: <2s overhead
    - Warehouse queries: <5s for policy checks
    - Activation gateway: <15ms p95 HTTP proxy latency
  - **Universal SLAs:**
    - Gateway: ≤15ms p95 baseline (+3ms with enforcement)
    - Recorder: ≤20ms p95 with metadata snapshots
    - Evidence bundles: DEF <5s, PEF <3s generation
  - **GenAI processing:**
    - Prompt analysis: <100ms built-in detectors
    - External detectors: <500ms with timeout/fallback
    - Kill-switch evaluation: <1s response time
  - **Back-pressure handling:** Bounded queues, 503 on overflow, circuit breakers.
- **Consequences:** Production-ready performance, predictable latency, graceful degradation.
- **15-Factor Compliance:** Telemetry with performance metrics, disposability for quick recovery.
- **Repo Impact:**
  - `internal/performance/*` SLA monitoring and enforcement
  - `test/k6/*` performance validation gates
  - Performance budgets in CI/CD pipelines

---

## **ADR-018: SIEM Integration (ECS/OCSF + Saved Searches)**

- **Status:** Accepted
- **Context:** Need seamless SIEM integration with pre-built correlation rules for GenAI threats and data governance.
- **Decision:**
  - **NDJSON format:** ECS (Elastic Common Schema) and OCSF (Open Cybersecurity Schema Framework) compliance.
  - **Enhanced fields:** GenAI threat indicators, data change correlation, voice session metadata.
  - **Saved searches:** Pre-built Splunk/Datadog queries for:
    - Deepfake/BEC detection workflows
    - Data change anomalies and approval patterns
    - Daily review automation (PCI Req-10)
    - GenAI threat posture monitoring
  - **Partner correlation:** Fields for UCaaS, IdP, and external system correlation.
- **Consequences:** Day-one SIEM value, reduced SOC integration time, proactive threat detection.
- **15-Factor Compliance:** Logs as event streams with structured format.
- **Repo Impact:**
  - `internal/siem/*` NDJSON generation and formatting
  - `docs/siem/queries/*` saved search templates
  - `examples/siem/*` integration examples

---

## **ADR-019: Shadow Mode and Kill-Switch Evolution**

- **Status:** Accepted
- **Context:** Need safe policy testing and emergency response across data platform and GenAI security scenarios.
- **Decision:**
  - **Enhanced shadow mode:** Parallel policy evaluation with <1ms overhead, comprehensive logging.
  - **Multi-trigger kill-switch:**
    - Data platform: Schema change bursts, dbt test failure spikes
    - GenAI security: Prompt injection campaigns, deepfake detection clusters
    - Universal: Error rate thresholds, approval failure patterns
  - **Recovery mechanisms:** TTL expiry, HITL manual override, automated threshold reset.
  - **Evidence preservation:** All shadow verdicts and kill-switch actions logged with signatures.
- **Consequences:** Safe policy evolution, comprehensive emergency response, audit trail completeness.
- **15-Factor Compliance:** Config-driven thresholds, telemetry for monitoring.
- **Repo Impact:**
  - `internal/shadow/*` parallel policy evaluation
  - `internal/killswitch/*` multi-trigger emergency response
  - Shadow verdict correlation in evidence bundles

---

## **ADR-020: 15-Factor App Compliance Architecture**

- **Status:** Accepted
- **Context:** Modern cloud-native architecture requirements beyond traditional 12-factor methodology.
- **Decision:**
  - **Factor 13 - API First:** All components expose RESTful APIs, OpenAPI 3.0 specs, service interoperability.
  - **Factor 14 - Telemetry:** Comprehensive metrics via OpenTelemetry, business/security/performance counters.
  - **Factor 15 - Authentication:** mTLS inter-service, HMAC request auth, SSO integration, identity binding.
  - **Infrastructure as Code:** Helm charts, Terraform modules, policy-as-code YAML.
  - **Immutable Infrastructure:** Non-root containers, signed artifacts, distroless base images.
  - **CI/CD Native:** GitHub Actions integration, automated verification, SLSA provenance.
- **Consequences:** Modern cloud-native deployment, operational excellence, security by design.
- **Repo Impact:**
  - All components designed with 15-factor principles
  - `deploy/*` IaC templates and configurations
  - API-first architecture across all services

---

## **ADR-021: Independent Verifier Ecosystem**

- **Status:** Accepted
- **Context:** Need vendor-neutral verification to build trust and prevent lock-in concerns.
- **Decision:**
  - **Multi-language verifiers:** Go (primary), TypeScript (secondary), Python (future).
  - **Specification-only dependencies:** Verifiers consume only public schemas, no Clyra binaries.
  - **Golden vector testing:** Comprehensive test suite ensuring cross-verifier consistency.
  - **CI/CD integration:** GitHub Action for automated verification in customer pipelines.
  - **Community governance:** Open development, external contributors, transparency.
- **Consequences:** Trust through independence, ecosystem growth, competitive differentiation.
- **15-Factor Compliance:** Disposable verification processes, specification-driven design.
- **Repo Impact:**
  - `verifier/go/*` primary verification implementation
  - `verifier/typescript/*` secondary implementation
  - `spec/vectors/*` golden test vectors

---

## **ADR-022: Data Platform Hybrid Architecture (Proxy + Hooks)**

- **Status:** Accepted
- **Context:** Data platform integration requires both HTTP proxy enforcement and warehouse-native operations.
- **Decision:**
  - **HTTP proxy pattern:** Reverse-ETL/activation flows, SaaS API integrations, microservice calls.
  - **Warehouse-native pattern:** dbt hooks, stored procedures, session tags, direct JDBC/ODBC connections.
  - **Hybrid enforcement:** Same policy engine, different execution contexts, unified evidence format.
  - **Network topology:** Proxy where natural (HTTP), hooks where practical (warehouse native).
- **Consequences:** Natural integration patterns, reduced friction, comprehensive coverage.
- **15-Factor Compliance:** Port binding for HTTP services, backing services for warehouses.
- **Repo Impact:**
  - `internal/proxy/*` HTTP enforcement for activation flows
  - `internal/warehouse/native/*` direct warehouse integration
  - Unified policy evaluation across both patterns

---

## **ADR-023: Retention and Archival Strategy**

- **Status:** Accepted
- **Context:** Compliance requirements for long-term evidence retention with cost-effective storage.
- **Decision:**
  - **Retention requirements:**
    - HIPAA: ≥6 years audit log retention
    - PCI DSS: ≥12 months hot + archival beyond
    - EU AI Act: Operational lifetime + post-market monitoring
  - **Storage tiers:** Hot (recent), warm (compliance access), cold (archival).
  - **WORM compatibility:** S3 Object Lock, Azure Immutability, Google Cloud Retention.
  - **Chain of custody:** Cryptographic integrity across storage transitions.
  - **Configurable policies:** Customer-controlled retention periods and storage tiers.
- **Consequences:** Compliance-ready retention, cost optimization, audit trail preservation.
- **15-Factor Compliance:** Backing services for storage, config-driven retention policies.
- **Repo Impact:**
  - `internal/storage/*` multi-tier storage management
  - `docs/compliance/retention/*` framework-specific guidance
  - Configurable retention policies in `policy.yaml`

---

## **ADR-024: Developer Experience and Automation**

- **Status:** Accepted
- **Context:** Need comprehensive developer tooling for AI agents and human developers building on Clyra.
- **Decision:**
  - **CLI completeness:** All operations scriptable, comprehensive help, shell completion.
  - **SDK coverage:** Python primary, TypeScript secondary, comprehensive examples.
  - **Documentation automation:** OpenAPI generation, schema docs, integration guides.
  - **Testing framework:** Golden vectors, integration tests, performance benchmarks.
  - **AI agent support:** Structured specs, clear decision boundaries, error handling.
- **Consequences:** High developer productivity, reduced onboarding friction, AI agent compatibility.
- **15-Factor Compliance:** Admin processes automation, API-first design.
- **Repo Impact:**
  - Comprehensive CLI with shell completion
  - SDK examples and documentation
  - AI agent-friendly specification structure

---

## **Cross-ADR Implementation Guidelines**

### **Security Requirements (All ADRs)**
- Every component must implement fail-closed behavior by default
- All evidence artifacts must be cryptographically signed
- Identity binding required for protected operations
- Privacy by default with explicit opt-in for payload storage

### **Performance Requirements (All ADRs)**
- SLA monitoring and enforcement across all components
- k6 performance gates in CI/CD pipeline
- Graceful degradation under load
- <1ms overhead for shadow mode operations

### **Compliance Requirements (All ADRs)**
- All timestamps RFC3339 UTC with time synchronization
- Policy hash embedding in evidence artifacts
- Comprehensive audit trail with tamper evidence
- Framework-specific overlays in attestations

### **15-Factor Compliance (All ADRs)**
- Config externalization with environment variables
- Structured logging to stdout with ECS/OCSF format
- API-first design with OpenAPI specifications
- Comprehensive telemetry with business/security metrics

### **Developer Experience (All ADRs)**
- Clear error messages with actionable guidance
- Comprehensive documentation with examples
- AI agent compatibility with structured specifications
- Shell completion and automation-friendly CLI

## **Developer Quick Reference**

### **When Adding New Features**
1. Identify which ADR(s) the feature impacts
2. Update relevant schemas with version bumps
3. Ensure 15-Factor compliance patterns
4. Add golden vectors for new functionality
5. Update performance budgets and tests

### **When Modifying Security-Critical Paths**
1. Update threat model documentation
2. Regenerate golden vectors
3. Update attestation overlays
4. Validate cryptographic implementations

### **When Integrating External Systems**
1. Follow backing services pattern (15-Factor)
2. Implement circuit breakers and timeouts
3. Add correlation fields for SIEM integration
4. Ensure evidence preservation
5. Update partner correlation documentation

### **Compliance Checklist for All Features**
- [ ] Cryptographic signatures implemented
- [ ] Privacy-by-default enforced
- [ ] Performance SLAs validated
- [ ] Evidence bundle integration
- [ ] SIEM correlation fields
- [ ] Framework overlay mapping
- [ ] Independent verification support
- [ ] Documentation updates completed

---

*End of ADR v4.0 - Comprehensive Architecture Decision Records*