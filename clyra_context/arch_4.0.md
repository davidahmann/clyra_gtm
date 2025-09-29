# **Clyra Architecture Doc v4.0**

*Last updated: September 2025*

*Status: Data-led, Agent-ready Architecture (PRD v4.0)*

---

## **1. Purpose & Scope**

Clyra provides a **data change firewall and audit platform for automation runtimes** (data pipelines, AI agents, RPA bots, ETL/dbt, SaaS integrations, microservices).

**Strategic positioning:** Data-led, agent-ready. Lead with data platform enforcement where budget exists today, maintain same architecture for AI agents tomorrow.

Scope for MVP (All Locked):

- **In (Data Platform Core):**
  - dbt integration (hooks, CI gates, SQL safety macros).
  - Warehouse-native anchors (Snowflake QUERY_HISTORY, Databricks Delta commits, Postgres WAL LSN).
  - DEF v0 (Data Evidence Format) + PEF v0 (automation).
  - Activation/Reverse-ETL gateway with full enforcement primitives.
  - SOX ITGC, PCI, HIPAA attestations for data changes.
  - Airflow/Dagster operator integration.

- **In (Universal Foundation):**
  - Postgres v15/16 fully supported; 13/14 demo-only (best-effort, non-production).
  - Gateway (SchemaLock + Data Firewall).
  - Recorder (Flight Data Recorder).
  - Replay + Replay Certificate.
  - Shadow Mode + Kill-switch.
  - Independent Go/TS verifiers.

- **In (GenAI Security Hardening):**
  - GenAI Risk Overlay policy templates.
  - Prompt injection heuristics (built-in detectors, shadow-mode).
  - BEC-grade approval certificates (SSO binding, challenge reference).
  - Enhanced HITL for deepfake-susceptible workflows.
  - External detector shim (deepfake/BEC services).
  - Prompt delta hashing for injection drift tracking.

- **In (Conversation + Coding Focus):**
  - Voice session handling (session IDs, disclaimer tracking, barge-in).
  - CI/CD enforcement (GitHub Actions, commit SHA binding, deploy rate limits).
  - Partner-log correlation fields (SSO principals, session IDs).
  - SOX ITGC attestation overlay for code changes.

- **In (Enhanced Enforcement Primitives):**
  - Idempotency keys (HMAC fingerprints, TTL-bound).
  - HITL Approval Certificates (payload-bound, BEC-grade).
  - Velocity guards (sliding windows, burst protection).
  - Tenant & actor fences (cross-tenant write prevention).
  - SQL-safety guardrails (advisory - block mass UPDATE/DELETE).
  - Prompt-loop/reflex-chain breaker.
  - JSON Schema business rules.
  - Daily review helper with GenAI threat posture.

- **Out (Deferred):**
  - Content governance (email, CMS, publishing).
  - UI/control plane dashboards.
  - SaaS delivery model.
  - Non-Postgres DBs (MySQL, Oracle).
  - Rollback orchestration.
  - Full lineage UI/catalog features.
  - WASM detector sandbox.

**Quality attributes:**

- **15-Factor App compliance:** API-first, telemetry, authentication.
- **Reliability:** Fail-closed, deterministic replay, metadata-only snapshots.
- **Transparency:** Tamper-evident bundles, independent verifiers.
- **Security:** GenAI threat hardening, OWASP/MITRE mapping, BEC defenses.
- **Compliance:** SOX ITGC, PCI, HIPAA, EU AI Act/NIST overlays.
- **Performance:** Data pipeline integration <2s overhead, Gateway ≤15ms p95.

---

## **2. System Context (C4-L1)**

**Primary Actors (Data-Led):**

- Data Platform Teams / Analytics Engineers (Primary buyers).
- Finance Controllers / SOX PMO (Co-sponsors).
- dbt Developers / Data Engineers (Daily users).
- Auditors / Compliance Teams (Evidence consumers).

**Strategic Actors (Agent-Ready):**

- AI Agents / Automation Apps (Future producers).
- Platform/SRE & SecOps (Infrastructure operators).
- System Integrators (Implementation partners).

**External Systems:**

**Data Platform Ecosystem:**

- Data Warehouses: Snowflake, Databricks, Postgres, BigQuery.
- Transformation: dbt Cloud/Core, Airflow, Dagster, Prefect.
- Activation: Hightouch, RudderStack, Segment, Census.
- BI/Analytics: Looker, Tableau, PowerBI.

**Universal Infrastructure:**

