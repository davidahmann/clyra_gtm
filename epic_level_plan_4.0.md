# Clyra v4.0 Epic-Level Plan (Data-Led, Agent-Ready)

**Execution Order**: 0 → 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10 → 11 → 12 → 13 → **14** → **15** → **16** → **17** → **18** → **19** → **20**
(then Phase 1.5, Phase 2, Phase 3)

---

## **Epic 0 — Enhanced Foundations (v4.0 Extensions)**
**Goal**: Extended foundations for data-led, agent-ready architecture with 15-Factor compliance and enhanced security.

**Stories & repo_paths** (continuing from implemented stories 1-7):

**0.8 15-Factor App Compliance Infrastructure**
Paths: `/internal/telemetry/`, `/internal/api/openapi/`, `/internal/auth/`, `.github/workflows/api-validation.yml`
✅ OpenAPI 3.0 specs auto-generated, comprehensive telemetry via OpenTelemetry, mTLS + HMAC authentication

**0.9 Enhanced Security Exceptions & CODEOWNERS**
Paths: `/.github/SECURITY_EXCEPTIONS.md`, `/CODEOWNERS`, `/internal/security/`
✅ Security-critical paths require approval, exceptions tracked with expiry dates, automated reminders

**0.10 Cross-Platform Compatibility Matrix**
Paths: `/docs/compatibility/`, `/test/compatibility/`, `/.github/workflows/cross-platform-ci.yml`
✅ Database compatibility (Postgres/Snowflake/Databricks), cloud provider validation, SDK consistency

---

## **Epic 14 — Data Platform Core (NEW)**
**Goal**: Native dbt integration, warehouse anchoring, activation gateways, DEF v0 format, SOX ITGC compliance.

**14.1 dbt Integration Framework**
Paths: `/internal/dbt/`, `/sdk/python/dbt/`, `/templates/projects/dbt/`, `/cmd/clyra/dbt/`
✅ Pre/post-run hooks emit DEF v0 bundles, SQL safety macros, CI gate integration

**14.2 Warehouse-Native Anchoring**
Paths: `/internal/warehouse/anchors/`, `/internal/warehouse/guards/`, `/docs/data-platform/warehouse-integration/`
✅ Snowflake QUERY_HISTORY + session tags, Databricks Delta commits + Unity Catalog, Postgres WAL LSN

**14.3 Activation/Reverse-ETL Gateway**
Paths: `/internal/activation/`, `/cmd/clyra/activation/`, `/examples/activation-flows/`
✅ HTTP proxy for Hightouch/Census/RudderStack with comprehensive enforcement primitives

**14.4 DEF v0 (Data Evidence Format)**
Paths: `/spec/def/`, `/internal/bundle/def_builder.go`, `/verifier/go/cmd/def-verify/`, `/verifier/typescript/src/def-verifier.ts`
✅ Warehouse-anchored evidence, semantic delta tracking, independent Go/TS verification

**14.5 SQL Safety Guards & Approval Tokens**
Paths: `/internal/warehouse/guards/`, `/sdk/python/dbt/macros/`, `/templates/policy/sql_safety.yaml`
✅ Advisory blocks on mass UPDATE/DELETE, approval token validation, allowlist maintenance

**14.6 Data Platform CLI Commands**
Paths: `/cmd/clyra/dbt/`, `/cmd/clyra/warehouse/`, `/cmd/clyra/demo/data.go`
✅ `clyra dbt init`, `clyra warehouse doctor`, `clyra demo data` with platform-specific examples

**14.7 SOX ITGC Compliance Integration**
Paths: `/docs/compliance/frameworks/sox-itgc/`, `/internal/compliance/sox/`, `/spec/compliance/sox_itgc.schema.json`
✅ Change control enforcement, segregation of duties, comprehensive audit trails

---

## **Epic 15 — GenAI Security Framework (NEW)**
**Goal**: Comprehensive GenAI threat detection, BEC prevention, external detector integration, multi-trigger kill-switch.

