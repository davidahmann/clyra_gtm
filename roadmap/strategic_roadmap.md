# Clyra Vision — Trust Fabric for the Data and AI Economy

Tagline: Safe today, settlement tomorrow. If it’s not provable, it doesn’t exist.

Version: v4.0 (central, living document)
Last updated: 2025-10-04
Owners: Product, Architecture, Compliance, Developer Experience

Purpose

- This is the single source of truth for Clyra’s strategy, product line, shared platform, sequencing, SLAs, and go-to-market. When implementation details conflict across docs, this document takes precedence. Update it as a first-class artifact.

------------------------------------------------------------

1) North Star and Guiding Principles

North Star
Clyra ensures every data or agent change is safe and audit-ready today, and becomes the trusted system to pay people, vendors, and AI agents based on verified results tomorrow.

Guiding Principles

- Data-led, agent-ready: Land with dbt/warehouses (clear budget, deadlines), keep architecture ready for agents (MCP) using the same evidence and enforcement core.
- Evidence before money: Signed, portable DEF/PEF proof precedes attribution; attribution precedes billing.
- Progressive adoption: Review (listen-only) → Gate (enforcement) → Attribution → Billing.
- Independence as moat: Portable formats and independent verifiers auditors can run offline.
- Privacy-by-default: Metadata-only capture; redaction mandatory on opt-in body storage; WORM retention guidance.
- Performance first: Strict SLAs, continuous perf testing, and failure isolation.

------------------------------------------------------------

2) Product Line — SKUs and Brand Mapping (Pre–Horizon 2)

Naming and brand architecture

- Guard Engine: The named enforcement core used across SKUs (AI Firewall + SchemaLock + Approval Certificates + kill-switch + enforcement primitives). “Powered by Guard” is used under Gate/Voice/Airlock.
- DEF/PEF Evidence Spine: The shared evidence architecture (Recorder, Replay, Bundle Builder, Verifiers) for all SKUs.
- CLI: Single namespace — clyra <verb> <track>. Marketing uses product brands (e.g., “Visus by Clyra”); developers use descriptive CLI subcommands.

SKU 1 — Clyra Visus (Review — Data Platform)
Value

- Fast, zero-disruption proof of SOX change control for dbt + warehouses with independent verification. Drives virality via badges and shareable verification links.
Capabilities
- dbt hooks/macros; DEF v0 bundles; anchors: Snowflake (QUERY_HISTORY + session tags), Postgres (WAL LSN). BigQuery fast-follow (Months 3–6); Databricks compatible (Months 6–9).
- Attested change tickets (ServiceNow/Jira); Daily Review (PCI Req-10).
- AI Firewall + GenAI Defense in shadow (observe, don’t block). Replay (data/DEF) with signed Replay Certificates.
- Independent Verifiers (Go primary, TS secondary) for offline auditor checks.
Personas & JTBD
- Analytics engineers / data platform leads: “Prove changes and stay safe without disruption.”
- Controllers/SOX PMO: “Get attested tickets and evidence for quarter-end.”
- Auditors/SIs: “Verify offline without trusting vendor binaries.”
KPIs & Acceptance
- First attested ticket ≤2 weeks; dbt hook <2s; Gateway ≤15ms p95; Recorder ≤20ms p95; >99% verification success; 3 design partners; 1 paid pilot.
CLI (examples)
- clyra review init — setup listen-only hooks/webhooks
- clyra review generate --servicenow — produce attested change ticket
- clyra verify evidence.zip --explain — independent verification
- clyra report --daily-review — PCI Req-10 rollup

SKU 2 — Clyra Lumyn (Verify Portal — Free)
Value

- One-click public verification pages and Slack/PR comments turn evidence into shareable proof; top-of-funnel for Review/Gate.
Capabilities
- Hosted verify pages/links; Slack/Teams unfurls; GitHub PR comments; receipt cards for Notion/Confluence; badges service (JWT) and procurement kit alignment.
- Uses independent Go/TS verifiers for offline parity.
Personas & JTBD
- Developers, leads, auditors: “Share and prove receipts where we work (Slack/PRs/wikis).”
KPIs & Acceptance
- Public verify load <1s; ≥30% sharing rate; ≥0.4 viral coefficient; ≥1K monthly verify clicks; ≥10 Slack bot installs by Month 6.
CLI (examples)
- clyra verify evidence.zip
- clyra share evidence.zip

