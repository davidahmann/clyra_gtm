# Clyra v4.0 Epic Plan - Data-Led, Agent-Ready Architecture

**Strategic Positioning**: Data-led market entry (dbt, warehouses, reverse-ETL) with agent-ready architecture for future AI governance

**Execution Order**: Dependencies drive logical sequencing - each epic builds on foundations from previous epics

---

## Epic 0: Foundational Infrastructure & Tooling

**Goal**: Establish monorepo structure, CI/CD automation, security scanning, and 15-Factor compliance foundations

### Story 0.1: Repository Scaffold & OSS Hygiene

**Description**: Create monorepo skeleton with all OSS/meta files and top-level directories
**Technical Implementation**:

- Root documentation files (README.md, LICENSE, CODE_OF_CONDUCT.md, CONTRIBUTING.md, SECURITY.md)
- Directory structure per v4.0 architecture
- CODEOWNERS with security-critical paths
**Repository Paths**: `/`, `/cmd/`, `/internal/`, `/sdk/`, `/verifier/`, `/spec/`, `/packs/`, `/examples/`, `/docs/`, `/kits/`, `/.github/`
**Dependencies**: None (foundation)
**Acceptance Criteria**:
- All OSS headers present
- Directory structure matches v4.0 scaffold
- CODEOWNERS gates sensitive paths requiring security approval

### Story 0.2: Development Environment & Build Tooling

**Description**: Establish Warp-first dev setup with comprehensive Make targets
**Technical Implementation**:

- Makefile with quickstart, test, verify-vectors, attest-sample, lint targets
- Docker Compose configurations for local development
- Warp workflows for developer productivity
**Repository Paths**: `/Makefile`, `/.warp/workflows.yaml`, `/examples/quickstart-compose/`, `/docs/dev_setup_*.md`
**Dependencies**: Story 0.1
**Acceptance Criteria**:
- `make quickstart` boots full stack <10 min
- `make quickstart-data` boots data platform stack
- All Make targets functional

### Story 0.3: Language Workspaces & Toolchains

**Description**: Configure Go, Python, and TypeScript workspaces with proper versioning
**Technical Implementation**:

- Go 1.25.x workspace with go.mod and go.work
- Python 3.13 via uv with pyproject.toml
- Node.js 22.x with npm workspace for TypeScript
**Repository Paths**: `/go.mod`, `/go.work`, `/package.json`, `/sdk/python/pyproject.toml`, `/verifier/ts/package.json`
**Dependencies**: Story 0.1
**Acceptance Criteria**:
- `go work sync` clean
- `uv run pytest` passes
- `npm -w verifier/ts test` passes

### Story 0.4: CI/CD Pipeline Foundation

**Description**: Path-filtered CI/CD with language-specific workflows
**Technical Implementation**:

- GitHub Actions with path filtering
- Release automation (release-please, GoReleaser)
- Publishing workflows for Python/npm packages
**Repository Paths**: `/.github/workflows/`, `/release-please-config.json`, `/goreleaser.yaml`
**Dependencies**: Story 0.3
**Acceptance Criteria**:
- Path-filtered CI triggers correctly
- Release automation functional
- Publish workflows ready

### Story 0.5: Security & Supply Chain Hardening

**Description**: Implement SBOM, vulnerability scanning, and signing infrastructure
**Technical Implementation**:

- SBOM generation with Syft
- Vulnerability scanning with Grype
- Artifact signing with cosign
- SLSA provenance generation
**Repository Paths**: `/.github/workflows/security/`, `/.cosign.pub`, `/.github/SECURITY_EXCEPTIONS.md`
**Dependencies**: Story 0.4
**Acceptance Criteria**:
- SBOM attached to releases
- Grype fails on critical vulnerabilities
- Artifacts signed with verifiable signatures

### Story 0.6: Architecture Documentation & ADRs (Completed)

**Description**: Base architecture documentation and ADR framework
**Technical Implementation**: Already completed per epic0_tasks.md
**Repository Paths**: `/docs/arch/`, `/docs/adr/`
**Dependencies**: Story 0.1
**Acceptance Criteria**: ✅ Already implemented

### Story 0.7: 15-Factor App Compliance Infrastructure

**Description**: Implement API-first design, comprehensive telemetry, and enhanced authentication
**Technical Implementation**:

- OpenAPI 3.0 specifications for all services
- OpenTelemetry integration with comprehensive metrics:
  - Business metrics: request rates, feature usage, customer actions
  - Security metrics: threat detections, authentication failures, policy violations
  - Performance metrics: latency percentiles, throughput, resource utilization
- mTLS inter-service communication
- HMAC request authentication
**Repository Paths**: `/internal/telemetry/`, `/internal/api/openapi/`, `/internal/auth/`, `/spec/api/`
**Dependencies**: Story 0.3
**Acceptance Criteria**:
- All services expose OpenAPI specs
- Business, security, and performance metrics collected
- Telemetry pipeline operational with OpenTelemetry
- Authentication framework functional

### Story 0.8: Database Compatibility Matrix & Testing

**Description**: Establish database support matrix and compatibility testing
**Technical Implementation**:

- Postgres 15/16 full support validation
- Postgres 13/14 best-effort documentation
- Cloud provider variant testing
**Repository Paths**: `/docs/compatibility/`, `/test/compatibility/`, `/internal/database/`
**Dependencies**: Story 0.3
**Acceptance Criteria**:
- Compatibility matrix documented
- Version detection in doctor command
- Cloud variant testing passes

### Story 0.9: CI/CD Workflow Completeness & Test Matrix

**Description**: Comprehensive CI/CD workflows with security scanning and test organization
**Technical Implementation**:

- Core CI workflows: ci.yml with Semgrep, Gitleaks, ZAP Baseline
- Nightly audit: k6 perf, ZAP Full, CodeQL, SBOM+Grype, OSV, Scorecard
- Specialized workflows: traceability.yml, policy-contract.yml, perf-budgets.yml
- Test matrix organization:
  - Integration tests: `/test/integration/{gateway_validator,canonical_merkle_parity,schema_matrix,externalization_roundtrip,recorder_flow}`
  - E2E tests: `/test/e2e/{verify_bundle,negative_vectors,determinism,recorder_contracts,recorder_etl,recorder_retail}`
  - Fuzz tests: `/test/fuzz/{canonicalization_fuzz_test.go,schema_negative/*}`
  - Performance tests: `/test/perf/k6_scenarios.js`
- Automated processes: procurement-kit-smoke.yml, key-rotation-reminder.yml, verifier-badge.yml
**Repository Paths**: `/.github/workflows/`, `/test/`, `/.github/actions/`
**Dependencies**: Story 0.4, Story 0.5
**Acceptance Criteria**:
- All CI workflows operational
- Test matrix organized by type
- Security scans (Semgrep, Gitleaks) integrated
- Key rotation reminders automated (180d)
- Traceability gates enforced

### Story 0.10: Operational Tooling & OSS Best Practices

**Description**: Development tooling, security guidelines, and OSS community features
**Technical Implementation**:

- License scanning: `/scripts/check_licenses.sh` for dependency license compliance
- Issue/PR templates: `/.github/ISSUE_TEMPLATE/`, `/.github/PULL_REQUEST_TEMPLATE.md`
- Container security: Non-root image guidance in `/docs/security.md`
- Egress control examples: `/examples/egress/{iptables_sidecar.md,envoy_filter.md,istio_policies.yaml}`
- PR review automation: `/internal/pr-agent/client.go` for automated PR analysis
- Performance calculation: `/scripts/calc_perf.py` for weekly performance curves
- Triage labels: `/docs/labels.md` for issue categorization
- Conformance guide: `/docs/conformance.md`, `/docs/implementers_guide.md`
**Repository Paths**: `/scripts/`, `/.github/`, `/docs/`, `/examples/egress/`, `/internal/pr-agent/`
**Dependencies**: Story 0.1
**Acceptance Criteria**:
- License violations blocked in CI
- PR/Issue templates active
- Container security documented
- Egress examples functional
- PR agent provides feedback
- Performance trends tracked

---

## Epic 1: Core Evidence Formats & Cryptographic Foundation

**Goal**: Establish DEF v0 (Data Evidence Format) and PEF v0 (Portable Evidence Format) with cryptographic integrity

### Story 1.1: Evidence Format Specifications

**Description**: Define DEF v0 and PEF v0 specifications with schemas
**Technical Implementation**:

- JSON Schema Draft 2020-12 compliant schemas
- Canonical JSON normalization (RFC 8785)
- Versioning strategy documentation
**Repository Paths**: `/spec/def/`, `/spec/pef/`, `/spec/common/`
**Dependencies**: Epic 0
**Acceptance Criteria**:
- DEF/PEF schemas validate with ajv
- Versioning strategy documented
- Common structures shared

### Story 1.2: Cryptographic Infrastructure

**Description**: Implement signature algorithms, key management, and hash chaining
**Technical Implementation**:

- Ed25519 primary, ECDSA/RSA support
- KMS integration (AWS, Azure, HashiCorp)
- Per-run hash chains for integrity
**Repository Paths**: `/internal/crypto/`, `/internal/crypto/kms/`
**Dependencies**: Story 1.1
**Acceptance Criteria**:
- Multi-algorithm support functional
- KMS integration operational
- Hash chains prevent tampering

### Story 1.3: Canonicalization & Merkle Trees

**Description**: Implement deterministic JSON canonicalization and Merkle tree generation
**Technical Implementation**:

- RFC 8785 JSON Canonicalization Scheme
- Merkle tree root calculation
- External artifact handling
**Repository Paths**: `/internal/bundle/canonical.go`, `/internal/bundle/merkle.go`, `/internal/bundle/externalization.go`
**Dependencies**: Story 1.1
**Acceptance Criteria**:
- Identical input produces identical bytes
- Merkle root stable across platforms
- Large artifacts externalized correctly

### Story 1.4: Bundle Builder Infrastructure

**Description**: Create unified DEF/PEF bundle builder with governance metadata
**Technical Implementation**:

- Manifest generation with metadata
- Journal event streaming
- Artifact packaging
**Repository Paths**: `/internal/bundle/`, `/internal/bundle/def_builder.go`, `/internal/bundle/pef_builder.go`
**Dependencies**: Story 1.3
**Acceptance Criteria**:
- DEF bundles include warehouse anchors
- PEF bundles include automation evidence
- Governance metadata embedded

### Story 1.5: Golden Test Vectors

**Description**: Create comprehensive test vectors for format validation
**Technical Implementation**:

- Valid vectors for success cases
- Forged vectors for security testing
- Negative vectors for error handling
**Repository Paths**: `/spec/def/test-vectors/`, `/spec/pef/test-vectors/`, `/test/golden_vectors/`
**Dependencies**: Story 1.4
**Acceptance Criteria**:
- Vectors cover all scenarios
- Cross-platform consistency
- Immutable after publish

### Story 1.6: Performance Metrics Embedding in Bundles

**Description**: Embed comprehensive performance and security metrics in evidence bundles
**Technical Implementation**:

- Gateway latency percentiles (p50, p95, p99)
- Recorder snapshot timing and lag metrics
- Data platform metrics: dbt run duration, warehouse query times
- GenAI security metrics: threat detection latency, false positive rates
- Bundle generation timing and size metrics
**Repository Paths**: `/internal/bundle/performance_metrics.go`, `/internal/bundle/governance_metadata.go`
**Dependencies**: Story 1.4
**Acceptance Criteria**:
- All performance metrics captured
- Metrics embedded in both DEF and PEF formats
- Governance metadata includes performance SLA compliance

### Story 1.7: Storage Management & Retention

**Description**: Evidence storage with compliance-driven retention and immutability
**Technical Implementation**:

- WORM (Write Once Read Many) storage integration
- S3 Object Lock for AWS deployments
- Azure immutable blob storage for Azure deployments
- Retention policies: HIPAA ≥6 years, PCI DSS ≥12 months hot + archive, EU AI Act operational lifetime
- Automated lifecycle management with compliance tags
**Repository Paths**: `/internal/storage/`, `/internal/storage/worm.go`, `/internal/storage/retention.go`, `/internal/storage/s3_object_lock.go`, `/internal/storage/azure_immutable.go`
**Dependencies**: Story 1.4
**Acceptance Criteria**:
- WORM storage functional for all cloud providers
- Retention policies automatically enforced
- Compliance tags applied to all evidence
- Immutability verified through API

---

## Epic 2: Independent Verification Ecosystem

**Goal**: Build vendor-neutral Go and TypeScript verifiers with consistent validation

### Story 2.1: Go Verifier Implementation

**Description**: Primary verifier in Go supporting DEF and PEF formats
**Technical Implementation**:

- Independent module structure
- Cryptographic verification
- Lineage validation
**Repository Paths**: `/verifier/go/`, `/verifier/go/cmd/def-verify/`, `/verifier/go/cmd/pef-verify/`
**Dependencies**: Epic 1
**Acceptance Criteria**:
- Imports only spec files
- Validates all golden vectors
- Consistent with TypeScript verifier

### Story 2.2: TypeScript Verifier Implementation

**Description**: Secondary verifier ensuring cross-language consistency
**Technical Implementation**:

- npm package structure
- Browser and Node.js support
- Same validation logic as Go
**Repository Paths**: `/verifier/ts/`, `/verifier/ts/src/def-verifier.ts`, `/verifier/ts/src/pef-verifier.ts`
**Dependencies**: Epic 1
**Acceptance Criteria**:
- npx execution works
- Matches Go verifier results
- Published to npm

### Story 2.3: GitHub Action for Verification

**Description**: Reusable composite action for CI/CD integration
**Technical Implementation**:

- Composite action structure
- Both verifier support
- External repository usage
**Repository Paths**: `/.github/actions/verify-bundle/`, `/.github/workflows/verifier-integration.yml`
**Dependencies**: Story 2.1, Story 2.2
**Acceptance Criteria**:
- Action validates bundles in CI
- Usable by external projects
- Fails on invalid bundles

