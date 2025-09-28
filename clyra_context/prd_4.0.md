# **Clyra Platform PRD v4.0**

**Date:** September 2025

**Status:** Finalized for MVP Development (Data-led, Agent-ready Architecture)

**License:** Apache 2.0 (OSS)

---

## **0) Business Case (short)**

*Clyra is the data change firewall and audit platform for automation runtimes — from data pipelines to AI agents, RPA bots, ETL/dbt, SaaS integrations, and microservices.*

It provides one control point, two guarantees:

- **Clyra Gateway (SchemaLock + Data Firewall):** Stops unsafe data changes and malformed outputs (fail-closed, OWASP-tagged, threat-classified).
- **Clyra Recorder (Flight Data Recorder):** Proves and replays every change, producing tamper-evident evidence bundles.

**Tagline:** *Data Change Control & Attestation for Modern Pipelines*

**Strategic positioning:** Data-led, agent-ready. Lead with data platform enforcement (dbt, warehouses, reverse-ETL) where budget exists today, while maintaining the same architecture that will protect AI agents tomorrow.

### **Product Packaging**

**Two-SKU Model for Progressive Adoption:**
- **Clyra Review** ($20-50K/year): Listen-only detection, attestation, daily reports, ServiceNow/Jira export
- **Clyra Gate** ($75-150K/year): Full enforcement with policy gates, idempotency, velocity controls, kill-switch

**Enterprise Integration Bridge:**
- **ServiceNow/Jira Certified**: Native "Attested Change Ticket" creation
- **Badge Program**: "Clyra Certified - SOX Compliant" badges for dbt projects
- **Audit Partner Network**: 2-3 Big 4 firms acknowledge our evidence format

Now extended with:

- **Data platform enforcement** (dbt hooks, warehouse anchors, DEF v0 bundles, activation gateway).
- **GenAI security hardening** (deepfake/BEC defenses, prompt injection detection, enhanced HITL).
- **AI Firewall features** (threat classification, detectors, kill-switch, ECS/OCSF NDJSON).
- **Compliance attestation packs** (PCI + HIPAA; EU AI Act/NIST overlays; SOX ITGC).
- **Self-serve PLG motion** (install → demo → attested bundle in <30 min).
- **Enhanced enforcement primitives:** idempotency, approval certs, tenant fences, velocity guards, SQL safety, BEC-grade certs.
- **Conversation + Coding focus** (voice handling, CI/CD enforcement, prompt delta tracking).
- **Governance pillars embedded in every bundle:** Reliability · Transparency · Accuracy · Oversight

---

## **1) Executive Summary**

**What is Clyra?**

"*Data change firewall + portable attestations across your stack. We block bad pushes and hand you signed proof auditors accept.*"

**Primary focus:** Data platform teams (dbt, Snowflake/Databricks, reverse-ETL) with immediate budget and compliance deadlines.
**Strategic expansion:** Same enforcement engine protects AI agents, RPA, automation workflows.

**The differentiation story:**
- **Evidence vs Observability:** Tools like Monte Carlo tell you what probably changed. Clyra gives you signed, tamper-proof receipts.
- **Prevention vs Detection:** Think seatbelt, not siren. Block unsafe changes before they hit production.
- **Independence matters:** Snowflake can't credibly audit itself. Neutral, portable evidence survives platform churn.
- **Ready for agents:** Today's data controls become tomorrow's AI agent governance.

Clyra intercepts data changes (dbt runs, schema migrations, activation syncs), anchors state to warehouse logs (WAL LSNs, Delta commits, QUERY_HISTORY), and produces portable, tamper-evident **DEF v0 + PEF v0 bundles** that auditors can verify independently.

The **10-minute PLG path** takes users from install → verified bundle → offline deterministic replay → signed **attestation report** (SOX/PCI/HIPAA/EU AI Act/NIST-ready).

**Strategic wedge:** Establish **DEF/PEF** as the neutral forensic & compliance standard that auditors and SIs can verify without trusting Clyra binaries.

---

## **2) The Problem ("Hair-on-Fire")**