SKU 3 — Clyra Gate (Data Platform Enforcement) — powered by Guard
Value

- Prevent unsafe changes with cryptographically provable approvals and policy controls. Measurable incident reduction and SOX/PCI evidence on every decision.
Capabilities (AI Firewall = SchemaLock + primitives)
- Enforce: allow/deny/HITL, idempotency, velocity guards, tenant/actor fences, SQL safety (advisory), multi-trigger kill-switch (<1s).
- BEC-grade Approval Certificates (RFC 8785 payload binding; SSO/MFA/nonce; short TTL; one-time use).
- Two-way ServiceNow/Jira approvals; CI/CD gates (commit binding, deploy rate limits).
- Replay for pre-prod checks and incident forensics.
Personas & JTBD
- SRE/Sec/data teams: “Block bad changes with low latency and prove why decisions were made.”
- Auditors: “See cryptographic approvals and control rationale.”
KPIs & Acceptance
- +≤3ms overhead with full enforcement; kill-switch drills 100% pass; ≥30% Review→Gate conversion in 90 days.
CLI (examples)
- clyra gate enable --policy policy.yaml
- clyra bec validate --certificate-path ./approvals/
- clyra policy lint --strict --frameworks sox,pci,hipaa

SKU 4 — Clyra Atlas (Attribution — Outcome Ledger + Certificates)
Value

- Evidence-backed ROI: map verified changes to business metrics; prepares finance and auditors for billing later (no money movement).
Capabilities
- Append-only Outcome Ledger; deterministic linkage (last-touch/time-decay v0) from DEF/PEF runs to metric observations.
- Signed Attribution Certificates referencing DEF/PEF + Replay Certificates;
- Shadow billing simulations and exports (CSV/JSON).
Personas & JTBD
- Finance/ops, product/data leaders: “Show what changed and the measured impact with proof.”
- Auditors: “Trace outcomes to signed evidence.”
KPIs & Acceptance
- 2+ customers using Attribution Certificates in QBRs; ≥1 public case study; zero methodology disputes.
CLI (examples)
- clyra attribution issue --from evidence.zip --metric <id>
- clyra attribution simulate --policy pricing.yaml

SKU 5 — Clyra Voice (Conversation Compliance — Pilot)
Value

- Provable TCPA/consent compliance and voice-to-action correlation without audio storage; operational safety (barge-in <200ms).
Capabilities
- Session IDs; disclaimer enforcement; UCaaS correlation (Teams/Zoom/Slack/Twilio); Daily Review metrics; barge-in <200ms.
- Uses Guard and GenAI Defense (shadow→ enforce).
Personas & JTBD
- Contact center ops, compliance, platform/security: “Meet TCPA with proof and minimal risk.”
KPIs & Acceptance
- Disclaimer check <10ms; correlation <5ms; barge-in <200ms; 1–2 pilots prior to GA.
CLI (examples)
- clyra voice session --correlation-id <id>
- clyra voice compliance --check-disclaimers

SKU 6 — Clyra Relia (Semantics — Open Control Plane, OSS-first)
Value

- “Define once, enforce everywhere” for metrics and access with signed decision receipts; reduce drift and audit exceptions.
Capabilities
- semantics.yaml + policy.yaml compiled to native artifacts: Snowflake DDM/RAP, Unity views/UDFs, Trino filters; identity bridge.
- Read-only “semantic API” for agents; verifiable decision receipts.
Personas & JTBD
- CDO/CISO/data platform; auditors; AI teams: “Consistent semantics/policies and proof of enforcement across engines.”
KPIs & Acceptance
- Demo parity across two engines; receipts verify offline; OSS adoption indicators (stars/contribs).
CLI (examples)
- clyra semantics compile --engine snowflake --out artifacts/
- clyra semantics verify --receipt decision.json

SKU 7 — Clyra Airlock (MCP — Conditional)
Value

