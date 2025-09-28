# CLAUDE.md

Clyra v4.0 Project Manifest (Data-Led, Agent-Ready)

Business Case (enhanced)

One control point, three strategic guarantees:
• Clyra Gateway (SchemaLock + Data Firewall): Stops unsafe data changes, malformed outputs, GenAI threats (fail-closed, OWASP LLM-tagged, deepfake/BEC-classified).
• Clyra Recorder (Flight Data Recorder): Proves and replays every change across data platforms and automation, producing tamper-evident evidence bundles (DEF v0 + PEF v0).
• Clyra Compliance Engine: Multi-framework attestations (SOX ITGC + PCI/HIPAA + EU AI Act/NIST + TCPA) with independent verification.
Tagline: Data Change Control & Attestation for Modern Pipelines

Strategic positioning: Data-led market entry, agent-ready architecture. Lead with data platform enforcement (dbt, warehouses, reverse-ETL) where budget exists today, maintain same architecture for AI agents tomorrow.

Product Packaging:
• Two-SKU Model: Clyra Review (listen-only detection) → Clyra Gate (full enforcement)
• ServiceNow/Jira Bridge: Native "Attested Change Ticket" creation via OSS stubs
• Badge Program: "Clyra Certified - SOX Compliant" badges for viral dbt community growth
• Audit Partner Network: 2-3 Big 4 firms acknowledge our evidence format

GenAI security extensions: deepfake detection, BEC-grade approvals, prompt injection heuristics, voice session compliance, external detector APIs, multi-trigger kill-switch.
Data platform integrations: dbt hooks, warehouse anchors (Snowflake/Databricks), activation gateways, SQL safety guards, semantic delta tracking.
Voice/conversation compliance: TCPA disclaimer enforcement, UCaaS correlation, session management, barge-in capabilities.
Self-serve PLG motion: webhook listen → ServiceNow ticket → badge earned → sox compliance in <30 min.
Progressive Adoption Path: Listen-Only (safe) → Review (detection) → Gate (enforcement) → Full Platform.
Enhanced enforcement primitives: BEC-grade approval certs, prompt-loop breakers, voice session fences, CI/CD gates.
Governance pillars embedded in every bundle: Reliability · Transparency · Accuracy · Oversight.

⸻

Project Overview (v4.0)

Clyra is an OSS data change control and attestation layer for modern data pipelines — from data pipelines to AI agents, dbt/ETL, reverse-ETL, RPA, SaaS integrations, microservices.

Data Platform Core (NEW):
• dbt Integration: on_run_start/end hooks emit DEF v0 bundles, CI gates block policy violations, SQL safety macros enforce approval tokens.
• Warehouse Anchors: Snowflake (QUERY_HISTORY + session tags), Databricks (Delta commits + Unity Catalog), Postgres (WAL LSN + REPEATABLE READ).
• Activation Gateway: HTTP proxy for reverse-ETL (Hightouch/Census/RudderStack) with full enforcement primitives.
• DEF v0 Format: Data Evidence Format with warehouse-native anchoring, semantic delta tracking, SOX ITGC compliance.

Universal Foundation (Enhanced):
• Gateway (SchemaLock + Data Firewall): streaming JSON validation, data-aware policies, GenAI threat detection, BEC-hardened receipts, voice session tracking.
• Recorder (Flight Data Recorder): HMAC ingestion, metadata-only snapshots, warehouse anchoring, deterministic diffs, enhanced replay (data + schema).
• Replay Engine: offline scratch schema, data recreation, warehouse isolation, signed certificates with enhanced failure codes.
• Bundle Builder: unified DEF/PEF formats, canonical JSON, Merkle trees, governance metadata, performance/security metrics.

GenAI Security Framework (NEW):
• Threat Detection: OWASP LLM Top 10 mapping, MITRE ATT&CK correlation, prompt injection heuristics, deepfake API integration.
• BEC Prevention: SSO-bound approval certificates, challenge-response, payload hash binding (RFC 8785), MFA enforcement.
• Kill-Switch Evolution: multi-trigger (data bursts + GenAI threats + error spikes), TTL recovery, HITL override.
• Shadow Mode: parallel policy evaluation, comprehensive threat logging, zero enforcement impact.

Voice/Conversation Compliance (NEW):
• TCPA Compliance: disclaimer enforcement, consent tracking, opt-out mechanisms, time restrictions.
• Session Management: voice session correlation with API actions, metadata-only capture, privacy preservation.
• UCaaS Integration: Teams/Zoom/Slack/Twilio correlation, SIP gateway support, WebRTC handling.
• Barge-in Capability: human interruption with <200ms response, quality metrics tracking.

