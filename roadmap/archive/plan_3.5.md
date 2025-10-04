Clyra v3.5 MVP Implementation Plan

Strategic Positioning: Data-led market entry (dbt, warehouses, reverse-ETL) with agent-ready architecture  
Execution Model: Dependency-driven sequencing - each epic builds on prior foundations  
Success Target: 10-minute PLG path, $300-600k ARR, 3+ design partners

> Note: This is the implementation plan for developers. See /docs/ADR_INDEX.md for architectural decisions, /docs/COMPLIANCE_SPECS.md for standards, and /docs/DEV_GUIDE.md for recipes.

***Quick Reference

Performance SLAs: Gateway ≤15ms p95, Recorder ≤20ms p95, dbt hooks <2s, warehouse queries <5s
Security Requirements: Zero critical vulnerabilities, SBOM+SLSA provenance, mTLS/HMAC auth
Database Support: Postgres 15/16 (full), Snowflake/Databricks (full), Postgres 13/14 (demo-only), BigQuery (Phase 1.5)
Compliance Frameworks: SOX ITGC, PCI DSS, HIPAA, EU AI Act/NIST (overlays), TCPA
Evidence Formats: DEF v0 (data platform), PEF v0 (automation/agents)

***Epic 0: Foundation & Tooling

Goal: Monorepo structure, CI/CD, security scanning, 15-Factor foundations

Story 0.1: Repository Scaffold
What: Complete monorepo structure with OSS hygiene files
Key Deliverables: README, LICENSE, CONTRIBUTING, CODE_OF_CONDUCT, SECURITY, directory structure
Critical Files: /CODEOWNERS with security-critical path gates
Acceptance: All OSS headers present, structure matches v4.0 architecture, CODEOWNERS enforced in PR checks

Story 0.2: Dev Environment & Build
What: Warp-first development with comprehensive Make targets
Key Deliverables: 
Makefile: quickstart, quickstart-data, test, verify-vectors, attest-sample, lint
Docker Compose: Local stack + data platform simulator
Warp workflows: .warp/workflows.yaml with productivity helpers
Acceptance: make quickstart boots full stack <10min, all targets functional
Example: make quickstart-data → Gateway + Recorder + Snowflake simulator + dbt project

Story 0.3: Language Workspaces
What: Go 1.25.x, Python 3.13 (uv), Node.js 22.x with proper isolation
Key Files: 
/go.mod, /go.work (Go workspace)
/sdk/python/pyproject.toml (Python uv)
/package.json (npm workspace root)
Acceptance: go work sync clean, uv run pytest passes, npm test passes across workspaces

Story 0.4: CI/CD Pipeline Foundation
What: Path-filtered GitHub Actions, release automation, publishing workflows
Key Files: 
.github/workflows/ci.yml - Main CI with Semgrep, Gitleaks, ZAP Baseline
.github/workflows/release.yml - GoReleaser + release-please
.github/workflows/publish-*.yml - Python/npm package publishing
Critical: Path filtering to avoid redundant builds, dependency caching
Acceptance: Path filters trigger correctly, release automation functional, parallel execution works

Story 0.5: Security & Supply Chain
What: SBOM generation (Syft), vulnerability scanning (Grype), signing (cosign), SLSA provenance
Key Workflows: 
.github/workflows/security/sbom.yml - Generate + attach SBOM
.github/workflows/security/sign.yml - Cosign artifact signing
Critical Requirements:
Grype fails CI on critical vulnerabilities (no exceptions without documented risk acceptance)
SLSA Level 3 provenance for all releases
Acceptance: SBOM attached to releases, artifacts signed with verifiable signatures, Grype gates enforced

Story 0.6: Architecture Documentation
What: Base architecture docs and ADR framework 
Key Files: /docs/arch/architecture.md, /docs/adr/ directory structure
Acceptance: Documentation complete, cross-references correct