- Zero standing credentials for agents; cross-firewall access; portable receipts; same enforcement/evidence as data flows.
Capabilities
- MCP proxy (dry-run → enforce), OAuth Token Exchange (RFC 8693), DPoP, reverse tunnel, signed allowlists, HITL on mutating ops.
- PEF v0 with MCP extension; Guard + GenAI Defense (shadow → enforce). Replay default for MCP receipts.
Activation Gate
- Start only if ANY: ≥2 existing customers request MCP; MCP ≥10k stars + 3 major platforms; notable incidents; or competitive move.
Personas & JTBD
- Platform/AI teams, security/identity, auditors: “Safely broker agent→tool access with verifiable controls.”
KPIs & Acceptance
- TTFSC <60 min; 0 standing creds; ≥90% receipt coverage; $100–200k incremental ARR.
CLI (examples)
- clyra airlock login | allow | verify | tunnel status

------------------------------------------------------------

3) Shared Clyra Platform — Common Plane for All SKUs

Evidence and Replay Backbone

- Recorder (Flight Data Recorder): HMAC capture; metadata-only snapshots; warehouse anchors (Snowflake QUERY_HISTORY + session tags; Databricks Delta commits/Unity Catalog; Postgres WAL LSN).
- Replay Engine: Deterministic sandbox (“scratch schema” for data) and signed Replay Certificates; simulation-only for third-party side effects.
- Bundle Builder: Canonical DEF v0 (data) and PEF v0 (automation) with Merkle roots, governance/perf metrics; PEF MCP extension (optional) and optional C2PA extension for generated assets (consent/likeness provenance).
- Independent Verifiers: Go (primary) and TypeScript (secondary) with cross-verifier consistency. Offline verification for auditors; GitHub Action support.
- Snapshot & Diff Engine (part of Recorder):
  - Capabilities: REPEATABLE READ isolation; metadata-only snapshots (no PITR); DSN hashed; replicas rejected; deterministic diffs with stable ordering; policy-driven snapshot coverage; anchor correlation for lineage; deterministic schema and row delta comparison.
  - Anchors: Postgres WAL LSN; Snowflake QUERY_HISTORY + session tags; Databricks Delta commits + Unity Catalog.
  - Failure codes: PRE_FAIL | LSN_MISSING | POST_TIMEOUT | REPLICA_LAG | POLICY_SKIP (emitted in receipts and Daily Review).
  - SLAs: Snapshot ≤50ms on ≤100 tables; Recorder ≤20ms p95; snapshot lag and completeness tracked; Replay runtime ≤2× baseline.
  - Observability: OpenTelemetry metrics (clyra.recorder.snapshot_duration_seconds, clyra.bundle.generation_duration_seconds), snapshot_lag_seconds, anchors_captured_total; ECS/OCSF NDJSON events for SIEM; success/failure counters per anchor type.
  - CLI and ops: Exercised via clyra replay, clyra report --daily-review, internal recorder operations; validated with clyra warehouse doctor (WAL level, session tags, Unity Catalog permissions).

Policy and Enforcement Plane

- Unified policy.yaml: data_platform, genai_security, voice_compliance, enforcement, compliance sections; canonicalized with policy_hash embedded in evidence.
- Guard Engine (AI Firewall): SchemaLock validation + enforcement primitives (allow/deny/HITL, idempotency, velocity guards, tenant/actor fences, SQL safety); multi-trigger kill-switch (<1s) with TTL recovery and HITL override; shadow-mode default in Review.
- GenAI Defense Pack: Prompt-injection heuristics, prompt-delta hashing (no body storage), external detector shims (deepfake/BEC) with timeout/fallback, BEC-grade approval certs (RFC 8785), OWASP LLM + MITRE mappings in receipts.

Bridges, Attestations, and PLG

- ServiceNow/Jira Bridges: Attested change tickets, two-way approval sync; formatter with configurable field mappings.
- Attestation Engine: Signed JSON (source of truth) + PDF referencing JSON digest; frameworks: SOX ITGC (controls with rationale), PCI/HIPAA (pass/fail), EU AI Act/NIST overlays, TCPA (voice).
- Daily Review Helper: PCI Req-10 automation; data/GenAI/voice posture; showback CSV/JSON exports.
- Verify Portal (Free): Hosted verify pages, Slack/PR comments, receipt cards for wikis; badges service (JWT, 90-day expiry) with public verification endpoints.
- Procurement Kit: Sample bundles and attestations; buyer/auditor one-pagers; verification guides.

Data Platform Integrations