**Data Platform Pain (Primary Market):**
- **Bad data pushes to prod** corrupt dashboards, ML features, finance reports; no fail-closed gate or instant "who/what/when/why" proof.
- **Metric/semantic drift** between periods; auditors need signed attestations, not logs and screenshots.
- **Risky activation to SaaS** (high-risk audiences to Salesforce/Braze) with no idempotency, tenant fences, HITL, or paper trail.
- **Cross-stack audit friction:** Snowflake + Databricks + dbt + Reverse-ETL have partial controls; no neutral, portable attestation.

**Automation/Agent Pain (Strategic Market):**
- **Malformed outputs (OWASP LLM-02)** corrupt ERP/CRM/Finance systems.
- **GenAI security risks:** 62% hit by deepfake social-engineering; 32% saw prompt-based attacks; 29% experienced GenAI infrastructure attacks.
- **No forensic trail** to show precisely what an automation or agent did.
- **Compliance friction:** PCI/HIPAA/EU auditors block pilots without tamper-evident, independently verifiable evidence.
- **High-risk actions (refunds, address changes, credit limits)** lack enforcement primitives (idempotency, approvals, rate limits).

**Universal Questions Enterprises Cannot Answer:**
1. What changed?
2. Can we prove it?
3. Does this evidence satisfy my auditor?
4. Can we replay it deterministically?

---

## **3) The Solution (Data-First Enforcement + Forensic Loop)**

### **Data Platform Enforcement (Primary)**

1. **Data Change Firewall (runtime, fail-closed)**
   - Gate schema/model/metric changes and activation syncs before they land.
   - Contracts & guards: JSON Schema + dbt test outcomes, idempotency keys, tenant/actor fences, rate/velocity caps, SQL safety.
   - Kill-switch: Run-level thresholds auto-block bursty failures.
   - HITL Approval Certificates (payload-bound): For "risky" pushes, require signed approval tied to exact change set.

2. **dbt Integration (hooks + macros)**
   - `on_run_end` hooks emit DEF v0 bundles (manifest, receipts, semantic deltas).
   - CI gate: block merges on unapproved semantic deltas, failing tests, policy breaches.
   - SQL safety macros: `clyra_guard.merge_with_cert()` enforces approval tokens.

3. **Warehouse-Native Anchors**
   - Snowflake: QUERY_HISTORY/Access History refs, session tags with approval tokens.
   - Databricks: Delta commit IDs, macro helpers requiring Clyra approval tokens.
   - Postgres: WAL LSN anchoring for operational data stores.

4. **Activation/Reverse-ETL Gateway (HTTP)**
   - Lightweight proxy for Hightouch/RudderStack/Segment-like flows.
   - Enforce idempotency, rate caps, tenant fences, HITL certs before SaaS syncs.
   - Signed receipts + daily review rollups.

### **Universal Forensic Loop (All Runtimes)**

5. **Capture:** HTTP/S proxy with HMAC validation, per-run hash chain, SSE notarization.
6. **SchemaLock:** Stream-validate JSON; auto-repair once else block; signed receipts with OWASP codes, **threat_class**, optional **mitre_id**.
7. **Snapshot:** **Policy-driven metadata snapshots** (not PITR), anchored to warehouse logs; DSN always hashed.
8. **Diff:** Deterministic comparison (schema drift, row deltas, checksums).
9. **Bundle:** Canonical, signed **DEF v0** (data) + **PEF v0** (automation) with receipts, snapshots, diffs, replay cert, governance + perf/cost/security metrics.
10. **Verify:** Independent Go/TS verifiers, golden vectors.
11. **Replay:** Offline deterministic replay in scratch schema; signed **Replay Certificate** with {success|partial|failed} status.
12. **Attestation v0:** Signed JSON/PDF summarizing lineage, replay, receipts, **SOX/PCI/HIPAA/EU AI Act/NIST** mappings, storage/KMS proofs.

### **GenAI Security Hardening (Integrated)**

13. **GenAI Risk Overlay (default policy starter)**
    - Idempotency required on high-risk routes (refunds, address changes).
    - Run-level kill-switch thresholds + TTL.
    - Rate limits + tenant fences.
    - Enhanced HITL for deepfake-susceptible workflows.

