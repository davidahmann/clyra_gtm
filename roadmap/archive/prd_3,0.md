# **Clyra Platform PRD v3.0**

**Date:** September 2025

**Status:** Finalized for MVP Development (+ frontline “Service” packs; EU AI Act/NIST overlays; PLG refinements; enforcement enhancements)

**License:** Apache 2.0 (OSS)

---

## **0) Business Case (short)**

*Clyra is the audit and enforcement platform for automation runtimes — from AI agents to RPA bots, ETL pipelines, SaaS integrations, and microservices.*

It provides one control point, two guarantees:

- **Clyra Gateway (SchemaLock + Firewall):** Stops malformed/unsafe outputs (fail-closed, OWASP-tagged, threat-classified).
- **Clyra Recorder (Flight Data Recorder):** Proves and replays every change, producing tamper-evident evidence bundles.

**Tagline:** *From pilot to production — with proof.*

Now extended with:

- **AI Firewall features** (threat classification, detectors, kill-switch, ECS/OCSF NDJSON).
- **Compliance attestation packs** (PCI + HIPAA; EU AI Act/NIST overlays).
- **Self-serve PLG motion** (install → demo → attested bundle in <30 min).
- **New enforcement primitives:** idempotency, approval certs, tenant fences, velocity guards, SQL safety checks.
- **Governance pillars embedded in every bundle:** Reliability · Transparency · Accuracy · Oversight

---

## **1) Executive Summary**

**What is Clyra?**

“*Audit & enforcement platform for automation runtimes — From pilot to production, with proof.*”

**Works for:** AI agents, RPA bots, ETL/dbt jobs, SaaS integrations, microservices.

Clyra protects production systems from automation mistakes, makes incidents provable and reproducible, and maps evidence to compliance frameworks.

It intercepts agent/tool/LLM traffic, anchors database state to Postgres WAL LSNs, and produces portable, tamper-evident **PEF v0 bundles** that can be independently verified.

The **10-minute PLG path** takes users from install → verified bundle → offline deterministic replay → signed **attestation report** (PCI/HIPAA/EU AI Act/NIST-ready).

**Strategic wedge:** Establish **PEF** as the neutral forensic & compliance standard that auditors and SIs can verify without trusting Clyra binaries.

---

## **2) The Problem (“Hair-on-Fire”)**

- **Malformed outputs (OWASP LLM-02)** corrupt ERP/CRM/Finance systems.
- **No forensic trail** to show precisely what an automation or agent did.
- **Compliance friction:** PCI/HIPAA/EU auditors block pilots without tamper-evident, independently verifiable evidence.
- **High-risk actions (refunds, address changes, credit limits)** lack enforcement primitives (idempotency, approvals, rate limits).
- **Enterprises cannot answer three critical questions:**
    1. What changed?
    2. Can we prove it?
    3. Does this evidence satisfy my auditor?

---

## **3) The Solution (Forensic Loop + Firewall + Attestation)**

1. **Capture:** HTTP/S proxy with HMAC validation, per-run hash chain, SSE notarization.
2. **SchemaLock:** Stream-validate JSON; auto-repair once else block; signed receipts with OWASP codes, **threat_class**, optional **mitre_id**.
3. **Snapshot:** **Policy-driven metadata snapshots** (not PITR), anchored to Postgres **WAL LSNs**; DSN always hashed.
4. **Diff:** Deterministic comparison (schema drift, row deltas, checksums).
5. **Bundle:** Canonical, signed **PEF v0** with receipts, snapshots, diffs, replay cert, governance + perf/cost/security metrics.
6. **Verify:** Independent Go/TS verifiers, golden vectors.
7. **Replay:** Offline deterministic replay in a scratch schema; signed **Replay Certificate** with {success|partial|failed} status.
8. **Attestation v0:** Signed JSON/PDF summarizing lineage, replay, receipts, **PCI/HIPAA/EU AI Act/NIST** mappings, storage/KMS proofs.
9. **AI Firewall Extensions:** threat_class, OWASP/MITRE mapping, ECS/OCSF NDJSON, kill-switch, pluggable detectors.
10. **New Enforcement Primitives (v3.0):**
    - **Idempotency keys** (one-time use, TTL-bound).
    - **HITL Approval Certificates** (payload-bound, signed).
    - **Velocity guards** (per-route rate/amount limits).
    - **Tenant & actor fences** (header/body/DSN consistency).
    - **SQL-safety guardrails** (block mass updates, require selectors).
    - **Daily review helper** (PCI Req 10 rollups).
    - **Business rules via JSON Schema** (ranges, enums, cross-field).
11. **Compliance Packs:** PCI/HIPAA attestations; EU AI Act Art. 12 and NIST AI RMF overlays.
12. **Frontline “Service” Packs:** Retail, FinServ, Travel/Hospitality schemas + HITL defaults.
13. **Shadow Mode:** Parallel dry-run of new policies with shadow verdicts logged.
14. **Self-serve PLG:** Quickstart demos, verifier badges, runtime stubs, success digests.
15. **Automation-agnostic:** Works for AI agents, RPA, ETL/dbt, SaaS integrations, microservices.