- dbt Integration: on_run_start/end hooks; macros (SQL safety); CI gates; semantic-delta capture; badge issuance.
- Activation Gateway: HTTP proxy for reverse-ETL (Hightouch/Census/RudderStack) with idempotency, rate limits, tenant fences, approval validation; <15ms p95 proxy latency.
- Multi-warehouse Anchors: Snowflake now; BigQuery fast-follow (3–6 months); Databricks compatible (6–9 months); Postgres for ops anchoring.

Security, Ops, and Supply Chain

- Security Model: Zero-trust; mTLS; HMAC request auth; Ed25519 signatures; cosign/SBOM/SLSA; ECS/OCSF NDJSON event formats for SIEM.
- Privacy-by-Design: Metadata-only by default; opt-in body storage with redaction; hashed IDs; WORM retention recipes; KMS key rotation.
- CI/CD and Code Change Control: GitHub Actions for verification, policy gates, perf/security tests; commit SHA binding; deploy rate limits; badge generation.

Performance SLAs (global targets)

- Gateway: ≤15ms p95 baseline (+≤3ms with full enforcement — AI Firewall); Recorder ≤20ms p95; dbt hook overhead <2s; warehouse policy query <5s.
- GenAI threats: built-in detectors <100ms; common patterns <50ms; external detectors <500ms with timeout/fallback.
- Replay/Verify: DEF bundle creation <5s; PEF <3s; verify <1s.

Observability & k6

- OpenTelemetry metrics: clyra.gateway.request_duration_seconds, clyra.recorder.snapshot_duration_seconds, clyra.bundle.generation_duration_seconds, clyra.verification.duration_seconds, plus business/security counters (bundles generated, violations, certificates issued, threats detected, killswitch activations, blocks, auth failures). Labels include tenant_id (hash), policy_hash, framework, warehouse_platform, threat_class, enforcement_decision.
- Performance tests (k6): staged load for Gateway, Recorder, dbt hook overhead, warehouse query impact; thresholds codify SLAs; perf regression detection with trend curves.

------------------------------------------------------------

4) Personas and Jobs To Be Done (JTBD)

Primary (Land)

- Analytics Engineer / Data Platform Lead: “Prove my dbt changes are safe in <10 minutes; share results with my team; avoid breaking prod.”
- Indie data/AI builders: “Get verifiable receipts without bureaucracy; works with my tools; CLI-first.”

Secondary (Expand)

- SRE / Security / Platform: “Turn on enforcement with low overhead; provable approvals; kill-switch drills pass; tie to CI/CD gates.”
- Controllers / SOX PMO: “Attested tickets and daily reviews for quarter-end; fewer audit exceptions.”

Tertiary (Strategic)

- Auditors / SIs: “Independent verification; control rationale documentation; clear procedures.”
- Finance / Ops Leaders: “Attributed outcomes with evidence; shadow billing simulations.”

------------------------------------------------------------

5) Sequencing and Decision Gates

Horizon 0 (Months 0–3) — Nail the Data Wedge

- Ship: Visus (Review) + Lumyn (Verify Portal), procurement kit, receipt sharing & virality engine; GenAI/AI Firewall shadow; Replay (DEF) in core; Snowflake + Postgres anchors.
- Plan: BigQuery fast-follow (3–6 months), Databricks compatible (6–9 months).
- Success criteria: Attested ticket ≤2 weeks; SLAs met; 3 design partners; 1 paid pilot; 1 auditor acknowledgment; 100+ GitHub stars; 10+ dbt badges.

Horizon 1A (Months 3–9) — Enforcement (Gate) for Data Platform

- Ship: Gate activation (AI Firewall enforce + approvals); two-way ServiceNow/Jira; CI/CD gates; SQL safety (advisory); kill-switch drills 100% pass.
- Expand: BigQuery support (3–6 months), Databricks compatible (6–9 months).
- Success: 10+ Review customers, 3+ Gate conversions, ≥30% conversion in 90 days; $500k+ ARR; zero critical vulns.

Horizon 1B (Months 3–9, Conditional) — Airlock (MCP) Review → Gate

- Decision: Activate if ANY signal (≥2 customer requests; MCP ≥10k stars + 3 major platforms; notable incidents; competitive threat).
- Ship (12 weeks): MCP proxy + receipts; Token Exchange + DPoP; reverse tunnel; signed allowlists; HITL; ServiceNow/Jira export. Reuse Guard/GenAI/Verifiers.
- Success: TTFSC <60 min; 0 standing creds; ≥90% receipt coverage; $100–200k ARR incremental.