### Story 2.4: Cross-Verifier Consistency Testing

**Description**: Ensure both verifiers produce identical results
**Technical Implementation**:

- Automated consistency testing
- Performance comparison
- Regression detection
**Repository Paths**: `/test/cross_platform/verifier_consistency/`, `/.github/workflows/cross-verifier-consistency.yml`
**Dependencies**: Story 2.1, Story 2.2
**Acceptance Criteria**:
- Identical results across verifiers
- Performance within tolerances
- CI catches regressions

---

## Epic 3: Universal Policy Engine

**Goal**: Unified policy system with data platform, GenAI security, and voice compliance support

### Story 3.1: Policy Schema & Loader

**Description**: Comprehensive policy schema with validation
**Technical Implementation**:

- JSON Schema for policy.yaml
- Multi-section structure
- Version management
**Repository Paths**: `/internal/policy/`, `/spec/policy/schemas/policy_v4.schema.json`
**Dependencies**: Epic 1
**Acceptance Criteria**:
- Schema validates all policy sections
- Backward compatibility maintained
- Policy hash generation works

### Story 3.2: Data Platform Policy Section

**Description**: Policy controls for dbt, warehouses, and activation
**Technical Implementation**:

- dbt hook configuration
- Warehouse guard settings
- Activation enforcement rules
**Repository Paths**: `/internal/policy/data_platform.go`, `/templates/policy/data_platform.yaml`
**Dependencies**: Story 3.1
**Acceptance Criteria**:
- dbt controls configurable
- Warehouse policies enforced
- Activation rules validated

### Story 3.3: GenAI Security Policy Section

**Description**: Threat detection and response configuration
**Technical Implementation**:

- Prompt injection settings
- BEC defense configuration
- Kill-switch thresholds
**Repository Paths**: `/internal/policy/genai_security.go`, `/templates/policy/genai_security.yaml`
**Dependencies**: Story 3.1
**Acceptance Criteria**:
- Threat detectors configurable
- Shadow mode defaults
- Kill-switch matrices work

### Story 3.4: Voice Compliance Policy Section

**Description**: TCPA and UCaaS integration configuration
**Technical Implementation**:

- Disclaimer requirements
- Session management rules
- Barge-in configuration
**Repository Paths**: `/internal/policy/voice_compliance.go`, `/templates/policy/voice_compliance.yaml`
**Dependencies**: Story 3.1
**Acceptance Criteria**:
- TCPA rules configurable
- UCaaS settings validated
- Session policies enforced

### Story 3.5: Shadow Mode Implementation

**Description**: Parallel policy evaluation without enforcement
**Technical Implementation**:

- Parallel execution engine
- Verdict logging
- SIEM forwarding
**Repository Paths**: `/internal/shadow/`, `/internal/siem/shadow_verdicts.go`
**Dependencies**: Story 3.1
**Acceptance Criteria**:
- <1ms overhead
- Comprehensive logging
- Zero enforcement impact

### Story 3.6: HITL Checkpoints & Two-Person Controls

**Description**: Human-in-the-loop checkpoints with pause/resume and two-person approval
**Technical Implementation**:

- Checkpoint definitions in policy: pause points for human review
- Resume tokens with expiry and approval binding
- Two-person promotion guard for sensitive changes
- Workflow state persistence across checkpoints
- Notification system for pending approvals
- SOP documentation: `/docs/sop/change-mgmt.md`
**Repository Paths**: `/internal/policy/hitl_checkpoints.go`, `/internal/policy/two_person.go`, `/docs/sop/`
**Dependencies**: Story 3.1
**Acceptance Criteria**:
- Workflows pause at defined checkpoints
- Resume requires valid approval token
- Two-person rule enforced for promotions
- State preserved across pause/resume
- Audit trail complete

### Story 3.7: Lineage Tracking & Trust Propagation

**Description**: Data and operation lineage with trusted write hints
**Technical Implementation**:

- Lineage graph construction from operations
- Trusted write hints for validated sources
- Lineage propagation through transformations
- Cross-system lineage correlation
- Trust score calculation
**Repository Paths**: `/internal/lineage/`, `/internal/lineage/lineage.go`, `/internal/lineage/trust_hints.go`
**Dependencies**: Story 3.1
**Acceptance Criteria**:
- Lineage graphs accurately constructed
- Trust hints properly propagated
- Cross-system correlation functional
- Performance impact minimal

---

## Epic 4: Gateway - SchemaLock & Data Firewall

**Goal**: Enhanced Gateway with data platform awareness, GenAI security, and voice compliance

### Story 4.1: Core Gateway Infrastructure

**Description**: Streaming JSON validator with repair-once capability
**Technical Implementation**:

- Streaming validation engine
- Schema hash verification
- Queue management with backpressure
**Repository Paths**: `/internal/proxy/`, `/internal/proxy/validator.go`, `/internal/proxy/queue.go`
**Dependencies**: Epic 3
**Acceptance Criteria**:
- ≤15ms p95 latency
- Repair once then block
- 503 on queue overflow

### Story 4.2: Enhanced Receipt Generation

**Description**: Signed receipts with comprehensive metadata
**Technical Implementation**:

- OWASP/MITRE classification
- Data platform fields
- GenAI threat indicators
**Repository Paths**: `/internal/proxy/receipts.go`, `/spec/common/schemas/receipt.json`
**Dependencies**: Story 4.1
**Acceptance Criteria**:
- All fields present
- Cryptographically signed
- Platform-specific metadata

### Story 4.3: Data Platform Integration

**Description**: Data-aware validation and enforcement
**Technical Implementation**:

- Schema change detection
- Warehouse anchor correlation
- SQL safety validation
**Repository Paths**: `/internal/proxy/data_aware.go`, `/internal/proxy/sql_validator.go`
**Dependencies**: Story 4.1
**Acceptance Criteria**:
- Schema changes detected
- SQL safety enforced
- Warehouse anchors captured

### Story 4.4: GenAI Threat Detection

**Description**: Built-in prompt injection and threat detection
**Technical Implementation**:

- Regex/JSONPath heuristics
- Reflex loop detection
- External detector integration
**Repository Paths**: `/internal/proxy/genai_detectors.go`, `/internal/proxy/external_detectors.go`
**Dependencies**: Story 4.1
**Acceptance Criteria**:
- <100ms detection latency
- Shadow mode default
- External API timeout handling

### Story 4.5: Voice Session Tracking

**Description**: Voice compliance and session management
**Technical Implementation**:

- Session ID generation
- Disclaimer tracking
- Barge-in window management
**Repository Paths**: `/internal/proxy/voice_session.go`, `/internal/proxy/tcpa_compliance.go`
**Dependencies**: Story 4.1
**Acceptance Criteria**:
- Session correlation works
- Disclaimer enforcement
- <200ms barge-in response

### Story 4.6: SIEM Integration & NDJSON

**Description**: ECS/OCSF compliant event streaming
**Technical Implementation**:

- NDJSON formatting
- Field mappings
- Saved search templates
**Repository Paths**: `/internal/proxy/ndjson.go`, `/internal/siem/`, `/docs/siem/`
**Dependencies**: Story 4.2
**Acceptance Criteria**:
- ECS/OCSF compliance
- Splunk/Datadog import works
- GenAI fields included

### Story 4.7: SSE Notarization & Bypass Detection

**Description**: Server-sent events notarization and bypass event tracking
**Technical Implementation**:

- SSE notarization for streaming responses
- Bypass detection and logging
- Notary evidence inclusion in bundles
- Bypass event correlation with security metrics
- Real-time alerting for bypass attempts
**Repository Paths**: `/internal/proxy/sse_notarization.go`, `/internal/proxy/bypass.go`
**Dependencies**: Story 4.1
**Acceptance Criteria**:
- SSE streams notarized
- Bypass events logged with context
- Notary evidence in bundles
- Security alerts triggered
- Audit trail complete

---

## Epic 5: Recorder - Flight Data Recorder

**Goal**: Enhanced Recorder with warehouse anchoring and metadata-only snapshots

### Story 5.1: Core Recording Infrastructure

**Description**: HMAC-validated capture with privacy controls
**Technical Implementation**:

- HMAC header validation
- Body storage policies
- Hash chain continuity
**Repository Paths**: `/internal/recorder/`, `/internal/recorder/capture.go`
**Dependencies**: Epic 4
**Acceptance Criteria**:
- HMAC enforced
- Privacy by default
- Hash chains unbroken

### Story 5.2: Warehouse Anchoring System

**Description**: Platform-specific anchoring mechanisms
**Technical Implementation**:

- Snowflake QUERY_HISTORY
- Databricks Delta commits
- Postgres WAL LSN
**Repository Paths**: `/internal/recorder/warehouse_anchor.go`, `/internal/warehouse/anchors/`
**Dependencies**: Story 5.1
**Acceptance Criteria**:
- Anchors captured correctly
- Platform detection works
- Lineage preserved

### Story 5.3: Metadata-Only Snapshots

**Description**: Lightweight snapshots without full data capture
**Technical Implementation**:

- Row counts and checksums
- Schema fingerprints
- Sample statistics
**Repository Paths**: `/internal/recorder/metadata_snapshot.go`, `/internal/snapshot/`
**Dependencies**: Story 5.1
**Acceptance Criteria**:
- <50ms for 100 tables
- No sensitive data
- Deterministic output

### Story 5.4: Deterministic Diff Engine

**Description**: Reproducible change detection
**Technical Implementation**:

- Stable ordering
- Schema drift detection
- Data change summaries
**Repository Paths**: `/internal/diff/`, `/internal/diff/semantic_diff.go`
**Dependencies**: Story 5.3
**Acceptance Criteria**:
- Identical diffs across runs
- Semantic changes detected
- Performance <2s

### Story 5.5: Replay Engine & Certificates

**Description**: Deterministic replay with signed certificates
**Technical Implementation**:

- Scratch schema isolation
- Network denylist
- Certificate generation
**Repository Paths**: `/internal/replay/`, `/spec/common/schemas/replay_certificate.json`
**Dependencies**: Story 5.4
**Acceptance Criteria**:
- Isolated execution
- Success/partial/failed status
- Signed certificates

---

## Epic 6: Data Platform Core Integration

**Goal**: Native dbt integration, warehouse guards, and activation gateways

### Story 6.1: dbt Hook Framework

**Description**: Pre/post-run hooks for evidence generation
**Technical Implementation**:

- on_run_start/on_run_end hooks
- Metadata extraction
- DEF bundle generation
**Repository Paths**: `/internal/dbt/hooks/`, `/sdk/python/dbt/`, `/templates/projects/dbt/`
**Dependencies**: Epic 5
**Acceptance Criteria**:
- <2s overhead per run
- Metadata captured
- DEF bundles generated

### Story 6.2: SQL Safety Macros

**Description**: dbt macros for safe SQL operations
**Technical Implementation**:

- clyra_guard.safe_merge()
- Approval token validation
- Allowlist management
**Repository Paths**: `/internal/dbt/macros/`, `/sdk/python/dbt/macros/`, `/examples/dbt-integration/macros/`
**Dependencies**: Story 6.1
**Acceptance Criteria**:
- Mass operations blocked
- Approval tokens work
- Allowlists functional

### Story 6.3: Warehouse Native Guards

**Description**: Platform-specific enforcement mechanisms
**Technical Implementation**:

- Snowflake stored procedures
- Databricks macro helpers with MLflow integration for model governance
- Postgres functions
- Note: BigQuery support explicitly deferred to Phase 1.5
**Repository Paths**: `/internal/warehouse/guards/`, `/examples/warehouse-integration/`
**Dependencies**: Epic 5
**Acceptance Criteria**:
- Session tags enforced
- Approval validation works
- MLflow model versioning tracked (Databricks)
- <5s query overhead

### Story 6.6: Databricks MLflow Integration

**Description**: MLflow integration for model governance and experiment tracking
**Technical Implementation**:

- MLflow experiment metadata capture
- Model version tracking and lineage
- Deployment record correlation with Unity Catalog
- Model registry integration for approval workflows
- Experiment reproducibility validation
**Repository Paths**: `/internal/warehouse/databricks/mlflow.go`, `/examples/warehouse-integration/databricks/mlflow/`
**Dependencies**: Story 6.3
**Acceptance Criteria**:
- MLflow experiments tracked in evidence bundles
- Model versions correlated with data lineage
- Deployment approvals enforced
- Experiment metadata preserved

### Story 6.4: Activation Gateway Proxy

**Description**: HTTP proxy for reverse-ETL enforcement
**Technical Implementation**:

- HTTP proxy server
- Enforcement primitives
- Rate limiting
**Repository Paths**: `/internal/activation/`, `/cmd/clyra/activation/`
**Dependencies**: Epic 4
**Acceptance Criteria**:
- <15ms p95 proxy latency
- All primitives enforced
- Tenant isolation works

### Story 6.5: Data Platform CLI Commands

**Description**: dbt and warehouse management commands
**Technical Implementation**:

- clyra dbt init
- clyra warehouse doctor (with platform detection including BigQuery Phase 1.5 notice)
- clyra activation gateway
**Repository Paths**: `/cmd/clyra/dbt/`, `/cmd/clyra/warehouse/`, `/cmd/clyra/activation/`
**Dependencies**: Story 6.1, Story 6.3, Story 6.4
**Acceptance Criteria**:
- Commands functional
- Help text complete
- Integration examples work
- BigQuery detection shows clear Phase 1.5 deferral message

---

## Epic 7: GenAI Security Framework

**Goal**: Comprehensive threat detection, BEC prevention, and kill-switch capabilities

### Story 7.1: Threat Classification System

**Description**: OWASP LLM and MITRE ATT&CK mapping
**Technical Implementation**:

- OWASP LLM v1.1 categories
- MITRE technique correlation
- Threat response automation
**Repository Paths**: `/internal/genai/threats/`, `/docs/genai-security/threat-detection/`
**Dependencies**: Epic 4
**Acceptance Criteria**:
- All threats classified
- Correlation accurate
- Response automated

