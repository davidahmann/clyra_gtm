# Clyra Strategic Roadmap v2.0

## Data-Led Market Entry, Agent-Ready Architecture, Results-Based Billing Vision

**Last Updated:** 2025-09-29
**Status:** Strategic Planning Document

---

## Executive Summary

**What we're building:** The neutral Data Change Control & Attestation layer that proves every change is safe and audit-ready—and grows into the trusted settlement fabric for paying people, vendors, and AI agents based on verified results.

**How we get there:** Land with data platform evidence (dbt/warehouses), expand to enforcement, add attribution and results-based billing, then broaden to AI agents via MCP when timing is right.

**Strategic Positioning:**

- **Primary wedge:** Data platform (dbt, Snowflake, Databricks, reverse-ETL) where budget exists TODAY
- **Agent-ready architecture:** Same enforcement engine, same evidence formats (DEF/PEF), ready for AI agents TOMORROW
- **Parallel optionality:** MCP Airlock as strategic hedge—can accelerate or defer based on market signals

---

## 0. North Star & Guiding Principles

### North Star Vision

> "Clyra makes sure every data or agent change is safe and audit-ready today, and is growing into the trusted system that lets companies pay people, vendors, and AI agents based on verified results tomorrow."

### Guiding Principles

1. **Data-led, agent-ready:** Prove value with dbt/Snowflake/Databricks first; same receipts/policies work for agents later
2. **Evidence before money:** Signed, portable proof (DEF/PEF) precedes attribution; attribution precedes payouts
3. **Progressive adoption:** Review (listen-only) → Gate (enforcement) → Attribution → Billing
4. **Minimal viable economics:** Simulate payouts before money movement; start with stablecoins via trusted custodians
5. **Disciplined sequencing:** Prove core thesis before expanding surface area

### Product Packaging

- **Clyra Review** (land): Listen-only detection, DEF/PEF bundles, ServiceNow/Jira export, badge program
- **Clyra Gate** (expand): Full enforcement with idempotency, fences, velocity caps, kill-switch, SQL guardrails
- **Clyra Airlock (MCP)** (strategic option): Agent security & connectivity for MCP protocol—activates when market signals confirm
- **Clyra Attribution** (future): Outcome ledger, attribution certificates, ROI proof
- **Clyra Billing** (future): Results-based pricing, invoice generation, payout rails

---

## 1. Horizon 0 (Months 0-3) — Nail the Data Wedge

### Objective

Prove value in ≤2 weeks for data teams; achieve product-market fit with data platform wedge.

### What Ships (MVP v4.0)

#### Data Platform Core

- ✅ **dbt Integration:** Hooks (pre/post-run), macros (SQL safety), CI gates, semantic delta detection
- ✅ **Warehouse Anchors:** Snowflake (QUERY_HISTORY + session tags), Databricks (Delta commits), Postgres (WAL LSN)
- ✅ **DEF v0 Format:** Data Evidence Format with warehouse-native anchoring, deterministic replay
- ✅ **Activation Gateway:** HTTP proxy for reverse-ETL (Hightouch/Census) with enforcement primitives
- ✅ **Listen-Only Ingestion:** dbt Cloud webhooks + dbt Core wrapper (`clyra run dbt`)

#### ServiceNow/Jira Bridge (MVP)

- ✅ **One-way export:** DEF/PEF bundles → Attested Change Ticket (JSON/CSV → REST API)
- ✅ **Ticket format:** Attestation hash, verification link, compliance status, evidence attachment

#### Badge Program

- ✅ **Verification service:** Independent Go/TS verifiers run offline
- ✅ **Badge issuance:** "Clyra Certified - SOX Compliant" badges for dbt projects
- ✅ **Badge endpoint:** `clyra.io/badge/{framework}/{project-id}` with JWT signing

#### Enhanced Universal Foundation

- ✅ **Gateway:** SchemaLock + Data Firewall with GenAI threat detection
- ✅ **Recorder:** Flight Data Recorder with HMAC ingestion, metadata snapshots, warehouse anchoring
- ✅ **Replay Engine:** Deterministic reproduction in scratch schemas
- ✅ **Bundle Builder:** Unified DEF/PEF formats with Merkle trees, governance metadata

