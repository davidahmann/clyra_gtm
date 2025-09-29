Clyra Roadmap — Data-led, Agent-ready (with Early Payout Hooks)

0) North Star

What we’re building: the neutral Data Change Control & Attestation layer that also becomes the settlement fabric for automation outcomes (agents, vendors, pipelines).
How we get there: land with Review (listen-only evidence), expand to Gate (enforcement), add Attribution, then Results-based Billing, and finally broaden rails (stablecoin → fiat) as volume and trust grow.

Packaging
 • Clyra Review (land): listen-only, DEF/PEF bundles, daily rollups, ServiceNow/Jira export, verifier, badge.
 • Clyra Gate (upsell): idempotency, fences, velocity caps, kill-switch, SQL guardrails.
 • Clyra Billing Add-On (later): pricing policies, invoice/billing bundles, payout exporters/rails.

⸻

1) Guiding Principles
 • Data-led, agent-ready: dbt/Snowflake/Databricks first; same receipts/policies work for agents later.
 • Evidence before money: signed, portable proof (DEF/PEF) precedes attribution; attribution precedes payouts.
 • Agentless first: start with webhooks/QUERY_HISTORY; proxies/enforcement are opt-in.
 • Minimal viable economics: simulate payouts before money movement; start with stablecoins via trusted custodians.

⸻

2) Horizon Plan

Horizon 0 (0–3 months) — Nail the Data Wedge, Seed Payout Metadata

Objective: Prove value in 2 weeks for data teams; plant identifiers needed for outcomes/payouts later.

Deliver
 • dbt integration: pre/post-run hooks & macros emit DEF v0 (who/what/when, semantic deltas, dbt tests).
 • Listen-only ingestion: dbt Cloud webhooks + dbt Core wrapper (clyra run dbt …).
 • ServiceNow/Jira bridge (one-way): export JSON/CSV → Attested Change Ticket.
 • Verifier + Badge: minimal verifier CLI; “Clyra Certified — SOX Ready.”
 • GenAI risk overlay (shadow): idempotency, rate caps, tenant fences, kill-switch defaults.

Seed payout hooks (metadata-only)
 • Add fields to receipts/bundles: run_id, actor_id, asset_id, change_intent, business_metric_refs[], payout_ref, currency.
 • Finance Pack (stub): “payout candidates” export (JSON/CSV) mapping agent_id|run_id → metric_ref → suggested_value (no billing).

KPIs
 • First attested ticket ≤ 2 weeks; 3 design partners live on Review; 1 paid pilot.