- SIEM: Splunk, Datadog, Elastic Stack.
- KMS: AWS KMS, Azure Key Vault, HashiCorp Vault.
- WORM Storage: S3 Object Lock, Azure Immutability.
- CI/CD: GitHub Actions, GitLab CI, Jenkins.
- Collaboration: Slack, Microsoft Teams (HITL approvals).
- Voice/UCaaS: Twilio, Webex, Teams (conversation correlation).

**Context Diagram (Data-Led Flow):**

```
[dbt Developer] → [dbt Hooks] → [DEF Bundle] → [Auditor]
                      ↓
[Data Changes] → [Data Firewall] → [Warehouse Anchors] → [SOX Attestation]
                      ↓
[Activation Flow] → [Reverse-ETL Gateway] → [SaaS Systems]
```

**Context Diagram (Agent-Ready Flow):**

```
[Agent/App] → [Gateway] → [Recorder] → [Postgres] → [PEF Bundle]
                   ↓                                    ↓
             [GenAI Security] → [BEC Defenses] → [Verifier/SIEM]
```

---

## **3. Component Catalog (C4-L2)**

| **Component** | **Lang** | **Key Tech** | **Role** | **15-Factor** |
| --- | --- | --- | --- | --- |
| **Data Platform Components** |
| dbt Plugin/Hooks | Python/Go | dbt-core, Jinja2 | Emit DEF bundles, CI gates | API-first |
| Warehouse Anchors | Go | ODBC/JDBC, REST APIs | Snowflake/Databricks/PG integration | Telemetry |
| Activation Gateway | Go | HTTP proxy, rate limiting | Reverse-ETL enforcement | Authentication |
| DEF Bundle Builder | Go | Canonical JSON, Merkle trees | Data evidence format | API-first |
| SQL Safety Guards | Go/SQL | Stored procedures, macros | Query safety enforcement | Config |
| **ServiceNow/Jira Bridge Components** |
| ServiceNow Exporter | Go | REST client, template engine | Create attested change tickets | API-first |
| Jira Connector | Go | Atlassian SDK | Export evidence to Jira | API-first |
| Ticket Formatter | Go | JSON/CSV transforms | Format evidence for ITSM tools | Config |
| Badge Service | Go | JWT signing, CDN cache | Issue & verify compliance badges | Stateless |
| Badge Registry | Go | PostgreSQL, REST API | Track certified projects | Backing services |
| **Universal Foundation** |
| Gateway (SchemaLock + Data Firewall) | Go | JSON Schema, hash chain, SSE | Enforce schemas, policies, receipts | Port binding |
| Recorder (FDR) | Go | PG driver, WAL/LSN, metadata | Capture, snapshot, diff | Processes |
| Replay Engine | Go | PG scratch schema, isolation | Deterministic replay, certificates | Disposability |
| Bundle Builder (PEF) | Go | Canonical JSON, Merkle trees | Build signed evidence bundles | Build/release |
| Policy Engine | Go | YAML parser, rule engine | Interpret policy.yaml, enforcement | Config |
| **GenAI Security Components** |
| Threat Detector Framework | Go | regex, JSONPath, HTTP clients | Prompt injection, deepfake detection | Backing services |
| BEC Certificate Manager | Go | Ed25519/ECDSA, KMS integration | Enhanced approval certificates | Authentication |
| Prompt Delta Tracker | Go | Hashing, sanitization | Track injection drift | Telemetry |
| External Detector Shim | Go | HTTP client, timeout handling | Vendor-agnostic deepfake API | Backing services |
| **Conversation + Coding** |
| Voice Session Manager | Go | SIP/WebRTC, session correlation | Voice compliance tracking | Telemetry |
| CI/CD Enforcer | Go | GitHub API, Git hooks | Code change control | API-first |
| Partner-Log Correlator | Go | UCaaS APIs, SSO integration | Cross-system audit trails | Logs |
| **Core Infrastructure** |
| Crypto Engine | Go | Ed25519/ECDSA/RSA, KMS | Sign receipts, bundles, certificates | Authentication |
| CLI | Go | Cobra, terminal UI | Commands (verify, replay, attest, demo) | Admin processes |
| SDK (Python) | Python | Decorators, headers, dbt macros | Easy integration, developer tools | Dependencies |
| SDK (TypeScript) | TypeScript | HTTP clients, type definitions | Future automation integration | Dependencies |
| Verifiers | Go + TS | Independent CLIs, crypto | Neutral verification, auditor tools | Disposability |
| Docs/Spec | Markdown, JSON Schema | spec/pef/, spec/def/ | Source of truth, API contracts | Codebase |

---

## **4. Runtime Views (C4-L3)**

**Listen-Only → Review → Gate Flow:**