#### GenAI Security (Shadow Mode)

- ✅ **Threat detection:** OWASP LLM mapping, prompt injection heuristics
- ✅ **BEC-grade approvals:** SSO binding, challenge-response, payload hash binding
- ✅ **Kill-switch:** Multi-trigger system (data + GenAI + universal)

#### Seed Payout Metadata (No Billing Logic)

- ✅ **Receipt fields:** `run_id`, `actor_id`, `asset_id`, `change_intent`, `business_metric_refs[]`, `payout_ref`, `currency`
- ✅ **Finance Pack stub:** "Payout candidates" export (JSON/CSV) mapping `agent_id|run_id → metric_ref → suggested_value`
- ✅ **No money movement:** Metadata-only preparation for Horizon 2

#### MCP Airlock Foundation (Schema-Only)

- ✅ **PEF v0 MCP extension:** Optional MCP fields in evidence schema (backward compatible)
- ✅ **Strategic roadmap:** `/docs/mcp/ROADMAP.md` documenting vision and decision gates
- ✅ **No enforcement logic:** Schema prep only, activates in Horizon 1B if market validates

### Success Criteria (Horizon 0)

**Technical:**

- ✅ First attested ticket generated in ≤2 weeks from installation
- ✅ Performance SLAs met: Gateway ≤15ms p95, Recorder ≤20ms p95, dbt hook <2s overhead
- ✅ Cross-verifier consistency: Go/TS verifiers produce identical results

**Business:**

- ✅ 3 design partners live on Clyra Review
- ✅ 1+ paid pilot ($25-60k ACV)
- ✅ 100+ GitHub stars from dbt community
- ✅ 10+ dbt projects displaying Clyra Certified badges

**Strategic:**

- ✅ ServiceNow/Jira integration proven in production
- ✅ 1+ auditor acknowledges DEF/PEF evidence format
- ✅ Badge program shows viral growth (≥50% badge adopters refer others)

### Repository Touchpoints

```
/spec/pef/* (DEF/PEF schemas + MCP extension)
/internal/warehouse/ (Snowflake/Databricks/Postgres anchoring)
/internal/dbt/ (hooks, macros, CI gates)
/internal/activation/ (reverse-ETL proxy)
/bridges/servicenow/ (REST client, ticket formatter)
/bridges/jira/ (Atlassian SDK, issue formatter)
/internal/badge/ (certification service, JWT signing)
/verifier/* (Go/TS independent verifiers)
/cmd/clyra/review/ (listen-only commands)
/docs/plg/* (10-minute PLG path)
/examples/quickstart-data/ (dbt demo project)
```

---

## 2. Horizon 1 (Months 3-9) — Enforcement + Outcome Attribution

### Decision Gate (Required Before Starting)

- ✅ 3+ paying customers on Clyra Review
- ✅ $300k+ ARR from data platform wedge
- ✅ 1+ auditor acknowledged DEF/PEF formats
- ✅ ServiceNow/Jira integration proven in production
- ✅ Badge program achieving >50% referral rate

### Objective

Enable full enforcement (Clyra Gate) for data platform customers AND tie changes to measurable business outcomes—no billing yet.

---

### Horizon 1A: Enforcement Activation (Primary Track)

#### What Ships

**Clyra Gate (Full Enforcement)**

- ✅ **Policy enforcement:** Allow/deny/HITL for data changes with <10ms latency overhead
- ✅ **Enhanced primitives:** BEC-grade approvals, prompt-loop breakers, voice session fences, CI/CD controls
- ✅ **Kill-switch activation:** Multi-trigger enforcement (schema bursts + GenAI threats + error spikes)
- ✅ **SQL safety guards:** Advisory blocks on mass UPDATE/DELETE, rows_affected limits, allowlist maintenance
- ✅ **Advanced GenAI security:** Full threat detection, external detector integration, shadow mode promotion

**Enhanced ServiceNow/Jira Integration**

- ✅ **Two-way sync:** Ticket status updates flow back to Clyra for audit trail
- ✅ **Approval workflows:** HITL approvals via ServiceNow/Jira with cryptographic binding
- ✅ **Badge automation:** Automatic badge issuance on successful attestation