### Story 7.2: Built-in Threat Detectors

**Description**: Prompt injection and reflex detection
**Technical Implementation**:

- Regex/JSONPath patterns
- Loop detection algorithms
- Confidence scoring
**Repository Paths**: `/internal/genai/detectors/prompt_injection.go`, `/internal/genai/detectors/reflex_loop.go`
**Dependencies**: Story 7.1
**Acceptance Criteria**:
- <50ms detection time
- Low false positive rate
- Configurable patterns

### Story 7.3: External Detector Integration

**Description**: Vendor-agnostic deepfake and BEC detection
**Technical Implementation**:

- HTTP API framework
- Timeout handling
- Fallback mechanisms
**Repository Paths**: `/internal/genai/detectors/external.go`, `/internal/genai/detectors/deepfake.go`
**Dependencies**: Story 7.1
**Acceptance Criteria**:
- <500ms with timeout
- Graceful degradation
- Multiple vendor support

### Story 7.4: BEC-Grade Approval Certificates

**Description**: Enhanced approval with identity binding
**Technical Implementation**:

- SSO subject binding
- Challenge-response
- RFC 8785 payload hashing
**Repository Paths**: `/internal/genai/security/bec_approval.go`, `/spec/genai/bec_certificate.schema.json`
**Dependencies**: Epic 1
**Acceptance Criteria**:
- SSO binding works
- Challenge validated
- Payload integrity preserved

### Story 7.5: Multi-Trigger Kill-Switch

**Description**: Comprehensive emergency response system
**Technical Implementation**:

- Multiple trigger sources
- TTL-based recovery
- HITL override
**Repository Paths**: `/internal/killswitch/`, `/internal/killswitch/multi_trigger.go`
**Dependencies**: Story 7.1
**Acceptance Criteria**:
- <1s response time
- All triggers functional
- Recovery mechanisms work

### Story 7.6: GenAI Security CLI

**Description**: Testing and analysis commands
**Technical Implementation**:

- clyra genai test
- clyra bec validate
- clyra threats analyze
**Repository Paths**: `/cmd/clyra/genai/`, `/cmd/clyra/bec/`
**Dependencies**: Story 7.2, Story 7.4
**Acceptance Criteria**:
- Attack vector testing works
- Certificate validation functional
- Threat analysis accurate

---

## Epic 8: Voice & Conversation Compliance

**Goal**: TCPA compliance, UCaaS integration, and privacy-preserving session management

### Story 8.1: TCPA Compliance Framework

**Description**: Disclaimer and consent management
**Technical Implementation**:

- Disclaimer enforcement
- Consent tracking
- Opt-out mechanisms
**Repository Paths**: `/internal/voice/compliance/`, `/docs/voice-compliance/tcpa-compliance.md`
**Dependencies**: Epic 4
**Acceptance Criteria**:
- Disclaimers enforced
- Consent documented
- Time restrictions validated

### Story 8.2: Voice Session Management

**Description**: Privacy-preserving session tracking
**Technical Implementation**:

- Unique session IDs
- Metadata-only capture
- Session correlation
**Repository Paths**: `/internal/voice/session/`, `/spec/voice/session.schema.json`
**Dependencies**: Story 8.1
**Acceptance Criteria**:
- No audio stored
- Correlation accurate
- Privacy preserved

### Story 8.3: UCaaS Integration Platform

**Description**: Teams, Zoom, Slack, Twilio integration
**Technical Implementation**:

- API integrations
- Webhook handlers
- SIP gateway support
**Repository Paths**: `/internal/voice/correlation/`, `/examples/voice-compliance/ucaas-integration/`
**Dependencies**: Story 8.2
**Acceptance Criteria**:
- All platforms integrated
- Correlation <5ms
- WebRTC handled

### Story 8.4: Barge-in Capability

**Description**: Human interruption with quality metrics
**Technical Implementation**:

- Interruption detection
- Response time tracking
- Quality metrics
**Repository Paths**: `/internal/voice/compliance/barge_in.go`, `/internal/voice/session/interruption.go`
**Dependencies**: Story 8.2
**Acceptance Criteria**:
- <200ms response time
- Metrics accurate
- Acknowledgment tracked

### Story 8.5: Voice Compliance CLI

**Description**: Session and compliance management commands
**Technical Implementation**:

- clyra voice session
- clyra voice compliance
- clyra voice correlate
**Repository Paths**: `/cmd/clyra/voice/`
**Dependencies**: Story 8.2, Story 8.3
**Acceptance Criteria**:
- Session management works
- Compliance checks functional
- Correlation accurate

---

## Epic 9: Enhanced Enforcement Primitives

**Goal**: Advanced enforcement mechanisms for data, GenAI, and voice scenarios

### Story 9.1: Idempotency System

**Description**: HMAC-based duplicate prevention
**Technical Implementation**:

- HMAC fingerprinting
- TTL management
- Tenant scoping
**Repository Paths**: `/internal/enforcement/idempotency/`, `/internal/proxy/idempotency/`
**Dependencies**: Epic 4
**Acceptance Criteria**:
- Duplicates prevented
- TTL enforced
- Tenant isolation works

### Story 9.2: Velocity Guards

**Description**: Rate limiting with burst protection
**Technical Implementation**:

- Sliding windows
- Per-actor/tenant/route
- Burst handling
**Repository Paths**: `/internal/enforcement/ratelimit/`, `/internal/proxy/ratelimit/`
**Dependencies**: Epic 4
**Acceptance Criteria**:
- Rate limits enforced
- Fair burst handling
- Metrics accurate

### Story 9.3: Tenant Fencing

**Description**: Cross-tenant isolation
**Technical Implementation**:

- Header validation
- DSN hash namespacing
- Privacy preservation
**Repository Paths**: `/internal/enforcement/fences/`, `/internal/proxy/fences/`
**Dependencies**: Epic 4
**Acceptance Criteria**:
- Cross-tenant prevented
- Namespacing works
- Privacy maintained

### Story 9.4: SQL Safety Guards

**Description**: Prevention of dangerous SQL operations
**Technical Implementation**:

- UPDATE/DELETE validation
- Rows affected limits
- Allowlist exceptions
**Repository Paths**: `/internal/enforcement/sqlguard/`, `/internal/proxy/sqlguard/`
**Dependencies**: Epic 6
**Acceptance Criteria**:
- Dangerous ops blocked
- Limits enforced
- Allowlists work

### Story 9.5: Prompt Loop Breaker

**Description**: Agent failure cascade prevention
**Technical Implementation**:

- Loop detection
- Cool-off policies
- Per-run counters
**Repository Paths**: `/internal/enforcement/prompt_loop/`, `/internal/genai/security/loop_breaker.go`
**Dependencies**: Epic 7
**Acceptance Criteria**:
- Loops detected
- Cool-off enforced
- Counters accurate

---

## Epic 10: Multi-Framework Compliance Engine

**Goal**: Comprehensive attestation support for all compliance frameworks

### Story 10.1: SOX ITGC Implementation