```
dbt Cloud Webhook → Clyra Review (listen-only)
   ↓
Evidence Bundle Generation → ServiceNow Ticket
   ↓
Daily Review + Badge Issuance → Audit Report
   ↓
[Customer requests enforcement]
   ↓
Enable Clyra Gate → Policy Enforcement Active
```

**ServiceNow Integration Flow:**

```
Evidence Bundle → Ticket Formatter → ServiceNow REST API
   ↓
Change Ticket Created with:
- Attestation hash
- Verification link
- Policy compliance status
- SOX/PCI/HIPAA mappings
   ↓
Auditor views in ServiceNow → Clicks verify link → Independent verification
```

**Badge Issuance Flow:**

```
dbt run completes → Clyra validates → Badge Service signs JWT
   ↓
Badge endpoint: clyra.io/badge/{framework}/{project-id}
   ↓
README.md displays → GitHub/GitLab renders → Auditors see compliance
```

**Data Platform Enforcement Flow:**

```
dbt Run → dbt Hooks → DEF Bundle Generation
   ↓
Schema Change → Warehouse Guards → Approval Token Check → Signed Receipt
   ↓
CI Pipeline → Policy Violation Check → Block Merge OR Allow
   ↓
Activation Sync → Reverse-ETL Gateway → Enforcement Primitives → SaaS API
```

**Universal Enforcement Flow:**

```
Agent → Gateway
   (validate JSON → idempotency check → approval cert check →
    velocity guard → tenant fence → sql_guard → genai detectors → receipt)
→ Recorder (HMAC verify → snapshot pre/post → diff)
→ Bundle (DEF v0 OR PEF v0)
```

**GenAI Security Flow:**

```
Request → Prompt Analysis → Injection Detection (shadow/enforce)
   ↓
Deepfake Check → External Detector → BEC Risk Assessment
   ↓
HITL Required? → BEC-Grade Approval Cert → Payload Binding
   ↓
Kill-Switch Check → Threshold Monitor → Block/Allow Decision
```

**Data Replay Flow:**

```
DEF Bundle → Data Replay Engine → Scratch Schema → dbt Run Recreation
   ↓
Warehouse State Recreation → Delta Comparison → Replay Certificate
```

**Conversation Flow:**

```
Voice Session → Disclaimer Check → Barge-in Window → API Action
   ↓
Session Correlation → Partner Log Sync → Audit Trail
```

**CI/CD Flow:**

```
Code Commit → GitHub Action → Policy Check → Approval Cert Required?
   ↓
Deploy Trigger → Rate Limit Check → Commit SHA Uniqueness
   ↓
SOX ITGC Tracking → Attestation Generation → Compliance Evidence
```

**Shadow Mode (Enhanced):**

```
Primary policy → Enforce
Shadow policy → Dry-run (log verdicts + SIEM forward + GenAI threat analysis)
```

**Kill Switch (Multi-Trigger):**

```
Data: Schema change burst → Block dbt runs
GenAI: Prompt injection spike → Block agent routes
General: Error rate threshold → Block entire run/app
Recovery: HITL manual resume OR TTL expiry
```

**HITL Approval Cert Flow (BEC-Grade):**

```
Approver (Slack/CLI) → SSO Authentication → Challenge Response
   ↓
Approval Cert Generation (payload hash + approver + SSO sub + challenge + expiry)
   ↓
Cryptographic Signing → Gateway Verification → One-time Use Enforcement
```

**Daily Review Helper (Enhanced):**

```
clyra report --daily-review → Data Changes + GenAI Threats + Voice Compliance
   ↓
Rollup JSON/PDF (signed) → SOX/PCI/HIPAA/TCPA mappings → Auditor Import
```

---

## **5. Data & Schemas**

**Schema Locations:**

- **Data Platform:** spec/def/schemas/
- **Automation:** spec/pef/schemas/
- **Common:** spec/common/schemas/

**Core Schemas (DEF v0 - Data Evidence Format):**

- **def_manifest.json:** dbt project metadata, model versions, test results.
- **data_receipt.json:** Schema changes, SQL safety checks, warehouse anchors.
- **semantic_delta.json:** Metric definition changes, schema evolution.
- **warehouse_anchor.json:** QUERY_HISTORY refs, Delta commits, WAL LSN.
- **attestation_sox.json:** SOX ITGC compliance mappings.

**Core Schemas (PEF v0 - Portable Evidence Format):**

- **manifest.json:** Run metadata, policy version, governance context.
- **receipt.json:** Enhanced with GenAI fields:

  ```json
  {
    "threat_class": "prompt_injection|deepfake|bec_attempt|normal",
    "prompt_delta_hash": "sha256:...",
    "voice_session_id": "uuid",
    "bec_approval_grade": "standard|enhanced",
    "genai_detector_results": {...}
  }
  ```