**Compliance Expansion**

- ✅ **Multi-framework attestations:** SOX ITGC, PCI DSS, HIPAA, EU AI Act, NIST AI RMF, TCPA
- ✅ **Automated daily reviews:** Enhanced with data changes + GenAI threat posture
- ✅ **Auditor toolkit:** Verification guides, evidence validation procedures, framework mappings

#### Success Criteria (1A)

- ✅ 10+ customers on Clyra Review, 3+ converted to Clyra Gate
- ✅ ≥30% Review → Gate conversion within 90 days
- ✅ Kill-switch drills: 100% success (blocked within 5s)
- ✅ Zero critical security vulnerabilities
- ✅ $500k+ ARR (70% Review, 30% Gate)

---

### Horizon 1B: Agent Security via MCP Airlock (Parallel Track - CONDITIONAL)

**⚠️ DECISION GATE: Only activate if ANY of these signals appear:**

1. ≥2 existing customers explicitly request agent security/MCP support
2. MCP adoption reaches critical mass (≥10k GitHub stars, ≥3 major platforms integrated)
3. Real security incidents create CISO demand (malicious MCP servers, credential leakage)
4. Strategic opportunity to own agent security category emerges
5. Competitive threat: observability vendors add agent security features

#### What Ships (If Activated)

**Clyra Airlock Review (MCP)**

- ✅ **MCP pass-through proxy:** Transparent relay with request/response canonicalization
- ✅ **Policy matcher (dry-run):** Evaluate policies, log verdicts, no enforcement
- ✅ **Signed receipts:** PEF v0 bundles with MCP extension fields
- ✅ **Identity integration:** Okta/Entra OIDC with OAuth 2.0 Token Exchange (RFC 8693)
- ✅ **Connectivity edge:** WebSocket reverse tunnel (client/server both dial out)
- ✅ **Supply-chain allowlist:** Signed manifests for approved MCP servers (GitHub, Jira, Slack, etc.)
- ✅ **HITL approvals:** Slack/Teams integration for write operations
- ✅ **ServiceNow/Jira export:** "Attested Agent Action" tickets

**Time to Ship:** 12 weeks with dedicated team (2-3 engineers)

**Investment Required:** ~$150-300k (engineering + design partner support)

#### Success Criteria (1B - If Shipped)

- ✅ TTFSC (Time-to-First Secure Call) < 60 minutes
- ✅ Standing credentials: 0 long-lived secrets in agent runtime
- ✅ Coverage: ≥90% of MCP calls produce valid receipts
- ✅ 2+ design partners running real workflows
- ✅ $100-200k ARR from MCP-specific deployments

#### Repository Impact (If Activated)

```
/internal/mcp/ (proxy, policy adapter, canonicalization)
/internal/identity/ (STS, DPoP, OIDC adapters)
/internal/connect/ (WebSocket relay, tunnel management)
/cmd/clyra/airlock/ (MCP-specific commands)
/examples/mcp-quickstart/ (GitHub, Jira demos)
/docs/mcp/ (quickstart, policy examples, IdP setup)
```

**Risk Mitigation:**

