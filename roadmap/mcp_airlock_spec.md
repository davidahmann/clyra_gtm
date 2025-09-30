# Clyra MCP Airlock - Technical Specification

**Product Name:** Clyra Airlock (MCP Edition)
**Status:** Ready to Execute (Conditional - See Decision Framework)
**Last Updated:** 2025-01-31

---

## Decision Framework for Activation

**⚠️ This spec is ready to execute when strategic conditions are met.**

See [strategic_roadmap.md - Horizon 1B Decision Gate](strategic_roadmap.md#horizon-1b-agent-security-via-mcp-airlock-parallel-track---conditional) for full strategic context.

### Activate if ANY Condition Met:

1. ≥2 existing customers explicitly request MCP support
2. MCP GitHub stars >10k AND ≥3 major platforms integrated
3. ≥3 documented security incidents create CISO demand
4. Strategic category ownership opportunity (first mover advantage)
5. Competitive threat emerges (observability vendors adding agent security)

### Prerequisites Before Starting:

- ✅ Horizon 0 success criteria fully met ($300k+ ARR from data platform)
- ✅ Data platform thesis proven (3+ paying customers)
- ✅ Dedicated team available (2-3 engineers for 12 weeks)
- ✅ Design partners committed to pilot

### Defer If:

- ❌ Data platform thesis not yet proven
- ❌ Execution bandwidth constrained
- ❌ Market signals unclear
- ❌ Higher ROI opportunities exist

**Current Status:** Schema-only preparation complete (PEF v0 MCP extension in Horizon 0). Full implementation ready when conditions met.

---

## Product Overview

**One-liner:** An MCP-native security & connectivity gateway that gives agents just-in-time identity, policy-guarded access, and verifiable audit receipts—so they can cross org boundaries and "land safely," not just connect.

**The Model Context Protocol (MCP)** is the open protocol many apps now use to attach agents to tools/data—becoming the "USB-C for agents ↔️ tools."

⸻

P0 Outcomes (what the MVP must prove)

 1. Zero standing credentials for agents. All access is short-lived and scoped.
 2. Inline guardrails on MCP traffic. Allow/deny by server, tool, operation, and parameters; block exfil patterns; optional HITL approvals for high-risk writes.
 3. Cryptographic receipts. Every tool call produces a signed, hash-chained record you can verify offline.
 4. Cross-firewall connectivity without hassle. Secure reverse-tunnel / lightweight mesh so an MCP client can reach an MCP server behind someone else’s firewall.
 5. Supply-chain sanity. Only known, signed MCP servers run; prevent the “malicious server” class of incidents we’re already seeing.  ￼

⸻

Who uses it first
 • Platform/AI teams integrating MCP clients/servers.
 • Security/identity teams that own OAuth/OIDC and token policy.
 • Auditors/GRC who need provable evidence.

⸻

Architecture (MVP components)

1) Control Plane
 • Policy service (YAML): resources (MCP servers/tools), actions (read, write, mutate types), data classes, allowlists/denylists, rate/concurrency limits, approval routes, kill-switch TTL.
 • Identity broker (STS): Implements OAuth 2.0 Token Exchange (RFC 8693) so agents never hold long-lived creds; exchanges an agent’s auth for scoped, short-lived tokens to each resource.  ￼
 • Optional DPoP to sender-constrain tokens and reduce replay.  ￼
 • Dynamic Client Registration (RFC 7591/7592): auto-register agent “clients” with your IdP (Okta/Entra/Auth0) at runtime.  ￼
 • Key & signing service: rotates keys; signs evidence receipts; publishes public keys for verification.

2) Data Plane
 • MCP Gateway/Proxy: Terminates mTLS/DPoP, enforces policy, redacts/blocks sensitive payloads, shapes traffic, and injects ephemeral tokens per call.
 • Recorder: Emits canonical JSON receipts for every call: {who (agent+user), what (server/tool/op), when, where, inputs/outputs digests, policy decision, token scope, latency}. Hash-chained (Merkle root) and signed for tamper-evidence.
 • Connectivity edge: Agent/Server connect outwards to Airlock; Airlock stitches a reverse tunnel (WireGuard/WebSocket) so both sides work behind NAT without opening inbound ports.