Repo touchpoints (examples)
 • /spec/pef/* (DEF/PEF fields), /verifier/*, /cmd/clyra/export.go, /docs/plg/*, /docs/compliance/*, /examples/quickstart-compose/*.

⸻

Horizon 1 (3–9 months) — Outcome Attribution (Auditable, Cross-Stack)

Objective: Tie safe changes (and agent runs) to measurable outcomes — no billing yet.

New components

 1. Outcome Ledger (append-only)
Records metric observations with: metric_id, value, ts, window, source_system, confidence, actor_id, run_ref(DEF|PEF); ingests from dbt exposures/tests, warehouse queries (QUERY_HISTORY/Delta), reverse-ETL job outcomes.
 2. Attribution Graph
Deterministic linkage from change → downstream assets → business metric (last-touch, time-decay v0). Emits signed Attribution Certificate referencing DEF/PEF run_ids.
 3. Outcome Policies (read-only)
YAML describing allowed metrics, lookback windows, minimum confidence, exclusion periods.

Shadow payout simulation
 • Generate “Shadow Billing Bundles” (JSON + PDF) from Attribution Certificates using hypothetical rate cards; clearly labeled non-settlement.

Agent hooks (lightweight)
 • Allow PEF runs (agents) to write outcomes (e.g., meetings booked, tickets resolved) to the Ledger; receive Attribution Certificates alongside dbt runs.

KPIs
 • 2 customers use Attribution Certs in QBRs; ≥1 public case study “change → metric lift”.

Repo
 • /internal/ledger/, /internal/attr/, /spec/pef/schemas/attribution_certificate.json, /cmd/clyra/attest.go, /docs/attestation.md.

⸻

Horizon 2 (9–18 months) — Results-Based Billing (Opt-in, Enterprise-Safe)

Objective: Convert attributable outcomes into invoices and (optionally) payouts.

New components

 1. Pricing Policy Engine
YAML→rules mapping Attribution Certs to billable units (floors/caps, per-metric rates, risk weights, exclusion windows). Policies are versioned & signed.
 2. Invoice Generator & Exporters
Billing Bundle: invoice.json, line_items.json, policy.yaml, attribution_certs/*.json, evidence_refs + human-readable PDF.
Exports: JSON/CSV first → ServiceNow/Jira ticket; NetSuite/Stripe adapters later.
 3. Dispute Workflow (lightweight)
Mark cert under_review, attach counter-evidence, deterministic re-run.
 4. Payout Rails v1 (stablecoins)
Coinbase Accounts/Prime integration for USDC/EURC corridors; payout receipts chained into DEF/PEF; AP exports (QuickBooks/Xero CSV).
 5. Agent Payouts (optional)
Register agent_id + allowed metrics; compute payouts via same Ledger/Graph; guard with deterministic methods + confidence thresholds.

Monetization
 • SaaS (Review/Gate) + 0.2–0.5% fee on stablecoin payouts (pilot corridors).

Compliance & safety
 • Every billed line traces to signed evidence (DEF/PEF + Attribution Cert).
 • SOX/PCI overlays extended to billing artifacts.

KPIs
 • 1–2 customers piloting outcome-linked payouts or internal chargebacks; <2% monthly disputes; time-to-resolve ≤ 5 days.

Repo
 • /internal/pricing/, /cmd/clyra/billing.go, /spec/pef/*(billing refs), /docs/compliance/* (billing overlays), /docs/sop/disputes.md.

⸻

Horizon 3 (18+ months) — Ecosystem & Standards

Objective: Make Clyra’s artifacts the trusted backbone across finance & audit workflows.

Scale-outs
 • Fiat rails via partners (Stripe Treasury, Wise, bank APIs).
 • Vertical outcome policy templates (Retail/FinServ/SaaS).
 • Auditor partnerships: 2–3 firms accept Billing Bundles as compliant evidence.
 • Open specs: DEF/PEF + Attribution Certs; third-party verifiers and SI playbooks.

KPIs
 • 5+ enterprise customers using Billing Bundles; 2–3 auditor acknowledgments; 3 finance system adapters (NetSuite/Workday/SAP).

⸻

Horizon 4 (3–7 years) — Visa-for-Agents Settlement Layer

Objective: Become the neutral, evidence-anchored settlement fabric for automation and data outcomes.

What it looks like
 • Unified rails (stablecoin + fiat) with Attribution Certificates as the contractable truth for payouts.
 • Agents/vendors register rate cards; enterprises settle via Clyra with auditor-grade proof.
 • Network economics: at scale, a 0.2–0.5% fee across flows creates a $1B+ ARR path.

Prereqs achieved earlier
 • Wide DEF/PEF adoption, auditor acceptance, connectors into AP/ERP, low dispute rates.

⸻

3) Engineering Focus & Guardrails

Performance/SLOs (carry-forward)
 • Gateway p95 ≤ 15 ms; Recorder p95 ≤ 20 ms; dbt hook overhead < 2 s; diff < 2 s on demo.

Security defaults
 • Fail-closed validators, privacy-by-default (no body storage unless enabled), HMAC, mTLS, signed bundles, cosign, SBOMs, Scorecard/OSV/ZAP.

Adoption sequencing
 • Agentless first (webhooks/history), Review first, Gate second, then Attribution, then Billing (simulation → stablecoin → fiat).

Repo discipline
 • Specs first (/spec/pef, /spec/pef/schemas/*), then engines; verifiers remain independent; sensitive paths gated by CODEOWNERS.

⸻

4) GTM & Pricing Hints
 • Land (Review): $25–60k ACV (enterprise) — SOX change control + attestation + SNOW/Jira bridge.
 • Expand (Gate): +30–70% uplift — fewer incidents, provable controls.
 • Billing Add-On: platform fee + per-line or % of attributed value (capped).
 • Payout fees: 0.2–0.5% on stablecoin flows (pilot corridors), fiat when partners are ready.

⸻

5) Risks & Mitigations (pragmatic)
 • Category confusion: Always lead with Data Change Control & Attestation; position Attribution as ROI proof; Billing as opt-in.
 • Integration friction: agentless first; Compose quickstarts; one-way SNOW/Jira early; avoid invasive SDKs.
 • Attribution skepticism: simple, deterministic methods; publish methodology; customer overrides; keep raw Ledger events.
 • Compliance acceptance: minimal, signed formats; ship verifier; secure 2–3 auditor letters early.
 • Money movement risk: simulate first; stablecoin via reputable custody; phased corridors; tight KYC/AML posture through partners.

⸻

6) What’s not changing
 • Recorder + diff/replay + proxy remain the OSS engine.
 • Review → Gate sequencing stays; enforcement is off by default until trust is earned.
 • Agent features leverage the same receipts/policies — no separate stack.

⸻

7) What’s newly emphasized
 • Payout metadata from Day 1 (no money movement).
 • Attribution Certificates before Billing.
 • Stablecoin payouts (small corridors) before fiat.
 • A clear, credible path to the settlement layer without derailing the core data wedge.