14. **Prompt Injection & Reflex Heuristics**
    - Built-in detectors (regex/JSONPath for "ignore previous instructions", "/bin/sh", etc.).
    - Prompt delta hashing (sanitized, no bodies) to flag injection drift.
    - Default = shadow-mode.

15. **BEC-Grade Approval Certificates**
    - Payload-bound + SSO sub + IdP + one-time challenge reference.
    - Hardens against impersonation while staying in signing pipeline.

### **Conversation + Coding Focus**

16. **Voice/Conversation Handling**
    - Voice session tracking: `voice_session_id`, `disclaimer_required`, `barge_in_window_ms`.
    - Daily report includes disclaimer compliance and barge-in failures.
    - Partner-log correlation with UCaaS/SIP gateways (Teams, Slack, Zoom).

17. **CI/CD + Code Change Control**
    - GitHub Actions enforcement: commit SHA uniqueness, rate limits on automated runs.
    - SOX ITGC attestation overlay: "who/what/when" change-control fields.
    - Idempotency enforcement for deploy events.

---

## **4) Personas & JTBD**

**Primary Champions (Data-Led):**
- **Head of Data Platform / Director of Analytics Eng:** "I need SOX change control for my dbt pipelines with ServiceNow tickets for audit."
- **Finance Controller / SOX PMO:** "Show me attested change tickets I can present to auditors."
- **Data Engineers:** "Give me a badge that proves my pipeline is compliant."
- **CISO/GRC (Co-sponsor):** "Neutral enforcement layer across data stack; evidence auditors can verify independently."

**Strategic Expansion (Agent-Ready):**
- **Platform/SRE:** "Same controls for data today, agents tomorrow; single enforcement layer."
- **Security/Compliance:** "GenAI-hardened enforcement with deepfake/BEC defenses."
- **System Integrator:** "Compliance-in-a-box for both data and automation runtimes."
- **AI Engineer / Automation Lead:** "Deterministic repro with minimal glue, future-proofed for agents."

---

## **5) Goals & Success Criteria (KPIs)**

**Data Platform (Primary Success Metrics):**
- **Time-to-Attestation:** ≤ 2 weeks to first signed SOX/PCI attestation from dbt run.
- **Audit Acceleration:** Cut compliance evidence gathering from 6 weeks to 2 days.
- **Change Safety:** Block ≥1 unsafe schema change or activation sync per customer per month.
- **Adoption Depth:** ≥50% of customer dbt runs under Clyra policy within 90 days.

**Universal Performance:**
- **Gateway p95 ≤ 15 ms** (≤ +5 ms with detectors + enforcement primitives)
- **Recorder p95 ≤ 20 ms**
- **Snapshot ≤ 50 ms** (≤100 tables)
- **Diff < 2 s** on demo dataset

**Onboarding & PLG:**
- **TTVB ≤ 10 min**; First Attested Run ≤ 30 min
- **Data-specific TTVB:** dbt hook + first DEF bundle ≤ 15 min

**Reliability:**
- **Lineage conclusive > 99%**
- **spill_policy=block**; no silent drops

**Verifiability:**
- **Independent verifiers pass golden vectors**
- **Attestations validate bundles** (SOX/PCI/HIPAA attestations; EU AI Act/NIST overlays)

**Commercial (12-Month Targets):**
- **3+ data platform pilots → paid conversions**
- **1+ attestation used in quarter-end close**
- **$300-600k ARR** primarily from data use cases
- **50% retention** measured by second bundle creation within 14 days

---

## **6) Scope: In & Out**

**In Scope (MVP Locked):**

**Data Platform Core:**
- **dbt plugin/hooks:** Emit DEF v0 bundles, CI gate integration, semantic delta detection.
- **Warehouse anchors:** Snowflake (QUERY_HISTORY, session tags), Databricks (Delta commits), Postgres (WAL LSN).
- **SQL contract guards:** Macros like `clyra_guard.merge_with_cert()`, enforce approval tokens, block unsafe ops.
- **Activation/Reverse-ETL gateway:** HTTP proxy with full enforcement primitives.
- **Attestation JSON/PDF exports:** SOX ITGC, PCI, HIPAA mappings for data changes.
- **Airflow/Dagster operator:** One-node `ClyraAuditTask` integration.