- **journal_event.json:** ECS/OCSF mapping with conversation correlation.
- **replay_certificate.json:** Enhanced status tracking, data replay support.
- **daily_review.json:** PCI Req 10 + GenAI threat posture rollup.

**Policy Schema (Enhanced):**

- **policy.schema.json:** Extended with data platform and GenAI sections:

  ```yaml
  data_platform:
    dbt_hooks: {enabled, test_failures_block, semantic_deltas_require_approval}
    warehouse_guards: {sql_safety, approval_tokens, session_tags}
    activation_enforcement: {idempotency, rate_limits, tenant_fences}

  genai_security:
    prompt_injection: {detectors, shadow_mode, thresholds}
    bec_defenses: {approval_grade, sso_binding, challenge_required}
    deepfake_integration: {external_detectors, confidence_thresholds}

  conversation:
    voice_compliance: {disclaimer_required, barge_in_window, session_correlation}
    partner_correlation: {ucaas_integration, sso_principals}
  ```

**15-Factor Compliance:**

- **Config:** All configuration via environment variables and policy.yaml.
- **Logs:** Structured JSON logs to stdout, ECS/OCSF NDJSON for SIEM.
- **Backing Services:** Database connections, KMS, external detectors as attached resources.

**Canonicalization (Enhanced):**

- UTF-8 normalized, sorted keys, RFC3339 UTC timestamps.
- Numeric fixed formats, JSON Canonicalization Scheme (RFC 8785).
- **Data-specific:** Deterministic SQL query normalization, schema fingerprinting.
- **GenAI-specific:** Sanitized prompt hashing, voice session normalization.

---

## **6. Security Model**

**Trust Boundaries:**

- **Data Platform:** dbt ↔ Hooks; Warehouse ↔ Guards; Activation ↔ Gateway.
- **Universal:** Agent ↔ Gateway; Gateway ↔ Recorder; DEF/PEF ↔ Verifier.
- **GenAI:** Prompt ↔ Detector; Voice ↔ Session Manager; External ↔ Detector APIs.

**Identity & Authentication (15-Factor Enhanced):**

- **mTLS:** Component-to-component communication.
- **HMAC headers:** Per-run authentication with short-lived secrets.
- **SSO integration:** Enhanced approval certificates with identity binding.
- **Session correlation:** Voice/UCaaS session linking to API actions.

**Privacy Controls:**

- **body_storage = none by default:** Explicit opt-in required for payload capture.
- **Redaction mandatory:** When body storage enabled, configurable rules.
- **Prompt sanitization:** Hash-only tracking for injection analysis.
- **Voice privacy:** Session metadata only, no audio storage.

**Enforcement Security:**

- **Fail-closed:** Default deny, spill_policy=block, bounded queues.
- **GenAI hardening:** Prompt injection detection, deepfake correlation.
- **BEC-grade approval certs:** SSO binding, challenge-response, payload hash binding.
- **Data safety:** SQL guards, schema change approval, activation rate limits.

**Enhanced Primitives Security:**

**Idempotency Keys:**

- **HMAC fingerprints:** Prevent key recovery, tenant-scoped namespacing.
- **Single-use enforcement:** TTL-bound, replay detection.
- **Data context:** Schema change idempotency, activation sync deduplication.

**Tenant Fences (Enhanced):**

- **Header validation:** tenant_id, actor_id, voice_session_id consistency.
- **Cross-reference:** DSN hash namespace, SSO principal validation.
- **Data isolation:** Multi-tenant warehouse access controls.

**Velocity Guards (Advanced):**

- **Sliding windows:** Fair burst handling, per-actor/tenant/route scoping.
- **GenAI-aware:** Prompt injection burst detection, deepfake attempt clustering.
- **Data-aware:** Schema change rate limits, activation volume caps.

**SQL Safety (Production-Ready):**

- **Advisory mode:** Block UPDATE/DELETE without WHERE (configurable).
- **Rows affected limits:** Policy-defined thresholds, allowlist exceptions.
- **Warehouse integration:** Native stored procedures, macro enforcement.

**Compliance Hooks (Comprehensive):**

- **SOX ITGC:** Data change control, segregation of duties, approval tracking.
- **PCI Req-10:** Daily review automation, access monitoring, change logging.
- **HIPAA:** Audit controls, integrity safeguards, voice session privacy.
- **TCPA:** Voice disclaimer compliance, consent tracking, barge-in rights.
- **EU AI Act/NIST:** Overlays in attestations, risk categorization.