3) Supply-Chain Guard
 • Signed server manifests: Only allow MCP servers from a signed allowlist; verify SBOM/provenance before activation. (Motivated by the malicious MCP server incident.)  ￼

⸻

Developer Experience
 • Sidecar / proxy: Drop a docker container or lightweight daemon next to an MCP client/server; point MCP to localhost:port.
 • CLI: airlock login, airlock allow <server> <tool>, airlock policy lint, airlock verify-receipt, airlock tunnel status.
 • SDK shims (TS, Python): Minimal wrappers for common MCP client/server libs; automatic header injection for DPoP and token refresh.
 • Verifier CLI: Offline verification of receipt chains for auditors.

⸻

MVP Scope — In
 • Protocol compatibility: MCP latest spec client↔️server pass-through with policy hooks.  ￼
 • IdP integrations (2 to start): Okta OIDC + Microsoft Entra (auth-code, device-code). Token Exchange (RFC 8693), DCR (RFC 7591/7592), optional DPoP.  ￼
 • Policy engine P0:
 • Match on {server, tool, operation, arg patterns, data class},
 • JIT approvals (Slack/Teams link) for “write/modify/financial” ops,
 • Kill-switch (deny-by-default for listed ops),
 • Egress controls (domains, MIME types), basic PII redaction patterns.
 • Evidence receipts: SHA-256 digests; per-session Merkle chain; signed (Ed25519). airlock verify to validate chain and signature.
 • Connectivity: Managed reverse tunnel (agent & server both outbound) + optional WireGuard peer; works across two firewalls without opening ports.
 • Starter allowlist catalog: Curated, signed manifests for 10 popular MCP servers (GitHub, Jira, Slack, Postgres, S3-ish, Email—read-only by default).

Out (for now)
 • Full anomaly detection/UEBA, AI-based DLP, fancy UI;
 • Broad IdP zoo;
 • Deep per-SaaS adapters (stick to MCP servers);
 • Multi-tenant SaaS at scale (start single-tenant cloud + easy self-host).

⸻

Threats we cover Day-1
 • Malicious/compromised MCP servers (allowlist + signing).  ￼
 • Prompt-injection induced bad writes (policy + HITL on mutating ops).
 • Credential sprawl & replay (STS token exchange + DPoP/mTLS).  ￼
 • Cross-firewall exposure (reverse tunnel, no inbound openings).
 • Audit gaps (tamper-evident receipts).

⸻

Reference Flows (MVP demos)

 1. Read-only research (safe path):
Claude/VSCode (MCP client) → Airlock Proxy → GitHub MCP (search/read only).

 • DCR registers the client; STS mints a read-scoped token; policy denies write ops; receipts emitted for each query.  ￼

 2. High-risk write with approval:
Agent tries finance.update_supplier_bank_account via ERP MCP server.

 • Policy marks as “sensitive-write”; requires manager HITL approval; STS issues a 1-minute, one-time token bound with DPoP; receipt stores approver principal and operation digest.  ￼

 3. Cross-org connection behind firewalls:
Vendor’s MCP server in a VPC; customer’s agent in another network.

 • Both dial out to Airlock; tunnel stitched; no inbound rules changed; policy & tokens enforced inline.

⸻

Success Metrics (first 60–90 days)
 • TTFSC (Time-to-first secure call): < 60 minutes from install to first approved MCP call.
 • Standing creds: 0 long-lived secrets in agent runtime.
 • Coverage: ≥ 90% of calls produce valid, verifiable receipts.
 • Adoption: 3 design-partners running 2+ real workflows each.
 • Kill-switch drills: 100% success (blocked within 5 seconds, receipts show denial).

⸻

Why now / proof points
 • MCP is rapidly becoming the standard “USB-C” for agents ↔️ tools.  ￼
 • We already have real supply-chain incidents (malicious MCP server stealing emails), which creates immediate CISO demand for an allowlist + signing + guardrail layer.  ￼
 • Reusing existing identity standards (OAuth DCR, Token Exchange, DPoP) lets us ship something credible fast without inventing a new auth scheme.  ￼

