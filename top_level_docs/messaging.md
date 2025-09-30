# Clyra — Data Change Control & Attestation

## 1. Pain (what data teams feel today)

**The Scattered Evidence Problem:**
"Quarter-end audit. Auditor asks: 'Show me proof your dbt changes follow SOX change control.' We have Slack approvals, Jira tickets, dbt Cloud logs, and Snowflake QUERY_HISTORY—but nothing connects them. 6-8 weeks to reconstruct the evidence trail."

**The Reality:**

- Approval in Slack (which channel? which thread?)
- Jira ticket exists (but doesn't reference dbt run ID)
- dbt Cloud shows successful run (but no approval record)
- Snowflake QUERY_HISTORY has the queries (but no link to ticket)
- Manual spreadsheet ties it together (6 weeks of work)
- Controller's reaction: "This can't be our process"

**The Cost:**

- 6-8 weeks of audit prep every quarter
- Evidence scattered across 4+ systems
- Manual correlation (error-prone, time-consuming)
- Controllers stressed, data teams frustrated
- Pipeline velocity slowed by compliance friction

---

## 2. Solution (what Clyra does)

**Data Change Control with Warehouse-Native Anchoring**

Clyra provides the complete workflow data teams need for SOX compliance:

**dbt Integration**

- on_run_start/end hooks emit evidence bundles automatically
- Schema diffs captured (before/after comparison)
- Approval records linked (GitHub PR, Jira ticket)
- All metadata in one place

**ServiceNow/Jira Bridge**

- Evidence automatically attached to change tickets
- Fields populated: dbt run ID + QUERY_HISTORY reference + approval + schema diff
- One ticket with ALL the proof auditors need
- No manual correlation required

**Warehouse-Native Anchoring**

- Snowflake: QUERY_HISTORY correlation + session tags
- Databricks: Delta commits + Unity Catalog lineage
- Evidence anchored to immutable warehouse truth
- Native integration, not external logging

**SOX Attestation**

- Signed attestations generated on demand
- Independent verification (auditors can validate)
- Multi-framework support (SOX/PCI/HIPAA/EU AI Act)
- PDF + JSON ready for audit review

**Two-SKU Progressive Adoption**

- Start with **Clyra Review** (listen-only, no enforcement risk)
- Graduate to **Clyra Gate** (full enforcement when ready)
- Proven 30% conversion rate (Review → Gate)

**Tagline:** "6-8 weeks → 3-5 days" (audit prep time reduction)

---

## 3. Proof (why believe us)

**ROI Metrics:**

- 6-8 weeks → 3-5 days (audit prep time)
- $192K/year → $35K/year (controller time savings vs. Clyra Review cost)
- Quarter-one payback (immediate ROI)

**Risk Reduction:**

- Schema changes blocked without approval
- SQL safety guards (mass UPDATE/DELETE advisory blocks)
- Kill-switch capabilities (emergency stop)
- Policy violations caught before prod

**Adoption Path:**

- 10-minute quickstart (clyra dbt init → hooks installed)
- 3-hour SOX setup (follow the checklist)
- 30-60 day pilot (Review SKU, listen-only)
- Production deployment (30% convert to Gate)

**Independent Verification:**

- Go + TypeScript verifiers (auditors run offline)
- Vendor-neutral evidence format (DEF v0)
- No "trust our dashboard" requirement
- Cryptographic proof, not screenshots

**OSS Foundation:**

- 4 standalone tools (ServiceNow bridge, evidence spec, dbt hooks, SOX checklist)
- 200+ teams using format
- 50+ dbt projects with hooks
- Community-proven, production-tested

---

## 4. Differentiation (vs. status quo)

**vs. Data Observability (Monte Carlo, Metaplane)**

- **Their Story:** "Detect data quality issues with monitoring"
- **Clyra:** "Prove data changes follow SOX change control"
- **Key Difference:** Detection ≠ Attestation. Alerts ≠ Audit evidence.

**vs. Data Catalogs (Alation, Atlan)**

- **Their Story:** "Understand your data with cataloging"
- **Clyra:** "Prove your data changes with evidence"
- **Key Difference:** Documentation ≠ Change control. Discovery ≠ Compliance.

**vs. Compliance Platforms (Vanta, Drata)**

- **Their Story:** "Automate compliance documentation"
- **Clyra:** "Automate compliance evidence from data operations"
- **Key Difference:** Generic compliance ≠ Data-specific controls. Checkboxes ≠ dbt governance.

**vs. dbt Cloud Features**

- **Their Story:** "We might build governance features eventually"
- **Clyra:** "We integrate with your dbt + Snowflake + ServiceNow stack today"
- **Key Difference:** Vendor lock-in vs. vendor-neutral. Wait vs. ship now.

**vs. Building It Yourself**

- **DIY:** 6 weeks to build, 3 months to harden, ongoing maintenance
- **Clyra:** 3 hours to SOX-ready, battle-tested, maintained by us
- **TCO:** DIY = $150K+ first year. Clyra Review = $35K/year.

---

## 5. Future-Proofing (data-led, agent-ready)

**The Strategic Positioning:**

**Data Platform Today (Where Budget Exists)**

- dbt + Snowflake/Databricks governance (immediate pain)
- ServiceNow/Jira integration (existing workflow)
- SOX ITGC compliance (concrete requirement)
- Activation controls (Hightouch/Census/RudderStack)

**AI Agents Tomorrow (Same Architecture)**

- Same control patterns (approval + evidence + attestation)
- Same ServiceNow/Jira integration
- Same compliance frameworks
- Data teams already own the budget category

**Why Data Teams Will Lead This:**

- You already understand change control
- You already integrate with SOX processes
- You already have budget for "data governance"
- You can expand scope to agents without creating new category
- CFO already trusts your dbt governance process

**The Architecture Advantage:**
Single control point (Gateway pattern):

- Validates requests before execution (dbt runs today, agent actions tomorrow)
- Enforces approval requirements (same workflow, different systems)
- Generates evidence automatically (unified format)
- Works for data AND agents (same architecture, expanding scope)

**Not Creating a New Category:**

- We're solving data platform governance (existing budget)
- Same architecture works for AI agents (future expansion)
- Data-led market entry, agent-ready architecture
- "Integrate don't rebuild" philosophy

---

## 6. Badge Effect (viral growth mechanism)

**The Clyra Certified Program:**

**How It Works:**

1. dbt project passes SOX checks → Badge service signs JWT
2. README displays: "Clyra Certified - SOX Compliant"
3. GitHub renders badge → Social proof → Viral adoption
4. Badge endpoint: clyra.io/badge/sox/{project-id}

**Why It Matters:**

- Makes compliance visible (not hidden in tickets)
- Social proof in READMEs (developers see it)
- Auditors ask for it ("Is this Clyra Certified?")
- Network effect: badge → interest → adoption → more badges

**The Flywheel:**

```
dbt Hooks Installed → Evidence Bundles Generated →
ServiceNow Tickets Created → Auditors See Proof →
Controllers Demand It → More dbt Projects Adopt →
Badges Displayed → Social Proof → Viral Growth →
dbt Hooks Installed
```

**Target:** 1,000+ badges in 18 months = industry standard

---

## 7. Objection Handling

**"We already have dbt Cloud"**
→ "Perfect. We integrate with dbt Cloud hooks. Let me show you the ServiceNow ticket this creates." [Demo ServiceNow integration]

**"We don't have SOX pressure yet"**
→ "When does your IPO timeline start? This takes 3 hours to implement vs. 6 weeks to build internally. Lock in the architecture now." [Show TCO]

**"This seems specific to dbt"**
→ "dbt is the wedge—where your pain is today. Same architecture works for activation (Hightouch/Census) and AI agents tomorrow. Data-led, agent-ready." [Show roadmap]

**"What about cost?"**
→ "Review is $35K/year. Your controller spends 6 weeks at $200/hour = $48K per quarter = $192K/year. This pays for itself in quarter one." [Show TCO calculation]

**"We might build this ourselves"**
→ "You could. 6 weeks to build, 3 months to harden, ongoing maintenance = $150K+ first year. Or 3 hours to SOX-ready with Clyra. What's the opportunity cost?" [Show build vs. buy]

**"How is this different from observability?"**
→ "Observability detects problems after they happen. Clyra prevents unsafe changes before they hit prod and generates audit-ready evidence. Different problems, different solutions." [Show demo]

**"Our auditors won't accept this"**
→ "Evidence format is vendor-neutral. Auditors can verify independently with our open-source CLI. No 'trust our dashboard' requirement. Here's how they validate it." [Show verifier]

**"What about vendor lock-in?"**
→ "Evidence format (DEF v0) is vendor-neutral. Independent Go/TS verifiers. Works across dbt, Snowflake, Databricks, Postgres. Your evidence survives platform churn." [Show multi-platform]

---

## 8. Bottom Line (the elevator pitch)

**30-Second Version:**
"Your dbt models change production schemas. Auditor asks: 'Show me proof these changes follow SOX change control.' You have logs. You don't have evidence. Clyra automates the complete workflow—dbt run → attested ServiceNow ticket—turning 6-8 weeks of audit prep into 3-5 days."

**60-Second Version:**
"Data teams face a scattered evidence problem: approvals in Slack, tickets in Jira, runs in dbt Cloud, queries in QUERY_HISTORY—nothing connects them. 6-8 weeks to reconstruct the trail every quarter. Clyra provides data change control with warehouse-native anchoring. dbt hooks emit evidence bundles, ServiceNow/Jira bridge attaches proof to tickets, signed attestations generated on demand. Start with Review (listen-only), graduate to Gate (enforcement). 6-8 weeks → 3-5 days. $192K/year → $35K/year. Data platform today, AI agents tomorrow—same architecture, expanding scope."

**2-Minute Version:**
"The problem: Quarter-end audit. Your dbt model changed the revenue calculation. Auditor asks: 'Show me the change ticket with approval proof.' You have Slack threads, Jira tickets, dbt Cloud logs, Snowflake QUERY_HISTORY—but nothing connects them. Manual spreadsheet, 6-8 weeks, controller is stressed.

The solution: Clyra provides the complete workflow. dbt hooks emit evidence bundles automatically. ServiceNow/Jira bridge attaches proof to tickets—dbt run ID + QUERY_HISTORY reference + approval record + schema diff—all in one ticket. Warehouse-native anchoring (Snowflake QUERY_HISTORY, Databricks Delta commits). Independent verification (auditors can validate offline).

Progressive adoption: Start with Review (listen-only, no enforcement risk). Graduate to Gate (full enforcement when ready). 30% conversion proven.

The metrics: 6-8 weeks → 3-5 days (audit prep). $192K/year → $35K/year (TCO). Quarter-one payback.

The strategy: Data platform today (dbt + Snowflake/Databricks—where budget exists). AI agents tomorrow (same architecture, expanding scope). Data-led market entry, agent-ready architecture.

The moat: OSS foundation (200+ teams using format). Badge program (viral growth). Independent verifiers (trust without vendor lock-in). Audit partner network (Big 4 acknowledgment).

What's different: Not observability (we prevent, they detect). Not catalogs (we prove changes, they document data). Not generic compliance (we integrate with dbt/Snowflake, they check boxes). We solve data platform SOX change control—concrete pain, existing budget, immediate ROI."

---

## 9. Messaging Hierarchy

**Problem Layer (Hook):**

- "6-8 weeks of audit prep every quarter"
- "Evidence scattered across 4 systems"
- "Manual spreadsheet correlation"
- "Controller: 'This can't be our process'"

**Solution Layer (Value):**

- "dbt run → attested ServiceNow ticket"
- "ONE ticket with ALL the proof"
- "6-8 weeks → 3-5 days"
- "Warehouse-native anchoring"

**Proof Layer (Trust):**

- "OSS foundation (200+ teams)"
- "Independent verification (auditors validate)"
- "Progressive adoption (listen-only → enforcement)"
- "Quarter-one payback ($192K → $35K)"

**Differentiation Layer (Moat):**

- "Not observability (prevent vs. detect)"
- "Not catalogs (prove vs. document)"
- "Not generic compliance (dbt-native vs. checkboxes)"
- "Data-led, agent-ready (not creating new category)"

**Future Layer (Vision):**

- "Data platform today (where budget exists)"
- "AI agents tomorrow (same architecture)"
- "1,000+ badges = industry standard"
- "Big 4 audit firms require DEF format"

---

## 10. Key Phrases (Messaging Consistency)

**Pain Phrases:**

- "Scattered evidence problem"
- "6-8 weeks of audit prep"
- "Nothing connects them"
- "This can't be our process"

**Solution Phrases:**

- "Data change control"
- "Warehouse-native anchoring"
- "ServiceNow/Jira bridge"
- "dbt run → attested ticket"

**Value Phrases:**

- "6-8 weeks → 3-5 days"
- "ONE ticket, ALL the proof"
- "Quarter-one payback"
- "3 hours to SOX-ready"

**Differentiation Phrases:**

- "Prevent vs. detect"
- "Prove vs. document"
- "dbt-native vs. generic"
- "Data-led, agent-ready"

**Technical Phrases:**

- "QUERY_HISTORY correlation"
- "Delta commits"
- "Evidence bundle (DEF v0)"
- "Independent verification"

---

**End of Messaging Document v4.0**
