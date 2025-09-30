# Clyra Strategic Roadmap

**Last Updated:** 2025-01-31
**Status:** Active Strategic Planning

---

## North Star Vision

> "Clyra makes sure every data or agent change is safe and audit-ready today, and is growing into the trusted system that lets companies pay people, vendors, and AI agents based on verified results tomorrow."

---

## Strategic Positioning

**Primary wedge:** Data platform (dbt, Snowflake, Databricks, reverse-ETL) where budget exists TODAY

**Agent optionality:** MCP Airlock (activate when market signals confirm) - ready TOMORROW

**Long-term vision:** Settlement fabric for verified results - "Visa for verified work"

---

## Roadmap Documents

### Core Strategy
- **[strategic_roadmap.md](strategic_roadmap.md)** - Comprehensive 4-horizon plan with decision gates, success metrics, and execution timeline

### Technical Specifications
- **[mcp_airlock_spec.md](mcp_airlock_spec.md)** - MCP Airlock detailed technical specification (activate when market signals confirm)

### Market Strategy
- **[multi_warehouse_strategy.md](multi_warehouse_strategy.md)** - Multi-warehouse hedge strategy (Snowflake primary, BigQuery/Databricks fast-follows)

### Archive
- **[archive/](archive/)** - Historical documents and prior versions

---

## Current Phase: Horizon 0 (Months 0-3)

### Objective
Nail the data platform wedge - prove value in ≤2 weeks for data teams.

### What Ships (MVP v4.0)

**Data Platform Core:**
- ✅ dbt Integration (hooks, macros, CI gates, semantic delta detection)
- ✅ Warehouse Anchors (Snowflake QUERY_HISTORY, Databricks Delta commits, Postgres WAL LSN)
- ✅ DEF v0 Format (Data Evidence Format with warehouse-native anchoring)
- ✅ Activation Gateway (HTTP proxy for reverse-ETL with enforcement)

**ServiceNow/Jira Bridge:**
- ✅ One-way export: DEF/PEF bundles → Attested Change Ticket
- ✅ Ticket format: Attestation hash, verification link, compliance status

**Badge Program:**
- ✅ "Clyra Certified - SOX Compliant" badges for dbt projects
- ✅ Independent Go/TS verifiers run offline

### Success Metrics

**Technical:**
- ✅ First attested ticket generated in ≤2 weeks from installation
- ✅ Performance SLAs met: Gateway ≤15ms p95, dbt hook <2s overhead
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

---

## Future Horizons (Summary)

### Horizon 1 (Months 3-9): Enforcement + Outcome Attribution

**1A: Clyra Gate (Primary Track)**
- Full enforcement with allow/deny/HITL
- Enhanced ServiceNow/Jira integration (two-way sync)
- Multi-framework attestations (SOX, PCI, HIPAA, EU AI Act, NIST, TCPA)
- **Target:** 10+ Review customers, 3+ Gate conversions, $500k+ ARR

**1B: MCP Airlock (Conditional - See Decision Gates Below)**
- MCP-native security & connectivity gateway for AI agents
- Listen-only monitoring with signed receipts
- **Activate only when market signals confirm timing**

**1C: Outcome Attribution**
- Outcome Ledger (append-only metric observations)
- Attribution Certificates linking changes to business outcomes
- Shadow billing simulation (no money movement)
- **Target:** 2+ customers using Attribution Certs in QBRs

### Horizon 2 (Months 9-18): Results-Based Billing
- Pricing Policy Engine mapping outcomes → invoices
- Payout Rails v1 (stablecoins via Coinbase custody)
- Dispute workflow with deterministic replay
- **Target:** 1-2 customers piloting payouts, <2% dispute rate, $50-100k platform fees

### Horizon 3 (Months 18-36): Ecosystem & Standards
- Fiat rails (Stripe Treasury, Wise, bank APIs)
- Auditor partnerships (2-3 Big 4 acknowledgments)
- Open standards (DEF/PEF spec publication)
- **Target:** 5+ enterprises on Billing Bundles, $2M+ ARR

### Horizon 4 (Years 3-7): Settlement Layer Vision
- Unified multi-currency rails (stablecoin + fiat)
- Attribution Certificates become contractable truth
- Network economics with 0.2-0.5% platform fees
- **Vision:** "Visa for agents, data, and verified work" at scale

---

## MCP Airlock Decision Gates (Horizon 1B)

### Activate if ANY of These Signals Appear:

1. ≥2 existing customers explicitly request agent security/MCP support
2. MCP adoption reaches critical mass (≥10k GitHub stars, ≥3 major platforms integrated)
3. Real security incidents create CISO demand (malicious MCP servers, credential leakage)
4. Strategic opportunity to own agent security category emerges
5. Competitive threat: observability vendors add agent security features