⸻

Build Plan (12 weeks, lean)

Weeks 1–2:
 • MCP proxy pass-through, policy matcher (deny/allow), receipts (signing), Okta OIDC auth-code; Token Exchange stub; CLI skeleton.

Weeks 3–5:
 • DCR with Okta/Entra; DPoP; reverse tunnel; starter allowlist/signing for 5–10 MCP servers.

Weeks 6–8:
 • HITL approvals (Slack/Teams link), rate/arg constraints, receipt verifier CLI, packager/helm for single-tenant cloud or self-host.

Weeks 9–12:
 • Hardening, docs, quickstarts; 3 design-partner integrations (GitHub read-only, Jira create-issue w/ approval, ERP write w/ approval).

⸻

Pricing & GTM (open-core)
 • OSS core: proxy + receipts + basic policy; single-user quickstarts (drives ecosystem trust).
 • Enterprise: IdP integrations, DCR/DPoP/STS, approvals, allowlist signing, auditor verifier, support/SLA.

⸻

If you want, I’ll adapt this to your Clyra/Guard AI stack: keep receipts compatible with your PEF bundles and slide the identity broker next to your “just-in-time” gateway—so you can own this meta-MCP category with minimal net new.

# Clyra Airlock for MCP - Strategic Roadmap

**Product Name**: Clyra Airlock (MCP Edition)  
**One-Liner**: MCP-native security & connectivity gateway providing just-in-time identity, policy-guarded access, and verifiable audit receipts for agents crossing organizational boundaries.  
**Strategic Fit**: Agent-facing sibling of Clyra's data-facing gateway; 70-80% code reuse; same policy → enforce → record → attest → verify loop.

---

## Executive Summary

### What is "Airlock for MCP"?

An MCP-native extension of Clyra that applies the same enforcement and attestation architecture to AI agents using the Model Context Protocol. Think of it as the **agent analogue of the data platform wedge**: same value proposition (prevention + portable proof), same GTM (Review → Gate), same auditor acceptance path.

**The Model Context Protocol (MCP)** is an open protocol that extends AI agents with custom tools and data sources through standardized interfaces — essentially acting as plugins for agents. Anthropic, OpenAI, and other major AI companies are adopting MCP as the "USB-C for agents ↔️ tools."

### Strategic Positioning

- **Data-led market entry TODAY**: Focus on dbt, warehouses, reverse-ETL where budget exists and compliance deadlines are real.
- **Agent-ready architecture TOMORROW**: Same enforcement engine, same evidence format (PEF v0 with MCP extensions), same independent verification.
- **Natural progression**: Customers who adopt Clyra for data platform compliance get agent security "for free" when they're ready.

### Why This Matters Now

1. **MCP is becoming the standard**: Rapidly adopted by major AI platforms as the unified protocol for agent-to-tool communication.
2. **Real supply-chain incidents**: Malicious MCP servers stealing emails, credential leakage — creating immediate CISO demand for allowlists, signing, and guardrails.
3. **Standards reuse**: OAuth DCR, Token Exchange (RFC 8693), DPoP — we're not inventing new auth; we're applying proven standards to MCP.
4. **Market timing**: Gap between MCP adoption and security solutions creates category-defining opportunity.

---

## How MCP Airlock Fits Clyra Architecture

### Perfect Architectural Alignment (70-80% Reuse)

| Clyra Component | MCP Airlock Adaptation | Reuse % |
|-----------------|------------------------|---------|
| **Policy Engine** | Add MCP resource model (server/tool/operation/args); same YAML structure | 90% |
| **Gateway (SchemaLock)** | Swap HTTP JSON validation for MCP request/response validation | 80% |
| **Recorder (FDR)** | Extend PEF v0 with MCP-specific fields; same Merkle chain logic | 85% |
| **Attestation/Verifiers** | No changes needed — same Go/TS verifiers work for MCP receipts | 100% |
| **GenAI Hardening** | Apply prompt injection heuristics to MCP tool calls; same HITL approvals | 90% |
| **Compliance Engine** | Same SOX/PCI/HIPAA/EU AI Act attestations | 100% |

