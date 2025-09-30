# Clyra v4.0 Go-to-Market Strategy

**"Data Change Control & Attestation for Modern Pipelines"**

---

## Executive Summary

**The Problem:** Your dbt models change production schemas every day. Your controller asks: "Show me proof these changes follow SOX change control." You have Slack approvals, Jira tickets, dbt Cloud logs, and Snowflake QUERY_HISTORY—but nothing connects them. 6-8 weeks to reconstruct the evidence trail.

**The Solution:** Clyra provides data change control with warehouse-native anchoring (Snowflake QUERY_HISTORY, Databricks Delta commits), ServiceNow/Jira integration, and automated SOX attestations. From dbt hook to attested change ticket in minutes.

**The Mission:** Become the data change control standard for modern pipelines within 18 months. When data teams ask "How do we prove our changes are SOX compliant?" the answer is "Clyra."

---

## 1. The Market Entry Problem

### The Scattered Evidence Reality

**What Data Teams Say:**
"We're covered—we have dbt docs, GitHub PRs, and Snowflake logs."

**What Auditors Need:**
When your dbt model changes the revenue calculation, auditors ask:

- ✓ "Show me the change ticket with approval proof"
- ✓ "What exactly changed in the schema?"
- ✓ "Link the Jira ticket to the dbt run ID and QUERY_HISTORY"
- ✓ "Prove the approved change matches what deployed"

**The 6-8 Week Problem:**

- Week 1-2: Identify all dbt model changes that quarter
- Week 3-4: Find Slack/GitHub approvals for each change
- Week 5: Match Jira tickets to dbt runs manually
- Week 6-8: Create evidence spreadsheet for auditor
- Result: Controller asks, "This can't be our process"

---

## 2. Strategic Positioning: Data-Led, Agent-Ready

### The Market Entry Strategy

**Lead with data platform** (budget exists today):

- dbt + Snowflake/Databricks governance (immediate pain)
- ServiceNow/Jira integration (existing workflow)
- SOX ITGC compliance (concrete requirement)
- Activation controls (Hightouch/Census/RudderStack)

**Expand to AI agents** (same architecture, tomorrow):

- Same control patterns (approval + evidence + attestation)
- Same ServiceNow/Jira integration
- Same compliance frameworks
- Data teams already own the budget category

### The Beachhead Market

**Target:** 200-2K employee public/pre-IPO companies

- **Pain:** SOX pressure on data platform operations
- **Stack:** dbt + Snowflake/Databricks + ServiceNow/Jira
- **Budget:** Existing "data governance" line item ($50-150K)
- **Timeline:** 60-90 days from pilot to production

### Two-SKU Progressive Adoption

**Clyra Review (Listen-Only → Detection)**

- Webhook listening (dbt Cloud, warehouse operations)
- Evidence bundle generation (no enforcement)
- ServiceNow/Jira ticket creation (attested proof)
- Badge issuance ("Clyra Certified - SOX Compliant")
- $20-50K/year

**Clyra Gate (Full Enforcement)**

- Everything in Review +
- Policy enforcement (approval requirements)
- SQL safety guards (mass UPDATE/DELETE blocks)
- Kill-switch capabilities
- Advanced compliance (PCI/HIPAA overlays)
- $75-150K/year

---

## 3. Problem-First Messaging Architecture

### Level 1: The Concrete Pain (Hook)

"Quarter-end audit. 9 AM Monday. Auditor asks: 'Show me proof your dbt changes follow SOX change control.' You have logs. You don't have evidence."

### Level 2: The Scattered Evidence Gap (Agitate)

"Approval in Slack (which channel?). Jira ticket exists (doesn't reference dbt run ID). dbt Cloud shows success. Snowflake QUERY_HISTORY has the queries. NOTHING links them together. 6 weeks to create the spreadsheet."

### Level 3: The Integration Bridge (Insight)