**15.1 OWASP LLM Top 10 & MITRE ATT&CK Integration**
Paths: `/internal/genai/threats/`, `/docs/genai-security/threat-detection/`, `/spec/genai/threat_classification.json`
✅ OWASP LLM v1.1 mapping, MITRE ATT&CK correlation, threat response automation

**15.2 Built-in Prompt Injection Detection**
Paths: `/internal/genai/detectors/prompt_injection.go`, `/internal/genai/detectors/reflex_loop.go`, `/test/genai_security/`
✅ Regex/JSONPath heuristics, reflex/loop detection, shadow-mode defaults for safety

**15.3 External Detector Integration Framework**
Paths: `/internal/genai/detectors/external.go`, `/internal/genai/detectors/deepfake.go`, `/examples/genai-security/external-detector/`
✅ Vendor-agnostic HTTP APIs, timeout/fallback mechanisms, confidence threshold tuning

**15.4 BEC-Grade Approval Certificates**
Paths: `/internal/genai/security/bec_approval.go`, `/internal/genai/security/sso_binding.go`, `/spec/genai/bec_certificate.schema.json`
✅ SSO binding (sso_sub + idp_domain), challenge-response, RFC 8785 payload hash binding

**15.5 Multi-Trigger Kill-Switch Evolution**
Paths: `/internal/killswitch/multi_trigger.go`, `/internal/killswitch/genai_triggers.go`, `/cmd/clyra/genai/threats.go`
✅ Data bursts + GenAI threats + error spikes, TTL recovery, HITL override capabilities

**15.6 Shadow Mode Enhancement**
Paths: `/internal/shadow/parallel_eval.go`, `/internal/shadow/genai_correlation.go`, `/internal/siem/genai_indicators.go`
✅ Parallel policy evaluation, comprehensive threat logging, zero enforcement impact

**15.7 GenAI Security CLI Commands**
Paths: `/cmd/clyra/genai/`, `/cmd/clyra/bec/`, `/test/golden_vectors/genai_vectors/`
✅ `clyra genai test`, `clyra bec validate`, `clyra threats analyze` with attack vector simulation

---

## **Epic 16 — Voice/Conversation Compliance (NEW)**
**Goal**: TCPA compliance, UCaaS integration, session management, privacy preservation.

**16.1 TCPA Compliance Framework**
Paths: `/internal/voice/compliance/tcpa.go`, `/internal/voice/compliance/disclaimer.go`, `/docs/voice-compliance/tcpa-compliance.md`
✅ Disclaimer enforcement, consent tracking, opt-out mechanisms, time restriction validation

**16.2 Voice Session Management**
Paths: `/internal/voice/session/manager.go`, `/internal/voice/session/privacy.go`, `/spec/voice/session.schema.json`
✅ Unique session IDs, metadata-only capture, correlation with API actions, privacy preservation

**16.3 UCaaS Integration Platform**
Paths: `/internal/voice/correlation/ucaas.go`, `/examples/voice-compliance/ucaas-integration/`, `/docs/voice-compliance/ucaas-integration/`
✅ Teams/Zoom/Slack/Twilio correlation, SIP gateway support, WebRTC handling

**16.4 Barge-in Capability**
Paths: `/internal/voice/compliance/barge_in.go`, `/internal/voice/session/interruption.go`, `/test/voice_compliance/barge_in_test.go`
✅ Human interruption <200ms response, quality metrics tracking, acknowledgment validation

**16.5 Voice Compliance CLI & Validation**
Paths: `/cmd/clyra/voice/`, `/internal/voice/validation/`, `/test/golden_vectors/voice_vectors/`
✅ `clyra voice session`, `clyra voice compliance --check-disclaimers`, correlation commands

---

## **Epic 17 — Enhanced Universal Foundation (v4.0 Upgrades)**
**Goal**: Upgrade existing components with data platform awareness, GenAI security, voice compliance.

**17.1 Enhanced Gateway (SchemaLock + Data Firewall)**
Paths: `/internal/proxy/` (enhanced), `/internal/proxy/data_aware.go`, `/internal/proxy/genai_enhanced.go`
✅ Data-aware validation, GenAI threat detection, voice session tracking, BEC-hardened receipts