### What's Net-New (Only 20-30% New Code)

1. **Identity Broker (STS)**: OAuth 2.0 Token Exchange (RFC 8693) to mint short-lived, scoped tokens per MCP call.
2. **Dynamic Client Registration (DCR)**: RFC 7591/7592 auto-registration with Okta/Entra.
3. **Connectivity Edge**: Reverse tunnel (WebSocket first, WireGuard later) so client↔️server work behind firewalls.
4. **Supply-Chain Allowlist**: Signed manifests of approved MCP servers; verify provenance before activation.
5. **MCP Protocol Adapter**: Request/response canonicalization, MCP-specific validation hooks.

### PEF v0 Extension for MCP (Schema-Only, Horizon 0)

Add optional MCP fields to PEF v0 format (backward compatible):

```json
{
  "schema_version": "pef/v0",
  "mcp_extension": {
    "server_id": "github.com/mcp-server",
    "tool": "create_issue",
    "operation": "write",
    "params_hash": "sha256:abc123...",
    "result_hash": "sha256:def456...",
    "token_scope": "repo:write issues:create",
    "dpop_jkt": "sha256:key-thumbprint",
    "approval_principal": "jane.doe@company.com",
    "mcp_session_id": "uuid-v4"
  }
}
```

**Implementation**: Extend `/spec/pef/schemas/pef_v0.schema.json` with optional `mcp_extension` object. No enforcement logic — schema-only preparation for Horizon 1.

---

## Phased Roadmap

### Horizon 0 (NOW - Within MVP v4.0)

**Goal**: Lay architectural foundations without building MCP-specific enforcement.

**What Ships**:

- ✅ **Story 1.8**: PEF v0 schema extended with optional MCP fields (2-3 days)
- ✅ `/docs/mcp/ROADMAP.md`: Strategic vision documented
- ✅ `/docs/mcp/mcp_pef_extension.md`: Technical spec for MCP fields
- ✅ WARP.md Phase 1.5 section updated with MCP Airlock plan

**What We're NOT Building**:

- ❌ No MCP proxy
- ❌ No identity broker (STS/DCR)
- ❌ No connectivity edge
- ❌ No enforcement logic

**Success Criteria**:

- PEF schema validates with and without MCP fields
- Verifiers ignore unknown fields gracefully
- Roadmap documented for future reference

**Rationale**: Minimal disruption to data-led MVP while maintaining strategic optionality. If customer demand materializes earlier than expected, we're ready to accelerate.

---

### Horizon 1 (3-6 Months Post-MVP) - Airlock Review (MCP)

**Goal**: Listen-only MCP monitoring with receipts and policy dry-run.

**Prerequisites (Must Be Met Before Starting)**:

- ✅ 3 paying data platform customers
- ✅ 1 auditor acknowledged DEF/PEF formats
- ✅ ServiceNow integration proven in production
- ✅ $300k+ ARR from data wedge

**What Ships**:

#### Week 1-2: Core MCP Proxy + Receipts

- **MCP pass-through proxy**: Transparent relay with request/response canonicalization
- **Policy matcher (dry-run)**: Evaluate policies, log verdicts, no enforcement
- **Signed receipts**: PEF v0 bundles with MCP extension fields
- **Okta OIDC integration**: Authorization code flow with token refresh
- **CLI skeleton**: `clyra airlock login`, `clyra airlock verify`

#### Week 3-5: Identity + Connectivity

- **Token Exchange (RFC 8693)**: Short-lived, scoped tokens per MCP call
- **DPoP support**: Sender-constrained tokens to prevent replay
- **Reverse tunnel (WebSocket)**: Client/server both dial out to Airlock
- **Starter allowlist**: Signed manifests for 5-10 popular MCP servers (GitHub, Jira, Slack, Postgres, S3, Email — read-only by default)
- **CLI enhancement**: `clyra airlock allow <server> <tool>`, `clyra airlock tunnel status`

#### Week 6-8: HITL + Export