---

## **7. Deployment & Topologies**

**Development & Testing:**

- **Local dev:** Docker Compose with Postgres + Snowflake/Databricks simulators.
- **dbt integration:** Local dbt projects with Clyra hooks enabled.
- **CI/CD testing:** GitHub Actions with policy validation, evidence verification.

**Production Topologies:**

**Data Platform Deployment:**

- **dbt Cloud integration:** Hooks deployed via dbt packages, centralized policy.
- **Warehouse-native:** Stored procedures, session tags, approval token validation.
- **Activation layer:** HTTP proxy for reverse-ETL tools, rate limiting, tenant isolation.
- **Evidence storage:** DEF bundles to WORM-compatible storage (S3 Object Lock).

**Universal Deployment:**

- **Kubernetes:** Helm charts (Phase 1.5), Istio/Envoy sidecar integration.
- **Database connectivity:** Direct DSN connections, replica detection/rejection.
- **Network security:** Egress deny-by-default, allowlist exceptions in policy.
- **High availability:** Gateway horizontal scaling, Recorder leader election.

**15-Factor Deployment Patterns:**

- **Disposability:** Fast startup/shutdown, graceful signal handling.
- **Port binding:** Services export via HTTP/HTTPS, no runtime dependencies.
- **Processes:** Stateless components, session state in external stores.
- **Concurrency:** Horizontal scaling via process replication.

**Data Platform HA:**

- **dbt hooks:** Distributed via package manager, version-controlled policy.
- **Warehouse guards:** Active-passive deployment, connection failover.
- **Activation gateway:** Multi-region deployment, session affinity.

**Universal HA:**

- **Gateway:** Stateless, auto-scaling based on latency/volume SLAs.
- **Recorder:** Singleton with leader election, health checks, automatic failover.
- **Evidence bundles:** Replicated to multiple WORM stores, integrity verification.

---

## **8. Integrations**

**Data Platform Ecosystem:**

**dbt Integration (Deep):**

- **Hooks:** on_run_start, on_run_end, post-hook model-level integration.
- **Macros:** clyra_guard.safe_merge(), clyra_audit.track_change().
- **Tests:** Custom dbt tests for policy compliance, semantic delta detection.
- **CI/CD:** dbt Cloud webhooks, GitHub Actions integration.
- **Package distribution:** dbt Hub, git submodules, version management.

**Warehouse Native (Production-Ready):**

**Snowflake:**

- **Session tags:** ClyraApprovalToken, RunId, ActorId, TenantId.
- **Stored procedures:** clyra_guard.verify_approval(), audit trail generation.
- **QUERY_HISTORY integration:** Lineage anchors, performance correlation.
- **Access History:** User activity correlation, compliance reporting.
- **Resource monitors:** Integration with kill-switch thresholds.

**Databricks:**

- **Delta Lake:** Commit version tracking, time travel integration.
- **Unity Catalog:** Lineage metadata, governance policy enforcement.
- **Cluster policies:** Clyra-required configurations, auto-termination.
- **Notebooks:** Magic commands for approval token injection.

**Activation/Reverse-ETL:**

- **Hightouch:** Webhook integration, sync policy enforcement.
- **RudderStack:** HTTP proxy, transformation governance.
- **Census:** Rate limiting, audience safety checks.
- **Segment:** Identity resolution, cross-system correlation.

**Universal Integrations:**

**KMS (Enhanced):**

- **AWS KMS:** IAM role-based access, key rotation automation.
- **Azure Key Vault:** Managed identity, certificate lifecycle.
- **HashiCorp Vault:** Dynamic secrets, audit logging integration.
- **Cosign:** Keyless signing, OIDC identity verification.

**SIEM (Comprehensive):**

**Splunk Enterprise/Cloud:**

- **ECS/OCSF NDJSON:** Pre-configured field mappings, correlation rules.
- **Saved searches:** GenAI threat detection, data change anomalies.
- **Dashboards:** Compliance posture, enforcement metrics.
- **Alert correlation:** Multi-event attack detection, BEC campaign tracking.

**Datadog:**

- **Custom metrics:** Performance SLIs, enforcement success rates.
- **Log aggregation:** Structured parsing, automated correlation.
- **APM integration:** Request tracing, latency attribution.
- **Incident management:** Workflow integration, runbook automation.

**Voice/Conversation:**

**UCaaS Integration:**

- **Microsoft Teams:** Graph API, call records correlation.
- **Slack:** Bot integration, approval workflow automation.
- **Zoom:** Webhook events, session metadata extraction.
- **Twilio:** SIP trunk integration, call detail record correlation.