Horizon 1C (Months 3–9) — Atlas (Attribution)

- Ship: Outcome Ledger; Attribution Certificates; lineage display; shadow billing sims.
- Success: 2+ customers use certificates in QBRs; ≥1 public case study; zero methodology disputes.

Phase 1.5 (Pre–H2) — Adjacent Enablers

- Relia (Semantics) minimal OSS; TS SDK parity upgrade; Prefect/Dagster operators if demanded; Helm/K8s manifests for enterprise pilots.

Horizon 2 (Months 9–18) — Results-Based Billing (Aspirational)

- Pricing policy engine; invoice/billing bundles; AP exports (NetSuite/Stripe); dispute workflow; stablecoin payouts (Coinbase corridors); payout receipts chained into evidence.
- Gates: Attribution GA; 3+ customer asks; $1M+ ARR core; 2+ auditor acknowledgments; 0 critical vulns for 6+ months.

Horizon 3 (Months 18–36) — Ecosystem & Standards (Aspirational)

- Publish DEF/PEF and Attribution specs; third-party verifiers; auditor/SI programs; fiat rails; vertical packs.

Horizon 4 (Years 3–7) — Settlement Layer (Aspirational)

- Neutral settlement fabric (stablecoin + fiat) with Attribution Certificates as contractable truth; <1% dispute rate; platform fees (0.2–0.5%) at scale.

Decision Gates (Roll-up)

- BigQuery: ≥2 active prospects blocked + core stability → proceed (2–3 weeks effort).
- Databricks: 1–2 named ML-heavy customers → Review-first compatible entry.
- Airlock: any trigger from the criteria; requires dedicated team (2–3 engineers/12 weeks) separate from data track.

------------------------------------------------------------

6) Multi-Warehouse Strategy (Hedge Without Dilution)

Primary wedge: dbt + SOX + Snowflake — fastest path to revenue (board deadlines; finance-owned budgets; uniform dbt surface).
Fast-follow: BigQuery (3–6 months) — near parity to Snowflake; avoid losing 30% of market.
Compatible entry: Databricks (6–9 months) — position as independent verification alongside Unity Catalog; Review-first; lower initial conversion.
Decision routing in discovery:

- Do you run dbt for board-facing models? What’s your SOX timeline? Warehouse: Snowflake / BigQuery / Databricks?

------------------------------------------------------------

7) AI Agent Replay, GenAI Security, and AI Firewall (Placement)

AI Agent Replay (PEF-based)

- Shared feature in core (CLI/SDK + verifiers). Available in Visus (validation) and Gate (pre-prod checks/forensics). Default for Airlock (MCP) receipts when activated.
- SLAs: ≥95% runs produce a Replay Certificate; ≤2× baseline runtime; no PII leakage (metadata-only).

GenAI Security (Defense Pack)

- Shared pack in policy/enforcement: prompt-injection heuristics, prompt-delta hashing, external detector shims (deepfake/BEC), BEC-grade approvals, kill-switch triggers.
- Shadow by default in Visus; enforce in Gate; reused in Airlock.
- SLAs: <0.1% false positives; prompt analysis <100ms; external detectors <500ms with timeout/fallback.

AI Firewall (Guard Engine)

- The enforcement layer combining SchemaLock + GenAI Defense + primitives + kill-switch. Shadowed in Visus; enforced in Gate (and Airlock Gate).
- SLAs: Gateway ≤15ms p95 (+≤3ms with enforcement); approval verification <10ms; kill-switch <1s.

------------------------------------------------------------

8) CLI Surface (Unified)

Principles

- One CLI: clyra <verb> <track>. Descriptive commands over brand names for dev ergonomics.
- Tracks: review, verify/share, gate, attribution, voice, semantics, airlock, dbt/warehouse/activation, policy, genai, attest/report, doctor.

Examples (non-exhaustive)