**17.2 Enhanced Recorder (Flight Data Recorder)**
Paths: `/internal/recorder/` (enhanced), `/internal/recorder/warehouse_anchor.go`, `/internal/recorder/metadata_only.go`
✅ Warehouse anchoring, metadata-only snapshots, enhanced replay with data recreation

**17.3 Unified DEF/PEF Bundle Builder**
Paths: `/internal/bundle/unified_builder.go`, `/internal/bundle/governance_metadata.go`, `/spec/common/governance.json`
✅ Unified DEF/PEF formats, governance metadata embedding, enhanced performance metrics

**17.4 Enhanced Policy Engine**
Paths: `/internal/policy/` (enhanced), `/spec/policy/schemas/policy_v4.schema.json`, `/templates/policy/comprehensive.yaml`
✅ Data platform + GenAI + voice sections, shadow mode promotion, kill-switch matrix

**17.5 Enhanced Enforcement Primitives**
Paths: `/internal/enforcement/` (enhanced), `/internal/enforcement/bec_grade.go`, `/internal/enforcement/prompt_loop.go`
✅ BEC-grade approvals, prompt-loop breakers, voice session fences, CI/CD enforcement

---

## **Epic 18 — Multi-Framework Compliance (Enhanced)**
**Goal**: Comprehensive compliance support with SOX ITGC, PCI/HIPAA, EU AI Act, NIST AI RMF, TCPA.

**18.1 SOX ITGC Implementation (Data Platform Focus)**
Paths: `/internal/compliance/sox/`, `/docs/compliance/frameworks/sox-itgc/`, `/cmd/clyra/attest.go` (enhanced)
✅ Data change control, segregation of duties, approval tracking, automated evidence generation

**18.2 Enhanced PCI/HIPAA with Data & GenAI**
Paths: `/internal/compliance/pci/`, `/internal/compliance/hipaa/`, `/docs/compliance/frameworks/pci-dss/`, `/docs/compliance/frameworks/hipaa/`
✅ Enhanced daily reviews with data changes + GenAI threat posture, privacy safeguards

**18.3 EU AI Act & NIST AI RMF Integration**
Paths: `/internal/compliance/eu_ai_act/`, `/internal/compliance/nist_rmf/`, `/spec/compliance/eu_ai_act.schema.json`
✅ High-risk AI system documentation, record-keeping requirements, risk management overlays

**18.4 TCPA Voice Compliance**
Paths: `/internal/compliance/tcpa/`, `/docs/compliance/frameworks/tcpa/`, `/internal/voice/compliance/audit.go`
✅ Voice consent documentation, disclaimer compliance, automated violation detection

**18.5 Multi-Framework Attestation Engine**
Paths: `/cmd/clyra/attest.go` (enhanced), `/internal/attestation/multi_framework.go`, `/docs/compliance/attestation-generation.md`
✅ Single pipeline for all frameworks, cross-framework evidence correlation, auditor-ready artifacts

---

## **Epic 19 — CI/CD & Code Change Control (NEW)**
**Goal**: GitHub Actions integration, commit SHA binding, SOX ITGC tracking, deployment controls.

**19.1 GitHub Actions Enhanced Integration**
Paths: `/.github/actions/` (enhanced), `/.github/workflows/data-platform-ci.yml`, `/.github/workflows/genai-security-ci.yml`
✅ Evidence verification, policy gates, badge generation, data platform validation

**19.2 Commit SHA Binding & Change Control**
Paths: `/internal/cicd/change_control/`, `/internal/cicd/commit_binding.go`, `/.github/workflows/sox-compliance-gate.yml`
✅ Approval certificates bound to commits, automated segregation of duties checking

**19.3 Deploy Rate Limiting & Approval Workflows**
Paths: `/internal/cicd/deployment/`, `/internal/enforcement/cicd_controls.go`, `/docs/operations/deployment/`
✅ Prevent runaway deployments, enforce approval workflows, automated rollback capabilities

**19.4 Cross-Verifier Consistency Validation**
Paths: `/.github/workflows/cross-verifier-consistency.yml`, `/test/cross_platform/verifier_consistency/`, `/scripts/verifier_validation.py`
✅ Ensure Go/TS verifiers produce identical results across DEF/PEF formats

