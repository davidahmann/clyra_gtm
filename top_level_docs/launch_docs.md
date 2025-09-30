# Critical Launch Documents (Data-Led, Agent-Ready)

## Pre-Launch Foundation (Weeks -8 to -1)

### 0. OSS Wedge Artifacts (Released Before Clyra Launch)

**Purpose:** Build credibility + urgency (NO Clyra branding until launch)

**Week 2: ServiceNow/Jira Bridge**
- Repo: `data-change-control/servicenow-jira-bridge`
- Bash scripts to attach dbt evidence to tickets
- Payload examples + setup guide
- Community asks: "Who built this?"

**Week 3: Evidence Bundle Spec**
- Repo: `data-change-control/evidence-bundle-spec`
- JSON schemas + verifier stub (Go)
- Auditor guide + sample bundles
- Vendor-neutral format

**Week 5: dbt SOX Hooks**
- Repo: `data-change-control/dbt-sox-hooks`
- on_run_end macros + ServiceNow integration
- Complete workflow examples
- 50+ projects adopt before launch

**Week 8: SOX Data Checklist**
- Repo: `data-change-control/sox-data-checklist`
- Implementation timeline + templates
- Role matrix + daily review queries
- Community says: "Is there one tool that does all this?"

**Success Metrics Before Launch:**
- 1,000 GitHub stars (across OSS repos)
- 200+ teams using evidence format
- 50+ dbt projects with hooks
- 500+ email subscribers (launch amplification)

---

## Launch Day Documents (Week 1)

### 1. README.md (GitHub repo)

**Purpose:** Perfect first impression for data teams who've been using OSS tools

**Structure:**

```markdown
# Clyra - Data Change Control & Attestation for Modern Pipelines

**The Problem:** Your dbt models change production schemas. Auditor asks: "Show me proof these changes follow SOX change control." You have Slack approvals, Jira tickets, dbt Cloud logs, and Snowflake QUERY_HISTORY—but nothing connects them. 6-8 weeks to reconstruct the evidence trail.

**The Solution:** Clyra automates the complete workflow—dbt run → attested ServiceNow ticket—turning 6-8 weeks of audit prep into 3-5 days.

## Quick Start (10 Minutes)

```bash
clyra dbt init my-project               # dbt hooks installed
make quickstart-data                     # Local stack up
clyra demo data --platform snowflake    # Evidence bundles generated
clyra verify evidence.zip               # Independent verification
clyra attest evidence.zip --framework sox  # Signed SOX attestation
```

## What Makes Clyra Different

**vs. Data Observability (Monte Carlo, Metaplane)**
- They detect. We prevent AND prove.
- Alerts ≠ Audit evidence.

**vs. Data Catalogs (Alation, Atlan)**
- They document. We prove changes.
- Discovery ≠ Compliance.

**vs. dbt Cloud Features**
- They might build eventually. We integrate today.
- Vendor lock-in vs. vendor-neutral.

## The OSS Foundation

Built from 8 weeks of community feedback:
- ServiceNow/Jira bridge (200+ teams using)
- Evidence bundle spec (50+ dbt projects)
- dbt SOX hooks (production-tested)
- SOX data checklist (your roadmap)

Now integrated into one platform.

## Badge Program

"Clyra Certified - SOX Compliant" badge for your README.

[See Example Badge]

## Architecture

Data-led (dbt + Snowflake/Databricks today), agent-ready (AI agents tomorrow).

Same control patterns (approval + evidence + attestation).
Same architecture, expanding scope.

## Get Started

- [Quick Start Guide](QUICKSTART.md)
- [Documentation](docs/)
- [OSS Tools](https://github.com/data-change-control)
```

**Key Elements:**
- Opens with concrete pain (6-8 weeks)
- 10-minute path clearly laid out
- OSS foundation prominently mentioned
- "Clyra Certified" badge visible
- Data-led, agent-ready positioning

---

### 2. QUICKSTART.md

**Purpose:** 10-minute dbt → SOX attestation success path

**Structure:**