- **HITL approvals**: Slack/Teams link for write operations
- **Arg/regex guards**: Pattern matching on MCP operation arguments
- **ServiceNow/Jira export**: "Attested Agent Action" tickets
- **Enhanced receipts**: Include approval principal, policy evaluation results
- **CLI completion**: `clyra airlock policy lint`, `clyra airlock threats analyze`

#### Week 9-12: Microsoft Entra + Hardening

- **Entra OIDC parity**: Same auth flows as Okta
- **Security hardening**: Secret rotation, connection pooling, rate limiting
- **Documentation**: Quickstart guides, IdP setup, policy examples
- **Design partner integrations**: 2 workflows (GitHub read-only, Jira create-issue with HITL)

**Key Deliverables**:

- `/internal/mcp/`: Proxy, policy adapter, canonicalization
- `/internal/identity/`: STS, DPoP, OIDC adapters (Okta + Entra)
- `/internal/connect/`: WebSocket relay
- `/cmd/clyra/airlock/`: All subcommands
- `/examples/mcp-quickstart/`: GitHub + Jira demos
- `/docs/mcp/quickstart.md`, `/docs/mcp/policy-examples.md`, `/docs/mcp/idp-setup.md`

**Acceptance Criteria**:

- ✅ TTFSC (Time-to-First Secure Call) < 60 minutes
- ✅ Standing creds: 0 long-lived secrets in agent runtime
- ✅ Coverage: ≥90% of calls produce valid, verifiable receipts
- ✅ Adoption: 2+ design-partners running real workflows
- ✅ ServiceNow export: Attested Agent Action tickets created

**Pricing/GTM**:

- **Airlock Review (MCP)**: Listen-only mode, receipts, policy dry-run
- Same pricing model as Clyra Review for data platform
- Early adopter discount for existing Clyra customers

---

### Horizon 2 (6-12 Months) - Airlock Gate (MCP)

**Goal**: Full enforcement with allow/deny/HITL, STS token exchange, signed allowlists.

**Prerequisites**:

- ✅ 1+ customer requests MCP enforcement (not just monitoring)
- ✅ Airlock Review proven with agents (receipts validated in production)
- ✅ Signed allowlist catalog covers 15+ MCP servers

**What Ships**:

#### Enforcement Activation

- **Allow/deny/HITL enforcement**: Policy-driven blocking of MCP operations
- **STS token exchange**: Full OAuth 2.0 Token Exchange implementation
- **DPoP hardening**: Mandatory sender-constrained tokens for write operations
- **Signed allowlist enforcement**: Only approved MCP servers can connect
- **Rate & arg constraints**: Per-tool rate limits, argument pattern validation
- **Enhanced kill-switch**: Multi-trigger (MCP-specific + inherited from core Clyra)

#### Advanced Policy Controls

```yaml
# Policy.yaml extension for MCP enforcement
mcp_enforcement:
  servers:
    - server_id: "github.com/mcp-server"
      allow: true
      tools:
        - tool: "create_issue"
          operation: "write"
          require_hitl: true
          rate_limit: {window: 300s, max: 10}
          arg_patterns:
            - field: "title"
              regex: "^[A-Za-z0-9 .-]+$"  # No special chars
        - tool: "search_code"
          operation: "read"
          require_hitl: false
```

#### Outcome Ledger Integration

- **Attribution Certificates**: Link MCP receipts to agent work outcomes
- **Payout candidates**: Export agent actions for results-based billing
- **Agent work metering**: Track agent-initiated operations for usage-based pricing

**Key Deliverables**:

- `/internal/mcp/enforcement.go`: Policy enforcement engine
- `/internal/mcp/allowlist.go`: Signed manifest verification
- `/internal/attribution/`: Outcome Ledger integration (stub for Horizon 3)
- Enhanced policy templates with MCP examples
- Production-ready deployment manifests (Helm charts, Docker Compose)

**Acceptance Criteria**:

- ✅ Policy enforcement <10ms latency overhead
- ✅ Kill-switch drills: 100% success (blocked within 5s)
- ✅ Signed allowlist prevents malicious servers
- ✅ 3+ customers paying for Airlock Gate (MCP)