---

## **Epic 20 — Enhanced Developer Experience (v4.0)**
**Goal**: Comprehensive tooling, documentation, and integration patterns for all v4.0 capabilities.

**20.1 Enhanced CLI with All Components**
Paths: `/cmd/clyra/` (comprehensive), `/docs/reference/cli-reference.md`, `/cmd/clyra/help_text.go` (updated)
✅ Data platform, GenAI security, voice compliance commands with comprehensive help

**20.2 Enhanced Python SDK**
Paths: `/sdk/python/clyra_sdk/` (enhanced), `/sdk/python/clyra_sdk/dbt/`, `/sdk/python/clyra_sdk/genai/`, `/sdk/python/clyra_sdk/voice/`
✅ dbt helpers, warehouse integration, GenAI security utilities, voice compliance helpers

**20.3 TypeScript SDK (Phase 1.5)**
Paths: `/sdk/typescript/`, `/sdk/typescript/src/genai/`, `/sdk/typescript/src/voice/`, `/examples/typescript/`
✅ Full feature parity with Python SDK, comprehensive type definitions, framework integration

**20.4 Comprehensive Documentation**
Paths: `/docs/` (comprehensive), `/docs/getting-started/`, `/docs/tutorials/`, `/docs/reference/`
✅ Multi-track getting started, comprehensive tutorials, complete API reference, troubleshooting guides

**20.5 Enhanced Testing Framework**
Paths: `/test/` (comprehensive), `/test/golden_vectors/` (enhanced), `/test/cross_platform/`, `/test/regression/`
✅ DEF/PEF golden vectors, cross-platform compatibility, regression testing, performance validation

**20.6 Integration Pattern Library**
Paths: `/examples/` (comprehensive), `/examples/dbt-integration/`, `/examples/genai-security/`, `/examples/voice-compliance/`
✅ Complete integration examples, best practices, performance optimization guides

---

## **Enhanced Epic Extensions (v4.0 Updates to Existing Epics)**

### **Epic 1+ — Enhanced Evidence & Spec Compliance**
**1.10 DEF/PEF Unified Verification**
Paths: `/verifier/go/pkg/verifier/` (enhanced), `/verifier/typescript/src/` (enhanced)
✅ Single verifier codebase supporting both DEF and PEF formats with lineage validation

**1.11 Cross-Platform Golden Vectors**
Paths: `/spec/def/test-vectors/`, `/spec/pef/test-vectors/` (enhanced), `/test/golden_vectors/compliance_vectors/`
✅ Database compatibility vectors, compliance framework vectors, GenAI security vectors

### **Epic 2+ — Enhanced Gateway (SchemaLock + Data Firewall)**
**2.9 Data Platform Integration**
Paths: `/internal/proxy/data_platform.go`, `/internal/proxy/warehouse_validation.go`
✅ Schema change validation, warehouse anchor correlation, activation flow enforcement

**2.10 GenAI Security Integration**
Paths: `/internal/proxy/genai_integration.go`, `/internal/proxy/voice_session.go`
✅ Prompt injection detection, voice session tracking, BEC-grade receipt enhancement

### **Epic 3+ — Enhanced Recorder (Flight Data Recorder)**
**3.6 Data Platform Recording**
Paths: `/internal/recorder/data_platform.go`, `/internal/recorder/warehouse_replay.go`
✅ Warehouse metadata capture, data lineage recording, schema change replay

**3.7 GenAI & Voice Session Recording**
Paths: `/internal/recorder/genai_recording.go`, `/internal/recorder/voice_session.go`
✅ GenAI threat correlation, voice session metadata, privacy-preserving audit trails

### **Epic 4+ — Enhanced Unified Policy Surface**
**4.10 Data Platform Policy Sections**
Paths: `/internal/policy/data_platform.go`, `/spec/policy/schemas/data_platform.schema.json`
✅ dbt hooks configuration, warehouse guards setup, activation enforcement rules