---

## **4) Personas & JTBD**

- **Platform/SRE:** “Don’t let automation blow up prod; give me rollback with SLOs.”
- **Security/Compliance (CISO, GRC):** “Firewall-like enforcement + tamper-evident logs mapped to PCI/HIPAA/EU AI Act/NIST.”
- **System Integrator:** “Compliance-in-a-box I can deploy in 30 days.”
- **AI Engineer / Automation Lead:** “Deterministic repro with minimal glue.”
- **Finance/Procurement:** “Show cost predictability and liability posture with signed evidence.”

---

## **5) Goals & Success Criteria (KPIs)**

**Onboarding:**

- TTVB ≤ 10 min; First Attested Run ≤ 30 min

**Performance:**

- Gateway p95 ≤ 15 ms (≤ +5 ms with detectors + enforcement primitives)
- Recorder p95 ≤ 20 ms
- Snapshot ≤ 50 ms (≤100 tables)
- Diff < 2 s on demo dataset

**Reliability:**

- Lineage conclusive > 99%
- spill_policy=block; no silent drops

**Verifiability:**

- Independent verifiers pass golden vectors
- Attestation validates bundles (PCI/HIPAA attestations; EU AI Act/NIST overlays)

**Adoption:**

- 3+ SI pilots; 1+ auditor validates a bundle
- ≥50% orgs create a second bundle within 14 days
- 2 public case studies (AP/AR + Service Ops)

---

## **6) Scope: In & Out**

**In Scope (MVP Locked):**

- **PostgreSQL 15/16 fully supported; 13/14 demo/pilot only (best-effort)**
  - Clyra doctor warns + exits non-zero unless --allow-best-effort.
- Gateway with SchemaLock receipts (signed, OWASP-tagged, **threat_class**).
- Recorder with HMAC headers, **metadata snapshots (not PITR)**, diffs, replay.
- PEF v0 bundles (canonical JSON, Merkle root, metrics).
- Unified **policy.yaml** (schemas, validators, lineage, body_storage, HITL, **threat_map**, **kill_switch**, cost caps, job/service/pipeline metadata, entry_wedge_examples).
- CLI: quickstart, demo (contracts, etl), doctor, init, policy lint/test/wizard, export, report, verify, replay, attest.
- SDK: Python (headers, decorators, LiteLLM wrapper; retry/backoff helper).
- Scenario Packs: Contracts, AP/AR, ETL/dbt demo, RPA invoice demo.
- Frontline “Service” Packs (Retail, FinServ, Travel/Hospitality; production-lean templates).
- Procurement Kit: sample bundle, verifier, attestation, auditor + buyer one-pagers.
- Public **hello-bundle repo** with CI verifier action.
- Runtime starter stubs (FastAPI, Express, Go chi).
- Success digest output (Merkle root, blocked/allowed counts, verify snippet).
- Verifier badge artifact (CI only; static SVG/PNG + README snippet).
- doctor –suggest-fixes CLI option.
- Independent **Go/TS verifiers**.
- Release integrity: SBOM, cosign, non-root images, key rotation.
- Shadow Mode (logging + optional SIEM forwarding).
- KMS & WORM recipes.
- SIEM-ready NDJSON (ECS/OCSF) + saved searches.
- OTEL/Fluent Bit recipes.
- **New Enforcement Primitives (MVP Locked unless noted):**
  - Idempotency keys (per-route, TTL-bound).
  - HITL Approval Certificates (payload-bound, signed).
  - Velocity guards (per-route).
  - Tenant & actor fences.
  - SQL-safety guardrails (Preview, advisory only).
  - Daily review helper.
  - JSON Schema business rules.

**Out of Scope (Deferred):**

- Other DBs (MySQL, Oracle, etc.).
- SaaS control plane & UI/dashboard.
- Packaged Splunk/Datadog dashboards (MVP ships saved searches).
- WASM detector sandbox & marketplace.
- Rollback orchestration.

---

## **7) Feature Specifications**

### **7.1 Gateway (SchemaLock + Firewall)**

- Stream-validate JSON; auto-repair once; then block.
- Signed receipts with schema hash, policy hash, owasp_code, threat_class, mitre_id, verdict, repair_applied, bypass, key_id, ts, signature.
- Per-run hash chain + SSE notarization.
- Spill_policy=block; bounded queue; 503 on overflow.
- Burst profile + back-pressure metrics.
- NDJSON events → ECS/OCSF.
- **New enforcement fields in receipts:**
  - idempotency_decision, idempotency_key_fingerprint.
  - approval_cert_ref.
  - rate_limit_bucket_state.
  - tenant_fence_check.
  - sql_guard_result.

### **7.2 Recorder (Flight Data Recorder)**