```markdown
# Quick Start Guide

Get from zero to signed SOX attestation in 10 minutes.

## Prerequisites

- dbt Core or Cloud (1.0+)
- Snowflake or Databricks account
- ServiceNow or Jira (optional but recommended)

## Step 1: Initialize dbt Project (2 min)

```bash
clyra dbt init my-project
cd my-project
```

What this does:
- Installs Clyra hooks in dbt_project.yml
- Adds macros for evidence generation
- Configures warehouse integration

## Step 2: Start Local Stack (3 min)

```bash
make quickstart-data
```

What starts:
- Clyra Gateway (port 8080)
- Clyra Recorder (port 8081)
- Snowflake simulator (port 5432)
- Sample dbt project

## Step 3: Run dbt with Evidence (2 min)

```bash
dbt run  # Hooks emit evidence automatically
ls evidence/  # See DEF bundles
```

What gets captured:
- dbt run ID
- QUERY_HISTORY reference
- Schema diff (before/after)
- Approval record

## Step 4: Verify Evidence (1 min)

```bash
clyra verify evidence.zip --explain
```

Output shows:
- Bundle validation (cryptographic proof)
- Lineage tracking (what changed)
- Approval verification

## Step 5: Generate SOX Attestation (2 min)

```bash
clyra attest evidence.zip --framework sox
```

Output:
- Signed SOX ITGC attestation
- PDF + JSON (auditor-ready)
- Independent verification instructions

## Next Steps

### Connect ServiceNow/Jira

```bash
clyra bridge configure --platform servicenow
# Evidence automatically attached to tickets
```

### Get Your Badge

```bash
clyra badge request --framework sox
# "Clyra Certified" badge for your README
```

### Explore OSS Tools

- [ServiceNow/Jira Bridge](https://github.com/data-change-control/servicenow-jira-bridge)
- [Evidence Bundle Spec](https://github.com/data-change-control/evidence-bundle-spec)
- [dbt SOX Hooks](https://github.com/data-change-control/dbt-sox-hooks)
- [SOX Data Checklist](https://github.com/data-change-control/sox-data-checklist)

## Troubleshooting

### Warehouse Connection Issues
- Snowflake: Check session tag support
- Databricks: Verify Unity Catalog access
- [See docs/troubleshooting.md]

### dbt Integration Issues
- Hook execution order
- Macro conflicts
- [See docs/dbt-integration.md]
```

**Key Elements:**
- 10-minute timeline with exact steps
- What gets captured at each step
- ServiceNow/Jira integration prominent
- Badge program callout
- OSS tools linked

---

### 3. Demo Script & Video Outline

**Purpose:** 5-minute "Data Governance Challenge" for launch day

**Script:**

```
[0:00-0:30] The Problem
"Quarter-end audit. Your dbt model changed the revenue calculation.
Auditor asks: 'Show me the change ticket.'
You have Slack threads, Jira tickets, dbt logs. Nothing connects them."

[0:30-1:00] The Setup
"Let me show you the complete workflow—dbt run to attested ServiceNow ticket."
[Screen: clyra dbt init command running]

[1:00-2:00] The dbt Integration
[Screen: dbt_project.yml with hooks]
"Hooks installed. Now watch what happens when we run dbt."
[Screen: dbt run executing, evidence bundle generated]

[2:00-3:00] The ServiceNow Integration
[Screen: ServiceNow ticket with ALL fields populated]
"One ticket. ALL the proof. dbt run ID + QUERY_HISTORY + approval + schema diff.
No manual correlation."

[3:00-4:00] The SOX Attestation
[Screen: clyra attest command]
"Signed SOX ITGC attestation. PDF + JSON. Ready for auditor."
[Screen: Badge appearing in README]
"Clyra Certified - SOX Compliant."

[4:00-4:30] The Architecture
"Data platform today (dbt + Snowflake). AI agents tomorrow (same patterns).
Data-led, agent-ready."

[4:30-5:00] The Challenge
"Can your data observability tools do this?
6-8 weeks → 3-5 days. Try Clyra."
[Screen: GitHub repo link]
```

**Camera Angles:**
- Split screen: Terminal + ServiceNow ticket
- Zoom on evidence bundle JSON
- README with badge prominently displayed

**Talking Points:**
- "Nothing connects them" (pain hook)
- "ONE ticket, ALL the proof" (value)
- "3-5 days" (metric that matters)
- "Data-led, agent-ready" (positioning)

---

## Go-to-Market Execution (Week 2-4)

### 4. Show HN Launch Package

**Title:** "Show HN: Clyra - Data Change Control for dbt + Snowflake"