Story 0.7: 15-Factor Compliance Infrastructure
What: API-first (OpenAPI 3.0), comprehensive telemetry (OpenTelemetry), enhanced auth (mTLS/HMAC)
Key Components:
OpenAPI specs: /spec/api/*.openapi.yaml for all services
Telemetry: /internal/telemetry/ with business/security/performance metrics
Authentication: /internal/auth/ with mTLS inter-service, HMAC request auth
Metrics Categories:
Business: request rates, feature usage, customer actions
Security: threat detections, auth failures, policy violations
Performance: latency percentiles, throughput, resource utilization
Acceptance: All services expose OpenAPI, telemetry pipeline operational, auth framework functional

Story 0.8: Database Compatibility Matrix
What: Version detection, cloud variant testing, documented support boundaries
Support Matrix (see ADR-001):
Postgres 15/16: Full production support
Postgres 13/14: Demo-only, best-effort, --allow-best-effort flag required
Snowflake/Databricks: Full production support
BigQuery: Phase 1.5 (clear messaging in clyra warehouse doctor)
Key Files: /docs/compatibility/database_matrix.md, /internal/database/version.go
Acceptance: Compatibility matrix documented, clyra doctor detects versions, cloud variants tested

Story 0.9: CI/CD Workflow Completeness
What: Comprehensive CI workflows with organized test matrix
Core Workflows:
ci.yml: Main CI with security scans (Semgrep, Gitleaks, ZAP)
nightly-audit.yml: k6 perf, ZAP Full, CodeQL, SBOM+Grype, OSV, Scorecard
traceability.yml: Feature/ADR/test coverage verification
policy-contract.yml: Policy schema validation
perf-budgets.yml: Performance SLA regression detection
Test Organization:
Integration: /test/integration/{gateway_validator,canonical_merkle_parity,schema_matrix}
E2E: /test/e2e/{verify_bundle,negative_vectors,determinism,recorder_*}
Fuzz: /test/fuzz/canonicalization_fuzz_test.go
Performance: /test/perf/k6_scenarios.js
Acceptance: All workflows operational, test matrix organized, security scans integrated, key rotation reminders (180d)

Story 0.10: Operational Tooling
What: License scanning, PR/issue templates, container security, egress examples
Key Scripts:
/scripts/check_licenses.sh - Dependency license compliance
/scripts/calc_perf.py - Weekly performance curve calculations
/internal/pr-agent/client.go - Automated PR analysis
Templates: .github/ISSUE_TEMPLATE/*, .github/PULL_REQUEST_TEMPLATE.md
Security Docs: Container security (non-root), egress control examples
Acceptance: License violations blocked in CI, templates active, security documented, performance trends tracked

Epic 0 Definition of Done: make quickstart functional, CI green, security scans passing, architecture docs complete

***Epic 1: Core Evidence Formats & Crypto

Goal: DEF v0 + PEF v0 with cryptographic integrity and independent verification

Story 1.1: Evidence Format Specifications
What: JSON Schema Draft 2020-12 compliant schemas for DEF/PEF
Key Files:
/spec/def/schemas/*.json - Data Evidence Format
/spec/pef/schemas/*.json - Portable Evidence Format
/spec/common/schemas/*.json - Shared structures (receipts, certificates)
Canonical JSON Rules: Sorted keys, UTF-8 NFC, RFC3339 UTC timestamps, fixed numeric formats
Acceptance: Schemas validate with ajv, versioning strategy documented, common structures shared

Story 1.2: Cryptographic Infrastructure
What: Multi-algorithm signing (Ed25519 primary, ECDSA/RSA support), KMS integration
Key Files: /internal/crypto/{signing.go,kms/}, support for AWS KMS, Azure Key Vault, HashiCorp Vault
Hash Chains: Per-run continuity for tamper detection
Acceptance: Multi-algorithm functional, KMS integration operational, hash chains prevent tampering

Story 1.3: Canonicalization & Merkle Trees
What: RFC 8785 (JCS) implementation, Merkle tree generation, external artifact handling
Key Files: /internal/bundle/{canonical.go,merkle.go,externalization.go}
Critical: Identical input → identical canonical bytes across platforms
Acceptance: Deterministic output validated, Merkle root stable, large artifacts externalized correctly

Story 1.4: Bundle Builder Infrastructure
What: Unified DEF/PEF builder with governance metadata, risk scoring, and payout fields
Key Files: /internal/bundle/{builder.go,def_builder.go,pef_builder.go,risk_scorer.go}
Manifest Generation: Run metadata, policy hash, warehouse anchors (DEF), threat classification (PEF), risk score
Journal Streaming: Ordered event log for audit replay
Risk Score Calculation: Multi-factor risk assessment including:
  Change magnitude: Schema changes (high), data changes (medium), config changes (low)
  Policy violations: Critical violations (weight: 10), warnings (weight: 3), passed checks (weight: 0)
  Context factors: Production environment (+2), off-hours execution (+1), approval bypassed (+5)
  Threat indicators: GenAI detections (+policy-defined weight), SQL safety violations (+3)
  Historical behavior: First-time actor (+2), anomalous patterns (+policy-defined weight)
  Score range: 0-100 (0=minimal risk, 100=critical risk), configurable thresholds in policy.yaml
Payout Metadata (stub for Phase 2 billing): run_id, actor_id, asset_id, change_intent, business_metric_refs[], payout_ref, currency
Acceptance: DEF includes warehouse anchors + risk score, PEF includes automation evidence + risk score, governance metadata embedded, risk score calculation tested across scenarios

Story 1.5: Golden Test Vectors
What: Immutable test vectors for cross-platform validation
Key Directories: /spec/def/test-vectors/, /spec/pef/test-vectors/, /test/golden_vectors/
Categories: Valid (success), forged (security), negative (error handling)
Acceptance: Vectors cover all scenarios, cross-platform consistency, immutable after publish

Story 1.6: Performance Metrics Embedding
What: Embed comprehensive metrics in evidence bundles
Metrics: Gateway latency (p50/p95/p99), recorder timing, dbt run duration, threat detection latency, bundle generation timing
Key Files: /internal/bundle/performance_metrics.go, /internal/bundle/governance_metadata.go
Acceptance: All metrics captured, embedded in DEF/PEF, governance metadata includes SLA compliance

Story 1.7: Storage Management & Retention
What: WORM storage integration with compliance-driven retention
Key Files: /internal/storage/{worm.go,retention.go,s3_object_lock.go,azure_immutable.go}
Retention Policies: HIPAA ≥6yr, PCI DSS ≥12mo hot + archive, EU AI Act operational lifetime
Acceptance: WORM functional (S3/Azure), retention policies enforced, compliance tags applied, immutability verified

Story 1.8: MCP Field Extensions to PEF v0 (Shadow-Only Prep)
What: Extend PEF v0 schema with optional MCP fields for future compatibility
Key Files: /spec/pef/schemas/pef_v0_mcp_extension.json
MCP Fields:
server_id: MCP server identifier
tool: Tool name being invoked
operation: MCP operation type (read/write/etc)
params_hash: SHA256 of operation parameters
result_hash: SHA256 of operation result
token_scope: OAuth scope for this operation
dpop_jkt: (optional) DPoP key thumbprint
approval_principal: Who approved this operation
Schema: Make all MCP fields optional, validate only when present
Acceptance: 
Schema validates with and without MCP fields
No enforcement logic (schema-only)
Verifiers ignore unknown fields gracefully
Forward compatibility documented

Story 1.9: Conformance & Implementers Documentation
What: Comprehensive guides for DEF/PEF implementers and conformance testing
Key Files: /docs/conformance.md, /docs/implementers_guide.md
Content:
Conformance testing procedures for DEF/PEF implementations
Must/should/may requirements clearly delineated
Implementer dos and don'ts with examples that compile
Cross-platform compatibility guidelines
Common pitfalls and anti-patterns
Reference implementations and golden vectors usage
Acceptance: Clear conformance criteria documented, implementer guide includes working examples, common mistakes highlighted with solutions, golden vectors reference complete

Epic 1 Definition of Done: Golden vectors pass cross-platform, signatures verify, bundles generate <5s (DEF)/<3s (PEF)
***Epic 2: Independent Verification Ecosystem

Goal: Vendor-neutral Go and TypeScript verifiers with consistent results

Story 2.1: Go Verifier (Primary) with Auditor Mode
What: Independent Go module verifying DEF/PEF formats with auditor-friendly explanations
Key Files: /verifier/go/cmd/{def-verify,pef-verify}/main.go, /verifier/go/internal/{auditor_mode.go,explain.go}, /spec/receipts/receipt_v0.1.schema.json
Critical: Import only spec files, zero dependency on internal Clyra code
Validation: Cryptographic signatures, Merkle roots, canonical JSON, lineage graphs, risk score validation
Auditor Mode Features:
  --auditor flag enables human-readable explanations with control rationale
  Control mapping: Links each verification step to SOX ITGC/PCI/HIPAA requirements
  Plain-language summaries: "This evidence shows schema change X was approved by Y on Z date"
  Risk explanation: Breaks down risk score calculation with contributing factors
  Violation details: Clear explanation of policy violations and their severity
  Remediation guidance: Actionable next steps for non-compliant evidence
  Evidence lineage: Visual ASCII tree showing data/operation lineage with trust scores
  PDF generation: --format=pdf produces human-readable attestation with embedded JSON digest reference
Receipt Spec v0.1 (Lightweight Auditor Format):
  Simplified schema: Subset of DEF/PEF optimized for auditor review (who/what/when + approval + risk_score)
  One-page evidence report: PDF renderer for quick auditor consumption (MTT-Evidence <5min)
  Schema extraction: Automated conversion from full DEF/PEF to lightweight receipt format
  Use case: Auditors need quick validation without full bundle complexity
  Fields: actor, timestamp, change_summary, approval_certificate_hash, risk_score, control_mapping, verification_command
Output Formats:
  JSON (default): Machine-readable verification results, exit code 0=valid, 1=invalid, 2=warning
  JSON + PDF (--format=pdf): PDF with verification summary + embedded JSON digest for auditor review
  Auditor mode (--auditor): Enhanced JSON with control rationale + plain-language explanations
  Combined (--auditor --format=pdf): PDF optimized for auditor review with control explanations
  Receipt format (--receipt): Lightweight receipt JSON + optional one-page PDF for auditors
Acceptance: Validates all golden vectors, independent module structure, consistent with TS verifier, auditor mode provides clear explanations, PDF generation works, control rationale accurate, receipt format extracts correctly from DEF/PEF, one-page PDF renders <1s

Story 2.2: TypeScript Verifier (Secondary)
What: npm package ensuring cross-language consistency
Key Files: /verifier/ts/src/{def-verifier.ts,pef-verifier.ts}
Runtime Support: Browser + Node.js
Acceptance: npx clyra-verify bundle.zip works, matches Go verifier results, published to npm

Story 2.3: GitHub Action Integration
What: Reusable composite action for CI/CD
Key Files: .github/actions/verify-bundle/action.yml
Usage: External repositories can verify evidence in their CI
Acceptance: Action validates bundles, usable by external projects, fails on invalid bundles

Story 2.4: Cross-Verifier Consistency
What: Automated testing ensuring Go/TS produce identical results
Key Files: /test/cross_platform/verifier_consistency/, .github/workflows/cross-verifier-consistency.yml
Test Matrix: All golden vectors × {Go, TS} verifiers
Acceptance: Identical results across verifiers, performance within tolerances, CI catches regressions

Epic 2 Definition of Done: Both verifiers pass all golden vectors, GitHub Action functional, consistency tests green

***Epic 3: Universal Policy Engine

Goal: Unified policy system covering data platform, GenAI security, voice compliance

Story 3.1: Policy Schema & Loader
What: JSON Schema for policy.yaml with multi-section structure
Key Files: /spec/policy/schemas/policy_v4.schema.json, /internal/policy/loader.go
Sections: data_platform, genai_security, voice_compliance, enforcement, compliance
Policy Hash: Cryptographic binding in all evidence artifacts
Acceptance: Schema validates all sections, backward compatibility maintained, policy hash generation works

Story 3.2: Data Platform Policy Section
What: dbt hook config, warehouse guard settings, activation enforcement rules
Key Files: /internal/policy/data_platform.go, /templates/policy/data_platform.yaml
Example Config:
  data_platform:
    dbt_hooks: {enabled: true, test_failures_block: true}
    warehouse_guards: {sql_safety: true, approval_tokens: required}
    activation_enforcement: {idempotency: true, rate_limits: {window: 60s, max: 1000}}

Acceptance: dbt controls configurable, warehouse policies enforced, activation rules validated

Story 3.3: GenAI Security Policy Section
What: Threat detection configuration, BEC defense settings, kill-switch thresholds
Key Files: /internal/policy/genai_security.go, /templates/policy/genai_security.yaml
Shadow Mode: New detectors start logging-only by default
Acceptance: Detectors configurable, shadow mode defaults enforced, kill-switch matrices functional

Story 3.4: Voice Compliance Policy Section
What: TCPA disclaimer requirements, session management, barge-in configuration
Key Files: /internal/policy/voice_compliance.go, /templates/policy/voice_compliance.yaml
Acceptance: TCPA rules configurable, UCaaS settings validated, session policies enforced

Story 3.5: Shadow Mode Implementation
What: Parallel policy evaluation without enforcement impact
Key Files: /internal/shadow/evaluator.go, /internal/siem/shadow_verdicts.go
Performance Target: <1ms overhead, zero enforcement disruption
Acceptance: Parallel execution <1ms, comprehensive logging, SIEM forwarding works, zero enforcement impact

Story 3.6: HITL Checkpoints & Two-Person Controls
What: Human-in-the-loop checkpoints with pause/resume and two-person approval
Key Files: /internal/policy/{hitl_checkpoints.go,two_person.go}, /docs/sop/change-mgmt.md
Features: Pause points for human review, resume tokens with expiry, two-person promotion for sensitive changes
Acceptance: Workflows pause at checkpoints, resume requires valid approval, two-person rule enforced, audit trail complete

Story 3.7: Lineage Tracking & Trust Propagation
What: Data and operation lineage with trusted write hints
Key Files: /internal/lineage/{lineage.go,trust_hints.go}
Features: Lineage graph construction, trusted write propagation, cross-system correlation, trust score calculation
Acceptance: Graphs accurately constructed, trust propagates correctly, cross-system correlation functional, minimal performance impact

Epic 3 Definition of Done: clyra policy lint passes, shadow mode validates, policy wizard generates valid configs

***Epic 4: Gateway - SchemaLock & Data Firewall

Goal: Enhanced Gateway with data awareness, GenAI security, voice compliance

Story 4.1: Core Gateway Infrastructure
What: Streaming JSON validator with repair-once capability
Key Files: /internal/proxy/{gateway.go,validator.go,queue.go}
Performance Target: ≤15ms p95 latency (+3ms with full enforcement)
Queue Management: Backpressure with 503 on overflow, bounded queue depth
Acceptance: ≤15ms p95, repair once then block, 503 on overflow

Story 4.2: Enhanced Receipt Generation with Risk Scoring
What: Signed receipts with OWASP/MITRE classification, risk scores, and platform metadata
Key Files: /internal/proxy/receipts.go, /spec/common/schemas/receipt.json, /internal/proxy/risk_calculation.go
Receipt Fields: request_id, enforcement_decision, threat_classification (OWASP LLM + MITRE), approval_certificate, warehouse_anchor, risk_score, risk_factors[]
Risk Score in Receipts:
  Calculated at gateway enforcement time using same algorithm as Story 1.4
  Included in cryptographic signature to prevent tampering
  Risk factors array documents calculation inputs for transparency
  Thresholds from policy.yaml determine enforcement decisions (e.g., risk_score >80 requires approval)
Acceptance: All fields present including risk_score and risk_factors, cryptographically signed, platform-specific metadata captured, risk calculation consistent with bundle builder

Story 4.3: Data Platform Integration
What: Data-aware validation with schema change detection and SQL safety
Key Files: /internal/proxy/{data_aware.go,sql_validator.go}
Features: Schema change detection, warehouse anchor correlation, SQL safety validation (block mass UPDATE/DELETE without WHERE)
Acceptance: Schema changes detected, SQL safety enforced, warehouse anchors captured

Story 4.4: GenAI Threat Detection
What: Built-in prompt injection detection and external detector integration
Key Files: /internal/proxy/{genai_detectors.go,external_detectors.go}
Detectors: Regex/JSONPath heuristics (<50ms), reflex loop detection, external API integration (<500ms timeout)
Acceptance: <100ms detection latency, shadow mode default, external API timeout handling works

Story 4.5: Voice Session Tracking
What: TCPA compliance with session correlation and barge-in management
Key Files: /internal/proxy/{voice_session.go,tcpa_compliance.go}
Features: Session ID generation, disclaimer tracking, barge-in window (<200ms response)
Acceptance: Session correlation works, disclaimer enforcement functional, <200ms barge-in response

Story 4.6: SIEM Integration & NDJSON
What: ECS/OCSF compliant event streaming to Splunk/Datadog/Elastic
Key Files: /internal/proxy/ndjson.go, /internal/siem/, /docs/siem/saved_searches/
Formats: ECS (Elastic Common Schema), OCSF (Open Cybersecurity Schema Framework)
Acceptance: ECS/OCSF compliance verified, Splunk/Datadog import works, GenAI fields included

Story 4.7: SSE Notarization & Bypass Detection
What: Server-sent events notarization and bypass event tracking
Key Files: /internal/proxy/{sse_notarization.go,bypass.go}
Features: SSE stream notarization, bypass detection/logging, notary evidence in bundles, real-time alerting
Acceptance: SSE streams notarized, bypass events logged with context, security alerts triggered, audit trail complete

Epic 4 Definition of Done: Gateway ≤15ms p95, all enforcement primitives functional, SIEM integration works

***Epic 5: Recorder - Flight Data Recorder

Goal: Enhanced Recorder with warehouse anchoring and metadata-only snapshots

Story 5.1: Core Recording Infrastructure
What: HMAC-validated capture with privacy-by-default body storage
Key Files: /internal/recorder/{recorder.go,capture.go}
Privacy Controls: Metadata-only default, explicit opt-in for bodies, hash chain continuity
Acceptance: HMAC enforced, privacy by default, hash chains unbroken

Story 5.2: Warehouse Anchoring System
What: Platform-specific anchoring (Snowflake QUERY_HISTORY, Databricks Delta, Postgres WAL)
Key Files: /internal/recorder/warehouse_anchor.go, /internal/warehouse/anchors/{snowflake.go,databricks.go,postgres.go}
Anchoring Methods:
Snowflake: QUERY_HISTORY ID + session tags
Databricks: Delta Lake commit versions + Unity Catalog lineage
Postgres: WAL LSN under REPEATABLE READ, optional logical decoding tap for upstream change capture
Enhanced Postgres Support (Optional):
  Logical decoding tap: wal2json/pgoutput listener for DDL/DML capture before downstream sync (e.g., Databricks/Mooncake)
  Drift receipt generation: Emit change receipts on schema/data modifications pre-replication
  Unity Catalog tag sync: Optional correlation with Databricks Unity Catalog (references Story 6.6 MLflow integration)
  Use case: Postgres → Databricks/Mooncake pipelines where upstream governance needed
  Performance: Asynchronous listener, minimal overhead on primary database
Acceptance: Anchors captured correctly, platform detection works, lineage preserved, optional logical decoding functional (opt-in), drift receipts generated on schema changes, UC sync tested with Databricks integration

Story 5.3: Metadata-Only Snapshots
What: Lightweight snapshots without full data capture
Key Files: /internal/recorder/metadata_snapshot.go, /internal/snapshot/
Snapshot Data: Row counts, checksums, schema fingerprints, sample statistics (no PII)
Performance Target: <50ms for ≤100 tables
Acceptance: <50ms for 100 tables, no sensitive data, deterministic output

Story 5.4: Deterministic Diff Engine
What: Reproducible change detection with stable ordering
Key Files: /internal/diff/{diff.go,semantic_diff.go}
Features: Stable ordering, schema drift detection, semantic data change summaries
Performance Target: <2s for typical diff operations
Acceptance: Identical diffs across runs, semantic changes detected, performance <2s

Story 5.5: Replay Engine & Certificates
What: Deterministic replay with scratch schema isolation and signed certificates
Key Files: /internal/replay/, /spec/common/schemas/replay_certificate.json
Safety: Scratch schema isolation (clyra_replay_<run_id>), network denylist (RFC1918, metadata endpoints)
Certificate Status: success|partial|failed with detailed failure codes
Acceptance: Isolated execution, success/partial/failed status correct, signed certificates, ≤2× baseline performance

Epic 5 Definition of Done: Recorder ≤20ms p95, warehouse anchors work, replay deterministic with certificates

***Epic 6: Data Platform Core Integration

Goal: Native dbt integration, warehouse guards, activation gateways

Story 6.1: dbt Hook Framework
What: Pre/post-run hooks for evidence generation
Key Files: /internal/dbt/hooks/, /sdk/python/dbt/, /templates/projects/dbt/
Hooks: on_run_start/on_run_end with metadata extraction
Performance Target: <2s overhead per run
Acceptance: <2s overhead, metadata captured (model lineage, test results), DEF bundles generated

Story 6.2: SQL Safety Macros
What: dbt macros for safe SQL operations with approval token validation
Key Files: /internal/dbt/macros/, /sdk/python/dbt/macros/, /examples/dbt-integration/macros/
Macros: clyra_guard.safe_merge(), clyra_guard.check_approval(), allowlist management routes
Acceptance: Mass operations blocked (UPDATE/DELETE without WHERE), approval tokens validated, allowlists functional

Story 6.3: Warehouse Native Guards with UDF/Stored Procedure Runtime Validation
What: Platform-specific enforcement (stored procedures, UDFs, session tags, macro helpers)
Key Files: /internal/warehouse/guards/{snowflake.go,databricks.go,postgres.go}, /examples/warehouse-integration/, /sql/{snowflake/,databricks/,postgres/}
Implementations:
Snowflake: 
  Session tag enforcement: ClyraApprovalToken, RunId, ActorId, TenantId tags validated at query time
  Stored procedures: clyra_guard.verify_approval(token TEXT) RETURNS BOOLEAN validates JWT tokens
  UDF for runtime tags: clyra_guard.get_session_context() RETURNS OBJECT extracts and validates session tags
  Schema change hooks: Event-driven validation using information_schema.tables and query_history correlation
  Role-based checks: WAREHOUSE/SCHEMA/ROLE diff detection via information_schema.grants
Databricks: 
  Macro helpers with MLflow integration for model governance
  Notebook magic commands: %clyra_approval <token> for interactive workflows
  Unity Catalog integration: Lineage extraction and governance metadata correlation
Postgres: 
  Functions for approval validation: clyra_guard.verify_approval(token TEXT) RETURNS BOOLEAN
  WAL-based lineage: Transaction log correlation with LSN anchoring
  Trigger functions: Schema change detection via event triggers
Note: BigQuery support explicitly deferred to Phase 1.5
SQL Artifacts in /sql/:
  {platform}/install.sql: DDL for stored procedures, UDFs, functions
  {platform}/uninstall.sql: Clean removal scripts
  {platform}/test.sql: Validation test suite
  {platform}/examples.sql: Usage examples with comments
Acceptance: Session tags enforced, approval validation works (stored proc + UDF), MLflow model versioning tracked (Databricks), role-based checks detect WAREHOUSE/SCHEMA/ROLE diffs, <5s query overhead, SQL artifacts complete and tested

Story 6.4: Activation Gateway Proxy
What: HTTP proxy for reverse-ETL (Hightouch/Census/RudderStack) with enforcement
Key Files: /internal/activation/, /cmd/clyra/activation/
Enforcement: Idempotency, rate limiting, tenant isolation, approval validation
Performance Target: <15ms p95 proxy latency
Acceptance: <15ms p95, all primitives enforced, tenant isolation works

Story 6.5: Data Platform CLI Commands
What: dbt and warehouse management commands
Commands:
clyra dbt init - Initialize dbt project with Clyra hooks
clyra warehouse doctor - Check connectivity, permissions, session tags (with BigQuery Phase 1.5 notice)
clyra activation gateway - Start reverse-ETL proxy
Key Files: /cmd/clyra/{cmd_dbt_init.go,cmd_warehouse_doctor.go,cmd_activation_gateway.go}
Acceptance: Commands functional, help text complete, integration examples work, BigQuery detection shows Phase 1.5 deferral

Story 6.6: Databricks MLflow Integration
What: MLflow model governance and experiment tracking
Key Files: /internal/warehouse/databricks/mlflow.go, /examples/warehouse-integration/databricks/mlflow/
Features: MLflow experiment metadata capture, model version tracking, deployment record correlation with Unity Catalog, reproducibility validation
Acceptance: Experiments tracked in evidence, model versions correlated with lineage, deployment approvals enforced, metadata preserved

Epic 6 Definition of Done: dbt hooks <2s, warehouse guards enforce, activation proxy <15ms p95, CLI commands functional

***Epic 7: GenAI Security Framework

Goal: Threat detection, BEC prevention, kill-switch capabilities

Story 7.1: Threat Classification System
What: OWASP LLM v1.1 and MITRE ATT&CK mapping
Key Files: /internal/genai/threats/{classification.go,owasp_mapping.go,mitre_mapping.go}, /docs/genai-security/threat-detection/
Classifications: OWASP LLM01-10, MITRE technique correlation, confidence scoring, automated response
Acceptance: All threats classified, correlation accurate, response automated

Story 7.2: Built-in Threat Detectors
What: Prompt injection and reflex loop detection
Key Files: /internal/genai/detectors/{prompt_injection.go,reflex_loop.go}
Patterns: Regex/JSONPath for common attacks, loop detection algorithms, configurable confidence thresholds
Performance Target: <50ms for common patterns, <100ms worst case
Acceptance: <50ms detection, low false positive rate, configurable patterns

Story 7.3: External Detector Integration
What: Vendor-agnostic deepfake and BEC detection
Key Files: /internal/genai/detectors/{external.go,deepfake.go}
Protocol: HTTP API framework with timeout (500ms) and fallback mechanisms
Acceptance: <500ms with timeout, graceful degradation on failure, multiple vendor support

Story 7.4: BEC-Grade Approval Certificates
What: Enhanced approval with SSO binding and payload integrity
Key Files: /internal/genai/security/bec_approval.go, /spec/genai/bec_certificate.schema.json
Certificate Fields: sso_sub, idp_domain, mfa_verified, challenge_nonce, payload_hash (RFC 8785), expires_at
Acceptance: SSO binding works, challenge validated, payload integrity preserved (JCS hashing)

Story 7.5: Multi-Trigger Kill-Switch
What: Emergency response with data/GenAI/universal triggers
Key Files: /internal/killswitch/{killswitch.go,multi_trigger.go}
Triggers: Data bursts, GenAI threat spikes, error rate thresholds
Recovery: TTL-based auto-recovery, HITL override capability
Response Target: <1s from trigger detection to enforcement action
Acceptance: <1s response time, all triggers functional, recovery mechanisms work

Story 7.6: GenAI Security CLI
What: Testing and analysis commands
Commands: clyra genai test, clyra bec validate, clyra threats analyze
Key Files: /cmd/clyra/{cmd_genai_test.go,cmd_bec_validate.go,cmd_threats_analyze.go}
Acceptance: Attack vector testing works, certificate validation functional, threat analysis accurate

Story 7.7: Content Provenance Helper (C2PA Integration)
What: Lightweight C2PA stamping for generated assets with consent tracking ("Sora-ready" positioning)
Key Files: /internal/genai/provenance/, /spec/pef/c2pa_extension.json, /examples/genai-security/c2pa/
Features:
  Optional PEF fields: c2pa_manifest_hash, consent_obtained, likeness_approved, model_provenance, asset_type
  Lightweight stamping helper: Attach C2PA metadata without heavy media processing (no transcoding/analysis)
  Receipt tracking: Consent/likeness approval evidence in audit trail
  Integration: Helper function callable from existing GenAI workflows
  Asset correlation: Link generated content to model runs and approval chains
Schema Design:
  All C2PA fields optional in PEF v0 (similar to MCP extension pattern in Story 1.8)
  Verifiers gracefully handle C2PA fields when present
  No enforcement logic in MVP (schema-only, forward compatibility prep)
Positioning:
  "Sora-ready" marketing without scope creep
  Cheap hedge for GenAI content wave (image/video/audio)
  Aligns with GenAI security brand and threat detection framework
Acceptance: Optional PEF schema fields validated, stamping helper <50ms execution, no media processing dependencies, example integration documented, verifiers handle C2PA fields correctly

Epic 7 Definition of Done: Threat detection <100ms, kill-switch <1s response, BEC certificates validated, C2PA helper functional

***Epic 8: Voice & Conversation Compliance

Goal: TCPA compliance, UCaaS integration, privacy-preserving session management

Story 8.1: TCPA Compliance Framework
What: Disclaimer enforcement, consent tracking, opt-out mechanisms
Key Files: /internal/voice/compliance/, /docs/voice-compliance/tcpa-compliance.md
Requirements: Disclaimer played before interaction, consent documented, time restrictions (8AM-9PM local)
Acceptance: Disclaimers enforced, consent documented, time restrictions validated

Story 8.2: Voice Session Management
What: Privacy-preserving session tracking with metadata-only capture
Key Files: /internal/voice/session/, /spec/voice/session.schema.json
Privacy: No audio storage, waveform analysis only, hashed correlation IDs, metadata-only capture
Acceptance: No audio stored, correlation accurate, privacy preserved

Story 8.3: UCaaS Integration Platform
What: Teams, Zoom, Slack, Twilio integration
Key Files: /internal/voice/correlation/, /examples/voice-compliance/ucaas-integration/
Integrations: API integrations, webhook handlers, SIP gateway support, WebRTC handling
Performance Target: <5ms session correlation, <100ms partner system correlation
Acceptance: All platforms integrated, correlation <5ms, WebRTC handled

Story 8.4: Barge-in Capability
What: Human interruption with quality metrics
Key Files: /internal/voice/compliance/barge_in.go, /internal/voice/session/interruption.go
Features: Interruption detection, response time tracking, quality metrics, acknowledgment tracking
Performance Target: <200ms response time
Acceptance: <200ms response, metrics accurate, acknowledgment tracked

Story 8.5: Voice Compliance CLI
What: Session and compliance management commands
Commands: clyra voice session, clyra voice compliance, clyra voice correlate
Key Files: /cmd/clyra/cmd_voice_*.go
Acceptance: Session management works, compliance checks functional, correlation accurate

Epic 8 Definition of Done: TCPA compliance enforced, UCaaS integration <5ms, barge-in <200ms

***Epic 9: Enhanced Enforcement Primitives

Goal: Advanced enforcement for data, GenAI, voice scenarios

Story 9.1: Idempotency System
What: HMAC-based duplicate prevention with TTL and tenant scoping
Key Files: /internal/enforcement/idempotency/, /internal/proxy/idempotency/
Features: HMAC fingerprinting, TTL management, tenant scoping, single-use default
Acceptance: Duplicates prevented, TTL enforced, tenant isolation works

Story 9.2: Velocity Guards
What: Rate limiting with burst protection
Key Files: /internal/enforcement/ratelimit/, /internal/proxy/ratelimit/
Features: Sliding windows, per-actor/tenant/route limits, fair burst handling
Acceptance: Rate limits enforced, burst handling fair, metrics accurate

Story 9.3: Tenant Fencing
What: Cross-tenant isolation with DSN hash namespacing
Key Files: /internal/enforcement/fences/, /internal/proxy/fences/
Features: Header validation, DSN hash namespacing, privacy preservation
Acceptance: Cross-tenant writes prevented, namespacing works, privacy maintained

Story 9.4: SQL Safety Guards
What: Prevention of dangerous SQL operations
Key Files: /internal/enforcement/sqlguard/, /internal/proxy/sqlguard/
Features: UPDATE/DELETE validation (require WHERE clause), rows_affected limits, allowlist exceptions
Acceptance: Dangerous ops blocked, limits enforced, allowlists work

Story 9.5: Prompt Loop Breaker
What: Agent failure cascade prevention
Key Files: /internal/enforcement/prompt_loop/, /internal/genai/security/loop_breaker.go
Features: Loop detection, cool-off policies, per-run counters, reflex detection
Acceptance: Loops detected, cool-off enforced, counters accurate

Epic 9 Definition of Done: All primitives functional with <5ms enforcement overhead, configurable via policy

***Epic 10: Multi-Framework Compliance Engine

Goal: Comprehensive attestation for SOX, PCI, HIPAA, EU AI Act, NIST, TCPA

Story 10.1: SOX ITGC Implementation with Control Rationale Documentation
What: Data change control for SOX compliance with comprehensive control mapping
Key Files: /internal/compliance/sox/, /docs/compliance/frameworks/sox-itgc/, /docs/compliance/sox_control_rationale.md
Requirements: Change control tracking, segregation of duties (separate dev/approval/deploy), approval workflows, control rationale documentation
SOX ITGC Control Mapping:
  Change Control (ITGC-3): All schema/data changes require approval, tracked with git SHA, approver SSO binding, timestamp
  Segregation of Duties (ITGC-4): Developer ≠ Approver ≠ Deployer, role enforcement at policy engine, violations blocked
  Access Management (ITGC-5): Role-based warehouse permissions, approval certificate validation, session tracking
  Monitoring & Logging (ITGC-6): Comprehensive audit trail, daily review generation, anomaly detection
Control Rationale Documentation:
  Each control includes: objective, implementation mechanism, evidence artifacts, testing procedures
  Auditor-friendly language explaining how Clyra satisfies control requirements
  Evidence mapping: Links DEF bundles to specific ITGC controls with field references
  Testing guidance: Step-by-step procedures for auditors to validate controls
  Exception handling: How policy TTL'd exceptions are documented and approved
Acceptance: Changes tracked with full lineage, duties segregated with role enforcement, approvals enforced with BEC-grade certificates, control rationale documentation complete and auditor-reviewed

Story 10.2: Enhanced PCI/HIPAA Support
What: Daily reviews with data changes and threat posture
Key Files: /internal/compliance/{pci/,hipaa/}
Features: PCI Req-10 automation, HIPAA audit controls, privacy safeguards
Acceptance: Daily reviews automated, privacy preserved, threat posture included

Story 10.3: EU AI Act & NIST RMF
What: AI governance overlays (not pass/fail enforcement)
Key Files: /internal/compliance/{eu_ai_act/,nist_rmf/}
Features: Record-keeping requirements (EU AI Act Art. 12), risk documentation, human oversight tracking
Acceptance: Requirements mapped, documentation complete, overlays functional

Story 10.4: TCPA Voice Compliance
What: Voice-specific compliance requirements
Key Files: /internal/compliance/tcpa/, /internal/voice/compliance/audit.go
Features: Consent documentation, disclaimer compliance, violation detection
Acceptance: Consent tracked, disclaimers validated, violations detected

Story 10.5: Unified Attestation Engine
What: Single pipeline for all frameworks
Key Files: /cmd/clyra/attest.go, /internal/attestation/
Output Formats: Signed JSON (primary source of truth), PDF (human-readable with JSON digest reference)
Command: clyra attest evidence.zip --framework sox|pci|hipaa|eu-ai-act|nist-rmf|tcpa
Acceptance: All frameworks supported, evidence correlated, attestations signed (Ed25519)

Story 10.6: Enhanced Daily Review with SOX ITGC Roll-Up Attestation
What: Comprehensive daily review with data/GenAI/voice summary and automated SOX attestation generation
Key Files: /internal/compliance/daily_review/, /cmd/clyra/report.go, /spec/compliance/daily_review.schema.json, /internal/attestation/daily_attestation.go
Content:
Data platform: schema migrations, row count deltas, dbt test results, warehouse role changes
GenAI threats: prompt injection attempts, deepfake detections, BEC attempts
Voice compliance: TCPA violations, session statistics, barge-in events
SOX ITGC Roll-Up Attestation:
  Aggregates all change control evidence from the day into single signed attestation
  Control summary: Count of changes by type, approval compliance rate, segregation of duties violations (if any)
  Risk summary: Aggregated risk scores, high-risk changes requiring review, policy exceptions granted
  Audit trail completeness: Verification that all changes have complete evidence chains
  Compliance status: Pass/fail for each ITGC control with supporting evidence references
  Attestation format: Signed JSON (cryptographic integrity) + PDF (human-readable with control rationale)
  Command: clyra report --daily-review --attest-sox generates both review and attestation
Showback Beta (EXPANDED from stub):
  Cost & risk aggregation: per project/team/model/framework with historical trending
  CSV export: QuickBooks/Xero compatible format (agent_id|run_id|date|risk_score|cost_attribution|framework_status)
  JSON export: Structured showback data for API consumption and future UI integration
  Dashboard data structure: Pre-formatted for executive reporting (by dept, by environment, by risk level)
  Metrics: Evidence bundles per team, approval rate trends, risk score distribution, policy exceptions by actor
  Command: clyra report --daily-review --showback --export-csv=./showback.csv
  CFO-friendly output: Translates technical evidence into cost/risk language with ROI indicators
Export Formats:
  ECS/OCSF NDJSON for SIEM ingestion
  Executive dashboard format (summary metrics)
  SOX attestation bundle (JSON + PDF with evidence references)
  Showback CSV (QuickBooks/Xero compatible)
  Showback JSON (API/future UI consumption)
Acceptance: Daily review includes all components, PCI Req-10 automated, SIEM-compatible exports, SOX ITGC attestation generated and mapped to controls, PDF includes control rationale, showback CSV exports correctly, QuickBooks/Xero format validated, JSON showback structure documented

Epic 10 Definition of Done: clyra attest generates signed attestations for all frameworks, daily review comprehensive

***Epic 11: CI/CD & Deployment Controls

Goal: GitHub Actions integration with SOX change control

Story 11.1: Enhanced GitHub Actions
What: Comprehensive CI/CD workflows with path filtering
Key Files: .github/workflows/{ci.yml,data-platform-ci.yml,genai-security-ci.yml,voice-compliance-ci.yml}
Features: Path-filtered triggers, evidence verification in CI, policy gates, performance/security testing
Acceptance: Workflows trigger correctly, verification works, gates enforce policies

Story 11.2: Commit SHA Binding
What: Change control with commit tracking and segregation of duties
Key Files: /internal/cicd/change_control/, .github/workflows/sox-compliance-gate.yml
Features: Approval certificates bound to commits, commit uniqueness validation, role-based duties separation
Acceptance: Commits bound to approvals, duties segregated, SOX compliance maintained

Story 11.3: Deploy Rate Limiting
What: Deployment control and safety with rollback
Key Files: /internal/cicd/deployment/, /internal/enforcement/cicd_controls.go
Features: Deployment rate limiting, approval workflows, automated rollback capabilities
Acceptance: Deploys rate limited, approvals enforced, rollback works

Story 11.4: Badge Generation System
What: Cryptographically signed compliance badges for dbt projects
Key Files: /internal/badge/, .github/workflows/badge-generation.yml
Badge Format: JWT with Ed25519 signature, 90-day expiration
Verification: Public endpoint https://clyra.io/verify/{badge_id}
Criteria: SOX (tests pass + schema reviewed + tickets created), PCI (daily reviews + data tagged), HIPAA (PHI marked + encryption verified)
Acceptance: Badges generated (JWT-signed), registry functional, verification works, displayed in README

Epic 11 Definition of Done: CI/CD workflows enforce SOX ITGC, badges issued for compliant projects, commits bound to approvals

***Epic 12: ServiceNow & Jira Integration

Goal: Enterprise ITSM integration for attested change tickets

Story 12.1: ServiceNow Bridge (Production-Ready)
What: Native ServiceNow REST API integration for Attested Change Tickets
Key Files: /bridges/servicenow/{client.go,auth.go,formatter.go,template.go,config.go}, /examples/servicenow-integration/
Authentication: OAuth 2.0 (primary) + Basic auth fallback
Ticket Creation:
Table: change_request (configurable)
Custom fields: u_attestation_hash, u_attestation_type, u_verification_link, u_sox_compliant, u_framework_status, u_badge_id
Attachments: Evidence bundle (JSON), optional PDF attestation
Template Engine: Go text/template with configurable field mapping via servicenow_config.yaml
Error Handling: Retry logic (3 attempts, exponential backoff), rate limiting, comprehensive error messages
CLI Commands: clyra export --servicenow evidence.zip, clyra review generate --servicenow
Acceptance: 
Tickets created in ServiceNow test instance with all custom fields populated
Evidence bundle attached, verification link functional
OAuth 2.0 works end-to-end, Basic auth fallback functional
Template engine renders correctly, configuration validated at startup
API latency <500ms p95 (excluding ServiceNow response time)

Story 12.2: Jira Connector
What: Atlassian Jira integration for issue export
Key Files: /bridges/jira/{client.go,formatter.go}, /examples/jira-integration/
Features: Atlassian SDK wrapper, issue formatting, field mapping, export scripts
Acceptance: Issues created in Jira, fields mapped correctly, export functional

Story 12.3: Review SKU Components
What: Listen-only mode infrastructure for progressive adoption
Key Files: /internal/review/, /cmd/clyra/review/
Features: Webhook listeners (dbt Cloud, etc.), log parsers, enrichment engine for evidence completion
Acceptance: Webhooks processed, logs parsed, evidence enriched without enforcement

Story 12.4: Gate SKU Components
What: Full enforcement mode activation
Key Files: /internal/gate/, /cmd/clyra/gate/
Features: Policy enforcement activation, primitive enablement, enforcement templates
Acceptance: Policies enforced, primitives active, templates applied

Epic 12 Definition of Done: ServiceNow tickets created in <30min demo, Jira export works, Review/Gate SKUs separated

***Epic 13: Enhanced SDKs & Developer Tools

Goal: Comprehensive SDK support with data platform, GenAI, voice capabilities

Story 13.1: Python SDK Enhancement
What: Full-featured Python SDK with dbt helpers, warehouse utilities, GenAI security, voice compliance
Key Files: /sdk/python/clyra_sdk/{dbt/,warehouse/,genai/,voice/}
Features: dbt macro helpers, warehouse connection utilities, threat detection helpers, voice session management
Package Management: uv-based with pyproject.toml
Acceptance: All helpers functional, examples work, tests pass, published to PyPI

Story 13.2: TypeScript SDK Foundation
What: TypeScript SDK for automation (Phase 1.5 full parity)
Key Files: /sdk/typescript/src/
Features: Core functionality, comprehensive type definitions, framework integration examples
Acceptance: Feature roadmap documented, types complete, examples functional, published to npm

Story 13.3: CLI Enhancement with Doctor Suggest-Fixes
What: Comprehensive CLI with enhanced doctor command providing remediation suggestions
Commands: All data platform, GenAI security, voice compliance commands PLUS:
clyra doctor - Enhanced with suggest-fixes:
Detects misconfigurations (database versions, connectivity, policy syntax)
Provides shell/SQL remediation commands (copy-pasteable)
Validates policy syntax with correction suggestions
Tests warehouse connectivity with connection string fixes
Policy analysis: Detects unreachable rules, missing coverage (e.g., tables without PII policy), suggests defaults by environment
Key Files: /cmd/clyra/{doctor.go,cmd_*.go}, /internal/cli/doctor_fixes.go, /internal/policy/static_analyzer.go
Acceptance: All commands work with comprehensive help, doctor provides actionable fixes, remediation commands copy-pasteable, unreachable policy rules detected, coverage gaps identified with suggestions

Story 13.4: Developer Documentation
What: Comprehensive getting started guides, API references, integration patterns
Key Files: /docs/{getting-started/,api-reference/,integration-patterns/}
Content: Multi-track guides (data platform, GenAI, voice), complete API docs, pattern library
Acceptance: Multi-track guides complete, API docs comprehensive, patterns documented with examples

Epic 13 Definition of Done: Python SDK published, TypeScript SDK foundation ready, CLI commands comprehensive with doctor fixes

***Epic 14: Performance & Reliability

Goal: Meet all SLAs with comprehensive monitoring

Story 14.1: Performance Testing Framework
What: k6-based performance validation with SLA definitions and trend analysis
Key Files: /test/perf/k6_scenarios.js, .github/workflows/performance-comprehensive.yml, /scripts/calc_perf.py
Scenarios: Gateway load, dbt hook overhead, warehouse query impact, activation proxy throughput
SLA Definitions: All performance targets from Epic 0 Quick Reference
Performance Trend Analysis: Weekly performance curve calculations via calc_perf.py, historical baseline tracking, regression detection with visual trend reports
Acceptance: All SLAs defined in k6, tests comprehensive, CI gates functional, regression detection works, calc_perf.py generates weekly audit curves

Story 14.2: SLA Monitoring System
What: Runtime SLA enforcement with metrics collection and alerting
Key Files: /internal/performance/{monitor.go,sla.go}, /internal/telemetry/
Features: Metric collection (OpenTelemetry), threshold monitoring, alert generation, SLO tracking
Acceptance: Metrics collected, thresholds enforced, alerts triggered on violations

Story 14.3: Circuit Breaker Implementation
What: Failure isolation and recovery for external dependencies
Key Files: /internal/performance/circuit_breaker.go
Dependencies: Warehouse connectivity, external detector APIs, UCaaS integrations
States: Closed → Open → Half-Open with configurable thresholds and recovery logic
Acceptance: Failures detected, circuits break/recover, state transitions correct, graceful degradation

Epic 14 Definition of Done: All SLAs met, k6 tests passing, circuit breakers prevent cascading failures

***Epic 15: Production Readiness

Goal: Security hardening, operational excellence, release integrity

Story 15.1: Security Hardening
What: Zero-trust architecture, secret management, vulnerability scanning, egress controls
Key Files: /internal/security/, .github/workflows/security/*.yml, /examples/egress/{iptables_sidecar.md,envoy_filter.md}, /docs/security.md
Features: mTLS inter-service, HMAC request auth, secret management (KMS integration), continuous scanning
Egress Controls: Network policy examples (iptables sidecar pattern), service mesh configurations (Envoy filter examples), allowlist-based egress enforcement, RFC1918 and metadata endpoint blocking for replay isolation
Acceptance: No critical vulnerabilities, secrets managed properly (no hardcoded values), scans automated, egress examples are copy-pasteable and production-ready

Story 15.2: Operational Runbooks
What: SOPs for production operations
Key Files: /docs/sop/{incident.md,change-mgmt.md,key-rotation.md}
Runbooks: Incident response, change management, key rotation, backup/recovery
Acceptance: Runbooks complete, procedures tested, links functional, SLAs documented

Story 15.3: Release & Distribution
What: Signed releases with SBOM and SLSA provenance
Key Files: .github/workflows/{release-*.yml,key-rotation-reminder.yml}, /goreleaser.yaml
Artifacts: Multi-arch builds (linux/amd64, linux/arm64, darwin/amd64, darwin/arm64), SBOM attached, artifacts signed
Key Rotation: Automated 180-day lifecycle with alerts at 150 days
Acceptance: Artifacts signed, SBOM attached, provenance verifiable, key rotation automated with alerts

Story 15.4: Key Rotation & Cryptographic Lifecycle
What: Automated key rotation with KMS integration
Key Files: /internal/crypto/kms/, .github/workflows/key-rotation-reminder.yml, /docs/sop/key-rotation.md
Features: 180-day rotation cycle, KMS integration (AWS/Azure/HashiCorp), overlap periods for verification, zero-downtime transitions
Acceptance: Automated reminders at 150 days, KMS supports all providers, zero-downtime transitions, complete audit trail

Epic 15 Definition of Done: Zero critical vulnerabilities, runbooks tested, signed releases with provenance, key rotation automated

***Epic 16: Demo & Quickstart Experience

Goal: 10-minute PLG path with comprehensive demos

Story 16.1: Quickstart Infrastructure
What: One-command local deployment with Docker Compose
Key Files: /examples/quickstart-compose/docker-compose.yml, /cmd/clyra/cmd_quickstart.go
Stacks: Full stack (all components), data platform stack (Gateway + Recorder + Snowflake simulator + dbt)
Sample Data: Pre-loaded fixtures for demo scenarios
Acceptance: Deploys in <10min (make quickstart), all components functional, sample data loaded

Story 16.2: Demo Scenarios
What: Comprehensive demonstration commands generating evidence
Commands: clyra demo data, clyra demo contracts, clyra demo etl
Key Files: /cmd/clyra/cmd_demo_*.go, /packs/{data/,contracts/,etl/}
Acceptance: Demos generate verifiable evidence, scenarios realistic, bundles include all metadata

Story 16.3: Procurement Kit
What: Auditor and buyer materials with sample evidence
Key Files: /kits/procurement/{evidence-samples/,attestations/,one-pagers/}
Content: Sample DEF/PEF bundles, multi-framework attestations, executive one-pagers, auditor guidance
Acceptance: Kit complete, samples verify independently, documentation clear for non-technical stakeholders

Story 16.4: Comprehensive Scenario & Service Packs
What: Production-ready scenario packs and industry-specific templates
Core Packs (at /packs/):
contracts/ - Contract operations with schemas, policies, fixtures, goldens
ap_ar/ - Financial operations with approval workflows
etl/ - Data pipeline operations
rpa/ - RPA automation scenarios
Industry Service Packs (at /packs/service/):
retail/ - order_update, refund_request, rma_create, address_change
finserv/ - case_update, account_note_add, limit_adjust_request
travel/ - booking_change, loyalty_update, invoice_issue
Structure: Each pack includes schemas, policies, fixtures, goldens, README.md, pack.yaml
Acceptance: All packs include working examples, policies validated, golden bundles verify, industry requirements met

Story 16.5: PLG Documentation & Success Digest
What: Product-led growth documentation and success reporting with builder-first messaging
Key Files: /docs/plg/{hello_bundle.md,quick_wins.md}, /cmd/clyra/report.go, /internal/plg/success_digest.go
Content:
Hello Bundle guide: First-time user journey to first bundle <10min
Success digest: Merkle root, blocks processed, replay results, badge achievements
Quick wins: 10-minute achievements for developer engagement
Onboarding metrics: time-to-first-bundle, time-to-first-attestation tracking
Builder-First Messaging:
  Hero pitch: "Prove your data changes are safe (in <1 minute)" NOT "Enterprise data change control and attestation"
  Pain-first use cases:
    - "Tired of hunting screenshots for auditors?"
    - "Schema migration broke prod last week?"
    - "Need to show your boss you did it right?"
  Developer-friendly tone: No compliance jargon on landing pages, code-first examples, "Works with your tools" focus
  Content hierarchy: Quick win (60s) → Share value (teammate) → Team adoption → Enterprise scale
  Community-focused: GitHub stars, open source, contributor guides, developer advocate engagement
Targeting:
  Primary: Indie data engineers, analytics leads, AI builders (prosumer/technical personas)
  Secondary: Team leads who want guardrails without bureaucracy
  Tertiary: Finance/compliance (pulled in by team adoption)
Acceptance: PLG docs guide to first bundle <10min, success digest includes all metrics, badges auto-awarded, metrics tracked, landing page copy is builder-focused (no enterprise jargon), sign-up conversion ≥5% from developer traffic

Story 16.6: Receipt Sharing & Virality Engine
What: Make receipts tangible and shareable for viral team adoption
Key Files: /internal/plg/receipt_sharing.go, /cmd/clyra/share.go, /docs/plg/sharing_patterns.md, /internal/integrations/slack_bot.go
Features:
  One-click sharing: clyra share evidence.zip generates shareable links
  Slack/Teams integration: Post receipt summaries with "Verified ✓" badges directly in threads
  Screenshot-ready reports: Visual receipt cards optimized for Notion/Confluence/wikis
  Email templates: "Look what I just prevented" copy-pasteable summaries
  GitHub PR comments: Auto-post verification status on pull requests (via GitHub Action)
  Public verification: https://clyra.cc/verify/{receipt_id} (no login required for basic verification)
Virality Mechanics:
  Receipt preview cards: Rich previews in chat tools (Slack unfurling, Teams message extensions)
  Social proof notifications: "5 devs in your company are using Clyra" when threshold reached
  Team analytics: "Your team blocked 12 unsafe changes this week" weekly digests
  Referral tracking: Track which shared receipts lead to new user signups
  Badge display: Auto-update README badges when receipts shared publicly
Integration Points:
  Slack bot: /clyra verify <bundle_url>, automatic receipt posting on dbt runs
  GitHub Action: Composite action posts verification results as PR comments
  Email: Plain-text + HTML templates for forwarding to managers/auditors
  Web: Embeddable receipt widgets for internal wikis/dashboards
Success Metrics:
  Receipt sharing rate: ≥30% of receipts shared within 7 days of generation
  Team expansion: ≥50% of shared receipts lead to new user signups from same org
  Slack installs: ≥10 teams with Clyra bot by Month 6
  Viral coefficient: ≥0.4 (each user brings 0.4 new users via sharing)
  Public verifications: ≥1K verification link clicks/month
Acceptance: Sharing links work across platforms, Slack bot functional, receipt cards render correctly in all chat tools, GitHub Action posts to PRs, viral loop metrics tracked, email templates deliverable, public verification pages load <1s

Epic 16 Definition of Done: make quickstart works in <10min, demos generate evidence, procurement kit complete, PLG onboarding <30min, receipt sharing functional, virality metrics tracked

***Epic 17: Integration Examples & Templates

Goal: Production-ready integration patterns

Story 17.1: Data Platform Examples
What: dbt and warehouse integration examples
Key Files: /examples/dbt-integration/, /examples/warehouse-integration/
Content: dbt project templates with Clyra hooks, warehouse configurations (Snowflake/Databricks/Postgres), activation examples
Acceptance: Examples functional out-of-box, best practices documented, performance optimized

Story 17.2: GenAI Security Examples
What: Threat detection patterns and mitigation strategies
Key Files: /examples/genai-security/
Content: Detector configurations, attack simulations (prompt injection, etc.), mitigation strategies
Acceptance: Patterns comprehensive, simulations realistic, strategies effective

Story 17.3: Voice Compliance Examples
What: UCaaS integration patterns
Key Files: /examples/voice-compliance/
Content: Platform integrations (Teams/Zoom/Slack/Twilio), session correlation examples, compliance workflows
Acceptance: Integrations work, correlation accurate, workflows complete

Story 17.4: SIEM Integration Templates
What: Vendor-specific SIEM configurations
Key Files: /examples/siem-integration/{splunk/,datadog/,elastic/}, /docs/siem/
Content:
Splunk: Saved searches, dashboards, alert correlation rules
Datadog: Custom metrics, log aggregation, incident workflows
Elastic/ELK: Index templates, Kibana visualizations
Generic: OpenTelemetry forwarding, Fluent Bit configuration
Pre-built Queries: GenAI threats, data platform changes, compliance violations, threat hunting playbooks
Acceptance: Vendor configs import correctly, dashboards functional with real data, alerts trigger on test events, documentation includes tuning

Story 17.5: LiteLLM & SDK Integration Examples
What: LiteLLM middleware integration and SDK usage patterns
Key Files: /examples/{litellm-recipe/,python-sdk/,typescript-sdk/}, /sdk/python/clyra_sdk/litellm_middleware.py
Content:
LiteLLM recipe: middleware config with GenAI security callbacks
Multi-vendor LLM examples: OpenAI, Anthropic, Bedrock
Python SDK: Comprehensive usage examples
TypeScript SDK: Browser and Node.js examples
Framework integrations: FastAPI, Express, Next.js, Django
Acceptance: LiteLLM middleware works with major providers, SDK examples cover all features, framework integrations production-ready, performance impact documented

Epic 17 Definition of Done: All integration examples functional, SIEM templates import correctly, SDK examples comprehensive

***Success Metrics & Exit Criteria

Technical Metrics
Performance: All SLAs met (Gateway ≤15ms p95, Recorder ≤20ms p95, dbt hooks <2s, warehouse queries <5s)
Reliability: >99% bundle verification success, <0.1% false positive rate
Security: Zero critical vulnerabilities, comprehensive threat coverage, signed artifacts

Business Metrics
Adoption: ≥3 design partners, ≥50% dbt runs under policy within 60 days
PLG Success: <30min time-to-first-attestation, ≥10 GitHub stars/week
Compliance: ≥1 attestation used in quarter-end close by design partner
Revenue: $300-600k ARR primarily from data platform use cases (70% Review SKU, 30% Gate SKU)

Strategic Metrics
Market Position: DEF/PEF referenced by competitors or standards bodies
Community: ≥100 dbt projects with badges, active GitHub community
Partnerships: ≥2 Big 4 audit firms acknowledge evidence format, integration agreements with dbt Labs or warehouse vendors

***Phase 1.5 Deferred Items

Explicitly out of scope for MVP v4.0:
BigQuery: Warehouse anchoring and full support (currently demo-only with clear messaging in clyra warehouse doctor)
Pipeline Operators: Prefect/Dagster integration
TypeScript SDK: Full feature parity (foundation only in MVP)
K8s/Istio/Helm: Production deployment manifests
Redis: Pluggable backend for rate limiting/idempotency (in-memory in MVP)
Diff-Agent CLI: Advanced diff capabilities
Rollback Orchestration: State management for automated rollback
WASM Detector Sandbox: Custom detector marketplace
Packaged SIEM Dashboards: Beyond templates
Self-Hosted Control Plane: UI/dashboard (CLI + API-first in MVP)

Phase 2 and Beyond: UI/dashboard, SaaS delivery, marketplace ecosystem

***Implementation Guidelines

Story Execution
Dependencies First: Never start a story until all dependencies are complete
Test-Driven: Write tests before implementation (golden vectors, integration tests, e2e tests)
Documentation Concurrent: Write docs alongside code, not after
Performance Validation: Test against SLAs before marking story complete
Security Review: All authentication/authorization code requires security approval

Code Quality Standards
Go: golangci-lint passing, gosec clean, >80% test coverage for critical paths
Python: ruff/mypy passing, pytest coverage >80%
TypeScript: ESLint passing, type-check clean, >80% coverage
All: Security scans (Semgrep, Gitleaks) passing, no critical vulnerabilities

Acceptance Criteria Enforcement
All criteria must pass before story is considered complete
Demo/PLG requirements are mandatory (not optional)
Performance SLAs must be validated with k6 tests
Documentation must include usage examples and troubleshooting

Reference Documentation
Architecture Decisions: See /docs/ADR_INDEX.md for all ADRs
Compliance Standards: See /docs/COMPLIANCE_SPECS.md for regulatory/security requirements
Developer Recipes: See /docs/DEV_GUIDE.md for copy-pasteable implementation recipes
Runtime Flows: See /docs/arch/runtime_flows.md for sequence diagrams

***Document Version: v3.5 MVP  