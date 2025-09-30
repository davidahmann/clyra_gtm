# Clyra Vision

# **Vision & Roadmap (2025 → 2030)**

---

## **Vision**

Clyra is the **runtime governance and evidence layer** for automated and AI-driven software.

It provides three guarantees:

1. **Fail-closed enforcement** — stop malformed or unsafe outputs at the boundary (SchemaLock).
2. **Tamper-evident forensics** — capture, hash-chain, and snapshot all changes with WAL-anchored lineage.
3. **Auditor-ready evidence** — signed, portable bundles (PEF) that can be independently verified and mapped to frameworks (PCI, HIPAA, SOX, EU AI Act).

Over five years, Clyra grows from **Postgres + LLM safety** to the **default forensic & control substrate for automation** — whether the actor is an AI agent, RPA bot, ETL pipeline, microservice, or autonomous robot.

---

## **Strategic Positioning**

- **Proof-first:** Signed, independently verifiable bundles (PEF) + offline deterministic replay.
- **Fail-closed:** SchemaLock at the boundary; predictable, low-latency budgets.
- **SIEM-native:** ECS/OCSF NDJSON, OWASP/PCI/HIPAA tags; daily review-ready.
- **Open & neutral:** Public spec + independent verifiers; easy to trust, easy to buy.
- **Automation-agnostic:** Works for AI *and* any high-risk automation (ETL, RPA, ERP/CRM writes).

---

## **Product Roadmap**

### **Year 1 (now–Sep 2026): Win US compliance compelling events**

Objective: Turn **PCI/HIPAA/SOX audit asks** into fast purchases.

- **Core (MVP+):** Gateway (SchemaLock), Recorder (WAL lineage), PEF bundles, offline replay, Go/TS verifiers, CLI quickstart, SIEM recipes, kill-switch, detector plug-ins, Attestation v0.
- **Compliance packs (US):**
  - **PCI DSS 4.0.1:** Req 10 logging/monitoring; ingest partner logs (6.4.3 / 11.6.1).
  - **HIPAA Security Rule:** 45 CFR 164.312(b), (c)(1) — audit controls + integrity.
  - **SOX ITGC:** Attestation fields for “who/what/when” change control.
- **Relia:** Bundle deny-by-default allowlists, redaction, HITL, kill-switch into a named governance module.
- **Developer reach:** Python SDK (LiteLLM wrapper, MCP/tool decorators); scenario packs (Contracts, AP/AR); one **non-AI demo pack** (ETL pipeline / RPA).
- **Metrics:** TTVB ≤10 min; ≥3 SI pilots; ≥1 external audit validated with Clyra artifacts.

---

### **Year 2 (Oct 2026–Sep 2027): Determinism & identity hardening**

Objective: Improve predictability and eliminate standing secrets.

- **Atlas (ContextCraft SDK v1):** Context hygiene middleware (prefix locks, append-only logs, isolation).
- **Guard (AgentScope Gateway v1):** Least-privilege broker (JIT STS/OAuth creds, ephemeral tokens, immutable ledger → PEF).
- **TypeScript SDK & tests.**
- **EU readiness pilots:** Map Attestation v0 to AI Act logging/traceability/post-market monitoring (full applicability Aug 2026; some extensions 2027).

---

### **Year 3 (Oct 2027–Sep 2028): Deterministic runtime & reliability**

Objective: Make workflows predictable & testable.

- **Lumyn (Deterministic runtime v1):** Compile narrow agent/automation patterns into finite-state graphs with schema contracts.
- **Trace (TraceEval v1):** Scenario-driven evals using PEF/replay as ground truth.
- **Evidence Registry (self-hosted):** Retention, legal hold, attestation automation.
- **SIEM packs:** Prebuilt dashboards (Splunk/Datadog) for OWASP events, blocks, kill-switch triggers.

---

### **Year 4 (Oct 2028–Sep 2029): Data foundation & inter-org evidence**

Objective: Safer experimentation and inter-team proof.

- **Visus (OSS data/memory v1):** PG-compatible fork-on-write branching, time travel, vector columns.
- **Inter-org PEF exchange:** Vendors/customers share signed bundles.
- **GRC/insurer hand-offs:** Map attestations to GRC tools; explore evidence-based insurance discounts.