**Launch Post:**

```
Hi HN,

8 weeks ago, I started releasing OSS tools to help data teams with SOX compliance:
- ServiceNow/Jira bridge (200+ teams using)
- Evidence bundle spec (50+ dbt projects)
- dbt SOX hooks (production-tested)
- SOX data checklist (complete roadmap)

You asked: "Is there one platform that does all this?"

Today we're launching Clyra—the automation layer that ties it together.

**The Problem:**
Quarter-end audit. Your dbt model changed the revenue calculation. Auditor asks:
"Show me the change ticket with approval proof." You have Slack approvals, Jira
tickets, dbt Cloud logs, Snowflake QUERY_HISTORY—but nothing connects them.
6-8 weeks to reconstruct the evidence trail.

**The Solution:**
Clyra automates the complete workflow—dbt run → attested ServiceNow ticket.
- dbt hooks emit evidence bundles
- ServiceNow/Jira bridge attaches proof to tickets
- Signed SOX attestations generated on demand
- 6-8 weeks → 3-5 days

**Demo:** [link to live demo]
**GitHub:** [link to repo]
**Quick Start:** 10 minutes from zero to signed SOX attestation

Built from 8 weeks of your feedback. OSS foundation, commercial platform.

Happy to answer any questions!
```

**FAQ Responses (Pre-written):**

Q: "How is this different from dbt Cloud features?"
A: "dbt Cloud provides tests and documentation. We provide SOX change control—linking approvals to dbt runs to QUERY_HISTORY to ServiceNow tickets. Vendor-neutral integration, not platform lock-in."

Q: "What databases do you support?"
A: "Snowflake and Databricks (production). Postgres (dev/pilot). We anchor evidence to QUERY_HISTORY (Snowflake), Delta commits (Databricks), WAL LSN (Postgres)."

Q: "Why would I use this vs. building it myself?"
A: "You could. 6 weeks to build, 3 months to harden = $150K+ first year. Or 3 hours to SOX-ready with Clyra for $35K/year. We've battle-tested this with 200+ teams using the OSS tools."

Q: "What about AI agents?"
A: "Data-led, agent-ready. Same architecture (approval + evidence + attestation) works for dbt runs today and agent actions tomorrow. Data platform is where budget exists now."

**Live Demo Links:**
- Quickstart recording (10-minute flow)
- ServiceNow ticket example (populated fields)
- Badge example (Clyra Certified in README)

---

### 5. Content Calendar (First 90 Days)

**Week 1-2: Launch Amplification**
- Monday: Show HN launch
- Tuesday: dbt Community Slack announcement
- Wednesday: r/dataengineering launch post
- Thursday: "Why Data Teams Will Own AI Agent Governance" (blog)
- Friday: First "Clyra Certified" badges issued

**Week 3-4: Case Studies & Social Proof**
- "How [Company] Went from 6 Weeks to 3 Days" (case study)
- "ServiceNow Integration Deep Dive" (technical post)
- "Badge Program Results: 50+ Certified Projects" (update)

**Week 5-8: Education & Adoption**
- "SOX ITGC for Data Teams: A Practical Guide" (long-form)
- "Jira vs ServiceNow for Data Change Control" (comparison)
- "dbt Hooks Performance: What We Learned" (technical)

**Week 9-12: Expansion & Validation**
- First Big 4 audit firm acknowledgment (announcement)
- "30% Review → Gate Conversion: What We Learned" (metrics)
- "Roadmap: Activation Controls Coming Soon" (strategic)

**Reddit Templates:**

r/dataengineering:
```
Title: "Released: Complete SOX change control for dbt + Snowflake"

Body: "We've been working on this for 8 weeks with the community.
The problem: dbt changes schemas, auditors need proof, evidence is scattered.
The solution: dbt hooks → evidence bundles → ServiceNow tickets.
6-8 weeks audit prep → 3-5 days.

Built from OSS tools 200+ teams are already using. Now integrated into one platform.

[Link to GitHub] [Link to quick start]

Would love feedback from data platform engineers."
```

**Social Media Templates:**

LinkedIn:
```
Your dbt model just changed the revenue calculation.

Auditor asks: "Show me the change ticket."

What ticket? Approval was in Slack, run was in dbt Cloud, queries are in QUERY_HISTORY.

Nothing connects them.

Until now.

[Demo link]
#DataEngineering #SOXCompliance #dbt
```