**Universal Foundation:**
- **PostgreSQL 15/16 fully supported; 13/14 demo/pilot only (best-effort)**
- **Gateway with SchemaLock receipts** (signed, OWASP-tagged, **threat_class**).
- **Recorder with HMAC headers**, **metadata snapshots (not PITR)**, diffs, replay.
- **DEF v0 + PEF v0 bundles** (canonical JSON, Merkle root, metrics).
- **Unified policy.yaml** (schemas, validators, lineage, body_storage, HITL, threat_map, kill_switch, cost caps).
- **Independent Go/TS verifiers**.

**GenAI Security Hardening (All MVP Locked):**
- **GenAI Risk Overlay** policy templates with sane defaults.
- **Prompt injection heuristics** (built-in regex/JSONPath detectors, shadow-mode).
- **Prompt delta hashing** (sanitized, no bodies) in receipts.
- **BEC-grade approval certificates** (SSO + challenge binding).
- **Enhanced HITL defaults** for deepfake-susceptible routes.
- **Kill-switch preconfigs** with run-level thresholds.
- **Deepfake/safety signal HTTP detector shim** (vendor-agnostic).

**Conversation + Coding (Priority Features):**
- **Voice session handling:** `voice_session_id`, disclaimer tracking, barge-in windows.
- **Partner-log correlation fields:** `approver_principal`, `actor_principal`, `client_app_id`, `session_id`.
- **CI/CD enforcement:** GitHub Actions integration, commit SHA uniqueness, deploy rate limits.
- **SOX ITGC attestation overlay** for code changes.

**Enhanced Enforcement Primitives (All MVP Locked):**
- **Idempotency keys** (per-route, TTL-bound, HMAC fingerprints).
- **HITL Approval Certificates** (payload-bound, signed, with BEC enhancements).
- **Velocity guards** (per-route, sliding windows).
- **Tenant & actor fences** (header/body consistency, DSN hash namespacing).
- **SQL-safety guardrails** (Preview, advisory - block UPDATE/DELETE w/o WHERE, rows_affected limits).
- **Daily review helper** (PCI Req 10 rollups + GenAI threat posture).
- **JSON Schema business rules** (ranges, enums, cross-field validation).
- **Prompt-loop/reflex-chain breaker** (per-run counters, cool-off policies).

**CLI & Integration:**
- **CLI:** quickstart, demo (contracts, etl, data), doctor, init, policy wizard/lint/test, export, report --daily-review, verify, replay, attest.
- **SDK:** Python (headers, decorators, LiteLLM wrapper, dbt helpers, retry/backoff).
- **Scenario Packs:** Contracts, AP/AR, ETL/dbt demo, RPA invoice demo, Data platform demo.
- **Service Packs:** Retail, FinServ, Travel/Hospitality (production-lean templates).
- **Procurement Kit:** sample bundle, verifier, attestation, auditor + buyer one-pagers.
- **hello-bundle repo** with CI verifier action + badge.
- **Runtime stubs:** FastAPI, Express, Go chi, dbt macros.

**Operations & Observability:**
- **Shadow Mode** (logging + optional SIEM forwarding).
- **KMS & WORM recipes**.
- **SIEM-ready NDJSON** (ECS/OCSF) + saved searches focused on GenAI threats.
- **OTEL/Fluent Bit recipes**.
- **Release integrity:** SBOM, cosign, non-root images, key rotation.
- **Saved SIEM searches:** deepfake/BEC workflows, HITL usage, burst anomalies, prompt deltas.