"You need one workflow: dbt run → evidence bundle → ServiceNow/Jira ticket with ALL the proof (dbt run ID + QUERY_HISTORY reference + approval record + schema diff). Auditors review ONE ticket instead of 4 systems."

### Level 4: The 3-Hour Implementation (Resolve)

"clyra dbt init → dbt hooks installed → run dbt → evidence attached to ServiceNow ticket → SOX compliance in place. From scattered evidence to attested change tickets in 3 hours."

### The Tagline

**"6-8 weeks → 3-5 days"** (audit prep time reduction)

---

## 4. Target Personas (Problem-Aware)

### Primary Champion: Data Platform Engineer

- **Current State:** "Our dbt PRs are reviewed, tests pass, we're good"
- **Hidden Pain:** "Can't prove to auditors that changes were approved"
- **Pain Point:** "6 weeks of manual evidence collection every quarter"
- **Hook:** "Watch—dbt run → attested ServiceNow ticket automatically"

### Validator: SOX-Weary Controller

- **Current State:** "Data team says they have controls"
- **Hidden Pain:** "Auditor asks for proof, we show Slack screenshots"
- **Pain Point:** "Evidence scattered across 4 systems, manual correlation"
- **Hook:** "One change ticket with ALL the proof auditors need"

### Economic Buyer: Head of Data Platform

- **Current State:** "We built modern data stack, governance is manual"
- **Hidden Pain:** "SOX audit prep delays pipeline velocity"
- **Pain Point:** "Can't ship fast without compliance friction"
- **Hook:** "Ship dbt models faster with automated SOX compliance"

### Technical Evaluator: Data/Analytics Engineer

- **Current State:** "I know my dbt models and warehouse"
- **Hidden Pain:** "No forensic trail for schema changes"
- **Pain Point:** "Manual change tracking doesn't scale"
- **Hook:** "Evidence anchored to QUERY_HISTORY and Delta commits—native warehouse integration"

---

## 5. Product Architecture (Problem-Led)

### The Data Platform Core

**dbt Integration**

- on_run_start/end hooks (emit evidence bundles)
- SQL safety macros (advisory guards on mass operations)
- CI gates (block policy violations before merge)
- Semantic delta tracking (before/after schema comparison)

**Warehouse Anchors**

- Snowflake: QUERY_HISTORY correlation + session tags
- Databricks: Delta commits + Unity Catalog lineage
- Postgres: WAL LSN anchoring (dev/pilot environments)

**ServiceNow/Jira Bridge**

- Automated change ticket creation
- Evidence bundle attachment (dbt run ID + QUERY_HISTORY + approvals)
- Approval workflow integration
- Daily review helper (failed changes, anomalies)

**Evidence Format (DEF v0)**

- Data Evidence Format (vendor-neutral JSON)
- Warehouse-native anchoring
- Independent verification (Go/TS verifiers)
- SOX ITGC attestation generation

### The Universal Foundation (Strategic)

**Gateway (SchemaLock + Data Firewall)**

- JSON schema validation
- Data-aware policies
- BEC-grade approval certificates
- GenAI threat detection (OWASP LLM)

**Recorder (Flight Data Recorder)**

- Metadata-only snapshots
- Deterministic diffs
- Warehouse anchoring
- Enhanced replay capability

**Compliance Engine**

- Multi-framework attestations (SOX/PCI/HIPAA/EU AI Act)
- Policy-as-code automation
- Daily review generation
- Badge issuance

### The 10-Minute Data Platform Experience

```bash
clyra dbt init my-project               # dbt project with Clyra hooks
make quickstart-data                     # Local stack (Gateway+Recorder+Snowflake)
clyra demo data --platform snowflake    # Generate DEF bundles
clyra warehouse doctor --platform snowflake  # Validate integration
clyra verify evidence.zip --validate-lineage  # Independent verification
clyra attest evidence.zip --framework sox     # Signed SOX attestation
clyra report --daily-review --include-data-changes  # Enhanced review
```