Evidence & Attestation (Enhanced):
• DEF v0 + PEF v0: unified formats with independent Go/TS verification, warehouse anchoring, governance embedding.
• Multi-Framework Attestations: SOX ITGC (change control), PCI/HIPAA (pass/fail), EU AI Act/NIST/TCPA (overlays).
• Daily Review Helper: enhanced with data changes + GenAI threat posture, automated PCI Req-10 compliance.

Enhanced Enforcement Primitives:
• BEC-Grade Approvals: SSO binding (approver_sso_sub + idp_domain + challenge_nonce), short TTLs, MFA flags.
• Prompt-Loop Breaker: per-run counters, cool-off policies, agent-specific reflex detection.
• Voice Session Fences: disclaimer requirements, session correlation validation, privacy-preserving audit.
• CI/CD Enforcement: GitHub Actions integration, commit SHA binding, deploy rate limits, SOX ITGC tracking.

Policy Engine (Enhanced):
• Unified policy.yaml: data_platform + genai_security + voice_compliance + enforcement + compliance sections.
• Shadow Mode Promotion: test new policies without enforcement impact, comprehensive verdict logging.
• Kill-Switch Matrix: data platform (schema bursts), GenAI (injection spikes), universal (error thresholds).

CLI & SDKs (Enhanced):
• Data Platform Commands: clyra dbt init, clyra warehouse doctor, clyra activation gateway.
• GenAI Security Commands: clyra genai test, clyra bec validate, clyra threats analyze.
• Voice Compliance Commands: clyra voice session, disclaimer tracking.
• Enhanced Universal: clyra demo data, enhanced verify with lineage, multi-framework attest.
• Python SDK: enhanced with dbt helpers, warehouse integration, GenAI security, voice compliance.
• TypeScript SDK: Phase 1.5 with automation focus.

Verifiers (Enhanced): Go (primary) + TS (secondary) with DEF/PEF support, lineage validation, compliance mapping.
Scenario & Service Packs: Data (dbt demo, ETL pipeline, activation flows), Enhanced Automation (Contracts, AP/AR, RPA), Industry Service Packs (Retail, FinServ, Travel) with GenAI hardening.

⸻