**CI/CD (Advanced):**

**GitHub Actions:**

- **Verifier action:** Evidence bundle validation in workflows.
- **Policy gates:** Block merges on compliance violations.
- **Badge generation:** Automated README updates, status displays.
- **SLSA provenance:** Build attestation, supply chain security.

**GitLab CI/CD:**

- **Pipeline templates:** Reusable compliance workflows.
- **Security scanning:** Integration with existing security tools.
- **Compliance dashboard:** Merge request compliance status.

---

## **9. Operations & SRE**

**15-Factor Operational Excellence:**

**Telemetry (Factor 14):**

- **Application metrics:** Request rates, latency percentiles, error rates.
- **Business metrics:** Enforcement blocks, approval usage, compliance posture.
- **Security metrics:** Threat detections, kill-switch triggers, BEC attempts.
- **Data metrics:** Schema changes, dbt run success, activation sync rates.

**Health Checks & Monitoring:**

**Doctor Checks (Enhanced):**

- **Data platform:** dbt package versions, warehouse connectivity, token validity.
- **Database:** WAL retention/lag, replication slots, version compatibility.
- **GenAI security:** Detector availability, external API health, model versions.
- **Infrastructure:** NTP synchronization, TLS certificate validity, KMS accessibility.

**SLIs/SLOs (Comprehensive):**

- **Data platform:** dbt hook execution <2s, warehouse queries <5s, CI gate <10s.
- **Universal:** Gateway ≤15ms p95 (+3ms enforcement), Recorder ≤20ms p95.
- **GenAI security:** Prompt analysis <100ms, external detectors <500ms, kill-switch <1s.
- **Evidence generation:** DEF bundles <5s, PEF bundles <3s, attestations <30s.

**Runbooks (Operational):**

**Data Platform:**

- **dbt hook failures:** Package rollback, policy override procedures.
- **Warehouse outages:** Failover procedures, evidence preservation.
- **Activation emergencies:** Circuit breaker activation, manual sync procedures.

**GenAI Security:**

- **False positive surge:** Detector tuning, shadow mode activation.
- **Deepfake campaign:** Threat response, approval grade escalation.
- **Kill-switch activation:** Emergency procedures, stakeholder communication.

**Universal:**

- **Key rotation:** Automated procedures, zero-downtime transitions.
- **Evidence corruption:** Integrity verification, backup recovery.
- **Compliance audit:** Evidence export, attestation generation.

**Incident Response:**

- **Data incidents:** Schema corruption, unauthorized changes, sync failures.
- **Security incidents:** BEC attempts, prompt injections, deepfake detections.
- **Operational incidents:** Performance degradation, service outages.

**Telemetry (Opt-in Enhanced):**

- **Data platform:** dbt_runs_protected, schema_changes_blocked, sox_attestations_generated.
- **GenAI security:** prompt_injections_detected, bec_attempts_blocked, deepfakes_identified.
- **Universal:** bundle_verified, replay_run, attest_run, kill_switch_triggered.

---

## **10. Performance & Capacity**

**Performance Budgets (SLA-Enforced):**

**Data Platform:**

- **dbt hooks:** Execution overhead <2s per run, memory <100MB.
- **Warehouse queries:** Policy checks <5s, approval validation <1s.
- **Activation gateway:** HTTP proxy latency <15ms p95, throughput >1K req/s.
- **DEF bundle generation:** Schema analysis <3s, bundle creation <5s.

**Universal Foundation:**

- **Gateway:** ≤15ms p95 baseline, +3ms with full enforcement primitives.
- **Recorder:** ≤20ms p95 with metadata snapshots, WAL LSN anchoring.
- **Replay:** Deterministic reproduction ≤2× baseline performance.
- **Evidence bundles:** PEF creation <3s, verification <1s.

**GenAI Security:**

- **Prompt analysis:** Built-in detectors <50ms, external APIs <500ms with timeout.
- **BEC certificate validation:** In-memory lookup <1ms, crypto verification <10ms.
- **Kill-switch evaluation:** Threshold checking <1ms, action execution <100ms.
- **Voice processing:** Session correlation <5ms, disclaimer validation <10ms.

**Capacity Planning:**

**Data Platform Scaling:**

- **dbt integration:** Supports 10K+ models, 100+ daily runs per customer.
- **Warehouse load:** <1% overhead on query performance, connection pooling.
- **Activation throughput:** 10K syncs/hour per gateway instance, horizontal scaling.

**Universal Scaling:**

- **Gateway throughput:** 10K requests/second per replica, auto-scaling enabled.
- **Evidence storage:** Designed for 1M+ bundles/month, WORM storage integration.
- **Verifier performance:** Independent verification <1s per bundle.