No other platform delivers SOX-attested data change control from dbt to ServiceNow in 10 minutes.

---

## 6. Go-to-Market Motion: The Data Platform Wedge

### Phase 1: The OSS Credibility Campaign (Days 1-90)

**Objective:** 1,000 GitHub stars, 100 dbt projects using hooks, 10 ServiceNow integrations

**OSS Wedge Strategy:**

Release 4 standalone, immediately useful tools (NO Clyra branding):

1. **ServiceNow/Jira Bridge** (Week 2): Bash scripts to attach dbt evidence to tickets
2. **Evidence Bundle Spec** (Week 3): Vendor-neutral format with verifier stub
3. **dbt SOX Hooks** (Week 5): on_run_end macros that emit SOX-ready evidence
4. **SOX Data Checklist** (Week 8): Complete implementation roadmap

**Problem-First Messaging:**
"6-8 weeks audit prep → 3-5 days. Here's how data teams are solving scattered evidence."

**Success Metrics:**

- 200+ repos using evidence bundle format
- 50+ dbt projects with SOX hooks installed
- 10+ teams using ServiceNow/Jira bridge in production
- Community asks: "Who built these tools?" → Week 9: "Clyra"

### Phase 2: The Badge & Integration Network (Days 91-180)

**Objective:** 50 "Clyra Certified" badges live, 2 Big 4 audit firm acknowledgments

**Badge Program Strategy:**

Make compliance visible and viral:

- dbt project passes SOX checks → Badge service signs JWT
- README displays: "Clyra Certified - SOX Compliant"
- GitHub renders badge → Social proof → Viral adoption
- Badge endpoint: clyra.io/badge/sox/{project-id}

**Audit Partner Network:**

- 2-3 Big 4 firms acknowledge DEF format
- QSAs can verify bundles independently
- Audit guidance materials (how to validate evidence)
- "Clyra-ready" becomes audit requirement in RFPs

**Success Metrics:**

- 100+ badges issued
- 2 Big 4 firms acknowledge format
- 5 QSA endorsements
- Published audit guidance

### Phase 3: The Platform Play (Days 181-365)

**Objective:** $300-600K ARR, 30% Review→Gate conversion, Series A ready

**Commercial Success Metrics:**

- ≥10 customers on Review SKU (listen-only start)
- ≥30% upsell to Gate SKU within 90 days
- 70% Review / 30% Gate revenue mix initially
- Average contract: Review $35K, Gate $100K

**Platform Network Effects:**

- Every dbt project using hooks → potential customer
- Every ServiceNow ticket → social proof
- Every badge → marketing asset
- Integration partners (dbt Labs, Snowflake, Databricks)

---

## 7. Channel Strategy: Problem Distribution

### Tier 1: Data Platform Channels (70% effort)

**dbt Community (Slack + Discourse)**

- Problem-first contributions (not promotional)
- Help with governance/compliance questions
- Share OSS tools when relevant
- Build reputation: "The SOX compliance expert"

**r/dataengineering + r/dbt**

- Technical tutorials (warehouse anchoring, evidence formats)
- Real audit war stories (6-week evidence hunts)
- OSS tool releases (ServiceNow bridge, dbt hooks)
- 10:1 help-to-promote ratio

**Data Engineering Podcasts/Newsletters**

- The Data Engineering Podcast
- Data Engineering Weekly
- Locally Optimistic
- Topic: "Why data teams fail SOX audits"

### Tier 2: Compliance/Audit Channels (20% effort)

**SOX Compliance Communities**

- IT Compliance Institute
- SOX forums (Controller/Finance perspective)
- Share audit time reduction case studies
- Position as "data governance bridge"

**QSA/Audit Firm Outreach**

- Big 4 SI partnerships (2-3 firms)
- Evidence format validation workshops
- Auditor guidance materials
- "Clyra-ready" audit procedures