**Pricing/GTM**:

- **Airlock Gate (MCP)**: Full enforcement, STS, signed allowlists, HITL
- Premium tier over Airlock Review (MCP)
- Enterprise features: Custom allowlists, advanced policy controls, SLA support

---

### Horizon 3 (12-18 Months) - Attribution & Results-Based Billing

**Goal**: Tie MCP receipts into results-based payout system.

**What Ships**:

- **Outcome Ledger**: Agent runs produce Attribution Certificates
- **Payout line items**: Map agent actions to business outcomes (e.g., "closed 3 tickets")
- **Trust spine**: Airlock receipts = ground truth of agent work for billing
- **Finance Pack integration**: `agent_id|run_id → metric_ref → suggested_value` exports
- **Auditor acceptance**: Attribution Certificates accepted by auditors for SOX compliance

**Acceptance Criteria**:

- ✅ Attribution Certificates generated for all agent work
- ✅ Payout candidates exported to finance systems
- ✅ 1+ customer using results-based billing with agents
- ✅ Auditor accepts Attribution Certificates in SOX audit

---

## Reference Flows (MVP Demos)

### Flow 1: Read-Only Research (Safe Path)

**Scenario**: Claude/VSCode (MCP client) → Airlock Proxy → GitHub MCP (search/read only)

1. Developer launches agent in VSCode with MCP client
2. Agent requests GitHub MCP server access
3. **Airlock intercepts**: DCR registers client with Okta, STS mints read-scoped token
4. **Policy evaluation (dry-run)**: Allow read operations, deny write operations
5. Agent searches GitHub code, reads issues
6. **Airlock records**: Signed receipts for each query with MCP extension fields
7. **Export**: Daily review includes MCP activity summary

**Value**: Zero standing credentials, full audit trail, no enforcement disruption.

---

### Flow 2: High-Risk Write with Approval

**Scenario**: Agent tries `finance.update_supplier_bank_account` via ERP MCP server

1. Agent initiates bank account update via MCP tool call
2. **Airlock intercepts**: Policy marks as "sensitive-write"
3. **HITL required**: Sends Slack message to manager: "Agent X wants to update Supplier Y bank account. Approve?"
4. Manager reviews context, clicks "Approve"
5. **STS issues token**: 1-minute, one-time token bound with DPoP
6. Agent executes update with scoped token
7. **Receipt stores**: Approver principal (`manager@company.com`), operation digest, approval timestamp
8. **ServiceNow export**: Attested Agent Action ticket created

**Value**: Prevents rogue agent actions, creates audit trail for finance compliance.

---

### Flow 3: Cross-Org Connection Behind Firewalls

**Scenario**: Vendor's MCP server in VPC, customer's agent in another network

1. Vendor deploys MCP server in VPC (no inbound ports open)
2. Customer runs agent in corporate network (strict egress rules)
3. **Both dial out to Airlock**: WebSocket connections to Airlock relay
4. **Airlock stitches tunnel**: Transparent bidirectional relay
5. **Policy enforced inline**: All MCP operations go through Airlock proxy
6. **Tokens issued per call**: No standing credentials, scoped access
7. **Receipts capture both sides**: Vendor and customer both get signed audit trail

**Value**: Zero firewall changes, secure cross-org agent collaboration, complete audit trail.

---

## Threats Addressed (Day-1)