**Out of Scope (Deferred):**
- **Content governance** (email, CMS, publishing - defer to Phase 2).
- **Other DBs** (MySQL, Oracle, etc.).
- **SaaS control plane & UI/dashboard**.
- **Packaged Splunk/Datadog dashboards** (MVP ships saved searches).
- **WASM detector sandbox & marketplace**.
- **Rollback orchestration**.
- **Full lineage UI/catalog** (integrate, don't rebuild).
- **Anomaly ML/streaming ingestion**.

---

## **7) Feature Specifications**

### **7.1 Data Platform Enforcement**

**dbt Integration (Core Value)**
- **Pre/post run hooks:** Emit DEF v0 bundles with manifest, receipts, semantic delta hashes.
- **CI gate integration:** Block merges on unapproved semantic deltas, failing dbt tests, policy violations.
- **SQL safety macros:** `clyra_guard.merge_with_cert()`, `clyra_guard.safe_update()` require approval tokens.
- **Metadata capture:** Table/column lineage, transformation steps, test results.
- **Performance:** Hook execution <2s overhead on typical dbt runs.

**Warehouse-Native Anchors & Guards**
- **Snowflake integration:**
  - Session tags with `ClyraApprovalToken`, `RunId`, `ActorId`.
  - Stored procedures verify approval certs, record signed receipts.
  - QUERY_HISTORY/Access History IDs captured as lineage anchors.
  - Block DDL/DML without valid approval tokens via RBAC + guards.
- **Databricks integration:**
  - Delta Lake commit version tracking.
  - Macro helpers requiring Clyra approval tokens before `MERGE INTO`.
  - Unity Catalog integration for metadata lineage.
- **SQL safety enforcement:**
  - Block `UPDATE`/`DELETE` without `WHERE` clauses.
  - Hard-limit `rows_affected` via policy-defined thresholds.
  - Allowlist maintenance routes for legitimate mass operations.

**Activation/Reverse-ETL Gateway (HTTP Proxy)**
- **Target integrations:** Hightouch, RudderStack, Segment-like activation flows.
- **Enforcement primitives:** Full suite (idempotency, rate caps, tenant fences, HITL approval certs).
- **SaaS protection:** Prevent high-risk audience pushes to Salesforce, Braze, etc.
- **Receipts + reporting:** NDJSON events, daily review rollups.

**DEF v0 (Data Evidence Format)**
- **Bundle structure:** `manifest.json`, `journal.jsonl`, `artifacts/` (same as PEF v0).
- **Data-specific artifacts:**
  - Semantic delta summaries (metric definitions, schema changes).
  - dbt test results and lineage metadata.
  - Warehouse anchor references (QUERY_HISTORY IDs, Delta commits).
  - Sample checksums for drift detection.
- **Attestation integration:** SOX ITGC, PCI Req-10, HIPAA mappings.
- **Independent verification:** Same Go/TS verifiers work for both DEF and PEF.

### **7.2 Gateway (SchemaLock + Data Firewall)**

**Enhanced from v3.0 with:**
- **Data-aware validation:** JSON Schema + dbt test outcome integration.
- **GenAI threat detection:** Built-in prompt injection heuristics (shadow-mode default).
- **BEC-hardened receipts:** Enhanced approval cert references with SSO binding.
- **Prompt delta tracking:** Sanitized hash of prompt changes (no body storage).
- **Voice session fields:** `voice_session_id`, `disclaimer_required`, `barge_in_window_ms`.

**New enforcement fields in receipts:**
- `semantic_delta_hash` (for schema/metric changes).
- `dbt_test_results` (pass/fail summary).
- `warehouse_anchor_ref` (QUERY_HISTORY ID, Delta commit, WAL LSN).
- `voice_compliance_check` (disclaimer, barge-in validation).
- `prompt_delta_hash` (injection drift detection).
- `bec_approval_grade` (enhanced approval cert security level).

### **7.3 Recorder (Flight Data Recorder)**

**Data platform enhancements:**
- **Metadata-only snapshots** with warehouse-specific anchoring.
- **Semantic drift detection:** Compare metric definitions, schema structures across runs.
- **Sample checksums:** Deterministic data fingerprints without full data capture.
- **dbt lineage integration:** Capture model dependencies and transformations.

**Replay capabilities:**
- **Data replay:** Reconstruct dbt runs in scratch schemas with same inputs.
- **Schema replay:** Re-execute DDL changes in isolated environments.
- **Activation replay:** Simulate reverse-ETL syncs with test endpoints.

### **7.4 Enhanced Enforcement Primitives**

**BEC-Grade Approval Certificates**
- **SSO binding:** Include `approver_sso_sub`, `idp_domain`, `challenge_nonce`.
- **Payload integrity:** RFC 8785 (JCS) hash binding prevents TOCTOU attacks.
- **Expiry enforcement:** Short TTLs (default 15 min) for high-risk operations.
- **MFA requirements:** Optional `mfa_required` flag with IdP verification.

**Prompt Loop/Reflex Breaker**
- **Per-run counters:** "actions per minute", "identical route repeats".
- **Cool-off policies:** Block high-risk routes when actor repeats N times in window.
- **Agent-specific:** Detect prompt injection loops, agentic failure cascades.

**Voice/Conversation Primitives**
- **Disclaimer enforcement:** Require audio disclaimer before high-risk voice actions.
- **Barge-in windows:** Allow human interruption during agent voice interactions.
- **Session correlation:** Link voice sessions to API actions for audit trails.

**CI/CD Enforcement**
- **Commit uniqueness:** Prevent duplicate merges/deploys via idempotency on commit SHA.
- **Deploy rate limits:** Throttle automated pipeline triggers, prevent runaway deployments.
- **Approval binding:** Require signed approval certificates for production deployments.

### **7.5 GenAI Security Hardening**

**GenAI Risk Policy Overlay (Default Template)**
```yaml
# templates/policy/genai_risk.overlay.yaml
enforcement:
  idempotency:
    - route: "/refunds/*"
      ttl_seconds: 3600
      mode: single_use
    - route: "/limits/*"
      ttl_seconds: 1800
      mode: single_use

  rate_limits:
    - route: "/refunds/*"
      key: "actor"
      window: 300
      max_actions: 5
      max_amount_cents: 100000

  tenant_fences:
    required_headers: ["x-tenant-id", "x-actor-id"]
    cross_check: true
    privacy: hash_ids

  kill_switch:
    triggers:
      - metric: "error_rate"
        threshold: 0.1
        window: 60
        action: "block_run"
        ttl: 300
```

**Built-in Threat Detectors**
- **Prompt injection patterns:** "ignore previous instructions", "as a system prompt", "/bin/sh", "curl http", "final answer: run".
- **Social engineering markers:** Executive impersonation, urgency language, financial requests.
- **Technical indicators:** Shell commands, metadata endpoints (169.254.x.x), paste-bin URLs.
- **Default mode:** Shadow (log only) to avoid false positive disruption.

**External Detector Integration**
- **HTTP detector shim:** Vendor-agnostic interface for deepfake/BEC detection services.
- **Media analysis:** Hash-based integration (no raw media sharing).
- **Verdict ingestion:** `likely_deepfake`, `spoofed_voice`, `high_risk_bec` signals.
- **Timeout/fallback:** Graceful degradation when external services unavailable.

### **7.6 Attestation v0 (Enhanced)**

**Data Platform Attestations**
- **SOX ITGC mapping:** "Who/what/when" change control for data modifications.
- **PCI DSS compliance:** Daily review automation, access control evidence.
- **dbt governance:** Model approval chains, test coverage, semantic change tracking.

**GenAI Threat Posture Section**
- **Threat coverage:** Detectors enabled, kill-switch thresholds, HITL rates.
- **BEC defenses:** Approval cert usage, deepfake detection integration.
- **Prompt safety:** Injection heuristic coverage, delta monitoring status.
- **Voice compliance:** Disclaimer rates, barge-in usage, session correlation.

**Attestation Artifacts**
- **Machine-readable JSON** (signed, canonical).
- **Human-readable PDF** referencing JSON digest.
- **Evidence bundle references** (DEF/PEF links).
- **Independent verification instructions** for auditors.

### **7.7 Voice/Conversation Features**

**Voice Session Management**
- **Session tracking:** Unique `voice_session_id` per interaction.
- **Compliance fields:** `disclaimer_played`, `disclaimer_acknowledged`, `barge_in_available`.
- **Integration points:** SIP gateways, WebRTC, UCaaS platforms (Teams, Zoom).

**Conversation Enforcement**
- **Disclaimer requirements:** Policy-driven audio disclaimers before risky actions.
- **Interruption windows:** Human barge-in capability during agent operations.
- **Correlation:** Link voice sessions to API actions in same audit trail.

**Daily Review Integration**
- **Compliance metrics:** Disclaimer coverage, barge-in usage rates.
- **Risk indicators:** Voice sessions without disclaimers, failed barge-in attempts.
- **Regulatory mapping:** TCPA compliance, HIPAA authorization tracking.

### **7.8 CI/CD & Code Change Control**

**GitHub Actions Integration**
- **Verifier action:** Auto-verify evidence bundles in CI pipelines.
- **Badge generation:** "Evidence Verified" badges for README display.
- **Policy enforcement:** Block merges that violate Clyra policies.

**Change Control Enforcement**
- **Commit binding:** Approval certificates bound to specific commit SHAs.
- **Deploy idempotency:** Prevent duplicate deployments via artifact fingerprints.
- **Rate limiting:** Throttle automated pipeline triggers, prevent runaway builds.

**SOX ITGC Compliance**
- **Change approval tracking:** Who approved, what changed, when deployed.
- **Segregation of duties:** Separate approval and deployment roles.
- **Audit trail:** Complete lineage from code commit to production deployment.

---

## **8) PLG Experience (Listen-Only → Review → Gate)**

**10-Minute Quickstart (Agentless):**
1. **Connect** → `clyra review init --dbt-cloud-webhook` (no proxy needed)
2. **Observe** → Watch changes flow through, no enforcement
3. **Ticket** → First ServiceNow change ticket auto-created
4. **Badge** → `clyra certify` → add badge to README
5. **Attest** → SOX compliance report generated

**30-Day Journey:**
- Week 1: Listen-only mode, daily reviews
- Week 2: First attested ServiceNow ticket
- Week 3: Badge in production dbt project
- Week 4: Controller sees value, asks about enforcement
- Month 2: Enable Gate SKU for policy enforcement

**Adoption Gates:**
- Gate 1: 3 customers using Review for 30 days
- Gate 2: 1 customer requests Gate features
- Gate 3: 1 auditor acknowledges format
- Gate 4: 1 customer pays for Gate SKU

---

## **9) Cross-Cutting Requirements**

**15-Factor App Compliance:**
- **API First (13):** All components expose RESTful APIs; Gateway/Recorder designed for interoperability.
- **Telemetry (14):** Comprehensive metrics via OpenTelemetry; performance/security counters.
- **Authentication (15):** mTLS between components; HMAC request auth; SSO integration for HITL.

**Modern Cloud-Native Patterns:**
- **Infrastructure as Code:** Helm charts, Terraform modules, policy-as-code YAML.
- **Immutable Infrastructure:** Non-root containers, artifact signing, distroless base images.
- **CI/CD Integration:** Native GitHub Actions, pluggable pipeline operators.

**Performance & Reliability:**
- **Data operations:** dbt hook overhead <2s; warehouse queries <5s; activation proxy <15ms p95.
- **Snapshots metadata-only** (no full data capture).
- **Replay always in scratch schema** (deterministic isolation).
- **Shadow Mode ≤1 ms overhead** (telemetry-only evaluation).
- **Enhanced enforcement ≤3 ms combined overhead** (BEC certs + prompt analysis).

**Security & Compliance:**
- **Zero-trust architecture:** Every component authenticated, encrypted in transit.
- **Evidence portability:** DEF/PEF bundles vendor-neutral, independently verifiable.
- **Secrets management:** KMS integration, no hardcoded credentials.
- **Audit readiness:** Every action logged with governance metadata.

**Operational Excellence:**
- **Opt-in telemetry** with privacy controls.
- **Postgres 15/16 supported; 13/14 demo only** with --allow-best-effort.
- **Clock skew detection + NTP doctor checks**.
- **Release integrity:** SBOM, cosign signatures, vulnerability scanning.

---

## **10) Risks & Mitigations**

**Data Platform Risks:**
- **Scope creep → observability platform:** Always lead with enforcement + attestations, not anomaly dashboards.
- **dbt integration friction:** Partner with dbt Labs early; contribute to dbt-labs/dbt-core.
- **Warehouse vendor pushback:** Emphasize independence and portability; avoid direct competition.
- **Performance overhead on data pipelines:** Strict SLAs; async processing where possible.

**GenAI Security Risks:**
- **False positive detector noise:** Shadow mode default; tunable thresholds; customer feedback loops.
- **Prompt injection evolution:** Detector updates via configuration; external detector integration.
- **BEC certificate complexity:** Start simple; iterate based on security team feedback.

**Technical & Operational:**
- **15-Factor compliance burden:** Implement incrementally; prioritize API-first and telemetry.
- **Multi-platform complexity:** Start with Postgres + Snowflake; expand based on traction.
- **Evidence bundle size:** Efficient serialization; metadata-only captures; compression.

**Commercial Risks:**
- **Data vs automation message confusion:** Clear positioning as "enforcement platform with data-led GTM."
- **Sales cycle complexity:** Focus on concrete ROI (audit time savings, incident prevention).
- **Competitive response:** Patent core algorithms; build community moat; emphasize independence.

**Mitigations:**
- **Tight scope enforcement:** No lineage UI, no ML anomaly detection, no catalog features in MVP.
- **Performance budgets:** k6 gates; inline profiling; SLA monitoring.
- **Community building:** Open source DEF/PEF specs; independent verifier ecosystem.
- **Customer co-development:** Design partners for each major use case.

---

## **11) Roadmap (Post-MVP)**

**Phase 1.5 (Data Platform Expansion):**
- **Enhanced warehouse support:** BigQuery, Redshift anchors.
- **Advanced dbt features:** Semantic layer integration, advanced lineage.
- **Prefect/Dagster operators:** Broader pipeline ecosystem coverage.
- **Commercial hosted registry:** Evidence retention, RBAC, dashboards.

**Phase 1.5 (Automation Expansion):**
- **TS SDK** for broader automation ecosystem.
- **Helm chart, Istio/Envoy integration** for Kubernetes deployments.
- **Advanced GenAI detectors:** Custom model integration, vector similarity.
- **Agent framework integrations:** LangChain, AutoGPT, AgentGPT connectors.

**Phase 2 (Platform Maturation):**
- **Self-hosted control plane** for enterprise deployments.
- **Advanced compliance packs:** Industry-specific frameworks (GDPR, SOX 404, FedRAMP).
- **Community RFC repo** for standards evolution.
- **WASM detector sandbox** for custom security logic.

**Phase 3 (Strategic Expansion):**
- **Content governance** (email, CMS, publishing) based on customer demand.
- **Advanced rollback orchestration** with state management.
- **UI/dashboard** for non-technical stakeholders.
- **SaaS delivery model** for mid-market segments.

---

## **12) Success Metrics & KPIs**

**Data Platform Success (Primary)**
- **Customer adoption:** ≥3 design partners → paid pilots within 90 days.
- **Technical adoption:** ≥50% of customer dbt runs under policy within 60 days.
- **Business impact:** ≥1 attestation used in customer quarter-end close.
- **Time-to-value:** ≤2 weeks from install to first signed SOX/PCI attestation.
- **Evidence quality:** 100% of DEF bundles pass independent verification.

**Automation/GenAI Success (Strategic)**
- **Threat prevention:** ≥1 blocked deepfake/BEC attempt per customer per quarter.
- **Agent readiness:** Policy framework proven with ≥2 AI agent integrations.
- **Enforcement effectiveness:** <0.1% false positive rate on GenAI detectors.

**Commercial Metrics**
- **Revenue targets:** $300-600k ARR by Month 12 (primarily data platform).
- **Customer retention:** ≥50% create second evidence bundle within 14 days.
- **Market validation:** ≥2 public case studies (one data, one automation).
- **Ecosystem adoption:** ≥10 GitHub stars per week; community contributions.

**Operational Excellence**
- **Performance SLAs:** All targets met (15ms Gateway, 20ms Recorder, 2s dbt hooks).
- **Reliability:** >99% bundle verification success rate.
- **Security posture:** Zero critical vulnerabilities; timely patches.
- **15-Factor compliance:** API-first architecture; comprehensive telemetry.

**Strategic Positioning**
- **Industry recognition:** Analyst briefings with Gartner, Forrester on data governance.
- **Standard adoption:** DEF/PEF referenced by competitors or standards bodies.
- **Partnership traction:** Integration partnerships with dbt Labs, Snowflake, Databricks.
- **Thought leadership:** Conference talks, published case studies, industry awards.

---

*End of PRD v4.0*