Tech Stack & Versions (v4.0)
• Go: 1.25.x (enhanced with data platform + GenAI modules)
• Tooling: golangci-lint ≥2.4.0, gosec ≥2.22.x, go vet
• Python: 3.13 (via uv) with dbt-core 1.0+ integration
• ruff 0.13.1, mypy 1.18.2, pytest 8.4.0
• Node.js: 22.x LTS (CI matrix: 22.x + 24.x)
• TypeScript: ~5.9, ESLint v9.17.0 (+ @typescript-eslint/*)
• Data Platform: dbt-core 1.0+, Snowflake Python Connector, Databricks SDK, asyncpg
• Schemas: JSON Schema Draft 2020-12; RFC 8785 (JCS) for BEC-grade approval cert payload hashing
• Supply Chain: cosign 2.5.x, syft 1.32.x, grype 0.99.x, SLSA Level 3
• Perf/Sec: k6 (enhanced scenarios), OWASP ZAP (Baseline on PRs; Full on nightly)
• GenAI Security: External detector APIs, OWASP LLM Top 10 v1.1, MITRE ATT&CK for GenAI
• Voice/UCaaS: SIP protocol support, WebRTC integration, Teams/Zoom/Slack APIs
• 15-Factor: OpenTelemetry, mTLS, HMAC auth, API-first (OpenAPI 3.0), comprehensive telemetry
• Other: pre-commit, Warp terminal (enhanced workflows), GitHub Actions (path-filtered + enhanced)

Database Support Matrix (ADR-001 Enhanced)
• Postgres 15/16: fully supported (WAL LSN anchoring, native guards, replay support)
• Postgres 13/14: demo/pilot only (best-effort) — production requires --allow-best-effort flag
• Snowflake: QUERY_HISTORY anchoring, session tags, stored procedures, resource monitors (full support)
• Databricks: Delta Lake commits, Unity Catalog lineage, cluster policies, macro helpers (full support)
• BigQuery: job metadata anchoring, schema validation (Phase 1.5)

Warehouse Integration Policy:
• Session-level enforcement via tags (Snowflake) or metadata (Databricks)
• Stored procedures for approval token validation
• Query history correlation for lineage tracking
• Resource monitor integration for kill-switch capabilities

⸻

Scope (MVP v4.0 - All Locked)

In Scope (Data Platform Core):
• dbt Integration: hooks (pre/post-run), macros (SQL safety), CI gates, semantic delta detection, model lineage
• Warehouse Anchors: Snowflake (QUERY_HISTORY + session tags), Databricks (Delta commits + Unity Catalog), Postgres (WAL LSN)
• DEF v0 bundles: Data Evidence Format with warehouse-native anchoring, metadata-only snapshots, deterministic replay
• Activation Gateway: HTTP proxy for Hightouch/Census/RudderStack with enforcement primitives + rate limits + tenant fences
• SQL Safety Guards: advisory blocks on mass UPDATE/DELETE, rows_affected limits, allowlist maintenance routes
• SOX ITGC Compliance: change control enforcement, segregation of duties, approval tracking, audit trail completeness

In Scope (GenAI Security Hardening):
• Threat Detection Framework: OWASP LLM Top 10 v1.1 mapping, built-in prompt injection heuristics, external deepfake APIs
• BEC-Grade Approvals: SSO binding (sso_sub + idp_domain), challenge-response, payload hash binding (RFC 8785), MFA flags
• Kill-Switch Evolution: multi-trigger (data + GenAI + universal), TTL recovery, HITL override, threshold monitoring
• Shadow Mode Enhancement: parallel policy evaluation, comprehensive logging, SIEM forwarding, zero enforcement impact
• Prompt Delta Tracking: sanitized hash changes for injection drift detection, no body storage
• External Detector Integration: vendor-agnostic HTTP APIs, timeout/fallback, confidence thresholds

In Scope (Voice/Conversation Compliance):
• TCPA Compliance: disclaimer enforcement, consent tracking, opt-out mechanisms, time restrictions (8AM-9PM local)
• Voice Session Management: unique session IDs, metadata-only capture, correlation with API actions
• UCaaS Integration: Teams/Zoom/Slack/Twilio correlation, SIP gateway support, WebRTC handling
• Barge-in Capability: human interruption <200ms response, quality metrics, acknowledgment tracking
• Privacy Preservation: no audio storage, waveform analysis only, hashed correlation IDs

In Scope (Enhanced Universal Foundation):
• Postgres 15/16 + Snowflake + Databricks; Gateway (SchemaLock + Data Firewall); enhanced Recorder
• DEF v0 + PEF v0 unified bundles: canonical JSON, Merkle roots, signatures, governance metadata, performance/security metrics
• Enhanced policy.yaml: data_platform + genai_security + voice_compliance + enforcement + compliance sections
• Enhanced enforcement primitives: BEC-grade approvals, prompt-loop breakers, voice session fences, CI/CD controls
• Multi-framework compliance: SOX ITGC + PCI/HIPAA + EU AI Act/NIST + TCPA with independent verification

In Scope (CLI & Integration):
• Enhanced CLI: data platform commands (dbt, warehouse, activation), GenAI security commands, voice compliance commands
• Enhanced SDK: Python with dbt helpers + warehouse integration + GenAI security + voice compliance
• TypeScript SDK: Phase 1.5 for broader automation ecosystem
• Enhanced Scenario Packs: Data platform demos, GenAI-hardened automation, industry service packs
• Enhanced Procurement Kit: multi-track evidence samples, compliance mapping, auditor guidance
• CI/CD Integration: GitHub Actions with evidence verification, policy gates, SOX compliance tracking
• 15-Factor Compliance: API-first design, comprehensive telemetry, enhanced authentication

Out of Scope (Deferred to Phase 1.5+):
• Content governance (email, CMS, publishing workflows)
• Non-Postgres databases beyond Snowflake/Databricks (MySQL, Oracle, etc.)
• SaaS control plane UI/dashboard (CLI + API-first in MVP)
• Packaged SIEM dashboards (saved searches + correlation rules in MVP)
• WASM detector sandbox & marketplace
• Advanced rollback orchestration with state management
• Full lineage UI/catalog features (integrate, don't rebuild)

⸻

Key Commands / Workflows (v4.0 Enhanced)

Data Platform Workflows:
• make quickstart-data — Docker Compose: Gateway + Recorder + Snowflake simulator + dbt project
• clyra dbt init my-project — initialize dbt project with Clyra hooks and macros
• clyra warehouse doctor --platform snowflake — check connectivity, permissions, session tag support
• clyra activation gateway --port 8080 — start reverse-ETL proxy with enforcement
• clyra demo data --platform snowflake — generate DEF bundles from warehouse operations

Universal Workflows (Enhanced):
• make quickstart — Docker Compose: enhanced stack with data platform examples
• make test / make test-comprehensive — Go/Py/TS tests with data platform + GenAI coverage
• make verify-vectors — run enhanced Go & TS verifiers on DEF/PEF golden bundles
• clyra demo contracts|etl|data — generate evidence with GenAI security hardening

GenAI Security Workflows:
• clyra genai test --attack-vectors prompt-injection,deepfake — test threat detectors
• clyra bec validate --certificate-path ./approvals/ — validate BEC-grade approval certificates
• clyra threats analyze evidence.zip — analyze GenAI threat patterns in bundles
• clyra policy wizard --template genai-security — interactive GenAI security policy creation

Voice/Conversation Workflows:
• clyra voice session --correlation-id <id> — manage voice session tracking
• clyra voice compliance --check-disclaimers — validate TCPA disclaimer compliance
• clyra voice correlate --ucaas teams --session-id <id> — correlate UCaaS sessions with actions

Enhanced Universal Workflows:
• clyra verify evidence.zip --explain --validate-lineage — enhanced verification with data lineage
• clyra replay --platform snowflake --scratch-schema clyra_replay — data-aware deterministic replay
• clyra attest evidence.zip --framework sox|pci|hipaa|eu-ai-act|nist-rmf|tcpa — multi-framework attestation
• clyra report --daily-review --include-genai --include-data-changes — enhanced daily review

Enhanced Warp Workflows (in .warp/workflows.yaml):
• quickstart-data: enhanced data platform quickstart
• test-comprehensive: full test suite with data + GenAI + voice coverage
• genai-security-test: GenAI threat detection testing
• voice-compliance-test: voice compliance validation
• warehouse-doctor: multi-platform warehouse health checks
• sox-compliance-check: SOX ITGC compliance validation
• k6-comprehensive: performance testing across all components
• zap-enhanced: security scanning with GenAI attack vectors
• verify-cross-platform: cross-verifier consistency testing
• attest-multi-framework: multi-framework attestation generation
• daily-review-enhanced: comprehensive daily review with all components

Enhanced GitHub Actions:
• data-platform-ci.yml: dbt integration, warehouse connectivity, DEF bundle validation
• genai-security-ci.yml: threat detection testing, BEC approval validation, external detector simulation
• voice-compliance-ci.yml: TCPA compliance, UCaaS integration, session management validation
• sox-compliance-gate.yml: SOX ITGC change control validation, segregation of duties checking
• cross-verifier-consistency.yml: ensure Go/TS verifiers produce identical results
• performance-comprehensive.yml: enhanced performance testing across all components
• traceability-enhanced.yml: enhanced traceability with data platform + GenAI coverage
• policy-contract-v4.yml: validate policies against enhanced v4.0 schemas
• perf-budgets-enhanced.yml: comprehensive performance budget validation
• procurement-kit-comprehensive.yml: multi-track procurement kit validation
• nightly-audit-enhanced.yml: comprehensive nightly audit with all frameworks

10-Minute PLG Path (Day-1 Enhanced)

Data Platform Track (Primary):

1) clyra dbt init demo-project → dbt project with Clyra hooks
2) make quickstart-data → local stack with Snowflake simulator
3) clyra demo data → DEF bundle generation from warehouse operations
4) clyra warehouse doctor → validate warehouse integration
5) clyra activation gateway → start enforcement proxy
6) clyra verify evidence.zip --validate-lineage → independent verification with lineage
7) clyra attest evidence.zip --framework sox → signed SOX ITGC attestation
8) clyra report --daily-review --include-data-changes → enhanced daily review

Universal Track (Strategic):

1) clyra init --template comprehensive → enhanced policy with all components
2) make quickstart → enhanced local stack
3) clyra demo contracts --with-genai-security → GenAI-hardened automation evidence
4) clyra genai test → validate threat detection capabilities
5) clyra verify evidence.zip --explain → comprehensive verification
6) clyra replay --enhanced → deterministic replay with data support
7) clyra attest evidence.zip --framework pci → multi-framework attestation
8) clyra report --daily-review --include-genai → comprehensive threat posture review

Enhanced Runtime Flows :

Listen-Only → Review → Gate Flow:
dbt Cloud Webhook → Clyra Review (listen-only) → Evidence Bundle → ServiceNow Ticket
→ Daily Review + Badge Issuance → Customer Trust Built
→ [Customer requests enforcement] → Enable Clyra Gate → Full Policy Active

ServiceNow Integration Flow:
Evidence Bundle → Ticket Formatter → ServiceNow REST API
→ Change Ticket with: attestation hash, verification link, compliance status
→ Auditor views → Clicks verify → Independent verification

Badge Issuance Flow:
dbt run completes → Clyra validates → Badge Service signs JWT
→ Badge endpoint: clyra.io/badge/{framework}/{project-id}
→ README displays → GitHub renders → Viral growth

Data Platform Enforcement Flow:
dbt Run → Hooks (pre/post) → Schema Change → Warehouse Guards → Approval Token Check → Session Tags → DEF Bundle → SOX Attestation

Universal Enforcement Flow (Enhanced):
Agent/Data Change → Gateway (JSON validation + data awareness + GenAI threats + voice session tracking) →
Enforcement Primitives (idempotency + BEC-grade approvals + velocity + fences + SQL safety + prompt-loop breaker) →
Recorder (HMAC verify + metadata snapshots + warehouse anchoring + diff) →
Enhanced Bundle (DEF/PEF + governance metadata + performance metrics)

GenAI Security Flow:
Request → Prompt Analysis (injection detection + delta tracking) → External Detectors (deepfake + BEC classification) →
BEC-Grade Approval Check (SSO binding + challenge validation) → Kill-Switch Evaluation (multi-trigger) →
Enhanced Receipt (threat classification + OWASP LLM + MITRE ATT&CK)

Voice Compliance Flow:
Voice Session → Disclaimer Check (TCPA requirements) → Session Correlation (UCaaS integration) →
Barge-in Window → API Action → Audit Trail (voice-to-action correlation + privacy preservation)

HITL Approval Cert Flow (BEC-Grade):
Approver (Slack/CLI + SSO) → Challenge-Response → BEC-Grade Cert (payload hash + SSO sub + IdP + challenge + expiry, signed) →
Gateway Validation (one-time use + crypto verification) → Policy Enforcement

⸻

Repository Structure & Architecture (v4.0)

Enhanced Component Boundaries :

ServiceNow/Jira Bridge Layer:
• bridges/servicenow/: REST client, ticket formatter, OSS export script
• bridges/jira/: Atlassian SDK, issue formatter, OSS export script
• internal/badge/: certification service, JWT signing, project registry, CDN cache

Review/Gate SKU Separation:
• internal/review/: webhook listeners, daily review generation, attestation
• internal/gate/: policy enforcement, primitives, enforcement templates
• cmd/clyra/review/: listen-only commands
• cmd/clyra/gate/: enforcement commands

Data Platform Layer:
• internal/warehouse/: Snowflake/Databricks/Postgres anchoring, native guards, lineage extraction
• internal/dbt/: hooks implementation, macro generation, CI gate integration, metadata capture
• internal/activation/: reverse-ETL proxy, enforcement integration, SaaS API protection
• sdk/python/dbt/: dbt helper utilities, SQL macro generation, metadata extraction

GenAI Security Layer:
• internal/genai/: threat detection, BEC prevention, external detector integration, shadow mode
• internal/genai/detectors/: prompt injection heuristics, deepfake correlation, custom detector framework
• internal/genai/threats/: OWASP LLM mapping, MITRE ATT&CK correlation, threat response automation

Voice/Conversation Layer:
• internal/voice/: session management, TCPA compliance, UCaaS integration, privacy preservation
• internal/voice/compliance/: disclaimer enforcement, consent tracking, opt-out mechanisms
• internal/voice/correlation/: session-to-action correlation, partner system integration

Enhanced Universal Foundation:
• internal/proxy/: enhanced with data awareness, GenAI threat detection, voice session tracking
• internal/recorder/: enhanced with warehouse anchoring, metadata-only snapshots, data replay
• internal/bundle/: unified DEF/PEF builder, governance metadata embedding, multi-format support
• internal/policy/: enhanced with data platform + GenAI + voice sections, shadow mode promotion

Enhanced Enforcement:
• internal/enforcement/: BEC-grade approvals, prompt-loop breakers, voice session fences, CI/CD controls
• internal/killswitch/: multi-trigger system (data + GenAI + universal), recovery mechanisms
• internal/shadow/: parallel policy evaluation, comprehensive logging, verdict correlation

CI/CD & Operations:
• internal/cicd/: GitHub Actions integration, commit SHA binding, SOX ITGC tracking, deploy controls
• internal/telemetry/: 15-Factor telemetry, OpenTelemetry integration, correlation ID management
• internal/siem/: enhanced ECS/OCSF NDJSON, cross-system correlation, GenAI threat indicators

Quality Attributes (v4.0):

15-Factor App Compliance:
• API First (13): OpenAPI 3.0 specs for all components, RESTful design, service interoperability
• Telemetry (14): comprehensive metrics (business + security + performance), OpenTelemetry standard
• Authentication (15): mTLS inter-service, HMAC requests, SSO integration, BEC-grade approvals

Performance SLAs (Enhanced):
• Data Platform: dbt hook execution <2s, warehouse queries <5s, activation proxy <15ms p95
• GenAI Security: prompt analysis <100ms, external detectors <500ms with fallback, kill-switch <1s
• Voice Compliance: session correlation <5ms, disclaimer validation <10ms, barge-in response <200ms
• Universal: Gateway ≤15ms p95 (+3ms enforcement), Recorder ≤20ms p95, evidence bundles <5s DEF/<3s PEF

Security Model (Enhanced):
• Zero-trust architecture: every component authenticated, encrypted in transit
• GenAI threat hardening: comprehensive attack vector coverage, proactive detection
• BEC-grade security: SSO binding, challenge-response, cryptographic payload binding
• Privacy-by-design: metadata-only capture, explicit opt-in for bodies, redaction mandatory

⸻

Testing & Quality Assurance (v4.0)

Enhanced Test Coverage:

Data Platform Testing:
• dbt integration: hook execution, macro validation, CI gate testing, semantic delta detection
• Warehouse integration: connectivity, anchoring, guard procedures, lineage extraction
• Activation gateway: enforcement integration, rate limiting, tenant isolation, SaaS protection
• DEF bundle validation: format compliance, anchor verification, independent verification

GenAI Security Testing:
• Threat detection: prompt injection vectors, deepfake simulation, BEC attack scenarios
• External detector integration: API mocking, timeout handling, fallback mechanisms
• Kill-switch validation: multi-trigger scenarios, recovery procedures, threshold tuning
• Shadow mode validation: parallel evaluation, verdict logging, zero-impact verification

Voice Compliance Testing:
• TCPA compliance: disclaimer enforcement, consent tracking, opt-out mechanisms
• Session management: correlation accuracy, privacy preservation, metadata capture
• UCaaS integration: Teams/Zoom/Slack correlation, SIP gateway testing, WebRTC handling
• Barge-in capability: response time validation, quality metrics, acknowledgment tracking

Enhanced Universal Testing:
• Cross-verifier consistency: Go/TS verifier result matching across DEF/PEF formats
• Performance validation: comprehensive SLA testing, regression detection, capacity limits
• Security penetration: enhanced attack scenarios, GenAI-specific vectors, voice attack simulation
• Compliance validation: multi-framework attestation testing, auditor procedure simulation

Golden Vector Enhancement:
• DEF vectors: warehouse-anchored evidence, data lineage validation, SOX compliance scenarios
• PEF vectors: GenAI-hardened automation, voice compliance scenarios, BEC prevention validation
• Cross-platform vectors: database compatibility, cloud provider variations, SDK consistency
• Compliance vectors: framework-specific evidence, attestation validation, auditor acceptance

⸻

Compliance & Governance (v4.0 Enhanced)

Multi-Framework Support:

SOX ITGC (Data Platform Focus):
• Change control: dbt model changes, schema migrations, activation sync approvals
• Segregation of duties: separate development/approval/deployment roles, automated tracking
• Access management: warehouse permissions, approval certificate tracking, role-based controls
• Monitoring: automated daily reviews, data change anomalies, approval usage analytics

PCI DSS (Enhanced):
• Req-10 (Logging): enhanced daily review with data changes + GenAI threat posture
• Req-6 (Development): dbt CI/CD integration, secure development practices, vulnerability scanning
• Req-8 (Access): BEC-grade approval certificates, session correlation, multi-factor enforcement
• Req-11 (Testing): automated security testing, vulnerability assessment, penetration validation

HIPAA (Privacy-Enhanced):
• §164.308 (Administrative): policy automation, comprehensive audit trails, access control evidence
• §164.312 (Technical): integrity safeguards, voice session privacy, data minimization enforcement
• §164.314 (Organizational): business associate compliance, third-party integration controls
• Voice compliance: TCPA integration, consent management, privacy preservation

EU AI Act Art. 12 (Record-Keeping Enhanced):
• High-risk AI systems: comprehensive evidence generation, lineage tracking, decision audit trails
• Transparency obligations: algorithmic decision documentation, explainability requirements
• Risk management: threat classification, mitigation evidence, continuous monitoring
• Human oversight: HITL approval workflows, human-AI interaction logs, override tracking

NIST AI RMF (Risk Management Enhanced):
• Govern: policy-as-code, governance metadata embedding, oversight mechanism documentation
• Map: threat classification, risk categorization, OWASP LLM + MITRE ATT&CK mapping
• Measure: performance metrics, bias detection, fairness assessment, threat detection accuracy
• Manage: incident response, continuous monitoring, automated remediation, kill-switch activation

TCPA (Voice/Conversation Compliance):
• Consent requirements: opt-in documentation, disclaimer enforcement, acknowledgment tracking
• Call recording: session metadata capture, privacy preservation, audit trail completeness
• Automation rules: voice agent identification, human transfer capabilities, barge-in rights
• Time restrictions: local time enforcement, compliance validation, violation prevention

Evidence Requirements (Enhanced):
• Retention: HIPAA (≥6 years), PCI DSS (≥12 months hot + archive), EU AI Act (operational lifetime)
• Integrity: cryptographic signing, tamper-evident storage, hash chain validation
• Portability: vendor-neutral formats, independent verification, auditor-friendly structure
• Completeness: comprehensive audit trails, governance metadata, correlation evidence

⸻

Performance & Reliability (v4.0)

Enhanced SLA Matrix:

Data Platform Performance:
• dbt hook execution: <2s overhead per run, memory <100MB footprint
• Warehouse policy queries: <5s response time, <1% query performance overhead
• Activation gateway proxy: <15ms p95 latency, >1K req/s throughput per replica
• DEF bundle generation: schema analysis <3s, bundle creation <5s, verification <1s

GenAI Security Performance:
• Prompt injection analysis: <100ms built-in detectors, <50ms for common patterns
• External detector APIs: <500ms with timeout/fallback, graceful degradation on failure
• BEC certificate validation: <10ms cryptographic verification, <1ms in-memory lookup
• Kill-switch evaluation: <1s from trigger detection to enforcement action

Voice Compliance Performance:
• Session correlation: <5ms voice-to-action correlation, metadata capture <2ms
• Disclaimer validation: <10ms compliance checking, <1ms cache lookup
• UCaaS integration: <100ms partner system correlation, <50ms webhook processing
• Barge-in response: <200ms human interruption capability, quality metrics <5ms

Universal Foundation Performance:
• Gateway: ≤15ms p95 baseline, +3ms with comprehensive enforcement primitives
• Recorder: ≤20ms p95 with metadata snapshots, WAL LSN anchoring <5ms overhead
• Enhanced replay: ≤2× baseline performance for deterministic reproduction
• Evidence bundles: <5s DEF creation, <3s PEF creation, unified verification <1s

Reliability & Resilience:

Fail-Closed Architecture:
• Data platform: schema changes blocked on policy violations, activation syncs require approval
• GenAI security: suspicious requests blocked, external detector failures trigger safe mode
• Voice compliance: sessions without disclaimers blocked, barge-in failures logged
• Universal: enforcement primitive failures result in blocked operations, comprehensive logging

Circuit Breaker Patterns:
• External dependencies: warehouse connectivity, external detector APIs, UCaaS integrations
• Performance degradation: automatic fallback to cached results, simplified enforcement
• Cascade failure prevention: bounded queues, graceful degradation, independent component failure

Back-Pressure Management:
• Queue depth monitoring: 503 responses on overflow, priority-based processing
• Rate limiting: per-tenant/actor limits, burst protection, fair resource allocation
• Resource management: memory bounds, connection pooling, CPU utilization monitoring

⸻

Deployment & Operations (v4.0)

Enhanced Deployment Patterns:

Development Environment:
• Enhanced Docker Compose: Gateway + Recorder + warehouse simulators + sample apps
• Data platform simulation: local Snowflake/Databricks environments, dbt project examples
• GenAI security testing: mock external detectors, attack vector simulation, threat correlation
• Voice compliance testing: mock UCaaS integrations, session simulation, disclaimer validation

Production Topologies:

15-Factor Deployment:
• API First: all services expose OpenAPI 3.0 specs, RESTful design, service mesh integration
• Telemetry: comprehensive OpenTelemetry integration, business/security/performance metrics
• Authentication: mTLS inter-service, HMAC request auth, SSO integration, identity binding

Data Platform Deployment:
• dbt Cloud integration: hooks via dbt packages, centralized policy management, CI/CD gates
• Warehouse-native deployment: stored procedures, session tag enforcement, resource monitoring
• Activation layer deployment: HTTP proxy with horizontal scaling, tenant isolation, rate limiting

Cloud-Native Patterns:
• Kubernetes: Helm charts with comprehensive configuration, resource limits, security contexts
• Service mesh: Istio/Envoy integration, traffic management, security policies, observability
• GitOps: infrastructure and policy changes through Git, automated deployment, rollback capabilities

High Availability:
• Gateway: stateless horizontal scaling, auto-scaling based on latency SLAs, load balancing
• Recorder: leader election with automatic failover, health checks, state replication
• Data dependencies: connection pooling, circuit breakers, multi-region support

Operational Excellence:

Monitoring & Alerting:
• SLI/SLO definitions: comprehensive service level indicators, error budgets, alerting thresholds
• Health checks: deep health validation, dependency checking, performance validation
• Incident response: automated escalation, runbook integration, recovery procedures

Key Rotation & Security:
• Automated key rotation: KMS integration, zero-downtime transitions, comprehensive validation
• Certificate management: automatic renewal, validation, secure distribution
• Security scanning: continuous vulnerability assessment, dependency updates, compliance validation

⸻

Developer Experience (v4.0)

Enhanced Developer Tooling:

CLI Completeness:
• Review SKU commands: webhook setup, ServiceNow/Jira export, badge management
• Gate SKU commands: enforcement enable, policy promotion, primitive configuration
• Data platform commands: comprehensive dbt integration, warehouse management, activation control
• GenAI security commands: threat testing, detector validation, attack simulation
• Voice compliance commands: session management, compliance validation, correlation tracking
• Enhanced universal commands: multi-format verification, cross-platform replay, comprehensive attestation

SDK Enhancement:
• Python SDK: comprehensive data platform integration, dbt helpers, warehouse utilities, GenAI security
• TypeScript SDK: automation-focused, comprehensive type definitions, framework integration
• Documentation: comprehensive examples, integration patterns, best practices, troubleshooting

Integration Patterns:
• Framework integration: comprehensive examples for popular frameworks, best practices, performance optimization
• CI/CD integration: GitHub Actions, GitLab CI, Jenkins support, policy gates, evidence verification
• Cloud platform integration: AWS/Azure/GCP deployment patterns, managed service integration

Testing Framework:
• Golden vector testing: comprehensive test coverage, cross-verifier validation, regression detection
• Integration testing: end-to-end scenarios, performance validation, security testing
• Property-based testing: canonicalization validation, edge case coverage, stress testing

Documentation Excellence:
• Comprehensive guides: step-by-step tutorials, integration examples, troubleshooting procedures
• API documentation: OpenAPI specifications, SDK references, example implementations
• Compliance guidance: framework mappings, auditor procedures, evidence validation

⸻

Strategic Roadmap (Post-MVP)

Phase 1.5 (Data Platform Expansion):
• Enhanced warehouse support: BigQuery anchoring, additional cloud variants, advanced lineage
• Advanced dbt features: semantic layer integration, advanced testing, performance optimization
• Prefect/Dagster operators: broader pipeline ecosystem coverage, comprehensive integration
• TypeScript SDK completion: full feature parity, comprehensive automation support

Phase 2 (Platform Maturation):
• Self-hosted control plane: enterprise deployment, comprehensive management, multi-tenancy
• Advanced compliance packs: industry-specific frameworks, regulatory compliance, audit automation
• UI/dashboard development: non-technical stakeholder interfaces, management reporting
• Advanced GenAI security: custom model integration, advanced threat detection, ML-based analysis

Phase 3 (Strategic Expansion):
• Content governance: email/CMS/publishing workflows, content compliance, editorial controls
• Advanced rollback orchestration: state management, automated recovery, dependency resolution
• SaaS delivery model: multi-tenant platform, managed infrastructure, enterprise features
• Marketplace ecosystem: detector marketplace, policy templates, community contributions

Commercial Targets (12-Month):
• Review SKU adoption: ≥10 customers on Review SKU within 6 months via listen-only start
• ServiceNow/Jira integration: ≥5 enterprises using attested change tickets in production
• Badge program success: ≥100 dbt projects displaying Clyra Certified badges
• Upsell metrics: ≥30% Review → Gate conversion within 90 days
• Revenue generation: $300-600k ARR (70% Review, 30% Gate initial mix)
• Audit partner success: ≥2 Big 4 firms acknowledge evidence format

Success Metrics (Enhanced with):
• Technical: all performance SLAs met, >99% evidence bundle verification success, <0.1% false positive rate
• Adoption: <30 min from webhook setup to first ServiceNow ticket
• Viral growth: >50% badge adopters refer at least one new project
• Business: >50% create second bundle within 14 days, proven ROI in audit time savings
• Strategic: DEF/PEF referenced by competitors/standards bodies, integration partnerships established
• Operational: zero critical vulnerabilities, comprehensive security posture, audit readiness maintained

⸻

Risk Mitigation (v4.0)

Technical Risks & Mitigations:
• Data platform complexity → phased rollout, comprehensive testing, customer co-development
• GenAI false positives → shadow mode defaults, tunable thresholds, customer feedback loops
• Performance impact → strict SLA enforcement, continuous monitoring, optimization priorities
• Integration challenges → comprehensive examples, partner collaboration, incremental adoption

Market Risks & Mitigations:
• Message confusion → "Data Change Control & Attestation" is clear, maps to budgets
• dbt/Snowflake build competing features → partner positioning, independent verifier moat, auditor network
• Enterprise integration friction → ServiceNow/Jira bridges, listen-only start, badge social proof
• Competitive response → patent core algorithms, community building, independence emphasis
• Scope creep → strict MVP enforcement, "integrate don't rebuild" philosophy, customer focus

Operational Risks & Mitigations:
• Compliance burden → automated validation, comprehensive documentation, auditor collaboration
• Security vulnerabilities → continuous scanning, rapid response, transparent communication
• Performance regression → continuous monitoring, automated detection, rollback procedures

Strategic Mitigations:
• Customer co-development: design partners for each major use case, continuous feedback integration
• Community building: open source approach, independent verifier ecosystem, transparent development
• Technical excellence: comprehensive testing, security-first design, performance optimization
• Market positioning: clear differentiation, concrete value delivery, measurable outcomes

⸻

End of CLAUDE.md v4.0