- Review: clyra review init | generate --servicenow | export --jira
- Verify/Share: clyra verify evidence.zip --explain | clyra share evidence.zip
- Gate: clyra gate enable --policy policy.yaml | clyra bec validate | clyra policy lint --strict
- Attribution: clyra attribution issue | simulate | export
- Voice: clyra voice session | compliance --check-disclaimers | correlate --ucaas teams
- Semantics: clyra semantics compile --engine snowflake | verify
- Airlock: clyra airlock login | allow <server> <tool> | verify | tunnel status
- Data platform: clyra dbt init | clyra warehouse doctor --platform snowflake|bigquery|databricks | clyra activation gateway --policy policy.yaml
- Compliance & attest: clyra attest evidence.zip --framework sox|pci|hipaa|eu-ai-act|nist-rmf|tcpa | clyra report --daily-review [--attest-sox]
- GenAI: clyra genai test --attack-vectors prompt-injection,deepfake | clyra threats analyze
- Doctor: clyra doctor --comprehensive --suggest-fixes

------------------------------------------------------------

9) PLG — Receipt Sharing & Virality Engine

What

- Make receipts tangible and shareable for viral team adoption.
Features
- clyra share evidence.zip → shareable link; Slack/Teams bot posts “Verified ✓” cards; GitHub PR comments; public verify pages (no login for basic verify); receipt widgets for wikis; email templates (“Look what I just prevented”).
Virality Mechanics
- Rich previews in chat; social proof notifications (“5 devs in your company use Clyra”); team analytics weekly digests; referral tracking; auto-updated badges.
Success Metrics
- ≥30% of receipts shared within 7 days; ≥50% of shared receipts lead to new seats in same org; ≥10 Slack installs by Month 6; viral coefficient ≥0.4; ≥1K verification clicks/month.
Acceptance
- Links functional; bots operate; cards render correctly; GitHub comments post; verify pages <1s.

------------------------------------------------------------

10) Performance Budgets, Monitoring, and Tests

SLA Matrix (examples)

- Gateway: JSON validation 10ms p95 (20ms p99); with enforcement 15ms p95 (25ms p99) @1K req/s.
- Recorder: Snapshot 15ms p95 (30ms p99) @100 tables.
- dbt hook: pre/post 1.5s p95 (2s p99) on medium project.
- Warehouse: policy query 3s p95 (5s p99) @1K rows.
- Activation proxy: 10ms p95 (15ms p99) @500 req/s.
- GenAI detection: 80ms p95 (150ms p99) @100 req/s.
- Verification: 800ms p95 (1.2s p99) for 10MB bundle.
OpenTelemetry metrics & labels
- Performance: clyra.gateway.request_duration_seconds, clyra.recorder.snapshot_duration_seconds, clyra.bundle.generation_duration_seconds, clyra.verification.duration_seconds.
- Business/Security: clyra.bundles.generated_total, clyra.policies.violations_total, clyra.approvals.certificates_issued_total, clyra.threats.detected_total, clyra.killswitch.activations_total, clyra.enforcement.blocks_total, clyra.authentication.failures_total.
- Labels: component, tenant_id (hash), policy_hash, framework, warehouse_platform, threat_class, enforcement_decision.
Testing examples
- k6 scenarios for gateway load; dbt hook overhead; warehouse query impact; activation throughput. Thresholds match SLAs; regression detection with trend curves.

------------------------------------------------------------

11) Compliance & Attestations

Frameworks

- SOX ITGC: Change control, segregation of duties, access management, monitoring/logging — with control rationale documentation and evidence mapping.
- PCI DSS & HIPAA: Pass/fail attestations, daily reviews (Req-10), privacy safeguards.
- EU AI Act & NIST RMF: Record-keeping overlays; risk documentation; human oversight tracking.
- TCPA: Voice disclaimers, consent tracking, violation detection.
Unified Attestation Engine
- clyra attest evidence.zip --framework sox|pci|hipaa|eu-ai-act|nist-rmf|tcpa → Signed JSON + PDF with JSON digest reference.
Daily Review
- Aggregates data changes, GenAI threats, voice compliance events; optional SOX roll-up attestation; showback exports (CSV/JSON) for CFO-friendly reporting.

------------------------------------------------------------

12) Risks & Mitigations (Top 10)