- ✅ Start only after data platform thesis proven
- ✅ Dedicate separate team (doesn't block data platform work)
- ✅ Reuse 70-80% of existing Clyra architecture
- ✅ Can defer indefinitely if market doesn't validate

---

### Horizon 1C: Outcome Attribution (Primary Track)

#### What Ships

**Outcome Ledger (Append-Only)**

- ✅ **Metric observations:** `metric_id`, `value`, `ts`, `window`, `source_system`, `confidence`, `actor_id`, `run_ref` (DEF/PEF)
- ✅ **Ingestion sources:** dbt exposures/tests, warehouse queries (QUERY_HISTORY/Delta), reverse-ETL job outcomes
- ✅ **Privacy-preserving:** Metadata-only, no raw data storage

**Attribution Graph**

- ✅ **Deterministic linkage:** Change → downstream assets → business metric (last-touch, time-decay v0)
- ✅ **Attribution Certificates:** Signed certificates referencing DEF/PEF `run_ids`
- ✅ **Lineage visualization:** CLI-based lineage display (`clyra verify --validate-lineage`)

**Outcome Policies (Read-Only)**

- ✅ **Policy YAML:** Allowed metrics, lookback windows, minimum confidence, exclusion periods
- ✅ **Shadow billing simulation:** Generate "Shadow Billing Bundles" (JSON + PDF) with hypothetical rate cards
- ✅ **Clear non-settlement labels:** All simulation outputs clearly marked as non-binding

**Agent Hooks (Lightweight)**

- ✅ **PEF runs:** Agents write outcomes (meetings booked, tickets resolved) to Outcome Ledger
- ✅ **Attribution parity:** Agents receive Attribution Certificates alongside dbt runs
- ✅ **Same evidence chain:** Agent outcomes use same DEF/PEF verification

#### Success Criteria (1C)

- ✅ 2+ customers use Attribution Certificates in QBRs
- ✅ ≥1 public case study: "change → metric lift"
- ✅ Shadow billing simulations run successfully for 3+ customers
- ✅ Zero disputes on attribution methodology (deterministic + transparent)

#### Repository Impact

```
/internal/ledger/ (append-only outcome storage)
/internal/attr/ (attribution graph, certificate generation)
/spec/pef/schemas/attribution_certificate.json
/cmd/clyra/attest.go (extended for attribution)
/docs/attribution.md (methodology, examples)
```

---

## 3. Horizon 2 (Months 9-18) — Results-Based Billing

### Decision Gate (Required Before Starting)

- ✅ 5+ customers actively using Attribution Certificates
- ✅ ≥3 customers request results-based billing capabilities
- ✅ $1M+ ARR from Review/Gate
- ✅ 2+ auditors acknowledge evidence format
- ✅ Zero critical security vulnerabilities for 6+ months

### Objective

Convert attributable outcomes into invoices and (optionally) payouts—opt-in, enterprise-safe.

### What Ships

#### Pricing Policy Engine

- ✅ **Policy YAML:** Mapping Attribution Certs → billable units (floors/caps, per-metric rates, risk weights)
- ✅ **Versioning:** Policies are versioned & signed, immutable after application
- ✅ **Customer overrides:** Manual adjustments with audit trail

#### Invoice Generator & Exporters

- ✅ **Billing Bundle format:** `invoice.json`, `line_items.json`, `policy.yaml`, `attribution_certs/*.json`, evidence refs
- ✅ **Human-readable PDF:** Auditor-friendly invoice with evidence links
- ✅ **Export targets:** JSON/CSV → ServiceNow/Jira tickets, NetSuite/Stripe adapters (later)

#### Dispute Workflow (Lightweight)

- ✅ **Mark under review:** Certificate status tracking with counter-evidence attachment
- ✅ **Deterministic re-run:** Replay capability for disputed attribution
- ✅ **Resolution tracking:** Time-to-resolve metrics, dispute rate monitoring

#### Payout Rails v1 (Stablecoins)

- ✅ **Coinbase integration:** Coinbase Accounts/Prime for USDC/EURC corridors
- ✅ **Payout receipts:** Chained into DEF/PEF evidence trail
- ✅ **AP exports:** QuickBooks/Xero CSV format
- ✅ **KYC/AML:** Partner-provided compliance through Coinbase

#### Agent Payouts (Optional)

- ✅ **Agent registration:** `agent_id` + allowed metrics + rate limits
- ✅ **Same Ledger/Graph:** Compute payouts via same attribution engine
- ✅ **Safety guards:** Deterministic methods + confidence thresholds + human review gates

### Monetization Model

- **SaaS revenue:** Clyra Review ($25-60k) + Gate ($75-150k)
- **Platform fee:** 0.2-0.5% on stablecoin payouts (pilot corridors only)
- **Enterprise Plus:** Custom billing packs, dedicated success manager

### Compliance & Safety

- ✅ **Evidence traceability:** Every billed line traces to signed evidence (DEF/PEF + Attribution Cert)
- ✅ **SOX/PCI overlays:** Extended to billing artifacts
- ✅ **Auditor acceptance:** Billing Bundles accepted as compliant evidence
- ✅ **Dispute resolution SLA:** <5 days time-to-resolve

### Success Criteria (Horizon 2)

- ✅ 1-2 customers piloting outcome-linked payouts or internal chargebacks
- ✅ <2% monthly dispute rate
- ✅ Time-to-resolve disputes ≤5 days
- ✅ $50-100k revenue from platform fees (stablecoin corridors)
- ✅ 1+ auditor accepts Billing Bundles as SOX/PCI evidence

### Repository Impact

```
/internal/pricing/ (policy engine, rate calculation)
/internal/billing/ (invoice generation, exports)
/internal/payout/ (stablecoin rails, payout receipts)
/cmd/clyra/billing.go (billing commands)
/spec/pef/schemas/billing_bundle.json
/docs/compliance/* (billing overlays)
/docs/sop/disputes.md (dispute workflow)
```

---

## 4. Horizon 3 (Months 18-36) — Ecosystem & Standards

### Decision Gate

- ✅ 5+ enterprise customers using Billing Bundles
- ✅ 2-3 auditor acknowledgments (Big 4 firms)
- ✅ $2M+ ARR with healthy unit economics
- ✅ <1% dispute rate sustained over 6 months

### Objective

Make Clyra's artifacts the trusted backbone across finance & audit workflows.

### What Ships

#### Fiat Rails

- ✅ **Partner integrations:** Stripe Treasury, Wise, bank APIs for USD/EUR/GBP
- ✅ **Compliance:** Enhanced KYC/AML through banking partners
- ✅ **Cross-border:** Multi-currency support with FX transparency

#### Vertical Templates

- ✅ **Industry packs:** Retail, FinServ, Healthcare, SaaS-specific outcome policies
- ✅ **Compliance mappings:** Industry-specific regulatory frameworks
- ✅ **Best practices:** Reference architectures, policy templates, auditor guides

#### Auditor Partnerships

- ✅ **Big 4 acknowledgment:** 2-3 firms accept Billing Bundles as compliant evidence
- ✅ **Training programs:** Auditor certification on Clyra verification
- ✅ **Hotline service:** Direct support for auditors during engagements

#### Open Standards

- ✅ **DEF/PEF spec publication:** Vendor-neutral format specification
- ✅ **Attribution Certificate standard:** Open format for outcome attribution
- ✅ **Third-party verifiers:** Community-built verifiers in additional languages
- ✅ **SI playbooks:** System integrator implementation guides

#### MCP Airlock Gate (If 1B Shipped)

- ✅ **Full enforcement:** Allow/deny/HITL for MCP operations
- ✅ **STS Token Exchange:** Complete OAuth 2.0 Token Exchange implementation
- ✅ **Signed allowlist enforcement:** Only approved MCP servers can connect
- ✅ **Advanced rate & arg constraints:** Per-tool rate limits, argument validation

### Success Criteria (Horizon 3)

- ✅ 5+ enterprise customers using Billing Bundles
- ✅ 2-3 auditor acknowledgments from Big 4 firms
- ✅ 3+ finance system adapters (NetSuite/Workday/SAP)
- ✅ 10+ SI partners implementing Clyra
- ✅ DEF/PEF referenced by competitors/standards bodies

### Monetization Evolution

- **Core SaaS:** Review ($25-60k) + Gate ($75-150k) + Enterprise Plus (custom)
- **Platform fees:** 0.2-0.5% on payment flows (stablecoin + fiat)
- **Partner revenue:** SI referral fees, auditor program fees

---

## 5. Horizon 4 (Years 3-7) — Settlement Layer Vision

### Objective

Become the neutral, evidence-anchored settlement fabric for automation and data outcomes—the "Visa for agents, data, and verified work."

### What It Looks Like

**Unified Rails**

- ✅ **Multi-currency:** Stablecoin + fiat with unified API
- ✅ **Attribution Certificates:** Contractable truth for all payouts
- ✅ **Network effects:** Agents/vendors register rate cards, enterprises settle via Clyra

**Trust Spine**

- ✅ **Auditor-grade proof:** Every payment traces to signed evidence
- ✅ **Dispute resolution:** <24hr resolution with deterministic replay
- ✅ **Compliance by default:** SOX/PCI/HIPAA/EU AI Act built into flows

**Network Economics**

- ✅ **Platform fees:** 0.2-0.5% across payment flows
- ✅ **Scale path:** At volume, creates $1B+ ARR opportunity
- ✅ **Neutral positioning:** Independent from any cloud/AI vendor

### Prerequisites (Achieved in Earlier Horizons)

- ✅ Wide DEF/PEF adoption across data + AI industries
- ✅ Auditor acceptance as standard evidence format
- ✅ Connectors into AP/ERP systems of major enterprises
- ✅ <1% dispute rate sustained over 24+ months
- ✅ Regulatory clarity on stablecoin/crypto settlement

---

## 6. Engineering Discipline & Guardrails

### Performance SLAs (Carried Forward All Horizons)

- **Data Platform:** dbt hook <2s, warehouse queries <5s, activation proxy <15ms p95
- **GenAI Security:** prompt analysis <100ms, external detectors <500ms, kill-switch <1s
- **Universal:** Gateway ≤15ms p95, Recorder ≤20ms p95, evidence bundles <5s DEF/<3s PEF

### Security Defaults (Non-Negotiable)

- **Fail-closed:** All validators fail closed on errors
- **Privacy-by-default:** No body storage unless explicitly enabled
- **Cryptographic integrity:** HMAC, mTLS, Ed25519 signatures, cosign verification
- **Supply chain:** SBOMs, Scorecard, OSV scanning, SLSA Level 3
- **Continuous testing:** OWASP ZAP, k6 performance, golden vector validation

### Adoption Sequencing (Locked)

1. **Agentless first:** Webhooks/QUERY_HISTORY before proxies
2. **Review first:** Listen-only before enforcement
3. **Gate second:** Prove value before blocking operations
4. **Attribution third:** Prove outcomes before billing
5. **Billing last:** Simulate before real money movement

### Repository Discipline

- **Specs first:** `/spec/pef`, `/spec/pef/schemas/*` defined before implementation
- **Verifiers independent:** Go/TS verifiers remain standalone, no core dependencies
- **CODEOWNERS:** Sensitive paths (enforcement, billing) require senior review
- **Golden vectors:** All format changes require test vector updates

---

## 7. GTM & Pricing Evolution

### Horizon 0-1: Land & Expand (Data Platform)

**Clyra Review** — $25-60k/year

- Listen-only detection, DEF/PEF bundles, ServiceNow/Jira export, badge program
- Hook: "Start safe with listen-only mode"

**Clyra Gate** — $75-150k/year (+30-70% uplift)

- Everything in Review + full enforcement, advanced GenAI security, kill-switch
- Hook: "Graduate to full enforcement when ready"

### Horizon 1B: Agent Security (If Activated)

**Clyra Airlock Review (MCP)** — $20-50k/year

- MCP monitoring, signed receipts, policy dry-run, ServiceNow/Jira export
- Hook: "Extend data controls to AI agents"

**Clyra Airlock Gate (MCP)** — $75-150k/year

- Everything in Airlock Review + full enforcement, STS, signed allowlists
- Hook: "Zero standing credentials for agents"

### Horizon 2: Results-Based Billing

**Clyra Attribution** — $10-25k/year add-on

- Outcome ledger, attribution certificates, shadow billing simulation
- Hook: "Prove ROI with outcome attribution"

**Clyra Billing** — Platform fee + 0.2-0.5% on payment flows

- Invoice generation, payout rails (stablecoin first), dispute resolution
- Hook: "Pay based on verified results"

### Horizon 3+: Enterprise & Ecosystem

**Enterprise Plus** — Custom ($200k+/year)

- Multi-framework compliance packs, dedicated success manager, custom detector development
- Hook: "Enterprise-scale data governance + results-based billing"

**Add-On Services:**

- **Forensic Accelerator** ($5k): PCI/HIPAA attestation setup, 30 days consulting
- **Auditor Confidence Pack** ($7.5k): Independent verification training, custom templates

---

## 8. Risk Management & Decision Framework

### Technical Risks

| Risk | Mitigation | Owner |
|------|-----------|-------|
| Data platform integration complexity | Phased rollout, design partners, comprehensive docs | Product |
| GenAI false positives | Shadow mode defaults, tunable thresholds | Engineering |
| Performance impact | Strict SLA enforcement, continuous monitoring | Platform |
| Attribution methodology disputes | Deterministic algorithms, transparent methodology, customer overrides | Data Science |
| MCP spec evolves rapidly | Pluggable proxy, versioned receipts, feature flags | Engineering (if 1B active) |

### Market Risks

| Risk | Mitigation | Owner |
|------|-----------|-------|
| Message confusion | Lead with "Data Change Control & Attestation" | Marketing |
| dbt/Snowflake build competing features | Partner positioning, independent verifier moat | BD/Product |
| Enterprise integration friction | ServiceNow/Jira bridges, listen-only start, badge social proof | Sales/Eng |
| Agent security timing wrong | Horizon 1B decision gate with clear activation criteria | Leadership |
| Payment vision creates category confusion | Always lead with compliance value, position billing as opt-in | CEO/Marketing |

### Operational Risks

| Risk | Mitigation | Owner |
|------|-----------|-------|
| Compliance burden | Automated validation, comprehensive docs | Compliance |
| Security vulnerabilities | Continuous scanning, rapid response | Security |
| Money movement risk (H2) | Simulate first, stablecoin via custody, phased corridors | CFO/Legal |
| Execution bandwidth | Clear decision gates, dedicated teams for parallel tracks | CEO/CTO |

### Decision Framework for MCP Airlock (Horizon 1B)

**Activate if ANY of these conditions met:**

1. ≥2 existing customers explicitly request MCP support
2. MCP GitHub stars >10k AND ≥3 major platforms integrated
3. ≥3 documented security incidents create CISO demand
4. Strategic category ownership opportunity (first mover advantage)
5. Competitive threat emerges (observability vendors adding agent security)

**Requirements before activation:**

- ✅ Horizon 0 success criteria fully met
- ✅ $300k+ ARR from data platform
- ✅ Dedicated team available (2-3 engineers for 12 weeks)
- ✅ Design partners committed to pilot

**Defer if:**

- ❌ Data platform thesis not yet proven
- ❌ Execution bandwidth constrained
- ❌ Market signals unclear
- ❌ Higher ROI opportunities exist

---

## 9. Success Metrics by Horizon

### Horizon 0 (Months 0-3)

- **Technical:** First attested ticket ≤2 weeks, SLAs met, cross-verifier consistency
- **Business:** 3 design partners, 1 paid pilot, 100+ GitHub stars
- **Strategic:** ServiceNow/Jira integration proven, 1+ auditor acknowledgment

### Horizon 1A (Months 3-9) — Enforcement

- **Technical:** <10ms enforcement overhead, 100% kill-switch drill success
- **Business:** 10+ Review customers, 3+ Gate conversions, ≥30% conversion rate
- **Revenue:** $500k+ ARR (70% Review, 30% Gate)

### Horizon 1B (Months 3-9) — MCP Airlock (If Activated)

- **Technical:** TTFSC <60 min, 0 standing credentials, ≥90% receipt coverage
- **Business:** 2+ design partners, real workflows in production
- **Revenue:** $100-200k ARR from MCP deployments

### Horizon 1C (Months 3-9) — Attribution

- **Technical:** Deterministic attribution, zero methodology disputes
- **Business:** 2+ customers using Attribution Certs in QBRs, ≥1 public case study
- **Strategic:** Shadow billing simulation proven

### Horizon 2 (Months 9-18)

- **Technical:** <5 day dispute resolution, evidence traceability 100%
- **Business:** 1-2 customers piloting payouts, <2% dispute rate
- **Revenue:** $50-100k from platform fees (stablecoin)

### Horizon 3 (Months 18-36)

- **Technical:** Fiat rails operational, <1% dispute rate sustained
- **Business:** 5+ enterprises on Billing Bundles, 2-3 Big 4 acknowledgments
- **Revenue:** $2M+ ARR, healthy unit economics

### Horizon 4 (Years 3-7)

- **Strategic:** Industry standard for data/agent evidence and settlement
- **Network:** Wide DEF/PEF adoption, SI ecosystem, auditor acceptance
- **Revenue:** $1B+ ARR path via platform fees at scale

### Timeline Realism & Market Evolution

#### Years 0-2: Evidence & Enforcement Revenue
- **Focus:** Sell evidence/enforcement → win SOX/dbt/Snowflake budgets
- **Revenue:** SaaS subscriptions (Review + Gate)
- **Target:** $300k-$1M ARR

#### Years 2-4: Outcome Attribution Standard
- **Focus:** Add outcome attribution → become ROI measurement standard
- **Revenue:** SaaS + Attribution add-on
- **Target:** $1M-$5M ARR

#### Years 4-6: Settlement Fabric Emergence
- **Scope:** Enterprise settlement between known parties (vendors, contractors, agents, internal chargebacks)
- **Position:** Middleware layer exporting to NetSuite/SAP/QuickBooks/Coinbase
- **Revenue Model:** Transaction fees (0.25-0.5%) become viable as trust is proven
- **Trust Level:** Customers trust Clyra within their own workflows and with close partners
- **Market Analogy:** Like Plaid or Bill.com—facilitate transactions, not yet universal network
- **Target:** $5M-$20M ARR

#### Years 6-10: Visa-like Neutral Layer
- **Scope:** DEF/PEF + Attribution Certs become multi-vendor, multi-platform standard
- **Position:** Not just middleware—the clearinghouse everyone plugs into for agent/data-driven outcomes
- **Revenue Model:** Transaction fees at scale (like Visa/MasterCard interchange); fee is unavoidable because Clyra is the neutral arbiter of attribution and proof
- **Trust Level:** Market-wide—enterprises, auditors, regulators, and even competitors treat Clyra receipts and certificates as the gold standard
- **Market Analogy:** Like Visa or SWIFT—not just connecting parties, but enforcing the rules of trust across the network
- **Target:** $100M-$1B+ ARR potential

---

## 10. What's Not Changing (Core Commitments)

1. **Open source foundation:** Recorder, diff/replay, proxy remain OSS
2. **Progressive adoption:** Review → Gate sequencing, enforcement off by default
3. **Evidence-first:** Signed, portable proof before any business logic
4. **Independent verification:** Go/TS verifiers work offline, no vendor lock-in
5. **Agent leverage:** Same receipts/policies for data and agents—no separate stack
6. **Privacy-by-design:** Metadata-only, explicit opt-in for bodies, redaction mandatory

---

## 11. What's Newly Emphasized (Strategic Evolution)

1. **Payout metadata from Day 1:** Receipt fields for attribution, no money movement until H2
2. **Attribution Certificates before Billing:** Prove outcomes before accepting payments
3. **Stablecoin before fiat:** Small corridors via trusted custody, phased rollout
4. **MCP Airlock optionality:** Strategic hedge with clear decision gates, can defer indefinitely
5. **Results-based billing vision:** Clear path from compliance to payment platform
6. **Settlement layer ambition:** "Visa for verified work" as North Star, phased execution

---

## 12. Bottom Line: Strategic Coherence

**Primary Bet:** Data platform evidence → enforcement → attribution → billing
**Strategic Option:** MCP Airlock when market signals confirm timing
**North Star:** Trusted settlement fabric for verified results
**Execution Discipline:** Prove each layer before expanding surface area

**The Elevator Pitch:**

> "Clyra makes sure every data or agent change is safe and audit-ready today, and is growing into the trusted system that lets companies pay people, vendors, and AI agents based on verified results tomorrow."

**Why This Works:**

- **Clear primary wedge:** Data platform (dbt, warehouses) with proven budget
- **Agent optionality:** Ready when market is, not forced prematurely
- **Compelling vision:** Payment based on verified results = simple, human concept
- **Disciplined execution:** Decision gates prevent premature expansion
- **Architectural leverage:** 70-80% code reuse across data/agent/billing

**The Strategic Bet:**

Nail data platform evidence (H0-1A), build attribution proof (H1C), enable results-based billing (H2), and maintain MCP Airlock as strategic hedge (H1B) that activates when—and only when—market timing is right. Win the long game by proving each layer before expanding.

---

*End of Clyra Strategic Roadmap v2.0*