### Tier 3: Technical Amplification (10% effort)

**Conference Speaking**

- dbt Coalesce: "SOX Change Control for Analytics Engineers"
- Snowflake Summit: "Warehouse-Native Data Governance"
- Data Council: "Why Data Teams Will Own AI Agent Governance"

**Technical Blog Series**

- Personal blog → HackerNews submission (best 2 pieces)
- Focus: Concrete problems, real solutions
- No philosophical concepts, just buyer pain

---

## 8. Problem-First Content Strategy

### The 8-Week Pre-Launch Campaign

**Theme:** Build credibility + urgency (NO Clyra mentions until Week 9)

**Week 1: The SOX Audit Evidence Scramble**

- Blog: "The Revenue Model Change That Failed SOX Audit"
- Twitter: Quarter-end reality (6 weeks creating spreadsheet)
- Reddit: "How do you handle data change control?"

**Week 2: The ServiceNow/Jira Bridge (OSS Release #1)**

- Blog: "How to Tie QUERY_HISTORY to a ServiceNow Change Ticket"
- GitHub: ServiceNow/Jira bridge scripts (bash, no dependencies)
- Focus: Solve immediate pain (evidence attachment)

**Week 3: The Evidence Bundle Format (OSS Release #2)**

- Blog: "Quarter-End Without Screenshots: A Practical Evidence Bundle Format"
- GitHub: Vendor-neutral spec + verifier stub + auditor guide
- HackerNews: "Show HN: Evidence Bundle Format for Data Compliance"

**Week 5: The dbt SOX Hooks (OSS Release #3)**

- Blog: "Why dbt Tests Aren't SOX Change Control (And What To Do Instead)"
- GitHub: on_run_end macros + ServiceNow integration
- dbt Community: "Released: dbt hooks for SOX compliance"

**Week 6: The ServiceNow/Jira Guide (THE WEDGE)**

- Blog: "Jira vs ServiceNow for Data Change Control: A Practical Guide"
- Detailed setup guides for both platforms
- Field configuration, automation examples
- Community asks: "Is there a tool that does all this?" (setup for Week 9)

**Week 7: The AI Agent Bridge**

- Blog: "Why Data Teams Will Own AI Agent Governance (And How to Prepare)"
- Position: Same patterns (dbt today, agents tomorrow)
- Architecture: Data-led, agent-ready (not creating new category)

**Week 8: The SOX Checklist (OSS Release #4)**

- Blog: "The SOX Data Change Control Checklist (Steal This)"
- GitHub: Complete implementation roadmap (4-week timeline)
- Launch Tease: "I've been working on something..." (Monday reveal)

**Week 9: The Clyra Launch**

- "The tool that automates this entire workflow"
- OSS foundation + commercial platform
- dbt + Snowflake/Databricks native
- From hook → attested ticket in one system

### Content Performance Targets

- **Blog posts:** 8 major pieces, 10,000+ total reads
- **GitHub stars:** 1,000+ (across OSS repos)
- **Community engagement:** 50+ high-value contributions
- **Email list:** 500+ subscribers (launch day amplification)
- **Badge adoption:** 100+ "Clyra Certified" badges live

---

## 9. Competitive Positioning (Problem-Led)

### vs. Data Observability (Monte Carlo, Metaplane)

**Their Story:** "Detect data quality issues with monitoring"
**Our Story:** "Prove data changes follow SOX change control"
**The Difference:** "Detection ≠ Attestation. Alerts ≠ Audit evidence."

### vs. Data Catalogs (Alation, Atlan)

**Their Story:** "Understand your data with cataloging"
**Our Story:** "Prove your data changes with evidence"
**The Difference:** "Documentation ≠ Change control. Discovery ≠ Compliance."

### vs. Compliance Platforms (Vanta, Drata)

**Their Story:** "Automate compliance documentation"
**Our Story:** "Automate compliance evidence from data operations"
**The Difference:** "Generic compliance ≠ Data-specific controls. Checkboxes ≠ dbt governance."

### vs. dbt Cloud Features

**Their Story:** "We might build governance features eventually"
**Our Story:** "We integrate with your dbt + Snowflake + ServiceNow stack today"
**The Difference:** "Vendor lock-in vs. vendor-neutral. Wait vs. ship now."

---

## 10. Pricing: Progressive Adoption

### Clyra Review ($20-50K/year)

**What's Included:**

- Listen-only webhook integration
- Evidence bundle generation (DEF v0)
- ServiceNow/Jira export (automated tickets)
- Daily review automation
- Badge program access
- Community support

**Hook:** "Start safe with listen-only mode—no enforcement risk"

**Target:** Pilot/POC phase (30-60 days)

### Clyra Gate ($75-150K/year)

**What's Included:**

- Everything in Review +
- Full policy enforcement
- SQL safety guards (mass operation blocks)
- Kill-switch capabilities
- BEC-grade approval certificates
- Advanced compliance (PCI/HIPAA overlays)
- Priority support

**Hook:** "Graduate to full enforcement when ready"

**Target:** Production deployment (30% conversion from Review)

### Enterprise Plus (Custom)

**What's Included:**

- Everything in Gate +
- Multi-framework compliance packs
- Dedicated success manager
- Custom policy development
- Multi-tenant deployment
- SLA guarantees

**Hook:** "Enterprise-scale data governance"

**Target:** 1,000+ employee organizations

### Add-On Services

**Audit Accelerator ($5,000)**

- SOX ITGC attestation setup
- QSA briefing materials
- 30 days compliance consulting

**Badge Plus ($2,000/year)**

- Premium badge (animated, verified)
- Compliance dashboard widget
- Public trust page

---

## 11. The Problem-First Sales Playbook

### Discovery: The Evidence Gap Analysis

**Key Questions:**

1. "Walk me through your last SOX audit prep. How long did it take?"
2. "Where are your dbt approvals stored? How do you link them to runs?"
3. "Show me a change ticket for a dbt model. What's missing?"
4. "How do you prove schema changes were approved?"
5. "What does your controller think of the current process?"

**Pain Qualification:**

- Current audit prep time: 6-8 weeks = high pain
- Evidence scattered across 4+ systems = high pain
- Manual spreadsheet correlation = high pain
- Controller/auditor frustration = economic urgency

### Demo: The 10-Minute Workflow

**Setup:** "I'm going to show you the complete workflow—dbt run to attested ServiceNow ticket."

**Step 1: dbt Integration (2 min)**

```bash
clyra dbt init demo-project
# Shows hooks installation, macro setup
```

**Step 2: Evidence Generation (3 min)**

```bash
dbt run  # Hooks emit evidence bundle
clyra verify evidence.zip --explain
# Shows: dbt run ID + QUERY_HISTORY + approval + schema diff
```

**Step 3: ServiceNow Integration (2 min)**

```bash
# Evidence automatically attached to change ticket
# Shows populated ticket with ALL required fields
```

**Step 4: SOX Attestation (2 min)**

```bash
clyra attest evidence.zip --framework sox
# Signed attestation ready for auditor
```

**Step 5: Badge Issuance (1 min)**

```bash
# "Clyra Certified - SOX Compliant" badge live
# README displays social proof
```

**The Question:** "How long does this take you today?"

### Objection Handling: Problem-Focused

**"We already have dbt Cloud"**
→ "Perfect. We integrate with dbt Cloud hooks. Let me show you the ServiceNow ticket this creates." [Demo]

**"We don't have SOX pressure yet"**
→ "When does your IPO timeline start? This takes 3 hours to implement vs. 6 weeks to build internally." [ROI calc]

**"This seems specific to dbt"**
→ "dbt is the wedge. Same architecture works for activation (Hightouch/Census) and AI agents. Data-led, agent-ready." [Roadmap]

**"What about cost?"**
→ "Review is $35K/year. Your controller spends 6 weeks at $200/hour = $48K per quarter = $192K/year. This pays for itself in quarter one." [TCO]

---

## 12. Success Metrics & KPIs

### Leading Indicators (Weekly)

- **OSS Adoption:** dbt hooks installed, ServiceNow bridge usage
- **Evidence Bundles Generated:** Actual usage proof (not vanity)
- **Badge Issuance:** "Clyra Certified" badges live in READMEs
- **Community Engagement:** Help given, credibility built

### Commercial KPIs (Monthly)

- **Review Signups:** New customers starting listen-only
- **Gate Conversions:** Review → Gate upsell (target 30%)
- **Time to Value:** Days from signup to first attested ticket
- **Audit Time Reduction:** 6-8 weeks → 3-5 days (realized)

### Strategic Milestones (Quarterly)

**Q1 (Days 1-90):**

- 1,000 GitHub stars across OSS repos
- 100 dbt projects with hooks installed
- 10 ServiceNow integrations live
- 5 pilot customers (Review SKU)

**Q2 (Days 91-180):**

- 100 "Clyra Certified" badges live
- 2 Big 4 audit firm acknowledgments
- 10 paying customers (8 Review, 2 Gate)
- $150K ARR

**Q3 (Days 181-270):**

- 30 paying customers (20 Review, 10 Gate)
- $400K ARR
- 30% Review→Gate conversion proven
- Series A positioning

**Q4 (Days 271-365):**

- 50 paying customers
- $600K ARR (runway + Series A ready)
- Integration partnerships (dbt Labs, Snowflake)
- "Industry standard" positioning achieved

### North Star Metric

**"Attested Change Tickets Created"**

- Month 3: 1,000 tickets (usage proof)
- Month 6: 10,000 tickets (network effect)
- Month 12: 100,000 tickets (industry standard)

---

## 13. The Launch Strategy

### Pre-Launch: 8-Week OSS Campaign (-60 to -1 Days)

**Goals:**

- Build credibility (no Clyra promotion)
- Create urgency (concrete pain focus)
- Establish patterns (evidence bundle format)
- Generate demand ("Is there a tool that does all this?")

**Tactics:**

- 4 OSS releases (ServiceNow bridge, evidence spec, dbt hooks, SOX checklist)
- 8 problem-first blog posts
- 50+ community contributions
- 500+ email subscribers

### Launch Week: "The Automation Layer" (Days 1-7)

**Monday: GitHub + Show HN**

- "Show HN: Clyra - Data Change Control for dbt + Snowflake"
- Built from 8 weeks of community feedback
- OSS tools → now integrated platform
- Founder online 12 hours

**Tuesday: dbt Community Launch**

- dbt Slack: "The tool that automates the SOX workflow"
- r/dbt: "Released: Complete dbt governance platform"
- Focus: ServiceNow integration (the wedge)

**Wednesday: Warehouse Community**

- Snowflake community: "QUERY_HISTORY-native governance"
- Databricks community: "Delta commit anchoring"
- Technical credibility focus

**Thursday: Compliance Community**

- SOX forums: "6-8 weeks → 3-5 days audit prep"
- Controller networks: "Automated evidence collection"
- Business value focus

**Friday: Case Study Publication**

- "How [Company] Achieved SOX Compliance in 3 Hours"
- Real numbers: audit time, cost savings
- Badge displayed in their README

### Post-Launch: Evidence Network (Days 8-30)

**Week 2: Badge Amplification**

- First 20 badges issued
- Social proof in READMEs
- Community shares screenshots
- Viral growth begins

**Week 3: Audit Partner Validation**

- First Big 4 acknowledgment
- QSA guidance published
- "Clyra-ready" audit procedures
- Professional services opportunity

**Week 4: Platform Expansion**

- First Review→Gate conversion
- Case study: "Why [Company] Upgraded to Full Enforcement"
- Commercial validation

---

## 14. Risk Mitigation

### Market Risks

**Risk:** "Data governance market is crowded"
**Mitigation:** We're not competing with observability/catalogs. We solve SOX change control (underserved pain). Different buyer, different budget.

**Risk:** "dbt/Snowflake build competing features"
**Mitigation:** Partner positioning ("we integrate with your stack"). Independent verifier moat (trust without vendor lock-in). Move fast with OSS adoption.

**Risk:** "Audit firms don't adopt"**
**Mitigation:** Evidence format is vendor-neutral. QSAs can verify independently. Start with 2-3 Big 4 champions. Make them the heroes.

### Technical Risks

**Risk:** "Warehouse integration complexity"
**Mitigation:** Start with Snowflake/Databricks (80% of market). Postgres for dev/pilot. Phased rollout strategy.

**Risk:** "dbt hook performance impact"
**Mitigation:** <2s overhead per run (benchmarked). Metadata-only capture. Async evidence generation. Performance SLAs documented.

### Commercial Risks

**Risk:** "Customers don't convert Review→Gate"
**Mitigation:** 30% target is conservative. Value is proven in listen-only. Enforcement is natural progression. Usage-based pricing considered.

**Risk:** "Badge program doesn't drive adoption"
**Mitigation:** Multiple entry points (OSS tools, badge, ServiceNow integration). Badge is one vector, not the only vector.

---

## 15. The 18-Month Vision

### Industry Standard Outcome

**When data teams ask:** "How do we prove our dbt changes are SOX compliant?"
**The answer is:** "Clyra"

**Indicators:**

- "Clyra Certified" badges in 1,000+ READMEs
- Big 4 audit firms require DEF format in RFPs
- dbt Labs partnership/integration
- Snowflake/Databricks marketplace listings
- "Data change control" = Clyra (category ownership)

### The Platform Flywheel

```
dbt Hooks Installed → Evidence Bundles Generated →
ServiceNow Tickets Created → Auditors See Proof →
Controllers Demand It → More dbt Projects Adopt →
Badges Displayed → Social Proof → Viral Growth →
dbt Hooks Installed
```

### Strategic Options (18-24 Months)

**Option 1: Independent Platform ($10M+ ARR path)**

- Expand to full data governance platform
- Add content governance (email/CMS)
- Build UI/dashboard for non-technical stakeholders
- Series B fundraise

**Option 2: Strategic Acquisition (dbt Labs, Snowflake, Databricks)**

- "Native governance layer" positioning
- Integration depth + adoption rate = acquisition premium
- Exit multiple: 15-20× ARR ($600K → $9-12M acquisition)

**Option 3: AI Governance Pivot (Agent-Ready)**

- Expand from data platform to AI agents
- Same architecture, broader scope
- "Data-led governance for AI" positioning
- Larger market, higher valuations

---

## Appendix A: The Problem-First Demo Script

### The 5-Minute Evidence Workflow

**Setup:** "Let me show you how this works—dbt run to attested ServiceNow ticket."

**Minute 1: The Problem**

```
"Show me your last SOX audit prep. How did you link Jira tickets to dbt runs?"
[Customer explains manual process, 6-8 weeks]
```

**Minute 2: The dbt Integration**

```bash
clyra dbt init demo-project
# Shows: hooks install, macros configured, 2 minutes
```

**Minute 3: The Evidence Generation**

```bash
dbt run  # Normal dbt run with hooks
clyra verify evidence.zip --explain
# Shows: dbt run ID, QUERY_HISTORY ref, approval, schema diff—all in one bundle
```

**Minute 4: The ServiceNow Ticket**

```
# Evidence automatically attached to change ticket
# Fields populated: change_id, dbt_run_id, query_history_ref, approver, schema_diff
# One ticket, all proof, ready for auditor
```

**Minute 5: The Attestation**

```bash
clyra attest evidence.zip --framework sox
# Signed SOX ITGC attestation generated
# PDF + JSON ready for audit review
```

**The Question:** "How long does your current process take?" [6-8 weeks → 3-5 days]

---

## Appendix B: Problem-First Messaging Templates

### Email Templates

**Subject:** "How do you link Jira tickets to dbt runs?"

Hi [Name],

Quick question: When auditors ask "Show me the change ticket for this dbt model change," what do you show them?

If you're like most data teams:

- Jira ticket exists (but doesn't reference dbt run ID)
- dbt Cloud shows the run (but no approval record)
- Snowflake has QUERY_HISTORY (but no link to ticket)
- Manual spreadsheet ties it together (6 weeks of work)

We built Clyra to automate this. dbt run → attested ServiceNow ticket automatically.

10-minute demo: [calendar link]
See the workflow: [demo video]

Best,
[Signature]

---

**Subject:** "6-8 weeks → 3-5 days (SOX audit prep)"

Hi [Name],

Your controller just asked: "How long will SOX audit prep take this quarter?"

If you answered "6-8 weeks of evidence collection," you have a problem.

What if it was 3-5 days instead?

Clyra automates evidence collection from dbt runs:
✓ dbt run ID + QUERY_HISTORY → linked automatically
✓ Approval records → attached to change tickets
✓ Schema diffs → captured and verified
✓ SOX attestations → generated on demand

See the workflow: [demo link]
Schedule walkthrough: [calendar]

Best,
[Signature]

---

### Social Media Templates

**LinkedIn: The Audit Prep Reality**

Quarter-end audit prep for data platform:

Week 1-2: Identify all dbt model changes
Week 3-4: Find Slack approvals for each
Week 5: Match Jira tickets to dbt runs manually
Week 6-8: Create evidence spreadsheet

Controller's reaction: "This can't be our process."

There's a better way. Automate evidence from dbt hooks.

6-8 weeks → 3-5 days.

# DataEngineering #SOXCompliance #dbt

---

**Twitter/X: The ServiceNow Integration**

Your dbt model just changed the revenue calculation.

Auditor asks: "Show me the change ticket."

What ticket? Approval was in Slack, run was in dbt Cloud, queries are in QUERY_HISTORY.

Nothing connects them.

Until now: [demo link]

# dbt #Snowflake #DataGovernance

---

## Appendix C: The OSS Wedge Artifacts

### Release Schedule (Pre-Launch)

**Week 2: ServiceNow/Jira Bridge**

- Repo: `data-change-control/servicenow-jira-bridge`
- Files: Bash scripts, payload examples, setup guide
- Value: Immediate—attach dbt evidence to tickets today

**Week 3: Evidence Bundle Spec**

- Repo: `data-change-control/evidence-bundle-spec`
- Files: JSON schemas, verifier stub (Go), auditor guide
- Value: Format standardization—vendor-neutral

**Week 5: dbt SOX Hooks**

- Repo: `data-change-control/dbt-sox-hooks`
- Files: on_run_end macros, ServiceNow integration, examples
- Value: Complete workflow—hooks + bridge + evidence

**Week 8: SOX Data Checklist**

- Repo: `data-change-control/sox-data-checklist`
- Files: Implementation checklist, timeline, templates
- Value: Roadmap—how to do this yourself

### Week 9: The Clyra Reveal

"These 4 OSS tools got 200+ teams started. But you asked: 'Is there one platform that does all this?'

Today we're launching Clyra—the automation layer that ties it together.

OSS foundation + commercial platform.
dbt + Snowflake/Databricks native.
From hook → attested ServiceNow ticket in one system.

Built from 8 weeks of your feedback."

---

**End of GTM Strategy v4.0**