Twitter/X:
```
Quarter-end audit prep for data teams:

Week 1-2: Find all dbt model changes
Week 3-4: Match approvals to runs
Week 5-6: Create evidence spreadsheet
Week 7-8: Still not done

There's a better way.

6-8 weeks → 3-5 days

[Link]
```

---

### 6. Sales Battlecards

**vs. Data Observability (Monte Carlo, Metaplane)**

**Their Positioning:** "Detect data quality issues with monitoring"
**Our Positioning:** "Prove data changes follow SOX change control"

**Key Differences:**
- Detection vs. Attestation
- Alerts vs. Audit evidence
- Data quality vs. Change control
- Post-incident vs. Pre-deployment

**Win Strategy:**
- Show ServiceNow ticket with complete evidence
- Demo SOX attestation generation
- Prove vendor-neutral approach
- "They monitor. We govern."

**Demo Flow:**
1. Show Monte Carlo dashboard (alerts, lineage)
2. Ask: "Where's the change ticket? Where's the approval proof?"
3. Show Clyra: dbt run → ServiceNow ticket with ALL evidence
4. Ask: "Can Monte Carlo do this?"

---

**vs. dbt Cloud Features**

**Their Positioning:** "We might build governance features eventually"
**Our Positioning:** "We integrate with your dbt + Snowflake + ServiceNow stack today"

**Key Differences:**
- Wait vs. Ship now
- Vendor lock-in vs. Vendor-neutral
- Tests vs. Change control
- dbt-only vs. Multi-platform

