# Clyra

**Data Change Control & Attestation for Modern Pipelines**

[![Clyra Certified](https://img.shields.io/badge/Clyra-SOX%20Compliant-green)](https://clyra.io/certified)

Clyra is an OSS data change control and attestation layer for modern data pipelines (data pipelines to AI agents, dbt/ETL, reverse-ETL, RPA, SaaS integrations, microservices).

**Strategic positioning:** Data-led, agent-ready. Lead with data platform enforcement where budget exists today, maintain same architecture for AI agents tomorrow.

## 🏆 Why Clyra?

- **ServiceNow/Jira Native**: Attested change tickets in your existing workflow
- **Start Safe**: Listen-only mode with zero pipeline changes
- **Get Certified**: SOX-compliant badges for your dbt projects
- **Two Products, One Platform**:
  - **Clyra Review**: Detection & attestation (start here)
  - **Clyra Gate**: Enforcement & prevention (upgrade when ready)

One control point, two guarantees:

- **Gateway** (SchemaLock + Data Firewall): Stops unsafe data changes and malformed outputs with GenAI-hardened enforcement, BEC defenses, and comprehensive audit trails
- **Recorder** (Flight Data Recorder): Proves and replays every change, producing tamper-evident evidence bundles (DEF v0 for data, PEF v0 for automation)

## 🚀 10-Minute PLG Path

**Data Platform Track (Primary):**
```bash
# 1. Listen-only start → zero disruption
clyra review init --dbt-cloud-webhook

# 2. First attested change ticket in ServiceNow
clyra review generate --servicenow

# 3. Get your SOX compliance badge
clyra certify --project my-dbt-project

# 4. Generate compliance report
clyra attest evidence.zip --framework sox

# 5. (Optional) Enable enforcement when ready
clyra gate enable --policy sox-controls.yaml
```

**Universal Track (Strategic):**
```bash
# 1. Install → local stack up
make quickstart

# 2. Demo → generate sample evidence
clyra demo contracts    # or: clyra demo etl

# 3. Bundle → independent verification
clyra verify evidence.zip --explain

# 4. Replay → deterministic scratch replay
clyra replay

# 5. Attest → signed attestation
clyra attest evidence.zip --framework pci

# 6. Daily Review → PCI Req-10 + GenAI threat posture
clyra report --daily-review
```

**Result**: Tamper-evident evidence bundle with signed attestation — ready for auditors, portable across platforms.

## 🎯 Key Differentiators

### **vs. Observability Tools (Datadog, Monte Carlo)**
- **Not just lineage, but proof**: Signed receipts vs. nice dashboards
- **Active enforcement**: Block unsafe changes vs. alert after the fact
- **Independence matters**: Platform-neutral evidence vs. vendor lock-in

### **vs. Database Governance (Snowflake, Databricks built-ins)**
- **Cross-platform**: Same evidence works across all your data stack
- **Enforcement-first**: Prevention, not just monitoring
- **Agent-ready**: Today's data controls become tomorrow's AI governance

## Key Features

### 📊 Data Platform Enforcement (New in v4.0)
- **dbt integration**: Hooks for evidence generation, CI gates for policy violations
- **Warehouse-native guards**: SQL safety macros, approval token validation
- **Activation gateway**: HTTP proxy for reverse-ETL with comprehensive enforcement
- **DEF v0 bundles**: Data Evidence Format with warehouse anchoring (QUERY_HISTORY, Delta commits, WAL LSN)
- **SOX ITGC compliance**: Change control, segregation of duties, signed attestations

### 🛡️ GenAI Security Hardening (Enhanced in v4.0)
- **Deepfake/BEC defenses**: 62% of orgs hit by deepfake attacks — comprehensive protection
- **Prompt injection detection**: Built-in heuristics with shadow-mode defaults
- **BEC-grade approval certificates**: SSO binding, challenge-response, payload hash binding
- **External detector integration**: Vendor-agnostic deepfake/safety signal APIs
- **Enhanced kill-switch**: Multi-trigger (data bursts, GenAI threats, error spikes)

### 🎙️ Voice/Conversation Compliance (New in v4.0)
- **TCPA compliance**: Disclaimer enforcement, consent tracking, opt-out mechanisms
- **Voice session correlation**: Link voice interactions to API actions in audit trails
- **UCaaS integration**: Teams, Slack, Zoom session correlation with metadata-only capture
- **Barge-in support**: Human interruption capability with <200ms response time

### 🔧 CI/CD + Code Change Control (New in v4.0)
- **GitHub Actions integration**: Evidence verification, policy gates, badge generation
- **Commit SHA binding**: Approval certificates tied to specific commits
- **SOX ITGC for code**: Change control, segregation of duties, deployment evidence
- **Deploy rate limiting**: Prevent runaway automation, enforce approval workflows

### 🔒 Enhanced Enforcement Primitives
- **Idempotency**: Prevent duplicate/retry operations with HMAC fingerprints
- **BEC-grade Approval Certificates**: Enhanced with SSO binding, challenge-response
- **Velocity Guards**: Sliding window rate limits and burst protection
- **Tenant Fences**: Cross-tenant isolation with DSN hash namespacing
- **SQL Safety**: Block mass UPDATE/DELETE without WHERE clauses
- **Prompt-loop breaker**: Cool-off policies for repetitive agent behaviors

### 📋 Multi-Framework Compliance
- **SOX ITGC**: Data change control, segregation of duties (NEW)
- **PCI/HIPAA**: Pass/fail attestations with enhanced daily reviews
- **EU AI Act/NIST**: Overlay mappings with governance metadata
- **TCPA**: Voice compliance and consent tracking (NEW)
- **Self-serve compliance**: Signed attestations in <30 min

## Architecture

**Data-Led Flow:**
```
[dbt Run] → [Hooks] → [DEF Bundle] → [SOX Attestation]
     ↓
[Schema Changes] → [Warehouse Guards] → [Approval Tokens] → [Audit Trail]
     ↓
[Activation Sync] → [Gateway Proxy] → [Enforcement] → [SaaS APIs]
```

**Universal Flow:**
```
[Agent/App] → [Gateway] → [Recorder] → [Postgres/Warehouse]
                   ↓
            [DEF/PEF Bundle]
                   ↓
        [Verifier / Auditor / SIEM]
```

### Core Components (Enhanced v4.0)

**Data Platform Components:**
- **dbt Integration**: Hooks, macros, CI gates with comprehensive metadata capture
- **Warehouse Anchors**: Native Snowflake/Databricks/Postgres integration with lineage tracking
- **Activation Gateway**: HTTP proxy for reverse-ETL with full enforcement primitive support
- **SQL Safety Guards**: Warehouse-native stored procedures and approval token validation

**Universal Foundation:**
- **Gateway**: Enhanced with GenAI threat detection, BEC defenses, voice session handling
- **Recorder**: Metadata-only snapshots with warehouse-specific anchoring mechanisms
- **Replay Engine**: Enhanced with data replay capabilities, deterministic schema recreation
- **Bundle Builder**: Unified DEF/PEF format with independent Go/TS verification
- **Verifiers**: Enhanced with data lineage validation, GenAI threat correlation

**GenAI Security Layer:**
- **Threat Detectors**: Built-in prompt injection, external deepfake APIs, BEC classification
- **Enhanced Approval System**: SSO binding, challenge-response, payload hash binding
- **Kill-Switch Evolution**: Multi-trigger system for data/GenAI/universal threat response
- **Voice Compliance**: Session management, disclaimer enforcement, UCaaS correlation

## Tech Stack (Updated v4.0)

- **Go** 1.25.x (CLI, Gateway, Recorder, Warehouse Guards)
- **Python** 3.13 (Enhanced SDK with dbt helpers via uv)
- **TypeScript** ~5.9 (Enhanced verifier, future SDK)
- **Node.js** 22.x LTS (CI/CD matrix includes 24.x)
- **Databases**:
  - **Postgres** 15/16 (fully supported), 13/14 (demo-only, best-effort)
  - **Snowflake** (QUERY_HISTORY anchoring, session tags)
  - **Databricks** (Delta Lake commits, Unity Catalog)
  - **BigQuery** (job metadata anchoring - Phase 1.5)
- **Schemas**: JSON Schema Draft 2020-12, RFC 8785 (JCS) for approval certs
- **15-Factor App**: API-first, comprehensive telemetry, enhanced authentication

## Repository Structure (Enhanced v4.0)

```
clyra/
├─ cmd/clyra/              # Enhanced CLI with data platform commands
├─ internal/
│  ├─ proxy/               # Gateway with GenAI security hardening
│  ├─ recorder/            # Enhanced with warehouse anchoring
│  ├─ warehouse/           # NEW: Native Snowflake/Databricks integration
│  ├─ dbt/                 # NEW: dbt hooks and macro implementations
│  ├─ activation/          # NEW: Reverse-ETL gateway proxy
│  ├─ genai/               # NEW: Security framework and threat detection
│  ├─ voice/               # NEW: Conversation compliance and correlation
│  ├─ cicd/                # NEW: GitHub Actions and deployment controls
│  ├─ bundle/              # Enhanced DEF/PEF unified builder
│  ├─ policy/              # Enhanced with data platform + GenAI sections
│  └─ crypto/              # Enhanced BEC-grade approval certificates
├─ verifier/               # Enhanced Go + TS verifiers (DEF/PEF support)
├─ sdk/
│  ├─ python/              # Enhanced with dbt helpers and data platform utils
│  └─ typescript/          # NEW: Future automation SDK
├─ spec/
│  ├─ def/                 # NEW: Data Evidence Format specifications
│  ├─ pef/                 # Enhanced Portable Evidence Format
│  ├─ policy/              # Enhanced unified policy schema
│  └─ compliance/          # Enhanced framework mappings
├─ packs/                  # Enhanced scenario + service packs
│  ├─ data/                # NEW: dbt, ETL, activation examples
│  ├─ contracts/           # Enhanced automation scenarios
│  └─ service/             # Enhanced retail/finserv/travel templates
├─ examples/
│  ├─ dbt-integration/     # NEW: dbt project templates
│  ├─ warehouse-guards/    # NEW: Native SQL safety implementations
│  └─ activation-flows/    # NEW: Reverse-ETL integration examples
├─ docs/                   # Enhanced with data platform and GenAI security
├─ kits/procurement/       # Enhanced with data platform materials
└─ .github/                # Enhanced CI/CD with multi-track testing
```

## Quick Start (Enhanced v4.0)

### Prerequisites

- Docker & Docker Compose
- Go 1.25.x
- Python 3.13 (via uv)
- Node.js 22.x LTS
- **Data Platform**: dbt-core 1.0+, Snowflake/Databricks account (optional)

### Data Platform Quick Start

```bash
# Clone and setup
git clone https://github.com/clyra-ai/clyra.git
cd clyra

# Initialize dbt project with Clyra integration
clyra dbt init my-project
cd my-project

# Install Clyra dbt package
echo 'packages:
  - git: "https://github.com/clyra-ai/dbt-clyra.git"
    revision: v4.0.0' > packages.yml
dbt deps

# Run with Clyra evidence generation
dbt run --vars '{clyra_enabled: true}'

# Generate data attestation
clyra attest evidence.zip --framework sox
```

### Universal Development

```bash
# Clone and setup
git clone https://github.com/clyra-ai/clyra.git
cd clyra

# Start enhanced local stack
make quickstart

# Run comprehensive test suite
make test

# Verify enhanced golden vectors (DEF + PEF)
make verify-vectors

# Generate sample attestations (all frameworks)
make attest-sample
```

## Key Commands (Enhanced v4.0)

### Data Platform Commands
```bash
# dbt project initialization with Clyra hooks
clyra dbt init [project-name]

# Warehouse connectivity and configuration checks
clyra warehouse doctor --platform snowflake|databricks

# Start activation gateway for reverse-ETL enforcement
clyra activation gateway --port 8080 --policy policy.yaml

# Generate data evidence from warehouse operations
clyra demo data --platform snowflake --tables 10
```

### Enhanced Universal Commands
```bash
# Initialize with enhanced policy templates
clyra init --template data|genai|universal

# Enhanced health checks (data + GenAI + universal)
clyra doctor --comprehensive

# Generate enhanced demo evidence
clyra demo contracts|etl|data --with-genai-threats

# Enhanced policy operations with data platform support
clyra policy wizard --track data|automation|voice
clyra policy lint --strict --frameworks sox,pci,hipaa
clyra policy test --golden-vectors --performance
```

### GenAI Security Commands
```bash
# Test GenAI threat detection against attack vectors
clyra genai test --attack-vectors prompt-injection,deepfake

# Validate BEC-grade approval certificates
clyra bec validate --certificate-path ./approvals/

# Analyze GenAI threat patterns in evidence
clyra threats analyze evidence.zip --output-format json
```

### Enhanced Evidence & Compliance
```bash
# Export with enhanced format support
clyra export --format ndjson|def|pef --platform snowflake

# Enhanced verification with data lineage
clyra verify evidence.zip --explain --validate-lineage

# Enhanced replay with data recreation capabilities
clyra replay --platform snowflake --scratch-schema clyra_replay

# Multi-framework attestation
clyra attest evidence.zip --framework sox|pci|hipaa|eu-ai-act|nist-rmf

# Enhanced daily review with GenAI threat posture
clyra report --daily-review --include-genai --include-data-changes
```

## 15-Factor App Compliance (New v4.0)

Clyra v4.0 implements modern cloud-native patterns:

- **Factor 13 - API First**: OpenAPI 3.0 specs, RESTful design, service interoperability
- **Factor 14 - Telemetry**: OpenTelemetry standard, business/security/performance metrics
- **Factor 15 - Authentication**: mTLS inter-service, HMAC requests, SSO integration
- **Infrastructure as Code**: Helm charts, Terraform modules, GitOps workflows
- **Immutable Infrastructure**: Non-root containers, signed artifacts, distroless images

## Governance Pillars (Enhanced v4.0)

Every evidence bundle embeds four enhanced governance pillars:

- **Reliability**: Fail-closed enforcement, deterministic replay, data platform SLAs
- **Transparency**: Tamper-evident bundles, independent verifiers, platform-neutral evidence
- **Accuracy**: Schema validation, canonical JSON, warehouse anchoring, GenAI threat classification
- **Oversight**: Enhanced HITL approvals, multi-framework compliance, comprehensive audit trails

## Performance SLAs (New v4.0)

**Data Platform:**
- dbt hook execution: <2s overhead per run
- Warehouse policy queries: <5s response time
- Activation gateway proxy: <15ms p95 latency
- Schema change validation: <1s per operation

**Universal Operations:**
- Gateway processing: ≤15ms p95 (+3ms with full enforcement)
- Recorder snapshots: ≤20ms p95 with metadata-only capture
- Evidence generation: <5s DEF, <3s PEF bundles
- Independent verification: <1s per bundle

**GenAI Security:**
- Prompt injection analysis: <100ms built-in detectors
- External deepfake APIs: <500ms with timeout/fallback
- BEC certificate validation: <10ms cryptographic verification
- Kill-switch response: <1s from trigger to action

## Differentiation Summary

### **Evidence vs. Observability**
While Monte Carlo tells you what probably changed, Clyra gives you **signed, tamper-proof receipts** with cryptographic integrity.

### **Prevention vs. Detection**
Think **seatbelt, not siren**. Block unsafe changes before they hit production vs. alerting after damage is done.

### **Independence Matters**
Snowflake can't credibly audit itself. Clyra provides **neutral, portable evidence** that survives platform changes and vendor relationships.

### **Ready for Agents**
Everyone else is building for today's pipelines. Clyra's architecture is **ready for tomorrow's GenAI agents** — same enforcement, same evidence format.

## Security

### Enhanced Security Model (v4.0)
- **Zero-trust architecture**: Every component authenticated, encrypted in transit
- **GenAI threat hardening**: Deepfake detection, BEC defenses, prompt injection protection
- **BEC-grade approval certificates**: SSO binding, challenge-response, payload hash binding
- **Multi-trigger kill-switch**: Data bursts, GenAI threats, error spikes with automated response

For security issues, see [SECURITY.md](SECURITY.md).

## License

Apache License 2.0 - see [LICENSE](LICENSE) for details.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for development setup and guidelines.

## Support

- **Community**: [GitHub Discussions](https://github.com/clyra-ai/clyra/discussions)
- **Documentation**: [docs.clyra.com](https://docs.clyra.com)
- **Enterprise**: [enterprise@clyra.com](mailto:enterprise@clyra.com)

---

## 🎖️ Clyra Certified Badge Program

Show your compliance status directly in your dbt project:

```yaml
# In your dbt_project.yml
clyra:
  certified: true
  badge_id: "proj-123-abc"
  last_attested: "2024-01-15T14:30:00Z"
```

```markdown
# In your README.md
[![Clyra Certified - SOX Compliant](https://clyra.io/badge/sox/proj-123)](https://clyra.io/verify/proj-123)
```

### Enterprise Integration Bridge

Export attested changes to your existing tools:

```bash
# ServiceNow integration
clyra export --servicenow --ticket-type change

# Jira integration
clyra export --jira --project DATAOPS
```

---

**Tagline v4.0**: Data Change Control & Attestation for Modern Pipelines

**Strategic positioning**: Data-led market entry, agent-ready architecture — from data pipelines today to AI agents tomorrow, with the same forensic foundation.