- Vendor encroachment (Snowflake/Databricks): Double down on independence (verifiers, auditor letters), cross-platform portability, and “logs ≠ evidence” positioning.
- False positives: Shadow by default; conservative thresholds; publish FP rate; tune iteratively; kill-switch UX first-class.
- Scope creep: Voice pilot-only; Semantics minimal OSS; Airlock gated; defer UI/control plane.
- Perf drift: CI perf gates; trend reporting; SLOs; circuit breakers for dependencies.
- Security posture: Continuous scanning; signed releases; key rotation; WORM retention.
- Sales cycle bloat: Developer-first copy; procurement kit; keep demos code-first; let finance/compliance be pulled in by proof.
- Multi-warehouse split-brain: Clear messaging on Snowflake-now, BigQuery-fast-follow, Databricks-compatible.
- Attribution disputes: Deterministic transparent methods; auditor guidance; customer overrides with audit trail.
- Ecosystem timing: Airlock strictly gated; Semantics OSS paced to interest.
- Hiring constraints: Solutions Eng (dbt/Snowflake), DevRel/Docs, Security Eng, PM with SOX background.

------------------------------------------------------------

13) Troubleshooting & Ops (Quick Reference)

Common errors

- Signature verification failed → clyra verify bundle.zip --debug; check key_id / cert expiry.
- Canonicalization mismatch → clyra verify --explain --show-canonical; ensure RFC 8785 JCS before signing.
- Cross-verifier inconsistency → clyra verify --verifier both --diff-output; check platform-specific JSON handling.
Data platform issues
- Snowflake: session tags missing → clyra warehouse doctor --check-session-tags; SET session tags pre-queries.
- Databricks: Unity Catalog denied → clyra warehouse doctor --check-permissions; grant access to system tables.
- Postgres: WAL LSN not available → clyra warehouse doctor --check-wal-level; set wal_level=replica.
Policy validation
- Unknown primitive → clyra policy validate --verbose; check schema spelling.
- Threshold out of range → clyra policy validate --show-limits; adjust to documented ranges.
Debug helpers
- Enable logs: export CLYRA_LOG_LEVEL=debug; CLYRA_TRACE_ENABLED=true.
- Golden vectors: clyra test vectors --path spec/*/test-vectors/ --verbose.
- Perf budgets: clyra perf check --budget-file perf_budgets.yaml --current-metrics.
- SIEM test: clyra siem test --format ecs --output /dev/stdout.

------------------------------------------------------------

14) Documentation Governance

- This document is reviewed quarterly (next review date set in repo’s docs index) and on any material change to SKUs, SLAs, or shared platform.
- ADR index: docs/ADR_INDEX.md — record architectural and policy changes that impact evidence or enforcement.
- Schema directories: spec/def/schemas/, spec/pef/schemas/, spec/policy/schemas/; test vectors under spec/*/test-vectors/.

------------------------------------------------------------

15) Appendix — Brand Mapping and Glossary

Brand mapping

- Visus by Clyra — Review (Data Platform)
- Lumyn by Clyra — Verify Portal (Free)
- Gate by Clyra — Enforcement (Data), powered by Guard
- Atlas by Clyra — Attribution (Outcome Ledger + Certificates)
- Voice by Clyra — Conversation Compliance (Pilot)
- Relia by Clyra — Semantics (Open Control Plane, OSS-first)
- Airlock by Clyra — MCP (Conditional)
- Guard Engine — Enforcement core used by Gate/Voice/Airlock
- DEF/PEF Evidence Spine — Recorder, Replay, Bundler, Verifiers

Glossary

- DEF v0: Data Evidence Format (canonical JSON, Merkle-rooted, signed), anchored to warehouses.
- PEF v0: Portable Evidence Format (canonical JSON, Merkle-rooted, signed) for automation/agents.
- PEF MCP Extension: Optional fields for MCP receipts (server_id, tool, operation, param/result hashes, token scope, dpop_jkt, approval_principal, session_id).
- C2PA Extension (optional): Consent/provenance for generated assets (manifest hash, consent, likeness, model provenance, asset type).
- SchemaLock: Streaming JSON validation receipts with OWASP codes, threat_class, optional mitre_id.
- Approval Certificate: One-time, payload-bound, signed HITL approval (RFC 8785 JCS payload hash).
- Daily Review: Signed rollup of changes and threat posture; PCI Req-10 automation; optional SOX roll-up.

------------------------------------------------------------

End of Clyra Vision v4.0 — central, living document.