**Description**: Data change control for SOX compliance
**Technical Implementation**:

- Change control tracking
- Segregation of duties
- Approval workflows
**Repository Paths**: `/internal/compliance/sox/`, `/docs/compliance/frameworks/sox-itgc/`
**Dependencies**: Epic 6
**Acceptance Criteria**:
- Changes tracked
- Duties segregated
- Approvals enforced

### Story 10.2: Enhanced PCI/HIPAA Support

**Description**: Daily reviews with threat posture
**Technical Implementation**:

- PCI Req-10 automation
- HIPAA audit controls
- Privacy safeguards
**Repository Paths**: `/internal/compliance/pci/`, `/internal/compliance/hipaa/`
**Dependencies**: Epic 7, Epic 8
**Acceptance Criteria**:
- Daily reviews automated
- Privacy preserved
- Threat posture included

### Story 10.3: EU AI Act & NIST RMF

**Description**: AI governance overlays
**Technical Implementation**:

- Record-keeping requirements
- Risk documentation
- Human oversight tracking
**Repository Paths**: `/internal/compliance/eu_ai_act/`, `/internal/compliance/nist_rmf/`
**Dependencies**: Epic 7
**Acceptance Criteria**:
- Requirements mapped
- Documentation complete
- Overlays functional

### Story 10.4: TCPA Voice Compliance

**Description**: Voice-specific compliance requirements
**Technical Implementation**:

- Consent documentation
- Disclaimer compliance
- Violation detection
**Repository Paths**: `/internal/compliance/tcpa/`, `/internal/voice/compliance/audit.go`
**Dependencies**: Epic 8
**Acceptance Criteria**:
- Consent tracked
- Disclaimers validated
- Violations detected

### Story 10.5: Unified Attestation Engine

**Description**: Single pipeline for all frameworks
**Technical Implementation**:

- Multi-framework support
- Evidence correlation
- Signed attestations
**Repository Paths**: `/cmd/clyra/attest.go`, `/internal/attestation/`
**Dependencies**: Story 10.1, Story 10.2, Story 10.3, Story 10.4
**Acceptance Criteria**:
- All frameworks supported
- Evidence correlated
- Attestations signed

### Story 10.6: Enhanced Daily Review with Data & GenAI

**Description**: Comprehensive daily review incorporating data changes and GenAI threat posture
**Technical Implementation**:

- Data platform change summaries: schema migrations, row count deltas, dbt test results
- GenAI threat posture: prompt injection attempts, deepfake detections, BEC attempts
- Voice compliance summary: TCPA violations, session statistics, barge-in events
- Automated PCI Req-10 compliance with enhanced logging
- Executive dashboard format with drill-down capabilities
- SIEM-ready export formats (ECS/OCSF NDJSON)
**Repository Paths**: `/internal/compliance/daily_review/`, `/cmd/clyra/report.go`, `/internal/review/daily_review/`, `/spec/compliance/daily_review.schema.json`
**Dependencies**: Story 10.1, Story 10.2, Epic 6, Epic 7, Epic 8
**Acceptance Criteria**:
- Daily review includes all data platform changes
- GenAI threat posture clearly summarized
- PCI Req-10 fully automated
- Export formats compatible with major SIEMs
- Executive-friendly visualization

---

## Epic 11: CI/CD & Deployment Controls

**Goal**: GitHub Actions integration with SOX change control and deployment governance

### Story 11.1: Enhanced GitHub Actions

**Description**: Comprehensive CI/CD workflows
**Technical Implementation**:

- Path-filtered workflows
- Evidence verification
- Policy gates
**Repository Paths**: `/.github/workflows/`, `/.github/actions/`
**Dependencies**: Epic 2
**Acceptance Criteria**:
- Workflows trigger correctly
- Verification works
- Gates enforce policies

### Story 11.2: Commit SHA Binding

**Description**: Change control with commit tracking
**Technical Implementation**:

- Approval certificate binding
- Commit uniqueness
- Segregation of duties
**Repository Paths**: `/internal/cicd/change_control/`, `/.github/workflows/sox-compliance-gate.yml`
**Dependencies**: Epic 10
**Acceptance Criteria**:
- Commits bound to approvals
- Duties segregated
- SOX compliance maintained

### Story 11.3: Deploy Rate Limiting

**Description**: Deployment control and safety
**Technical Implementation**:

- Rate limiting
- Approval workflows
- Rollback capabilities
**Repository Paths**: `/internal/cicd/deployment/`, `/internal/enforcement/cicd_controls.go`
**Dependencies**: Epic 9
**Acceptance Criteria**:
- Deploys rate limited
- Approvals enforced
- Rollback works

### Story 11.4: Badge Generation System

**Description**: Compliance badge issuance
**Technical Implementation**:

- JWT-signed badges
- Project registry
- Verification endpoints
**Repository Paths**: `/internal/badge/`, `/.github/workflows/badge-generation.yml`
**Dependencies**: Epic 10
**Acceptance Criteria**:
- Badges generated
- Registry functional
- Verification works

---

## Epic 12: ServiceNow & Jira Integration

**Goal**: Enterprise ITSM integration for attested change tickets

### Story 12.1: ServiceNow Bridge

**Description**: Native ServiceNow integration
**Technical Implementation**:

- REST API client
- Ticket formatting
- Template engine
**Repository Paths**: `/internal/bridges/servicenow/`, `/examples/servicenow-integration/`
**Dependencies**: Epic 10
**Acceptance Criteria**:
- Tickets created
- Formatting correct
- Templates work

### Story 12.2: Jira Connector

**Description**: Atlassian Jira integration
**Technical Implementation**:

- Atlassian SDK wrapper
- Issue formatting
- Export scripts
**Repository Paths**: `/internal/bridges/jira/`, `/examples/jira-integration/`
**Dependencies**: Epic 10
**Acceptance Criteria**:
- Issues created
- Fields mapped
- Export functional

### Story 12.3: Review SKU Components

**Description**: Listen-only mode infrastructure
**Technical Implementation**:

- Webhook listeners
- Log parsers
- Enrichment engine
**Repository Paths**: `/internal/review/`, `/cmd/clyra/review/`
**Dependencies**: Story 12.1, Story 12.2
**Acceptance Criteria**:
- Webhooks processed
- Logs parsed
- Evidence enriched

### Story 12.4: Gate SKU Components

**Description**: Full enforcement mode
**Technical Implementation**:

- Policy enforcement
- Primitive activation
- Enforcement templates
**Repository Paths**: `/internal/gate/`, `/cmd/clyra/gate/`
**Dependencies**: Epic 9
**Acceptance Criteria**:
- Policies enforced
- Primitives active
- Templates applied

---

## Epic 13: Enhanced SDKs & Developer Tools

**Goal**: Comprehensive SDK support with data platform, GenAI, and voice capabilities

### Story 13.1: Python SDK Enhancement

**Description**: Full-featured Python SDK
**Technical Implementation**:

- dbt helpers
- Warehouse utilities
- GenAI security utils
- Voice compliance helpers
**Repository Paths**: `/sdk/python/clyra_sdk/`
**Dependencies**: Epic 6, Epic 7, Epic 8
**Acceptance Criteria**:
- All helpers functional
- Examples work
- Tests pass

### Story 13.2: TypeScript SDK Foundation

**Description**: TypeScript SDK for automation
**Technical Implementation**:

- Core functionality
- Type definitions
- Framework integration
**Repository Paths**: `/sdk/typescript/`
**Dependencies**: Epic 1
**Acceptance Criteria**:
- Feature parity planned
- Types complete
- Examples functional

### Story 13.3: CLI Enhancement with Doctor Suggest-Fixes

**Description**: Comprehensive CLI commands including enhanced doctor with remediation suggestions
**Technical Implementation**:

- Data platform commands: dbt init, warehouse doctor, activation gateway
- GenAI security commands: genai test, bec validate, threats analyze
- Voice compliance commands: voice session, voice compliance, voice correlate
- Enhanced doctor command with suggest-fixes:
  - Detects common misconfigurations
  - Provides shell/SQL remediation commands
  - Checks database versions and suggests upgrades
  - Validates policy syntax and suggests corrections
  - Tests warehouse connectivity and provides connection string fixes
**Repository Paths**: `/cmd/clyra/`, `/cmd/clyra/doctor.go`, `/internal/cli/doctor_fixes.go`
**Dependencies**: Epic 6, Epic 7, Epic 8
**Acceptance Criteria**:
- All commands work with comprehensive help text
- Doctor provides actionable fix suggestions
- Remediation commands are copy-pasteable
- Version compatibility warnings clear
- Examples documented

### Story 13.4: Developer Documentation

**Description**: Comprehensive documentation
**Technical Implementation**:

- Getting started guides
- API references
- Integration patterns
**Repository Paths**: `/docs/`
**Dependencies**: All previous epics
**Acceptance Criteria**:
- Multi-track guides
- Complete API docs
- Patterns documented

---

## Epic 14: Performance & Reliability

**Goal**: Meet all SLAs with comprehensive monitoring

### Story 14.1: Performance Testing Framework

**Description**: k6-based performance validation
**Technical Implementation**:

- Performance scenarios
- SLA definitions
- Regression detection
**Repository Paths**: `/test/perf/`, `/.github/workflows/performance-comprehensive.yml`
**Dependencies**: All component epics
**Acceptance Criteria**:
- All SLAs defined
- Tests comprehensive
- CI gates functional

### Story 14.2: SLA Monitoring System

**Description**: Runtime SLA enforcement
**Technical Implementation**:

- Metric collection
- Threshold monitoring
- Alert generation
**Repository Paths**: `/internal/performance/`, `/internal/telemetry/`
**Dependencies**: Epic 0 (Story 0.7)
**Acceptance Criteria**:
- Metrics collected
- Thresholds enforced
- Alerts triggered

### Story 14.3: Circuit Breaker Implementation

**Description**: Failure isolation and recovery
**Technical Implementation**:

- Failure detection
- Circuit states
- Recovery logic
**Repository Paths**: `/internal/performance/circuit_breaker.go`
**Dependencies**: Epic 4, Epic 5
**Acceptance Criteria**:
- Failures detected
- Circuits break/recover
- State transitions correct

---

## Epic 15: Production Readiness

**Goal**: Security, operational excellence, and release integrity

### Story 15.1: Security Hardening

**Description**: Comprehensive security posture
**Technical Implementation**:

- Zero-trust architecture
- Secret management
- Vulnerability scanning
**Repository Paths**: `/internal/security/`, `/.github/workflows/security/`
**Dependencies**: Epic 0 (Story 0.5)
**Acceptance Criteria**:
- No critical vulnerabilities
- Secrets managed properly
- Scans automated

### Story 15.2: Operational Runbooks

**Description**: SOPs for production operations
**Technical Implementation**:

- Incident response
- Change management
- Key rotation
**Repository Paths**: `/docs/sop/`
**Dependencies**: All component epics
**Acceptance Criteria**:
- Runbooks complete
- Procedures tested
- Links functional

### Story 15.3: Release & Distribution

**Description**: Signed releases with provenance
**Technical Implementation**:

- Multi-arch builds
- SBOM generation
- Artifact signing
- Automated key rotation with 180-day lifecycle
**Repository Paths**: `/.github/workflows/release-*.yml`, `/goreleaser.yaml`, `/.github/workflows/key-rotation-reminder.yml`
**Dependencies**: Epic 0 (Story 0.5)
**Acceptance Criteria**:
- Artifacts signed
- SBOM attached
- Provenance verifiable
- Key rotation automated with alerts

### Story 15.4: Key Rotation & Cryptographic Lifecycle Management

**Description**: Automated key rotation with KMS integration for production security
**Technical Implementation**:

- 180-day key rotation cycle with automated reminders
- KMS integration for key lifecycle (AWS KMS, Azure Key Vault, HashiCorp Vault)
- Overlap periods for backward compatibility during rotation
- Automated rotation workflows with zero-downtime transitions
- Key metadata tracking and audit trail
**Repository Paths**: `/internal/crypto/kms/`, `/.github/workflows/key-rotation-reminder.yml`, `/docs/sop/key-rotation.md`
**Dependencies**: Epic 1 (Story 1.2)
**Acceptance Criteria**:
- Automated rotation reminders trigger at 150 days
- KMS integration supports all major providers
- Zero-downtime key transitions
- Complete audit trail of key lifecycle
- Backward compatibility for verification during overlap

---

## Epic 16: Demo & Quickstart Experience

**Goal**: 10-minute PLG path with comprehensive demos

### Story 16.1: Quickstart Infrastructure

**Description**: One-command local deployment
**Technical Implementation**:

- Docker Compose stacks
- Sample data
- Auto-configuration
**Repository Paths**: `/examples/quickstart-compose/`, `/cmd/clyra/quickstart.go`
**Dependencies**: All component epics
**Acceptance Criteria**:
- Deploys in <10 min
- All components functional
- Sample data loaded

### Story 16.2: Demo Scenarios

**Description**: Comprehensive demonstration commands
**Technical Implementation**:

- clyra demo data
- clyra demo contracts
- clyra demo etl
**Repository Paths**: `/cmd/clyra/demo/`, `/packs/`
**Dependencies**: Epic 6, Epic 7
**Acceptance Criteria**:
- Demos generate evidence
- Scenarios realistic
- Bundles verifiable

### Story 16.3: Procurement Kit

**Description**: Auditor and buyer materials
**Technical Implementation**:

- Sample evidence
- Attestation examples
- One-pagers
**Repository Paths**: `/kits/procurement/`
**Dependencies**: Epic 10
**Acceptance Criteria**:
- Kit complete
- Samples verify
- Documentation clear

### Story 16.4: Comprehensive Scenario & Service Packs

**Description**: Production-ready scenario packs and industry-specific service templates
**Technical Implementation**:

