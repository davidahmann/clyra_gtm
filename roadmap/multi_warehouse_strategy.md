# Clyra Multi-Warehouse Strategy

**Last Updated:** 2025-01-31
**Status:** Active Hedge Strategy

---

## Executive Summary

**Primary Thesis:** dbt + SOX + Snowflake is the best first wedge for fast, budget-backed traction.

**Strategic Question:** Is this the only winning combo, or should we hedge?

**Answer:** It's the strongest lead, but not universally dominant. We need fast-follow support for BigQuery and Databricks to avoid losing hot leads and maximize market coverage.

---

## Why dbt + SOX + Snowflake is the Primary Wedge

### Budget & Urgency
- SOX sits with finance/audit and shows up in board timelines (quarter-end/IPO deadlines)
- **Immediate pain + budget authority** = fastest path to revenue
- Controllers have $50-200k discretionary budget for compliance tools

### Standardized Surface
- **dbt:** Uniform hooks/tests/exposures across all deployments
- **Snowflake:** Clean lineage anchors (QUERY_HISTORY, Access History)
- **Together:** Ship listen-only → attested ticket in days (not weeks)

### Complementary Positioning
- We're an **independent attestation/enforcement layer**
- We don't compete with dbt/Snowflake—we make their outputs audit-grade
- "Your dbt/Snowflake work, now provable to auditors"

### Market Evidence
- **Data platform stack share:**
  - Snowflake: ~40% of data warehouse market (pre-IPO/public companies)
  - dbt: ~70% of transformation tool market (where analytics engineering exists)
  - SOX: 100% of public companies + pre-IPO (12-18 months out)

---

## Where Other Warehouse Combos Win

### dbt + SOX + BigQuery 🟢 FAST-FOLLOW (High Priority)

**When it wins:**
- Google-first shops (adtech, media, consumer apps, gaming)
- Organizations with deep GCP commitment
- ML-heavy teams using Vertex AI + BigQuery together

**Market characteristics:**
- **Stack share:** ~30% of data warehouse market
- **Budget authority:** Same as Snowflake (finance/audit owns SOX)
- **Integration complexity:** Similar to Snowflake (Audit Logs vs. QUERY_HISTORY)
- **Time-to-value:** Nearly identical to Snowflake primary wedge

**Why this is strong:**
- BigQuery Audit Logs provide equivalent anchoring to Snowflake QUERY_HISTORY
- dbt works identically on both platforms
- SOX urgency is the same
- **Risk if we don't support:** Lose 30% of addressable market

**Fast-Follow Timeline:**
- **Month 3-6 post-MVP:** Add BigQuery anchoring
- **Engineering effort:** 2-3 weeks (reuse 90% of Snowflake logic)
- **Expected conversion:** Same as Snowflake (Review → Gate 30%)

---

### dbt + SOX + Databricks 🟡 COMPATIBLE (Medium Priority)

**When it wins:**
- ML/lakehouse-heavy enterprises
- Organizations with heavy Spark usage
- Data science-first culture (not analytics engineering-first)

**Market characteristics:**
- **Stack share:** ~20% of data warehouse/lakehouse market
- **Budget authority:** Mixed (data science + finance/audit)
- **Integration complexity:** Moderate (Delta commits + Unity Catalog)
- **Time-to-value:** Slower (governance story "owned" by platform)

**Why this is strategic but not urgent:**
- Databricks has stronger native governance story (Unity Catalog)
- Longer sales cycles (more platform overlap concerns)
- Still valuable market but requires more positioning work

**Compatible Timeline:**
- **Month 6-9 post-MVP:** Add Databricks Delta commit anchoring
- **Engineering effort:** 3-4 weeks (Unity Catalog lineage integration)
- **Expected conversion:** Lower initially (20-25% Review → Gate)