| Threat | MCP Airlock Mitigation | Industry Reference |
|--------|------------------------|-------------------|
| **Malicious/Compromised MCP Servers** | Signed allowlist + provenance verification | [Real incident: Malicious MCP server stealing emails](https://modelcontextprotocol.io/security) |
| **Prompt Injection Induced Bad Writes** | Policy evaluation + HITL on mutating ops | OWASP LLM01 |
| **Credential Sprawl & Replay** | STS Token Exchange + DPoP/mTLS | RFC 8693, RFC 9449 |
| **Cross-Firewall Exposure** | Reverse tunnel, no inbound openings | Zero Trust architecture |
| **Audit Gaps** | Tamper-evident receipts with independent verification | SOX ITGC, PCI DSS Req-10 |

---

## Repository Impact (Minimal, Surgical)

### Horizon 0 (NOW)

```
/spec/pef/schemas/pef_v0_mcp_extension.json  (NEW)
/docs/mcp/ROADMAP.md  (NEW - this file)
/docs/mcp/mcp_pef_extension.md  (NEW)
/WARP.md  (UPDATED - Phase 1.5 section)
```

### Horizon 1 (3-6mo Post-MVP)

```
/internal/mcp/
  ├── proxy.go                # MCP pass-through proxy
  ├── policy_adapter.go       # Policy matcher for MCP resources
  ├── canonicalization.go     # MCP request/response normalization
  └── receipts.go             # PEF v0 bundle generation with MCP fields

/internal/identity/
  ├── sts/
  │   ├── token_exchange.go   # RFC 8693 implementation
  │   └── dpop.go             # RFC 9449 DPoP support
  └── oidc/
      ├── okta.go             # Okta integration
      └── entra.go            # Microsoft Entra integration

/internal/connect/
  ├── relay.go                # WebSocket relay
  └── tunnel.go               # Tunnel management

/cmd/clyra/airlock/
  ├── login.go                # Authentication commands
  ├── allow.go                # Allowlist management
  ├── verify.go               # Receipt verification
  └── tunnel.go               # Tunnel control

/spec/pef/test-vectors/mcp/  # MCP-specific golden vectors

/examples/mcp-quickstart/
  ├── github-readonly/        # GitHub MCP demo
  └── jira-hitl/              # Jira with HITL approval

/docs/mcp/
  ├── quickstart.md           # Getting started guide
  ├── policy-examples.md      # MCP policy configurations
  └── idp-setup.md            # Okta/Entra setup instructions
```

---

## Risks & Mitigations

| Risk | Impact | Mitigation |
|------|--------|-----------|
| **MCP spec evolves rapidly** | Medium | Keep proxy pluggable; version receipts; gate new ops behind feature flags |
| **Becomes a VPN product** | High | Limit connectivity to MCP-only relay; no general L3; clear positioning |
| **IdP integration complexity** | Medium | Start with Okta + Entra only; ship adapters later based on demand |
| **PII in receipts** | High | Store hashes/digests only; no raw payloads (existing Clyra policy) |
| **Customer demand misjudged** | Low | Horizon 0 prep = minimal investment; can accelerate or defer based on signals |
| **Execution bandwidth** | High | Horizon 1 requires dedicated team; don't start until MVP v4.0 is stable |

---

## Success Metrics (Horizon 1)

### Technical Metrics

- **TTFSC (Time-to-First Secure Call)**: < 60 minutes from install to first approved MCP call
- **Standing creds**: 0 long-lived secrets in agent runtime
- **Coverage**: ≥90% of calls produce valid, verifiable receipts
- **Performance**: <10ms proxy latency overhead (excluding MCP server response time)

### Business Metrics

- **Adoption**: 3 design-partners running 2+ real workflows each
- **Conversion**: ≥50% of Airlock Review (MCP) users request Gate features within 90 days
- **Revenue**: $100-200k ARR from MCP-specific deployments (incremental to data platform)

### Strategic Metrics

- **Kill-switch drills**: 100% success (blocked within 5 seconds, receipts show denial)
- **Auditor acceptance**: ≥1 auditor acknowledges MCP receipts as valid evidence
- **Community adoption**: ≥10 GitHub stars/week for MCP-related repos

---

## Why This is Worth It

1. **Agent analogue of data wedge**: Same value story (prevention + portable proof), same GTM (Review → Gate), same auditor acceptance path.
2. **Seeds attribution → results-based payouts**: Airlock receipts = ground truth of agent work for future billing models.
3. **"USB-C for agents" security story**: Customers can adopt today without ripping anything out; modular MCP integration.
4. **Category-defining opportunity**: Gap between MCP adoption and security solutions; we can own this with proven architecture.
5. **Natural upsell for data platform customers**: "You're already using Clyra for dbt — extend the same controls to your agents."