- Core Scenario Packs:
  - Contracts pack: `/packs/contracts/` with contract operation schemas, policies, fixtures, goldens
  - AP/AR pack: `/packs/ap_ar/` with financial operation schemas, approval workflows
  - ETL pack: `/packs/etl/` with data pipeline schemas, transformation policies
  - RPA pack: `/packs/rpa/` with automation schemas, robot policies
- Industry Service Packs:
  - Retail: `/packs/service/retail/` with order_update, refund_request, rma_create, address_change schemas
  - FinServ: `/packs/service/finserv/` with case_update, account_note_add, limit_adjust_request schemas
  - Travel: `/packs/service/travel/` with booking_change, loyalty_update, invoice_issue schemas
- Each pack includes: schemas, policies, fixtures, goldens, README.md, pack.yaml
**Repository Paths**: `/packs/`, `/packs/contracts/`, `/packs/ap_ar/`, `/packs/etl/`, `/packs/rpa/`, `/packs/service/`
**Dependencies**: Epic 6, Epic 7, Epic 10
**Acceptance Criteria**:
- All packs include working examples
- Policies validated against schemas
- Golden bundles verify correctly
- Industry-specific requirements met
- Documentation explains hardening

### Story 16.5: PLG Documentation & Success Digest

**Description**: Product-led growth documentation and success reporting
**Technical Implementation**:

- PLG documentation: `/docs/plg/hello_bundle.md` for first-time users
- Success digest: Enhanced report showing Merkle root, blocks processed, replay results
- Badge generation: Integration with success digest for achievement display
- Quick wins guide: `/docs/plg/quick_wins.md` with 10-minute achievements
- Onboarding metrics: Tracking time-to-first-bundle, time-to-first-attestation
- Success dashboard format: Executive-friendly visualizations
**Repository Paths**: `/docs/plg/`, `/cmd/clyra/report.go`, `/internal/plg/success_digest.go`, `/scripts/badge_artifact.sh`
**Dependencies**: Epic 10, Story 11.4
**Acceptance Criteria**:
- PLG docs guide to first bundle <10 min
- Success digest includes all key metrics
- Badges automatically awarded
- Onboarding metrics tracked
- Dashboard visualizations clear

---

## Epic 17: Integration Examples & Templates

**Goal**: Production-ready integration patterns

### Story 17.1: Data Platform Examples

**Description**: dbt and warehouse integrations
**Technical Implementation**:

- dbt project templates
- Warehouse configurations
- Activation examples
**Repository Paths**: `/examples/dbt-integration/`, `/examples/warehouse-integration/`
**Dependencies**: Epic 6
**Acceptance Criteria**:
- Examples functional
- Best practices documented
- Performance optimized

### Story 17.2: GenAI Security Examples

**Description**: Threat detection patterns
**Technical Implementation**:

- Detector configurations
- Attack simulations
- Mitigation strategies
**Repository Paths**: `/examples/genai-security/`
**Dependencies**: Epic 7
**Acceptance Criteria**:
- Patterns comprehensive
- Simulations realistic
- Strategies effective

### Story 17.3: Voice Compliance Examples

**Description**: UCaaS integration patterns
**Technical Implementation**:

- Platform integrations
- Session correlation
- Compliance workflows
**Repository Paths**: `/examples/voice-compliance/`
**Dependencies**: Epic 8
**Acceptance Criteria**:
- Integrations work
- Correlation accurate
- Workflows complete

### Story 17.4: SIEM Integration Templates

**Description**: Security monitoring integration with vendor-specific configurations
**Technical Implementation**:

- Splunk integration: `/examples/siem-integration/splunk/` with saved searches, dashboards, alert correlation
- Datadog integration: `/examples/siem-integration/datadog/` with custom metrics, log aggregation, incidents
- Elastic/ELK integration: `/examples/siem-integration/elastic/` with index templates, Kibana visualizations
- Generic SIEM: OpenTelemetry forwarding, Fluent Bit configuration
- Pre-built queries for: GenAI threats, data platform changes, compliance violations
- Alert correlation rules and threat hunting playbooks
**Repository Paths**: `/examples/siem-integration/`, `/integrations/siem/`, `/docs/siem/`
**Dependencies**: Epic 4 (Story 4.6)
**Acceptance Criteria**:
- Vendor-specific configs import correctly
- Dashboards functional with real data
- Alerts trigger on test events
- Threat correlation rules work
- Documentation includes tuning guidance

### Story 17.5: LiteLLM & SDK Integration Examples

**Description**: LiteLLM middleware integration and SDK usage patterns
**Technical Implementation**:

- LiteLLM recipe: `/examples/litellm-recipe/` with middleware configuration and examples
- GenAI security integration: threat detection with LiteLLM callbacks
- Multi-vendor LLM support examples (OpenAI, Anthropic, Bedrock)
- Python SDK integration: `/examples/python-sdk/` with comprehensive examples
- TypeScript SDK examples: `/examples/typescript-sdk/` for browser and Node.js
- Framework integrations: FastAPI, Express, Next.js, Django examples
**Repository Paths**: `/examples/litellm-recipe/`, `/examples/python-sdk/`, `/examples/typescript-sdk/`, `/sdk/python/clyra_sdk/litellm_middleware.py`
**Dependencies**: Epic 13
**Acceptance Criteria**:
- LiteLLM middleware works with major providers
- SDK examples cover all features
- Framework integrations production-ready
- Performance impact documented

---

## Success Metrics & Exit Criteria

### Technical Metrics

- **Performance**: All SLAs met (Gateway ≤15ms p95, Recorder ≤20ms p95, dbt hooks <2s)
- **Reliability**: >99% bundle verification success, <0.1% false positive rate
- **Security**: Zero critical vulnerabilities, comprehensive threat coverage

### Business Metrics

- **Adoption**: ≥3 design partners, ≥50% dbt runs under policy within 60 days
- **Compliance**: ≥1 attestation used in quarter-end close
- **Revenue**: $300-600k ARR primarily from data platform use cases

### Strategic Metrics

- **Market Position**: DEF/PEF referenced by competitors or standards bodies
- **Community**: ≥100 dbt projects with badges, ≥10 GitHub stars per week
- **Partnerships**: Integration agreements with dbt Labs, warehouse vendors

---

**Note**: This plan represents the complete MVP scope for Clyra v4.0. The following items are explicitly deferred to Phase 1.5:

- **BigQuery warehouse anchoring and full support** (currently demo-only with clear messaging in `clyra warehouse doctor`)
- Prefect/Dagster pipeline operators
- Full TypeScript SDK feature parity
- K8s/Istio/Helm deployment: `/deploy/helm/`, enriched Envoy filters
- Redis rate/idempotency store: Pluggable backend for `/internal/proxy/{ratelimit,idempotency}`
- Diff-Agent CLI: Advanced diff capabilities in `/cmd/clyra/`, `/internal/diff/`
- Rollback manifest pointer: State management in `/internal/bundle/`
- Advanced WASM detector sandbox
- Packaged SIEM dashboards beyond templates
- Self-hosted control plane UI/dashboard

Phase 2 and beyond items (UI/dashboard, SaaS delivery, marketplace ecosystem) are excluded from this epic plan but documented for future reference.