---

### **Year 5 (Oct 2029–Sep 2030): Default audit/control layer**

Objective: Standardize; widen reach.

- **Control plane (SaaS/managed option):** Evidence registry & policy pack distribution.
- **Policy/Detector marketplace:** Curated OWASP-mapped detectors, quarterly updates.
- **Certification program:** “Clyra-Attested Workflow” badges for partners/SIs.

---

## **PEF Evolution (compatibility-first)**

- **v0 (MVP):** trace, snapshot_manifest, diff_report, replay_certificate, manifest.
- **v0.1 (Phase 1):** dataset_manifest (training/eval set fingerprints), regulatory_tags.
- **v0.2 (Phase 2):** simulation_manifest + sim_replay_certificate.
- **v0.3 (Phase 3):** sensor_manifest (video/LiDAR/audio hashes/pointers), action_log, safety_envelope.
- **v1.0 (Phase 4/5):** Stable schemas; regulator tags (PCI/HIPAA/AI Act); remote attestation fields.

---

## **Industries (sequenced)**

1. Payments & ecommerce — PCI deadlines (Req 10; 6.4.3/11.6.1).
2. Healthcare — HIPAA audit controls & integrity.
3. FinServ/Fintech SaaS — SOX/GLBA posture; SOC2.
4. B2B SaaS / Ops tech — ERP/CRM write paths; contracts/AP/AR.
5. Insurance, logistics, manufacturing — evidence + replay for ERP/claims.
6. Public sector (select) — where self-host + evidence mandates are clear.
7. **Expansion (post-2027):** Robotics, industrial autonomy, safety-critical ops (sensor & sim manifests).

---

## **Geographies**

- **Years 1–2:** US focus (PCI/HIPAA/SOX).
- **Years 2–3:** EU/UK pilots (AI Act alignment).
- **Years 3–5:** Canada, DACH, Nordics; selective APAC (audit-heavy markets).

---

## **Go-to-Market**

- **System Integrators:** Primary sellers; compliance-in-a-box kits + attestations.
- **Security & platform teams:** Secondary; SIEM recipes, kill-switch demos.
- **Partners:** PCI vendors, identity/cloud security, GRC suites.
- **Cloud marketplaces:** Private offers later; self-host always available.

---

## **Standards & mappings (anchors)**

- **PCI DSS 4.0.1:** Req 10, 6.4.3/11.6.1.
- **HIPAA Security Rule:** 164.312(b), (c)(1).
- **SOX ITGC:** Change control.
- **OWASP LLM Top-10:** Tag receipts.
- **EU AI Act:** Logging/traceability, post-market monitoring.

---

## **Priority Use Cases Beyond LLMs**

- ETL pipelines / RPA bots: schema drift + replay proof.
- Robotics/industrial autonomy: sim replay + sensor forensics.
- Synthetic data pipelines: dataset provenance & compliance packs.
- Safety-critical ops: shadow-mode safety envelopes + HITL.

---

## **Success Metrics**

- TTVB ≤10 min; First Attested Run ≤30 min.
- p95 ≤15 ms (security add-ons ≤5 ms).
- Audits passed with Clyra artifacts.
- % lineage conclusive; % evidence WORM-retained.
- Logos in PCI/HIPAA segments; SI-led deals; ≥50% repeat usage in 14 days.

---

## **Risks & Mitigations**

- **Platform sprawl:** Ship config-first features; defer DSLs.
- **Performance regression:** CI perf gates; publish perf in bundles.
- **PCI scope creep:** Ingest partner data; don’t build a browser agent.
- **Over-promising compliance:** Provide evidence & mappings, not certification.
- **Media bloat (future phases):** Hash/pointer only; externalize heavy artifacts.

---

## **Bottom Line**

Clyra starts as the **compliance firewall + forensic recorder** for US enterprises (PCI, HIPAA, SOX).

It hedges against “AI agent hype” by covering **any automation**.

By 2030, it will expand into **datasets, simulations, sensors, and actions** — making PEF the **standard evidence format** for both digital and physical AI.

---