- HMAC headers; policy-driven body_storage + redaction.
- Snapshots: REPEATABLE READ; WAL LSN capture; DSN hashed; replicas rejected.
- Failure codes: PRE_FAIL | LSN_MISSING | POST_TIMEOUT | REPLICA_LAG | POLICY_SKIP.
- Deterministic diffs with stable ordering.
- Replay in scratch schema (clyra_replay_<run_id>); signed Replay Certificate with {success|partial|failed}.

### **7.3 Unified Policy (policy.yaml)**

- Canonicalized; embedded policy_hash.
- Defines schemas, validators, lineage, HITL checkpoints.
- New blocks:
  - idempotency: [{route, ttl_seconds, mode}].
  - approval_cert: [{route, required, mfa_required, max_ttl_seconds}].
  - rate_limits: [{route, key, window, max_actions, max_amount_cents, distinct_targets}].
  - tenant_fences: {required_headers, cross_check, privacy}.
  - sql_guard: {require_selector, rows_affected_limit, allowlist_routes}.
- Threat map, kill_switch, cost caps.
- Automation context fields optional (job_id, service_id, pipeline_id).

### **7.4 Evidence Bundle (PEF v0)**

- Canonical JSON: manifest.json, journal.jsonl, artifacts/.
- Signature object.
- Governance references.
- **New artifacts:** approval certificates, daily_review rollups.
- **Metrics expanded:** idempotency blocks, approval cert usage, rate-limit triggers, fence violations, sql_guard events.

### **7.5 Attestation v0**

- clyra attest evidence.zip –framework <pci|hipaa|eu-ai-act|nist-rmf>.
- JSON (signed) = source of truth; PDF references JSON digest.
- Overlays for EU AI Act + NIST are mappings/labels only (not pass/fail).
- PCI/HIPAA remain enforceable attestation passes.

### **7.6 Detectors**

- Built-ins: regex, jsonpath.
- External HTTP detectors.
- SQL-safety guardrails (Preview, advisory).

### **7.7 SDK & Packs**

- Python SDK minimal: headers, decorators, LiteLLM middleware, retry helper.
- Packs: Contracts, AP/AR, PCI, HIPAA, ETL demo, RPA invoice demo, Service Packs (Retail, FinServ, Travel).

### **7.8 Procurement Kit**

- Auditor one-pager (controls mapping).
- Buyer one-pager (outcomes, risk reduction).
- Hello-bundle repo with CI verifier action.

### **7.9 CLI Coverage**

- clyra quickstart, clyra demo contracts|etl, clyra doctor, clyra init, clyra policy wizard|lint|test, clyra export, clyra report –daily-review, clyra verify, clyra replay, clyra attest.

---

## **8) PLG Experience (10-Minute Quickstart)**

1. Install → brew/apt/tarball.
2. Setup → clyra init → minimal policy.yaml scaffold.
3. Run → clyra quickstart.
4. Demo → clyra demo contracts|etl.
5. Verify → clyra verify evidence.zip or fork hello-bundle.
6. Attest → clyra attest evidence.zip –framework pci.
7. Review → clyra report –daily-review (PCI Req 10 helper).

---

## **9) Cross-Cutting Requirements**

- Snapshots metadata-only.
- Replay always in scratch schema.
- Shadow Mode ≤1 ms overhead.
- Enforcement primitives ≤2 ms combined overhead.
- Opt-in telemetry.
- Non-root images, SBOM, cosign.
- Postgres 15/16 supported, 13/14 demo only.
- Clock skew detection + NTP doctor check.

---

## **10) Risks & Mitigations**

- Perf creep → inline budgets + async tap; k6 gates.
- SQL guard false positives → mark Preview/advisory only.
- HA counters → local mode default, Redis later.
- Compliance bloat → overlays, not new passes.
- Version drift → provider/model metadata optional.

---

## **11) Roadmap (Post-MVP)**

**Phase 1.5:**

- TS SDK.
- Packaged dashboards.
- Helm chart, Istio/Envoy.
- Diff-Agent CLI.
- Rollback manifest pointer.
- WASM detector sandbox.
- Verifier badge gallery.

**Phase 2:**

- Self-hosted control plane.
- Advanced compliance packs.
- Community RFC repo.

**Phase 3:**

- UI/dashboard, SaaS delivery.

---

## **12) Appendices**

- **A:** Glossary.
- **B:** Example policy.yaml (with idempotency, approval certs, rate limits, fences, sql_guard).
- **C:** Example Enforcement Receipt (with idempotency_decision, approval_cert_ref, fence_check).
- **D:** Example PEF Manifest (with new enforcement metrics).
- **E:** Journal Event Schema (ECS/OCSF mappings).
- **F:** Snapshot Clarification (Postgres 15/16 supported; 13/14 demo only).
- **G:** Replay Isolation & Prod-Guard.
- **H:** Doctor Checklist (WAL retention, NTP drift, PG version warnings).
- **I:** Compliance Mapping (PCI, HIPAA, EU AI Act overlays, NIST AI RMF overlays).
- **J:** Procurement Kit contents.
- **K:** OTEL/Fluent Bit recipes.