**Back-Pressure & Circuit Breaking:**

- **Bounded queues:** 503 responses on overflow, graceful degradation.
- **External detector timeouts:** Fallback to built-in detectors, shadow mode.
- **Database connection limits:** Pool management, failover logic.

**k6 Performance Gates:**

- **Data platform:** dbt hook execution, warehouse query performance.
- **GenAI security:** Burst profile testing, detector response times.
- **Universal:** Enforcement primitive overhead, bundle generation speed.

---

## **11. Risks & Mitigations**

**Data Platform Risks:**

**Integration Complexity:**

- **Risk:** dbt package compatibility, breaking changes across versions.
- **Mitigation:** Automated testing across dbt versions, backward compatibility guarantees.

**Warehouse Performance Impact:**

- **Risk:** SQL guards cause query slowdowns, session tag overhead.
- **Mitigation:** Performance benchmarking, opt-out mechanisms, cached validations.

**Evidence Volume Growth:**

- **Risk:** DEF bundles consume excessive storage, costly retention.
- **Mitigation:** Configurable retention policies, compression, metadata-only defaults.

**GenAI Security Risks:**

**False Positive Management:**

- **Risk:** Prompt injection detectors block legitimate traffic.
- **Mitigation:** Shadow mode defaults, tunable thresholds, customer feedback loops.

**External Detector Dependencies:**

- **Risk:** Third-party deepfake services unavailable, costly API usage.
- **Mitigation:** Graceful fallbacks, caching, rate limiting, vendor diversity.

**Evolving Threat Landscape:**

- **Risk:** New attack vectors not covered by current detectors.
- **Mitigation:** Detector updates via configuration, community threat intelligence.

**Universal Technical Risks:**

**15-Factor Compliance Burden:**

- **Risk:** Complex deployment requirements, operational overhead.
- **Mitigation:** Incremental implementation, automated tooling, clear documentation.

**Multi-Platform Complexity:**

- **Risk:** Feature parity across databases/warehouses, testing complexity.
- **Mitigation:** Feature flagging, platform-specific testing, staged rollouts.

**Evidence Integrity:**

- **Risk:** Bundle corruption, signature verification failures.
- **Mitigation:** Cryptographic integrity checks, redundant storage, automated verification.

**Commercial & Operational Risks:**

**Message Confusion:**

- **Risk:** "Data tool" vs "automation platform" positioning unclear.
- **Mitigation:** Clear positioning as "enforcement platform with data-led GTM."

**Scope Creep:**

- **Risk:** Feature bloat, observability tool comparison, catalog expectations.
- **Mitigation:** Strict scope enforcement, "integrate don't rebuild" philosophy.

**Performance Regression:**

- **Risk:** Feature additions degrade core performance SLAs.
- **Mitigation:** Continuous performance monitoring, k6 gates, SLA enforcement.

**Competitive Response:**

- **Risk:** Established vendors add similar features, market commoditization.
- **Mitigation:** Patent core algorithms, community building, independence emphasis.

**Mitigation Strategies:**

**Technical Excellence:**

- **Automated testing:** Golden vector validation, integration test suites.
- **Performance monitoring:** Real-time SLA tracking, automated alerting.
- **Incremental deployment:** Feature flags, canary releases, rollback procedures.

**Market Positioning:**

- **Clear differentiation:** Enforcement + evidence vs observability + alerting.
- **Community building:** Open source specs, independent verifier ecosystem.
- **Customer co-development:** Design partners, feedback loops, success metrics.

---

## **12. Compliance Appendix**

**SOX ITGC (Enhanced for Data Platform):**

- **Change control:** dbt model changes, schema migrations, approval workflows.
- **Access management:** Warehouse permissions, approval certificate tracking.
- **Monitoring:** Automated daily reviews, segregation of duties enforcement.
- **Evidence:** Signed attestations, tamper-evident audit trails, replay capabilities.

**PCI DSS (Data-Aware):**

- **Req-10 (Logging):** Enhanced daily review with data changes, activation monitoring.
- **Req-6 (Development):** dbt CI/CD integration, secure coding practices.
- **Req-8 (Access):** Multi-factor approval certificates, session correlation.
- **Req-11 (Testing):** Automated security testing, vulnerability assessment.

**HIPAA (Privacy-Enhanced):**

- **§164.308 (Administrative):** Policy enforcement automation, audit trail completeness.
- **§164.312 (Technical):** Access controls, integrity safeguards, voice session privacy.
- **§164.314 (Organizational):** Business associate compliance, third-party integration.
- **Voice compliance:** TCPA disclaimer requirements, consent tracking.