**4.11 GenAI Security Policy Sections**
Paths: `/internal/policy/genai_security.go`, `/spec/policy/schemas/genai_security.schema.json`
✅ Threat detection configuration, BEC-grade approval settings, kill-switch thresholds

**4.12 Voice Compliance Policy Sections**
Paths: `/internal/policy/voice_compliance.go`, `/spec/policy/schemas/voice_compliance.schema.json`
✅ TCPA compliance settings, UCaaS integration config, session management rules

### **Epic 5+ — Enhanced Attestation v0**
**5.4 Multi-Framework Enhancement**
Paths: `/internal/attestation/multi_framework.go`, `/docs/compliance/attestation-generation.md` (enhanced)
✅ SOX ITGC + PCI/HIPAA + EU AI Act + NIST + TCPA support with unified pipeline

**5.5 Data Platform Attestations**
Paths: `/internal/attestation/data_platform.go`, `/docs/compliance/frameworks/` (enhanced)
✅ dbt run attestations, warehouse change evidence, activation sync compliance

### **Epic 12+ — Enhanced Performance & Reliability**
**12.5 Data Platform Performance Validation**
Paths: `/test/perf/data_platform_perf.js`, `/test/perf/genai_security_perf.js`, `/test/perf/voice_compliance_perf.js`
✅ dbt hook <2s, warehouse queries <5s, activation proxy <15ms p95, GenAI analysis <100ms

**12.6 Comprehensive SLA Monitoring**
Paths: `/internal/performance/sla_monitor.go`, `/internal/performance/budgets.go`, `/.github/workflows/performance-comprehensive.yml`
✅ All component SLAs monitored, automated regression detection, performance budget enforcement

---

## **Enhanced Workflow Integration (v4.0)**

### **Enhanced Warp Workflows**
Paths: `/.warp/workflows.yaml` (comprehensive)
- `quickstart-data`: Data platform focused quickstart
- `test-comprehensive`: Full test suite (data + GenAI + voice)
- `genai-security-test`: GenAI threat detection validation
- `voice-compliance-test`: Voice compliance validation
- `warehouse-doctor`: Multi-platform health checks
- `sox-compliance-check`: SOX ITGC validation
- `verify-cross-platform`: Cross-verifier consistency
- `attest-multi-framework`: All framework attestation

### **Enhanced GitHub Actions**
- `data-platform-ci.yml`: dbt integration, warehouse connectivity, DEF validation
- `genai-security-ci.yml`: Threat detection, BEC validation, external detector simulation
- `voice-compliance-ci.yml`: TCPA compliance, UCaaS integration, session management
- `sox-compliance-gate.yml`: Change control, segregation of duties validation
- `cross-verifier-consistency.yml`: Ensure verifier result matching
- `performance-comprehensive.yml`: All component performance validation

---

## **Phase 1.5+ (Post-MVP Enhancements)**

### **Data Platform Expansion**
- BigQuery anchoring and advanced warehouse support
- Advanced dbt features (semantic layer, advanced lineage)
- Prefect/Dagster operators for broader pipeline ecosystem

### **GenAI Security Evolution**
- Custom model integration and advanced threat detection
- ML-based analysis and behavioral anomaly detection
- Community threat intelligence integration

### **Voice/Conversation Enhancement**
- Advanced UCaaS integrations and real-time analysis
- Multi-language disclaimer support and regional compliance
- Advanced voice analytics and quality metrics

### **Platform Maturation**
- Self-hosted control plane with enterprise features
- Advanced compliance packs for industry-specific requirements
- UI/dashboard for non-technical stakeholders

---

**Success Metrics (v4.0)**:
- **Data Platform**: ≥3 design partners, ≥50% customer dbt runs under policy within 60 days
- **GenAI Security**: ≥1 blocked deepfake/BEC attempt per customer per quarter, <0.1% false positive rate
- **Voice Compliance**: 100% TCPA compliance validation, comprehensive UCaaS correlation
- **Technical**: All performance SLAs met, >99% evidence bundle verification success
- **Commercial**: $300-600k ARR primarily from data platform, ≥1 attestation used in quarter-end close