**Win Strategy:**
- Acknowledge dbt Cloud is great (don't compete)
- Position as "dbt governance layer" (integrate)
- Show ServiceNow/Jira integration (they don't have)
- "We love dbt. That's why we built this for dbt teams."

**Demo Flow:**
1. Show dbt Cloud (tests, docs, runs)
2. Ask: "How do you link these runs to ServiceNow tickets?"
3. Show Clyra hooks: automatic evidence + ticket creation
4. Ask: "When will dbt Cloud have this?"

---

**Demo Flow by Persona:**

**Data Platform Engineer (Primary Champion)**
- Pain: "Can't prove changes were approved"
- Hook: "Watch—dbt run → attested ticket automatically"
- Demo: Full technical workflow (hooks, evidence, verification)
- Close: "3 hours to SOX-ready. Try Review SKU (listen-only)."

**Controller (Validator)**
- Pain: "6-8 weeks of audit prep every quarter"
- Hook: "ONE ticket with ALL the proof"
- Demo: ServiceNow ticket populated, auditor validation
- Close: "$192K/year → $35K/year. Quarter-one payback."

**Head of Data Platform (Economic Buyer)**
- Pain: "Compliance friction slows pipeline velocity"
- Hook: "Ship dbt models faster with automated SOX compliance"
- Demo: Badge program, audit partner network, roadmap
- Close: "Data platform today, AI agents tomorrow. Lock in architecture."

---

**ROI Calculator:**

```
Current State (Manual):
- Controller time: 6 weeks × 4 quarters = 24 weeks/year
- @ $200/hour × 40 hours/week = $192K/year
- Data engineer support: 2 weeks × 4 quarters = 8 weeks/year
- @ $150/hour × 40 hours/week = $48K/year
Total: $240K/year

With Clyra Review ($35K/year):
- Audit prep time: 3 days × 4 quarters = 12 days/year
- @ $200/hour × 8 hours/day = $19.2K/year
- Setup time: 3 hours = $600
Total: $19.8K/year + $35K Clyra = $54.8K/year

Savings: $185K/year (77% reduction)
Payback: Quarter one

With Clyra Gate ($100K/year):
- Same audit prep savings
- + Policy enforcement value
- + Kill-switch capabilities
Total: Still $85K/year savings (35% reduction)
```

---

## Technical Foundation (Week 2-3)

### 7. Architecture Decision Records (ADRs)

**ADR-001: Warehouse Anchors Over Timestamps**

**Context:** Need immutable truth for data change tracking

**Decision:** Use warehouse-native anchoring:
- Snowflake: QUERY_HISTORY query_id
- Databricks: Delta commit SHA
- Postgres: WAL LSN

**Rationale:**
- Clock drift eliminated (NTP issues)
- Immutable sequence (can't be manipulated)
- Warehouse-native (no external dependency)
- Audit-grade proof (cryptographic correlation)

**Consequences:**
- Requires warehouse integration (complexity)
- Snowflake/Databricks focus initially
- Performance overhead <1ms (acceptable)

---

**ADR-002: Independent Verifier Philosophy**

**Context:** Auditors need trust without vendor lock-in

**Decision:** Dual verifiers (Go + TypeScript), open source, vendor-neutral format

**Rationale:**
- Auditors can verify offline (no Clyra dependency)
- Cross-language consistency (Go/TS match)
- Vendor-neutral format (DEF/PEF open spec)
- Trust through mathematics (not vendor claims)

**Consequences:**
- Dual implementation cost (maintain 2 verifiers)
- Format must be stable (breaking changes costly)
- Community contribution encouraged

---

**ADR-003: dbt Hook Performance Budget**

**Context:** dbt runs must stay fast

**Decision:** <2s overhead per dbt run

**Rationale:**
- Metadata-only capture (no data movement)
- Async evidence generation (non-blocking)
- Schema diff optimization (incremental)
- QUERY_HISTORY correlation (indexed lookup)

**Consequences:**
- Must benchmark continuously
- Performance SLA in docs
- Degradation = critical bug

---

### 8. API Documentation

**CLI Command Reference:**

```bash
# dbt Integration
clyra dbt init <project-name>        # Initialize dbt project with hooks
clyra dbt hooks install              # Add hooks to existing project
clyra dbt hooks test                 # Validate hook configuration

# Warehouse Management
clyra warehouse doctor --platform snowflake  # Check connectivity
clyra warehouse anchor test                  # Validate QUERY_HISTORY
clyra warehouse session create               # Start tracked session

# Evidence Generation
clyra demo data --platform snowflake   # Generate sample DEF bundles
clyra verify evidence.zip --explain    # Independent verification
clyra replay evidence.zip              # Deterministic reproduction

# Attestation
clyra attest evidence.zip --framework sox      # SOX ITGC attestation
clyra attest evidence.zip --framework pci      # PCI DSS attestation
clyra attest evidence.zip --framework hipaa    # HIPAA attestation

# ServiceNow/Jira Integration
clyra bridge configure --platform servicenow  # Setup integration
clyra bridge test                             # Validate connection
clyra bridge export evidence.zip              # Attach to ticket

# Badge Program
clyra badge request --framework sox    # Request certification
clyra badge verify --project-id <id>   # Verify badge authenticity

# Daily Review
clyra report --daily-review --include-data-changes  # Enhanced review
clyra report --weekly-summary                       # Week summary
clyra report --quarterly-audit                      # Audit prep export
```

---

**Policy.yaml Schema:**

```yaml
# Data Platform Controls
data_platform:
  dbt:
    approval_required: true
    schema_changes_require_review: true
    sql_safety_guards: true

  warehouse:
    anchor_type: query_history  # or delta_commits, wal_lsn
    session_tags_required: true

  activation:
    enforce_approval: false  # start with listen-only
    rate_limits:
      hightouch: 1000/hour
      census: 1000/hour

# Enforcement Controls
enforcement:
  mode: listen_only  # or review, gate

  approval:
    bec_grade: true
    sso_binding: true
    ttl: 3600

  kill_switch:
    data_burst: 10000/minute
    error_threshold: 5%

# Compliance Frameworks
compliance:
  frameworks: [sox, pci, hipaa]
  attestation_auto_generate: true
  daily_review: true
  badge_program: true
```

---

## Compliance & Sales Support (Week 4-6)

### 9. Compliance Mapping Documents

**SOX ITGC Controls → Clyra Features**

| Control | Requirement | Clyra Feature |
|---------|-------------|---------------|
| CC6.1 | Logical access controls | Approval certificates (SSO-bound) |
| CC7.2 | System operations | dbt hooks + warehouse anchors |
| CC8.1 | Change management | ServiceNow/Jira integration |
| CC6.6 | Logical access reviews | Daily review automation |
| CC6.8 | Segregation of duties | Role-based approvals |

**Auditor Briefing:** "Clyra automates change control for data platform operations, providing the evidence SOX auditors need in the format they expect (ServiceNow/Jira change tickets)."

---

**PCI DSS Requirements → Clyra Features**

| Requirement | Description | Clyra Feature |
|-------------|-------------|---------------|
| Req-10.1 | Audit trails | Enhanced daily review |
| Req-10.2.7 | Database object access | Warehouse anchor tracking |
| Req-6.5 | Secure development | dbt CI/CD gates |
| Req-8.7 | Database access | Session correlation |

**QSA Briefing:** "Clyra provides the audit trail completeness PCI Req-10 requires, with warehouse-native anchoring that can't be tampered with."

---

### 10. Case Study Templates

**"The Revenue Model Change That SOX Auditors Approved"**

**Customer Profile:**
- Company: [200-2K employee SaaS, pre-IPO]
- Stack: dbt + Snowflake + ServiceNow
- Pain: 6-8 weeks audit prep, scattered evidence

**The Problem:**
"Quarter-end close: Our dbt model changed revenue calculation. Tests passed. Auditor asked: 'Show me who approved this and where's the proof.' We had Slack threads, Jira tickets, QUERY_HISTORY—nothing connected them. 6 weeks to reconstruct the trail."

**The Solution:**
"Deployed Clyra Review (listen-only) in Week 1. dbt hooks installed in 3 hours. Evidence bundles generated automatically. ServiceNow integration configured Week 2. First attested change ticket Week 3."

**The Results:**
- Audit prep time: 6-8 weeks → 3 days
- Evidence completeness: Manual spreadsheet → Automated bundles
- Controller satisfaction: "This is actually our process now"
- Badge earned: "Clyra Certified - SOX Compliant" in README

**Quotes:**
- Data Engineer: "3 hours to SOX-ready. We should have done this quarter one."
- Controller: "ONE ticket with ALL the proof. This is what I've been asking for."
- Head of Data: "Data platform governance without slowing velocity."

**Metrics:**
- Time to first bundle: 30 minutes
- Review → Gate conversion: Day 90
- ROI: $192K → $35K (quarter-one payback)

---

## Channel & Partner Materials (Week 6-8)

### 11. SI Enablement Kit

**White-Label Presentation Deck:**

Slide 1: "Data Change Control Challenges"
- 6-8 weeks audit prep
- Evidence scattered across systems
- Manual correlation required

Slide 2: "Clyra Solution Architecture"
- dbt hooks → Evidence bundles → ServiceNow tickets
- Warehouse-native anchoring
- Independent verification

Slide 3: "Implementation Timeline"
- Week 1: Pilot (Review SKU, listen-only)
- Week 2-4: Integration (ServiceNow/Jira)
- Week 5-8: Production (Gate SKU, enforcement)

Slide 4: "ROI & Business Case"
- $192K/year → $35K/year
- Quarter-one payback
- Badge program participation

**Procurement Checklist:**

For Data Platform Teams:
- [ ] dbt version compatibility (1.0+)
- [ ] Warehouse support (Snowflake/Databricks)
- [ ] ServiceNow/Jira access
- [ ] 3-hour setup window

For Finance Teams:
- [ ] Budget approval ($35K Review, $100K Gate)
- [ ] ROI validation (audit prep time)
- [ ] Contract review (SaaS terms)
- [ ] Badge program participation

**Partnership Details:**

ServiceNow Integration:
- Change Management module required
- Custom fields: dbt_run_id, query_history_ref, schema_diff
- REST API access
- Workflow automation enabled

Jira Integration:
- Custom issue type: "Data Change"
- Custom fields: dbt Run ID, Query History Link
- Automation rules for approval flow
- Atlassian SDK integration

---

### 12. Community Building Assets

**Discord Server Structure:**

#announcements - Product updates, new features
#dbt - dbt integration help
#snowflake - Snowflake integration help
#databricks - Databricks integration help
#servicenow-jira - Bridge integration help
#badge-program - Certification questions
#general - Community chat

**GitHub Issue Templates:**

Bug Report:
- dbt version
- Warehouse platform
- Hook execution logs
- Evidence bundle (if applicable)

Feature Request:
- Use case description
- Current workaround
- Expected behavior
- Data platform context

Integration Request:
- Platform name
- API documentation
- Community size
- Business case

**Livestream Format: "dbt Bundle Analysis"**

Episode 1: "Anatomy of a DEF Bundle"
- dbt run → evidence generation
- Bundle structure walkthrough
- Verification demonstration
- Q&A

Episode 2: "ServiceNow Integration Deep Dive"
- Change ticket creation
- Field population
- Approval workflow
- Auditor validation

Episode 3: "Badge Program: How It Works"
- Certification process
- JWT signing
- README integration
- Social proof

---

## Metrics & Operations (Ongoing)

### 13. Analytics & KPI Dashboard Spec

**Funnel Tracking:**
```
GitHub Star → README Read → Quick Start → Evidence Bundle →
ServiceNow Ticket → SOX Attestation → Badge Request →
Review Signup → Gate Conversion
```

**Drop-off Points:**
- README → Quick Start (target: >40%)
- Quick Start → Evidence Bundle (target: >60%)
- Evidence Bundle → ServiceNow (target: >50%)
- Review → Gate (target: >30%)

**Technical Metrics:**
- dbt hook performance (target: <2s overhead)
- Warehouse anchor success rate (target: >99%)
- DEF verification speed (target: <1s)
- ServiceNow API latency (target: <500ms)

**Community Health:**
- GitHub stars (target: 1,000 in 90 days)
- Badge adoption (target: 100 in 180 days)
- dbt project integrations (target: 50 production)
- Discord members (target: 500 active)

**Sales Pipeline:**
- Review signups (target: 10 in 90 days)
- Gate conversions (target: 30% in 90 days post-signup)
- Data platform penetration (Snowflake/Databricks customers)
- Average contract value (Review $35K, Gate $100K)

---

### 14. Customer Success Playbooks

**Onboarding Checklist (Review SKU):**

Day 1-7:
- [ ] Kickoff call (30 min)
- [ ] dbt version check
- [ ] Warehouse connectivity test
- [ ] Hooks installation (3 hours)
- [ ] First evidence bundle generated

Day 8-14:
- [ ] ServiceNow/Jira integration configured
- [ ] First attested change ticket created
- [ ] Badge request submitted
- [ ] Daily review automation enabled

Day 15-30:
- [ ] 10+ evidence bundles generated
- [ ] 5+ change tickets created
- [ ] Controller validation completed
- [ ] Badge issued

**Common Implementation Patterns:**

FinServ (SOX + PCI):
- Heavy ServiceNow integration
- Strict approval workflows
- Multi-framework attestations
- Badge program participation

Retail (SOX + HIPAA):
- Jira for data team
- ServiceNow for compliance
- Activation controls (Hightouch)
- Badge program participation

Healthcare (HIPAA + SOX):
- Privacy-preserving evidence
- Voice compliance future
- Multi-framework attestations
- Audit partner validation

**Escalation Procedures:**

Warehouse Connectivity:
- Snowflake: Session tag support, QUERY_HISTORY access
- Databricks: Unity Catalog permissions, Delta commit access
- Postgres: WAL LSN access (dev/pilot only)

dbt Integration:
- Hook execution order conflicts
- Macro naming collisions
- Performance degradation (>2s overhead)

ServiceNow/Jira:
- API authentication failures
- Custom field configuration
- Workflow automation issues

**Reference Customer Development:**

Review → Gate Progression:
- Week 1-4: Review SKU pilot (listen-only)
- Week 5-8: Evidence validation (controller sign-off)
- Week 9-12: Gate SKU trial (enforcement testing)
- Month 4: Gate SKU production (full enforcement)

Success Criteria:
- 30+ evidence bundles generated (Review phase)
- 10+ change tickets validated by auditor (Review phase)
- Badge issued (social proof)
- Controller recommends Gate SKU (economic validation)

---

## Priority Order

**Pre-Launch (Week -8 to -1):**
1. OSS Wedge Artifacts (ServiceNow bridge, evidence spec, dbt hooks, SOX checklist)
2. Pre-launch content (8-week campaign, 500+ email subscribers)

**Launch Day (Week 1):**
1. README.md + QUICKSTART.md (data team traction)
2. Demo Script + Show HN Package (launch execution)

**Week 2-4:**
3. Content Calendar + Battlecards (GTM execution)
4. API Docs + Compliance Mapping (technical credibility)

**Week 5-8:**
5. SI Enablement + Badge Program (viral adoption)
6. Analytics + Customer Success (scale operations)

---

**End of Launch Docs v4.0**