**EU AI Act Art. 12 (Record-Keeping):**

- **High-risk AI systems:** Evidence bundle generation, lineage tracking.
- **Transparency obligations:** Algorithmic decision audit trails.
- **Risk management:** Threat classification, mitigation evidence.
- **Human oversight:** HITL approval workflows, human-AI interaction logs.

**NIST AI RMF (Risk Management):**

- **Govern:** Policy-as-code, governance pillar embedding.
- **Map:** Threat classification, risk categorization.
- **Measure:** Performance metrics, bias detection.
- **Manage:** Incident response, continuous monitoring.

**TCPA (Voice/Conversation Compliance):**

- **Consent requirements:** Disclaimer enforcement, opt-out mechanisms.
- **Call recording:** Session metadata only, privacy preservation.
- **Automation rules:** Voice agent identification, human transfer rights.

**Industry-Specific Extensions:**

**Financial Services:**

- **FFIEC guidance:** IT risk management, audit trail requirements.
- **MiFID II:** Transaction reporting, best execution evidence.
- **Basel III:** Operational risk capital, model risk management.

**Healthcare:**

- **FDA validation:** Medical device software, clinical decision support.
- **Joint Commission:** Patient safety, quality improvement.
- **State privacy laws:** CCPA/CPRA compliance, data subject rights.

---

## **13. API / CLI Reference**

**CLI Commands (Enhanced for v4.0):**

**Data Platform Commands:**

- **clyra demo data** → Generate DEF bundles from dbt run simulation.
- **clyra dbt init** → Initialize dbt project with Clyra hooks.
- **clyra warehouse doctor** → Check Snowflake/Databricks connectivity and configuration.
- **clyra activation gateway** → Start reverse-ETL proxy with enforcement.

**Universal Commands:**

- **clyra quickstart** → Docker Compose with data platform examples.
- **clyra demo contracts|etl** → Generate PEF bundles from automation simulation.
- **clyra doctor** → Enhanced health checks including GenAI detectors.
- **clyra init** → Policy scaffold with data platform and GenAI sections.

**Policy Management:**

- **clyra policy wizard** → Interactive policy creation with data/GenAI templates.
- **clyra policy lint** → Validate policy syntax and semantic consistency.
- **clyra policy test** → Execute policy tests against golden vectors.
- **clyra policy convert** → Migrate v3.0 policies to v4.0 format.

**Evidence & Attestation:**

- **clyra export --format ndjson|def|pef** → Export evidence in various formats.
- **clyra report --daily-review** → Enhanced with data changes and GenAI threats.
- **clyra verify --explain** → Detailed verification output including data lineage.
- **clyra replay** → Enhanced with data replay capabilities.
- **clyra attest --framework <sox|pci|hipaa|eu-ai-act|nist-rmf>** → Extended frameworks.

**GenAI Security Commands:**

- **clyra genai test** → Test prompt injection detectors against attack vectors.
- **clyra bec validate** → Validate BEC-grade approval certificates.
- **clyra threats analyze** → Analyze GenAI threat patterns in evidence bundles.

**APIs (15-Factor Compliant):**

**Data Platform APIs:**

- **dbt Integration API:** Hook registration, policy validation, evidence submission.
- **Warehouse Anchor API:** Metadata capture, lineage tracking, compliance reporting.
- **Activation Control API:** Sync policy enforcement, rate limiting, audit trails.

**Universal APIs:**

- **Evidence Bundle API:** DEF/PEF creation, verification, attestation generation.
- **Policy Management API:** Configuration updates, validation, deployment.
- **Verification API:** Independent bundle verification, golden vector testing.

**GenAI Security APIs:**

- **Threat Detection API:** Prompt analysis, deepfake correlation, BEC assessment.
- **Approval Certificate API:** Enhanced certificate generation, validation, revocation.
- **Kill-Switch API:** Threshold monitoring, emergency activation, recovery procedures.

**Voice/Conversation APIs:**

- **Session Management API:** Voice session tracking, correlation, compliance.
- **Disclaimer API:** Requirement checking, playback verification, opt-out handling.
- **Partner Correlation API:** UCaaS integration, log synchronization, audit trails.

**Schema Locations (Enhanced):**

- **DEF schemas:** spec/def/schemas/ (data evidence format).
- **PEF schemas:** spec/pef/schemas/ (portable evidence format).
- **Policy schemas:** spec/policy/schemas/ (configuration validation).
- **API schemas:** spec/api/schemas/ (OpenAPI 3.0 definitions).

---

*End of Architecture Doc v4.0*