### Prerequisites Before Activation:

- ✅ Horizon 0 success criteria fully met
- ✅ $300k+ ARR from data platform wedge
- ✅ Dedicated team available (2-3 engineers for 12 weeks)
- ✅ Design partners committed to pilot

### Defer If:

- ❌ Data platform thesis not yet proven
- ❌ Execution bandwidth constrained
- ❌ Market signals unclear
- ❌ Higher ROI opportunities exist

**Current Status:** Schema-only preparation complete (PEF v0 MCP extension). Full implementation ready to activate when conditions met.

---

## Guiding Principles

1. **Data-led, agent-ready:** Prove value with dbt/Snowflake/Databricks first; same receipts/policies work for agents later
2. **Evidence before money:** Signed, portable proof (DEF/PEF) precedes attribution; attribution precedes payouts
3. **Progressive adoption:** Review (listen-only) → Gate (enforcement) → Attribution → Billing
4. **Minimal viable economics:** Simulate payouts before money movement; start with stablecoins via trusted custodians
5. **Disciplined sequencing:** Prove core thesis before expanding surface area

---

## Product Packaging

- **Clyra Review** ($25-60k/year): Listen-only detection, DEF/PEF bundles, ServiceNow/Jira export, badge program
- **Clyra Gate** ($75-150k/year): Everything in Review + full enforcement, GenAI security, kill-switch, SQL guardrails
- **Clyra Airlock (MCP)** (conditional): Agent security & connectivity for MCP protocol—activates when market signals confirm
- **Clyra Attribution** ($10-25k/year add-on): Outcome ledger, attribution certificates, shadow billing simulation
- **Clyra Billing** (platform fee 0.2-0.5%): Results-based pricing, invoice generation, payout rails

---

## Key Success Factors

1. **Clear primary wedge:** Data platform (dbt, warehouses) with proven budget
2. **Agent optionality:** Ready when market is, not forced prematurely
3. **Compelling vision:** Payment based on verified results = simple, human concept
4. **Disciplined execution:** Decision gates prevent premature expansion
5. **Architectural leverage:** 70-80% code reuse across data/agent/billing

---

## What's Not Changing (Core Commitments)

1. **Open source foundation:** Recorder, diff/replay, proxy remain OSS
2. **Progressive adoption:** Review → Gate sequencing, enforcement off by default
3. **Evidence-first:** Signed, portable proof before any business logic
4. **Independent verification:** Go/TS verifiers work offline, no vendor lock-in
5. **Agent leverage:** Same receipts/policies for data and agents—no separate stack
6. **Privacy-by-design:** Metadata-only, explicit opt-in for bodies, redaction mandatory

---

## Repository Structure

```
/roadmap/
├── README.md                     # This file - executive summary
├── strategic_roadmap.md          # Comprehensive 4-horizon plan
├── mcp_airlock_spec.md           # MCP Airlock technical specification
├── multi_warehouse_strategy.md   # Multi-warehouse hedge strategy
└── archive/                      # Historical documents
    └── founder_memo_2024.md      # Original founder memo (Sept 2024)
```

---

## The Elevator Pitch

**30-Second Version:**

"Clyra provides data change control & attestation for dbt + Snowflake/Databricks. Your dbt run generates a signed evidence bundle that becomes an attested ServiceNow ticket. 6-8 weeks of audit prep → 3-5 days. Start with listen-only Review, graduate to enforcement Gate when ready. Same architecture works for AI agents when you need it."

**60-Second Version:**

"Data teams face a scattered evidence problem: approvals in Slack, tickets in Jira, dbt runs in Cloud, queries in QUERY_HISTORY—nothing connects them. 6-8 weeks to reconstruct the audit trail every quarter.

Clyra automates the complete workflow: dbt hooks emit evidence bundles, ServiceNow/Jira bridge attaches proof to change tickets, signed attestations generated on demand. Start with Review (listen-only), graduate to Gate (enforcement). Independent verification—auditors can validate offline.

6-8 weeks → 3-5 days. $192K/year → $35K/year. Data platform today, AI agents tomorrow—same architecture, expanding scope."

---

## Strategic Bet

Nail data platform evidence (H0-1A), build attribution proof (H1C), enable results-based billing (H2), and maintain MCP Airlock as strategic hedge (H1B) that activates when—and only when—market timing is right. Win the long game by proving each layer before expanding.

---

*For detailed technical specifications, timelines, and decision frameworks, see the individual roadmap documents linked above.*