**Positioning strategy:**
- Lead with Review SKU (attested tickets) first
- Promise Gate enforcement later (after trust built)
- Emphasize **independent verification** (auditors don't trust vendor-only logs)

---

### Airflow/Dagster + SOX + Snowflake/BigQuery 🔵 FOLLOW-ON

**When it wins:**
- Orchestration-centric teams (data engineering > analytics engineering)
- Heterogeneous pipeline landscapes (not dbt-native)
- Custom transformation logic (Python > SQL)

**Market characteristics:**
- **Integration complexity:** Higher (less standardized surface)
- **Time-to-value:** Slower (heterogeneity creates edge cases)
- **Budget authority:** Data engineering (not finance/audit directly)

**Why this is follow-on, not primary:**
- Orchestration tools have wider variance in implementation
- Integration lift is heavier (custom hooks per workflow type)
- Slower time-to-value = harder to prove ROI quickly

**Timeline:**
- **Month 9-12 post-MVP:** Add Airflow/Dagster operators
- **Engineering effort:** 4-6 weeks (operator development + testing)
- **Use case:** Expansion within existing customers (land via dbt, expand to orchestration)

---

### Non-SOX Anchors (SOC2/ISO/HIPAA/PCI) 🟣 VERTICAL PACKS

**When they win:**
- Healthcare (HIPAA critical, SOX less relevant)
- Payment processors (PCI-DSS primary)
- SaaS vendors (SOC2 for customer trust)

**Market characteristics:**
- **Budget authority:** Security/IT (not finance/audit)
- **Procurement cycle:** Longer (security reviews + legal)
- **Urgency:** Lower (no board-driven deadlines like IPO)

**Why these are packs, not primary wedge:**
- Slower procurement cycles
- Budget sits with teams with longer evaluation processes
- SOX urgency creates faster path to initial revenue

**Timeline:**
- **Month 12-18:** Package compliance overlays
- **Positioning:** Upsell to existing SOX customers ("extend to HIPAA")
- **Revenue model:** Add-on packs ($5-10k/year per framework)

---

## Market Segmentation by Warehouse

### Snowflake (Primary - 40% market share)

**Ideal Customer Profile:**
- 200-2,000 employees
- Pre-IPO or recently public (SOX deadlines)
- Analytics engineering team using dbt
- Snowflake as primary data warehouse
- Finance/controller owns compliance budget

**Win Rate:** 60-70% (if we find the right buyer)

**Pricing:** Review $25-60k, Gate $75-150k

---

### BigQuery (Fast-Follow - 30% market share)

**Ideal Customer Profile:**
- 200-2,000 employees
- Google Cloud-first shops
- Pre-IPO or recently public
- dbt + BigQuery stack
- Similar compliance urgency as Snowflake

**Win Rate:** 55-65% (after BigQuery support ships)

**Pricing:** Same as Snowflake (no platform premium)

---

### Databricks (Compatible - 20% market share)

**Ideal Customer Profile:**
- 500-5,000 employees (larger, more mature)
- ML/data science-heavy culture
- Unity Catalog governance already in place
- Looking for **independent verification** layer
- Longer sales cycle (6-9 months vs. 3-6 months)

**Win Rate:** 40-50% (positioning as complementary, not competitive)

**Pricing:** May need discount for initial adoption (Review $20-50k)

---

### Postgres/Other (10% market share)

**Ideal Customer Profile:**
- Smaller teams (<200 employees)
- Budget constraints
- Self-hosted/OSS-first culture
- Pilot/POC opportunity

**Win Rate:** 30-40% (lower ACV, longer support burden)

**Pricing:** Community tier or small business discount

---

## Integration Complexity Matrix

| Warehouse | Anchor Mechanism | Engineering Effort | Code Reuse % | Time-to-Ship |
|-----------|------------------|-------------------|--------------|--------------|
| **Snowflake** | QUERY_HISTORY + session tags | Baseline | 100% | MVP (Done) |
| **BigQuery** | Audit Logs + job metadata | 2-3 weeks | 90% | Month 3-6 |
| **Databricks** | Delta commits + Unity Catalog | 3-4 weeks | 85% | Month 6-9 |
| **Postgres** | WAL LSN + audit triggers | 4-6 weeks | 70% | Month 9-12 |

---

## Decision Routing Questions

In discovery calls, ask these three questions **immediately:**

### 1. "Do you run dbt for financial/board-facing models?"
- **Yes + SOX urgency** → Primary wedge applies
- **Yes + no SOX** → Still valuable, longer cycle
- **No** → Orchestration follow-on (defer to later)

### 2. "What's your primary warehouse—Snowflake / BigQuery / Databricks?"
- **Snowflake** → MVP ready, full speed ahead
- **BigQuery** → Fast-follow (Month 3-6), can pre-sell
- **Databricks** → Compatible (Month 6-9), Review SKU first
- **Other** → Assess fit vs. engineering investment

### 3. "Are you public or pre-IPO? SOX timeline?"
- **Pre-IPO (12-18mo out)** → Highest urgency, budget unlocked
- **Recently public (first 2 years)** → Active SOX pain, proven budget
- **Mature public** → Existing process, harder to displace
- **Private, no IPO plans** → Lower priority (focus on others first)

---

## Revenue Impact by Warehouse Support

### Scenario: Year 1 (Snowflake Only)
- **Addressable market:** 40% of data warehouse market
- **Expected wins:** 10-15 customers
- **ARR:** $300k-$750k
- **Risk:** Lose 60% of qualified leads to "we use BigQuery/Databricks"

### Scenario: Year 1 (Snowflake + BigQuery)
- **Addressable market:** 70% of data warehouse market (+75% expansion)
- **Expected wins:** 18-25 customers
- **ARR:** $500k-$1.2M
- **Risk:** Lose 30% of qualified leads (Databricks-only shops)

### Scenario: Year 1 (Snowflake + BigQuery + Databricks)
- **Addressable market:** 90% of data warehouse market (+29% expansion)
- **Expected wins:** 25-35 customers
- **ARR:** $700k-$1.8M
- **Risk:** Minimal (covers all major platforms)

---

## Recommended Roadmap

### Phase 1: MVP (Month 0-3) - Snowflake Primary
- ✅ Ship dbt + SOX + Snowflake MVP
- ✅ Prove product-market fit with 3-5 customers
- ✅ Validate Review → Gate conversion (target 30%)

### Phase 2: Fast-Follow (Month 3-6) - BigQuery Parity
- ✅ Add BigQuery Audit Log anchoring
- ✅ Test with 2 design partners (Google-first shops)
- ✅ Target 5-8 BigQuery customers by Month 6

### Phase 3: Compatible (Month 6-9) - Databricks Entry
- ✅ Add Databricks Delta commit anchoring
- ✅ Test with 1-2 ML-heavy customers
- ✅ Positioning as "independent verification layer"

### Phase 4: Expansion (Month 9-12) - Orchestration Follow-On
- ✅ Airflow/Dagster operators for expansion
- ✅ Target upsell within existing customer base
- ✅ Custom transformation pipeline support

---

## Competitive Positioning by Warehouse

### vs. Snowflake Native Governance
- **Their story:** "We have audit logs and access history"
- **Our story:** "Independent verification—auditors don't trust vendor-only logs"
- **Key difference:** We're neutral; they can't audit themselves

### vs. Databricks Unity Catalog
- **Their story:** "We have built-in governance and lineage"
- **Our story:** "Complement Unity Catalog with independent attestation and enforcement"
- **Key difference:** We provide vendor-neutral evidence + progressive enforcement

### vs. BigQuery Audit Logs
- **Their story:** "Audit logs capture everything"
- **Our story:** "Turn logs into signed, portable evidence auditors can verify offline"
- **Key difference:** Logs ≠ evidence; we provide cryptographic proof

---

## Bottom Line

**Primary Bet:** dbt + SOX + Snowflake is the strongest lead for fast revenue and proven budget authority.

**Strategic Hedge:** Add BigQuery support by Month 6 (captures 70% of market vs. 40% Snowflake-only).

**Databricks Compatible:** Add by Month 9 as complementary positioning (captures 90% of market).

**Moat:** The real defensibility isn't the warehouse trio itself—it's our **independent, portable evidence + progressive enforcement** that rides on whichever warehouse the customer has today.

**Risk Mitigation:** Fast-follow approach prevents us from losing 60% of qualified leads while maintaining focus on the proven primary wedge.

---

## Success Metrics by Warehouse

### Snowflake (Primary)
- **Target:** 10-15 customers Year 1
- **Win rate:** 60-70%
- **Average ACV:** $40-80k (Review + Gate mix)

### BigQuery (Fast-Follow)
- **Target:** 5-8 customers Year 1 (post-Month 6)
- **Win rate:** 55-65%
- **Average ACV:** $35-75k (similar to Snowflake)

### Databricks (Compatible)
- **Target:** 2-4 customers Year 1 (post-Month 9)
- **Win rate:** 40-50%
- **Average ACV:** $30-60k (Review-first adoption)

### Total Year 1
- **Combined target:** 17-27 customers
- **Total ARR:** $600k-$1.5M
- **Market coverage:** 70-90% of data warehouse market

---

*For overall strategic context, see [strategic_roadmap.md](strategic_roadmap.md) and [README.md](README.md).*
