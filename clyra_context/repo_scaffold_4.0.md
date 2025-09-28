# **Clyra v4.0 Monorepo Repository Scaffold**

**Data-Led, Agent-Ready Architecture**

*This repository structure reflects Clyra v4.0's strategic positioning: leading with data platform enforcement where budget exists today, while maintaining the same architecture that will protect AI agents tomorrow.*

---

## **Root Structure**

```
clyra/
├─ README.md                              # Enhanced v4.0 positioning: "Evidence, not observability"
├─ LICENSE                                # Apache 2.0 (OSS)
├─ CODE_OF_CONDUCT.md
├─ CONTRIBUTING.md
├─ SECURITY.md                            # Enhanced with GenAI security disclosures
├─ SUPPORT.md
├─ CHANGELOG.md                           # managed by release-please
├─ .editorconfig
├─ .gitignore
├─ .gitattributes
├─ .pre-commit-config.yaml                # Enhanced with ruff 0.13.1, mypy 1.18.2
├─ CODEOWNERS                             # Security-critical paths require approval
├─ Makefile                               # Enhanced with data platform targets
├─ go.mod                                 # Go 1.25.x (github.com/clyra/clyra)
├─ go.work                                # includes ./, ./verifier/go
├─ package.json                           # npm workspace for verifier/ts (Node 22.x LTS)
├─ release-please-config.json
├─ goreleaser.yaml                        # Multi-arch builds with cosign signatures
├─ .cosign.pub                            # Public key for release verification
├─ .warp/
│  └─ workflows.yaml                      # Enhanced Warp workflows (data-platform targets)
│
```

---

## **Command-Line Interface (Enhanced v4.0)**

```
├─ cmd/
│  └─ clyra/
│     ├─ main.go
│     ├─ help_text.go                     # Updated: "data pipelines to AI agents, dbt/ETL, reverse-ETL"
│     ├─ init.go                          # Enhanced with data platform templates
│     ├─ demo/                            # Enhanced demo scenarios
│     │  ├─ contracts.go
│     │  ├─ etl.go
│     │  ├─ data.go                       # NEW: data platform demo (dbt simulation)
│     │  └─ retail.go
│     ├─ quickstart.go                    # Enhanced with data platform examples
│     ├─ report.go                        # Enhanced with --daily-review (GenAI threat posture)
│     ├─ verify.go                        # Enhanced with --validate-lineage
│     ├─ replay.go                        # Enhanced with data replay capabilities
│     ├─ policy/                          # Enhanced policy management
│     │  ├─ wizard.go                     # Interactive policy creation (data/GenAI/voice templates)
│     │  ├─ lint.go                       # Validate against enhanced schema
│     │  ├─ test.go                       # Test against golden vectors (DEF/PEF)
│     │  └─ convert.go                    # NEW: Convert v3.0 policies to v4.0
│     ├─ export.go                        # Enhanced: --format ndjson|def|pef
│     ├─ doctor.go                        # Enhanced health checks (data platform + GenAI)
│     ├─ attest.go                        # Enhanced frameworks (SOX|PCI|HIPAA|EU-AI-Act|NIST)
│     ├─ dbt/                             # NEW: dbt-specific commands
│     │  ├─ init.go                       # Initialize dbt project with Clyra hooks
│     │  └─ doctor.go                     # dbt project health checks
│     ├─ warehouse/                       # NEW: warehouse integration commands
│     │  └─ doctor.go                     # Warehouse connectivity and configuration checks
│     ├─ activation/                      # NEW: activation/reverse-ETL commands
│     │  └─ gateway.go                    # Start activation gateway proxy
│     ├─ genai/                           # NEW: GenAI security commands
│     │  ├─ test.go                       # Test threat detectors against attack vectors
│     │  └─ threats.go                    # Analyze GenAI threat patterns
│     ├─ bec/                             # NEW: BEC certificate management
│     │  └─ validate.go                   # Validate BEC-grade approval certificates
│     └─ voice/                           # NEW: voice/conversation compliance
│        └─ session.go                    # Voice session management and correlation
│
```

---

## **Core Internal Architecture (Enhanced v4.0)**

```
├─ internal/
│  ├─ proxy/                              # Enhanced Gateway: SchemaLock + Data Firewall
│  │  ├─ validator.go                     # Enhanced with data-aware validation
│  │  ├─ csv_validator.go                 # Minimal CSV validator
│  │  ├─ receipts.go                      # Enhanced with data platform fields
│  │  ├─ hashchain.go                     # Per-run SHA-256 chains
│  │  ├─ sse_notarization.go
│  │  ├─ bypass.go
│  │  ├─ queue.go                         # Fail-closed with bounded queues
│  │  ├─ detectors.go                     # Enhanced GenAI threat detection
│  │  ├─ ext_detectors.go                 # External deepfake/BEC detector integration
│  │  ├─ idempotency/
│  │  │  ├─ store.go                      # HMAC fingerprints, tenant-scoped
│  │  │  └─ replay_bypass.go
│  │  ├─ approvals/
│  │  │  ├─ verify.go                     # BEC-grade certificates with SSO binding
│  │  │  ├─ challenge.go                  # NEW: challenge-response for BEC prevention
│  │  │  └─ signer_kms.go                 # KMS integration for signing
│  │  ├─ ratelimit/
│  │  │  ├─ sliding_window.go             # Enhanced with GenAI-aware bursts
│  │  │  └─ state_debug.go
│  │  ├─ fences/
│  │  │  ├─ tenant_actor_check.go         # Cross-tenant isolation
│  │  │  └─ privacy_hash.go               # Privacy-preserving audit trails
│  │  ├─ sqlguard/
│  │  │  ├─ advisory.go                   # SQL safety (advisory mode)
│  │  │  └─ allowlist.go                  # Maintenance job allowlists
│  │  ├─ voice/                           # NEW: voice session handling
│  │  │  ├─ session.go                    # Voice session management
│  │  │  └─ compliance.go                 # TCPA disclaimer enforcement
│  │  └─ ndjson.go                        # Enhanced ECS/OCSF with GenAI fields
│  ├─ warehouse/                          # NEW: data platform native integration
│  │  ├─ anchors/                         # Warehouse-specific anchoring
│  │  │  ├─ snowflake.go                  # QUERY_HISTORY, session tags
│  │  │  ├─ databricks.go                 # Delta Lake commits, Unity Catalog
│  │  │  ├─ postgres.go                   # WAL LSN anchoring
│  │  │  └─ bigquery.go                   # Job metadata anchoring (Phase 1.5)
│  │  ├─ guards/                          # SQL safety guards
│  │  │  ├─ snowflake_guards.go           # Stored procedures with approval validation
│  │  │  ├─ databricks_guards.go          # Macro helpers with token requirements
│  │  │  └─ postgres_guards.go            # Native function guards
│  │  └─ lineage/                         # Warehouse lineage extraction
│  │     ├─ snowflake_lineage.go
│  │     ├─ databricks_lineage.go
│  │     └─ postgres_lineage.go
│  ├─ dbt/                                # NEW: dbt integration
│  │  ├─ hooks/                           # dbt hook implementations
│  │  │  ├─ pre_run.go                    # on_run_start hook
│  │  │  ├─ post_run.go                   # on_run_end hook with DEF generation
│  │  │  └─ model_hooks.go                # Model-level post-hooks
│  │  ├─ macros/                          # SQL safety macros
│  │  │  ├─ guard_macros.go               # clyra_guard.safe_merge(), etc.
│  │  │  └─ audit_macros.go               # clyra_audit.track_change()
│  │  ├─ metadata/                        # dbt metadata capture
│  │  │  ├─ manifest.go                   # dbt manifest processing
│  │  │  ├─ lineage.go                    # Model dependency extraction
│  │  │  └─ tests.go                      # Test result integration
│  │  └─ ci/                              # CI/CD integration
│  │     ├─ gates.go                      # Policy violation blocking
│  │     └─ semantic_deltas.go            # Semantic change detection
│  ├─ activation/                         # NEW: reverse-ETL gateway
│  │  ├─ gateway.go                       # HTTP proxy with enforcement
│  │  ├─ enforcement.go                   # All enforcement primitives
│  │  ├─ hightouch.go                     # Hightouch integration
│  │  ├─ rudderstack.go                   # RudderStack integration
│  │  └─ census.go                        # Census integration
│  ├─ bridges/                            # NEW: Enterprise integration bridges
│  │  ├─ servicenow/                      # ServiceNow ticket creation
│  │  │  ├─ client.go                     # ServiceNow REST client
│  │  │  ├─ formatter.go                  # Ticket formatting
│  │  │  ├─ templates/                    # Ticket templates
│  │  │  └─ export.sh                     # OSS stub script
│  │  ├─ jira/                            # Jira integration
│  │  │  ├─ client.go                     # Atlassian SDK wrapper
│  │  │  ├─ formatter.go                  # Issue formatting
│  │  │  └─ export.sh                     # OSS stub script
│  │  └─ README.md                        # Integration guide
│  ├─ badge/                              # NEW: Certification badge service
│  │  ├─ service/                         # Badge issuance service
│  │  │  ├─ issuer.go                     # Badge generation
│  │  │  ├─ verifier.go                   # Badge verification
│  │  │  └─ registry.go                   # Project registry
│  │  ├─ templates/                       # Badge SVG templates
│  │  ├─ cdn/                             # CDN configuration
│  │  └─ examples/                        # README integration examples
│  ├─ review/                             # NEW: Review SKU components
│  │  ├─ listener/                        # Webhook/log listeners
│  │  │  ├─ dbt_cloud.go                  # dbt Cloud webhook parser
│  │  │  ├─ dbt_core.go                   # dbt Core log tailer
│  │  │  └─ airflow.go                    # Airflow listener
│  │  ├─ daily_review/                    # Daily rollup reports
│  │  └─ attestation/                     # Attestation generation
│  ├─ gate/                               # NEW: Gate SKU components
│  │  ├─ enforcement/                     # Policy enforcement
│  │  ├─ primitives/                      # Idempotency, velocity, etc.
│  │  └─ policies/                        # Policy templates
│  ├─ genai/                              # NEW: GenAI security framework
│  │  ├─ detectors/                       # Built-in and external detectors
│  │  │  ├─ prompt_injection.go           # Prompt injection heuristics
│  │  │  ├─ deepfake.go                   # External deepfake API integration
│  │  │  ├─ bec.go                        # BEC detection and classification
│  │  │  └─ reflex_loop.go                # Prompt loop/reflex chain detection
│  │  ├─ threats/                         # Threat classification and response
│  │  │  ├─ classifier.go                 # OWASP LLM + MITRE ATT&CK mapping
│  │  │  ├─ response.go                   # Threat response automation
│  │  │  └─ correlation.go                # Cross-event threat correlation
│  │  ├─ security/                        # Enhanced security primitives
│  │  │  ├─ approval_bec.go               # BEC-grade approval certificates
│  │  │  ├─ sso_binding.go                # SSO identity binding
│  │  │  └─ challenge_response.go         # Challenge-response mechanisms
│  │  └─ shadow/                          # Shadow mode for threat detection
│  │     ├─ parallel_eval.go              # Parallel policy evaluation
│  │     └─ verdict_correlation.go        # Shadow verdict logging
│  ├─ voice/                              # NEW: voice/conversation compliance
│  │  ├─ session/                         # Voice session management
│  │  │  ├─ manager.go                    # Session tracking and correlation
│  │  │  ├─ metadata.go                   # Session metadata capture
│  │  │  └─ privacy.go                    # Privacy-preserving session handling
│  │  ├─ compliance/                      # TCPA compliance
│  │  │  ├─ disclaimer.go                 # Disclaimer enforcement
│  │  │  ├─ consent.go                    # Consent tracking and validation
│  │  │  └─ barge_in.go                   # Human interruption capability
│  │  └─ correlation/                     # Partner system correlation
│  │     ├─ ucaas.go                      # UCaaS integration (Teams, Zoom, etc.)
│  │     ├─ sip.go                        # SIP gateway integration
│  │     └─ webrtc.go                     # WebRTC session correlation
│  ├─ cicd/                               # NEW: CI/CD enforcement and integration
│  │  ├─ github/                          # GitHub Actions integration
│  │  │  ├─ actions.go                    # GitHub Actions automation
│  │  │  ├─ policy_gates.go               # Policy violation blocking
│  │  │  └─ badge_generation.go           # "Evidence Verified" badge generation
│  │  ├─ change_control/                  # SOX ITGC change control
│  │  │  ├─ commit_binding.go             # Approval certificates bound to commits
│  │  │  ├─ sox_tracking.go               # "Who/what/when" tracking
│  │  │  └─ segregation.go                # Segregation of duties enforcement
│  │  └─ deployment/                      # Deployment controls
│  │     ├─ rate_limiting.go              # Deploy rate limiting
│  │     ├─ approval_required.go          # Deploy approval workflows
│  │     └─ rollback.go                   # Automated rollback capabilities
│  ├─ policy/                             # Enhanced unified policy engine
│  │  ├─ loader.go                        # Enhanced with data platform sections
│  │  ├─ kill_switch.go                   # Multi-trigger kill-switch
│  │  ├─ cost_caps.go                     # Cost and resource caps
│  │  ├─ threat_map.go                    # OWASP LLM + MITRE ATT&CK mapping
│  │  ├─ data_platform.go                # NEW: data platform policy section
│  │  ├─ genai_security.go                # NEW: GenAI security policy section
│  │  ├─ voice_compliance.go              # NEW: voice/conversation policy section
│  │  ├─ idempotency.go                   # Enhanced idempotency policies
│  │  ├─ approvals.go                     # Enhanced approval certificate policies
│  │  ├─ ratelimits.go                    # Enhanced rate limiting policies
│  │  ├─ fences.go                        # Enhanced tenant fence policies
│  │  └─ sqlguard.go                      # SQL safety guard policies
│  ├─ lineage/                            # Enhanced lineage processing
│  │  ├─ lineage.go                       # Lineage extraction and validation
│  │  ├─ data_lineage.go                  # NEW: data platform lineage
│  │  └─ correlation.go                   # Cross-system lineage correlation
│  ├─ snapshot/                           # Enhanced recorder with warehouse anchoring
│  │  ├─ snapshot.go                      # Enhanced with metadata-only capture
│  │  ├─ manifest.go                      # Enhanced with warehouse anchors
│  │  ├─ warehouse_snapshot.go            # NEW: warehouse-specific snapshots
│  │  ├─ metadata_only.go                 # NEW: metadata-only capture strategy
│  │  └─ errors.go                        # Enhanced error handling and codes
│  ├─ diff/                               # Enhanced deterministic diff
│  │  ├─ diff.go                          # Enhanced diff algorithms
│  │  ├─ semantic_diff.go                 # NEW: semantic change detection
│  │  └─ data_diff.go                     # NEW: data-specific diff handling
│  ├─ replay/                             # Enhanced replay with data support
│  │  ├─ replay.go                        # Enhanced deterministic replay
│  │  ├─ data_replay.go                   # NEW: data platform replay capabilities
│  │  ├─ schema_replay.go                 # NEW: schema change replay
│  │  ├─ isolation.go                     # Scratch schema isolation
│  │  ├─ denylist.go                      # Network deny list for replay safety
│  │  └─ certificate.go                   # Replay certificate generation
│  ├─ bundle/                             # Enhanced unified DEF/PEF bundle builder
│  │  ├─ canonical.go                     # Enhanced JSON canonicalization
│  │  ├─ merkle.go                        # Merkle tree integrity
│  │  ├─ externalization.go               # External artifact handling
│  │  ├─ def_builder.go                   # NEW: Data Evidence Format builder
│  │  ├─ pef_builder.go                   # Enhanced Portable Evidence Format builder
│  │  ├─ unified_builder.go               # NEW: unified DEF/PEF builder
│  │  ├─ performance_metrics.go           # Enhanced performance and security metrics
│  │  └─ governance_metadata.go           # NEW: governance pillar embedding
│  ├─ crypto/                             # Enhanced cryptographic operations
│  │  ├─ signature.go                     # Enhanced multi-algorithm support
│  │  ├─ kms/                             # NEW: KMS integration
│  │  │  ├─ aws_kms.go                    # AWS KMS integration
│  │  │  ├─ azure_keyvault.go             # Azure Key Vault integration
│  │  │  └─ hashicorp_vault.go            # HashiCorp Vault integration
│  │  ├─ jcs.go                           # NEW: RFC 8785 JSON Canonicalization Scheme
│  │  ├─ hash_chain.go                    # Enhanced hash chaining
│  │  └─ integrity.go                     # Bundle integrity verification
│  ├─ siem/                               # NEW: SIEM integration
│  │  ├─ ndjson.go                        # Enhanced ECS/OCSF NDJSON generation
│  │  ├─ correlation.go                   # Cross-system event correlation
│  │  ├─ splunk.go                        # Splunk-specific formatting
│  │  ├─ datadog.go                       # Datadog-specific formatting
│  │  └─ elastic.go                       # Elasticsearch/ELK formatting
│  ├─ storage/                            # NEW: evidence storage management
│  │  ├─ worm.go                          # WORM storage integration
│  │  ├─ retention.go                     # Compliance-driven retention policies
│  │  ├─ s3_object_lock.go               # S3 Object Lock integration
│  │  └─ azure_immutable.go               # Azure immutable storage integration
│  ├─ telemetry/                          # NEW: 15-Factor telemetry
│  │  ├─ otel.go                          # OpenTelemetry integration
│  │  ├─ metrics.go                       # Business/security/performance metrics
│  │  ├─ traces.go                        # Distributed tracing
│  │  └─ correlation.go                   # Correlation ID management
│  ├─ performance/                        # NEW: performance monitoring and SLA enforcement
│  │  ├─ sla_monitor.go                   # SLA monitoring and enforcement
│  │  ├─ budgets.go                       # Performance budget tracking
│  │  └─ circuit_breaker.go               # Circuit breaker implementation
│  ├─ shadow/                             # NEW: shadow mode implementation
│  │  ├─ parallel_eval.go                 # Parallel policy evaluation
│  │  ├─ verdict_logging.go               # Shadow verdict capture
│  │  └─ correlation.go                   # Shadow/live correlation
│  ├─ killswitch/                         # NEW: enhanced kill-switch system
│  │  ├─ multi_trigger.go                 # Multi-trigger kill-switch
│  │  ├─ data_triggers.go                 # Data platform specific triggers
│  │  ├─ genai_triggers.go                # GenAI security triggers
│  │  ├─ recovery.go                      # Recovery mechanisms
│  │  └─ notification.go                  # Kill-switch notification system
│  ├─ cli/                                # CLI helper utilities
│  │  ├─ common.go                        # Common CLI utilities
│  │  ├─ output_format.go                 # Output formatting helpers
│  │  └─ progress.go                      # Progress indication
│  └─ pr-agent/                           # Custom PR review agent integration
│     └─ client.go                        # PR agent client implementation
│
```

---

## **Enhanced Templates (v4.0)**

```
├─ templates/                             # Enhanced scaffold templates
│  ├─ policy/                             # Policy templates
│  │  ├─ minimal.policy.yaml              # Basic policy template
│  │  ├─ data_platform.policy.yaml        # NEW: data platform focused policy
│  │  ├─ genai_security.policy.yaml       # NEW: GenAI security focused policy
│  │  ├─ voice_compliance.policy.yaml     # NEW: voice/conversation compliance
│  │  ├─ retail.policy.yaml               # Enhanced retail service pack policy
│  │  ├─ finserv.policy.yaml              # Enhanced financial services policy
│  │  ├─ travel.policy.yaml               # Enhanced travel/hospitality policy
│  │  ├─ etl.policy.yaml                  # Enhanced ETL/data pipeline policy
│  │  ├─ sox_itgc.overlay.yaml           # NEW: SOX ITGC compliance overlay
│  │  ├─ pci_hipaa.overlay.yaml          # Enhanced PCI/HIPAA overlays
│  │  ├─ eu_ai_act.overlay.yaml          # NEW: EU AI Act compliance overlay
│  │  └─ nist_rmf.overlay.yaml           # NEW: NIST AI RMF overlay
│  ├─ schemas/                            # Schema templates
│  │  ├─ skeleton.json                    # Basic schema skeleton
│  │  ├─ data_platform/                   # NEW: data platform schemas
│  │  │  ├─ dbt_model_change.json
│  │  │  ├─ schema_migration.json
│  │  │  └─ activation_sync.json
│  │  ├─ genai_security/                  # NEW: GenAI security schemas
│  │  │  ├─ prompt_validation.json
│  │  │  ├─ bec_detection.json
│  │  │  └─ deepfake_analysis.json
│  │  ├─ voice_compliance/                # NEW: voice compliance schemas
│  │  │  ├─ voice_session.json
│  │  │  ├─ disclaimer_tracking.json
│  │  │  └─ consent_management.json
│  │  ├─ retail/                          # Enhanced retail schemas
│  │  │  ├─ order_update.json
│  │  │  ├─ refund_request.json
│  │  │  ├─ address_change.json
│  │  │  └─ rma_create.json
│  │  ├─ finserv/                         # Enhanced financial services schemas
│  │  │  ├─ case_update.json
│  │  │  ├─ account_note_add.json
│  │  │  └─ limit_adjust_request.json
│  │  └─ travel/                          # Enhanced travel schemas
│  │     ├─ booking_change.json
│  │     ├─ loyalty_update.json
│  │     └─ invoice_issue.json
│  └─ projects/                           # NEW: project initialization templates
│     ├─ dbt/                             # dbt project templates
│     │  ├─ dbt_project.yml
│     │  ├─ packages.yml
│     │  └─ macros/
│     │     └─ clyra_guards.sql
│     ├─ python/                          # Python project templates
│     │  ├─ pyproject.toml
│     │  ├─ requirements.txt
│     │  └─ main.py
│     └─ typescript/                      # TypeScript project templates
│        ├─ package.json
│        ├─ tsconfig.json
│        └─ src/
│           └─ index.ts
│
```

---

## **Enhanced Verifier Ecosystem**

```
├─ verifier/                              # Independent verification ecosystem
│  ├─ go/                                 # Primary Go verifier
│  │  ├─ go.mod                           # Independent module
│  │  ├─ cmd/
│  │  │  ├─ def-verify/                   # NEW: Data Evidence Format verifier
│  │  │  │  └─ main.go
│  │  │  └─ pef-verify/                   # Enhanced Portable Evidence Format verifier
│  │  │     └─ main.go
│  │  ├─ pkg/
│  │  │  ├─ verifier/                     # Core verification logic
│  │  │  │  ├─ verifier.go
│  │  │  │  ├─ def_verifier.go            # NEW: DEF verification
│  │  │  │  ├─ pef_verifier.go            # Enhanced PEF verification
│  │  │  │  └─ crypto_verifier.go         # Enhanced cryptographic verification
│  │  │  ├─ lineage/                      # NEW: lineage validation
│  │  │  │  ├─ data_lineage.go
│  │  │  │  └─ warehouse_validation.go
│  │  │  └─ compliance/                   # NEW: compliance framework validation
│  │  │     ├─ sox_validator.go
│  │  │     ├─ pci_validator.go
│  │  │     ├─ hipaa_validator.go
│  │  │     └─ eu_ai_act_validator.go
│  │  └─ tests/                           # Comprehensive test suite
│  │     ├─ golden_vectors_test.go
│  │     ├─ def_validation_test.go
│  │     └─ pef_validation_test.go
│  └─ typescript/                         # Secondary TypeScript verifier
│     ├─ package.json                     # Independent npm package
│     ├─ tsconfig.json
│     ├─ src/
│     │  ├─ index.ts                      # Main verifier entry point
│     │  ├─ def-verifier.ts               # NEW: DEF verification
│     │  ├─ pef-verifier.ts               # Enhanced PEF verification
│     │  ├─ crypto/                       # Cryptographic verification
│     │  │  ├─ signatures.ts
│     │  │  └─ merkle.ts
│     │  ├─ lineage/                      # NEW: lineage validation
│     │  │  └─ validator.ts
│     │  └─ compliance/                   # NEW: compliance validation
│     │     ├─ sox.ts
│     │     ├─ pci.ts
│     │     ├─ hipaa.ts
│     │     └─ eu-ai-act.ts
│     ├─ tests/                           # Test suite
│     │  ├─ golden-vectors.test.ts
│     │  ├─ def-validation.test.ts
│     │  └─ pef-validation.test.ts
│     └─ bin/                             # CLI executables
│        ├─ def-verify
│        └─ pef-verify
│
```

---

## **Enhanced SDK (v4.0)**

```
├─ sdk/                                   # SDK implementations
│  ├─ python/                             # Enhanced Python SDK (primary)
│  │  ├─ pyproject.toml                   # Python 3.13, enhanced dependencies
│  │  ├─ clyra_sdk/
│  │  │  ├─ __init__.py
│  │  │  ├─ headers.py                    # Enhanced header management
│  │  │  ├─ decorators.py                 # Enhanced decorators with GenAI support
│  │  │  ├─ litellm_middleware.py         # Enhanced LiteLLM middleware
│  │  │  ├─ dbt/                          # NEW: dbt integration helpers
│  │  │  │  ├─ __init__.py
│  │  │  │  ├─ hooks.py                   # dbt hook helpers
│  │  │  │  ├─ macros.py                  # SQL macro helpers
│  │  │  │  └─ metadata.py                # Metadata extraction helpers
│  │  │  ├─ warehouse/                    # NEW: warehouse integration helpers
│  │  │  │  ├─ __init__.py
│  │  │  │  ├─ snowflake.py               # Snowflake integration
│  │  │  │  ├─ databricks.py              # Databricks integration
│  │  │  │  └─ postgres.py                # PostgreSQL integration
│  │  │  ├─ genai/                        # NEW: GenAI security helpers
│  │  │  │  ├─ __init__.py
│  │  │  │  ├─ detectors.py               # Threat detection helpers
│  │  │  │  ├─ bec.py                     # BEC protection helpers
│  │  │  │  └─ approval.py                # BEC-grade approval helpers
│  │  │  ├─ voice/                        # NEW: voice compliance helpers
│  │  │  │  ├─ __init__.py
│  │  │  │  ├─ session.py                 # Voice session management
│  │  │  │  ├─ compliance.py              # TCPA compliance helpers
│  │  │  │  └─ correlation.py             # UCaaS correlation helpers
│  │  │  ├─ retry.py                      # Enhanced retry with backoff
│  │  │  ├─ evidence.py                   # Evidence bundle helpers
│  │  │  └─ compliance.py                 # Compliance framework helpers
│  │  ├─ tests/                           # Comprehensive test suite
│  │  │  ├─ test_headers.py
│  │  │  ├─ test_decorators.py
│  │  │  ├─ test_dbt_integration.py       # NEW
│  │  │  ├─ test_warehouse_integration.py # NEW
│  │  │  ├─ test_genai_security.py        # NEW
│  │  │  └─ test_voice_compliance.py      # NEW
│  │  └─ examples/                        # Usage examples
│  │     ├─ basic_usage.py
│  │     ├─ dbt_project_example.py        # NEW
│  │     ├─ warehouse_integration.py      # NEW
│  │     ├─ genai_security_example.py     # NEW
│  │     └─ voice_compliance_example.py   # NEW
│  └─ typescript/                         # NEW: TypeScript SDK (Phase 1.5)
│     ├─ package.json                     # TypeScript SDK package
│     ├─ tsconfig.json
│     ├─ src/
│     │  ├─ index.ts
│     │  ├─ headers.ts
│     │  ├─ decorators.ts
│     │  ├─ genai/                        # GenAI integration
│     │  │  ├─ detectors.ts
│     │  │  └─ approval.ts
│     │  └─ voice/                        # Voice integration
│     │     ├─ session.ts
│     │     └─ compliance.ts
│     ├─ tests/                           # Test suite
│     └─ examples/                        # Usage examples
│
```

---

## **Enhanced Specifications (v4.0)**

```
├─ spec/                                  # Enhanced specifications
│  ├─ def/                                # NEW: Data Evidence Format (DEF v0)
│  │  ├─ SPEC.md                          # DEF specification document
│  │  ├─ VERSIONING.md                    # DEF versioning strategy
│  │  ├─ schemas/                         # DEF JSON schemas
│  │  │  ├─ def_manifest.json             # DEF manifest schema
│  │  │  ├─ data_receipt.json             # Data operation receipt
│  │  │  ├─ warehouse_anchor.json         # Warehouse anchoring schema
│  │  │  ├─ semantic_delta.json           # Schema/semantic change tracking
│  │  │  ├─ dbt_metadata.json             # dbt-specific metadata
│  │  │  ├─ lineage_graph.json            # Data lineage representation
│  │  │  └─ attestation_sox.json          # SOX ITGC attestation
│  │  └─ test-vectors/                    # DEF test vectors
│  │     ├─ valid/                        # Valid DEF bundles
│  │     │  ├─ dbt_run_success.zip
│  │     │  ├─ schema_migration_ok.zip
│  │     │  ├─ activation_sync_ok.zip
│  │     │  └─ warehouse_anchor_ok.zip
│  │     ├─ forged/                       # Forged/invalid DEF bundles
│  │     │  ├─ schema_change_unapproved.zip
│  │     │  └─ warehouse_anchor_mismatch.zip
│  │     └─ negative/                     # Negative test cases
│  │        ├─ dbt_test_failures.zip
│  │        ├─ semantic_delta_violation.zip
│  │        └─ sql_safety_violation.zip
│  ├─ pef/                                # Enhanced Portable Evidence Format (PEF v0)
│  │  ├─ SPEC.md                          # Enhanced PEF specification
│  │  ├─ VERSIONING.md                    # Enhanced versioning strategy
│  │  ├─ schemas/                         # Enhanced PEF schemas
│  │  │  ├─ manifest.json                 # Enhanced manifest with governance metadata
│  │  │  ├─ receipt.json                  # Enhanced receipt with GenAI fields
│  │  │  ├─ replay_certificate.json       # Enhanced replay certificates
│  │  │  ├─ daily_review.json             # Enhanced daily review with GenAI threats
│  │  │  ├─ approval_certificate.json     # Enhanced BEC-grade approval certificates
│  │  │  ├─ voice_session.json            # NEW: voice session schema
│  │  │  ├─ genai_threat.json             # NEW: GenAI threat classification
│  │  │  ├─ bec_detection.json            # NEW: BEC detection result
│  │  │  ├─ journal_event.json            # Enhanced ECS/OCSF event mapping
│  │  │  └─ attestation.json              # Enhanced multi-framework attestation
│  │  └─ test-vectors/                    # Enhanced PEF test vectors
│  │     ├─ valid/                        # Valid test cases
│  │     │  ├─ genai_security_ok.zip      # NEW: GenAI security success
│  │     │  ├─ voice_compliance_ok.zip    # NEW: voice compliance success
│  │     │  ├─ bec_approval_ok.zip        # NEW: BEC approval success
│  │     │  ├─ idempotency_ok.zip
│  │     │  ├─ approval_cert_ok.zip
│  │     │  ├─ velocity_ok.zip
│  │     │  └─ fences_ok.zip
│  │     ├─ forged/                       # Forged/tampered bundles
│  │     │  ├─ genai_threat_forged.zip    # NEW: forged GenAI threat data
│  │     │  ├─ bec_approval_forged.zip    # NEW: forged BEC approval
│  │     │  ├─ voice_session_forged.zip   # NEW: forged voice session
│  │     │  ├─ approval_cert_mismatch.zip
│  │     │  └─ cross_tenant.zip
│  │     └─ negative/                     # Negative test cases
│  │        ├─ genai_injection_blocked.zip # NEW: blocked prompt injection
│  │        ├─ deepfake_detected.zip      # NEW: deepfake detection
│  │        ├─ voice_disclaimer_failed.zip # NEW: voice compliance failure
│  │        ├─ duplicate_idempotency.zip
│  │        ├─ rate_limit_burst.zip
│  │        └─ sql_mass_update.zip
│  ├─ policy/                             # Enhanced policy specifications
│  │  ├─ SPEC.md                          # Policy specification document
│  │  ├─ schemas/                         # Policy schemas
│  │  │  ├─ policy_v4.schema.json         # Enhanced unified policy schema
│  │  │  ├─ data_platform.schema.json     # NEW: data platform policy section
│  │  │  ├─ genai_security.schema.json    # NEW: GenAI security policy section
│  │  │  ├─ voice_compliance.schema.json  # NEW: voice compliance policy section
│  │  │  ├─ enforcement.schema.json       # Enhanced enforcement primitives
│  │  │  └─ compliance.schema.json        # Enhanced compliance overlays
│  │  └─ examples/                        # Policy examples
│  │     ├─ minimal_policy.yaml
│  │     ├─ data_platform_policy.yaml     # NEW
│  │     ├─ genai_security_policy.yaml    # NEW
│  │     ├─ voice_compliance_policy.yaml  # NEW
│  │     └─ comprehensive_policy.yaml     # Full-featured example
│  ├─ compliance/                         # NEW: compliance framework specifications
│  │  ├─ sox_itgc/                        # SOX ITGC compliance mapping
│  │  │  ├─ SPEC.md
│  │  │  ├─ control_mapping.json
│  │  │  └─ evidence_requirements.json
│  │  ├─ pci_dss/                         # PCI DSS compliance mapping
│  │  │  ├─ SPEC.md
│  │  │  ├─ requirement_mapping.json
│  │  │  └─ audit_procedures.json
│  │  ├─ hipaa/                           # HIPAA compliance mapping
│  │  │  ├─ SPEC.md
│  │  │  ├─ safeguard_mapping.json
│  │  │  └─ audit_requirements.json
│  │  ├─ eu_ai_act/                       # EU AI Act compliance mapping
│  │  │  ├─ SPEC.md
│  │  │  ├─ article_12_mapping.json
│  │  │  └─ high_risk_requirements.json
│  │  └─ nist_ai_rmf/                     # NIST AI RMF mapping
│  │     ├─ SPEC.md
│  │     ├─ function_mapping.json
│  │     └─ outcome_requirements.json
│  ├─ api/                                # NEW: API specifications
│  │  ├─ openapi.yaml                     # OpenAPI 3.0 specification
│  │  ├─ data_platform_api.yaml           # Data platform API specification
│  │  ├─ genai_security_api.yaml          # GenAI security API specification
│  │  └─ voice_compliance_api.yaml        # Voice compliance API specification
│  └─ common/                             # Common/shared specifications
│     ├─ schemas/                         # Shared schemas
│     │  ├─ base_types.json               # Common type definitions
│     │  ├─ cryptographic.json            # Cryptographic structures
│     │  ├─ temporal.json                 # Time and date structures
│     │  └─ governance.json               # Governance metadata structures
│     └─ test-vectors/                    # Common test vectors
│        ├─ cryptographic/                # Cryptographic test vectors
│        ├─ canonicalization/             # JSON canonicalization tests
│        └─ temporal/                     # Time/date handling tests
│
```

---

## **Enhanced Scenario & Service Packs (v4.0)**

```
├─ packs/                                 # Enhanced scenario and service packs
│  ├─ data/                               # NEW: data platform packs
│  │  ├─ dbt_demo/                        # dbt demonstration pack
│  │  │  ├─ schemas/                      # dbt model schemas
│  │  │  ├─ policies/                     # dbt-specific policies
│  │  │  ├─ fixtures/                     # Sample dbt projects
│  │  │  ├─ goldens/                      # Golden DEF bundles
│  │  │  ├─ README.md
│  │  │  └─ pack.yaml
│  │  ├─ etl_pipeline/                    # ETL pipeline demonstration pack
│  │  │  ├─ schemas/                      # ETL operation schemas
│  │  │  ├─ policies/                     # ETL-specific policies
│  │  │  ├─ fixtures/                     # Sample ETL workflows
│  │  │  ├─ goldens/                      # Golden DEF bundles
│  │  │  ├─ README.md
│  │  │  └─ pack.yaml
│  │  └─ activation_demo/                 # Reverse-ETL/activation demonstration
│  │     ├─ schemas/                      # Activation operation schemas
│  │     ├─ policies/                     # Activation-specific policies
│  │     ├─ fixtures/                     # Sample activation flows
│  │     ├─ goldens/                      # Golden DEF bundles
│  │     ├─ README.md
│  │     └─ pack.yaml
│  ├─ contracts/                          # Enhanced contracts scenario pack
│  │  ├─ schemas/                         # Contract operation schemas
│  │  ├─ policies/                        # Enhanced with GenAI security
│  │  ├─ fixtures/                        # Sample contracts
│  │  ├─ goldens/                         # Enhanced golden bundles
│  │  ├─ README.md
│  │  └─ pack.yaml
│  ├─ ap_ar/                              # Enhanced AP/AR scenario pack
│  │  ├─ schemas/                         # AP/AR operation schemas
│  │  ├─ policies/                        # Enhanced financial controls
│  │  ├─ fixtures/                        # Sample AP/AR operations
│  │  ├─ goldens/                         # Enhanced golden bundles
│  │  ├─ README.md
│  │  └─ pack.yaml
│  ├─ etl/                                # Enhanced ETL scenario pack
│  │  ├─ schemas/                         # ETL operation schemas
│  │  ├─ policies/                        # Enhanced data governance
│  │  ├─ fixtures/                        # Sample ETL workflows
│  │  ├─ goldens/                         # Enhanced golden bundles
│  │  ├─ README.md
│  │  └─ pack.yaml
│  ├─ rpa/                                # Enhanced RPA scenario pack
│  │  ├─ schemas/                         # RPA operation schemas
│  │  ├─ policies/                        # Enhanced automation governance
│  │  ├─ fixtures/                        # Sample RPA workflows
│  │  ├─ goldens/                         # Enhanced golden bundles
│  │  ├─ README.md
│  │  └─ pack.yaml
│  └─ service/                            # Enhanced service packs (industry-specific)
│     ├─ retail/                          # Enhanced retail service pack
│     │  ├─ schemas/                      # Retail-specific schemas
│     │  │  ├─ order_update.json          # Enhanced order update schema
│     │  │  ├─ refund_request.json        # Enhanced refund schema
│     │  │  ├─ rma_create.json            # RMA creation schema
│     │  │  └─ address_change.json        # Address change schema
│     │  ├─ policies/                     # Retail-specific policies
│     │  │  ├─ pci_compliance.yaml        # PCI compliance policy
│     │  │  ├─ pii_protection.yaml        # PII protection policy
│     │  │  └─ hitl_defaults.yaml         # HITL workflow defaults
│     │  ├─ fixtures/                     # Retail scenario fixtures
│     │  ├─ goldens/                      # Retail golden bundles
│     │  ├─ README.md
│     │  └─ pack.yaml
│     ├─ finserv/                         # Enhanced financial services pack
│     │  ├─ schemas/                      # FinServ-specific schemas
│     │  │  ├─ case_update.json           # Case update schema
│     │  │  ├─ account_note_add.json      # Account note schema
│     │  │  └─ limit_adjust_request.json  # Credit limit adjustment
│     │  ├─ policies/                     # FinServ-specific policies
│     │  │  ├─ strict_approval.yaml       # Strict approval requirements
│     │  │  ├─ sox_compliance.yaml        # SOX compliance policy
│     │  │  └─ fraud_prevention.yaml      # Fraud prevention policy
│     │  ├─ fixtures/                     # FinServ scenario fixtures
│     │  ├─ goldens/                      # FinServ golden bundles
│     │  ├─ README.md
│     │  └─ pack.yaml
│     └─ travel/                          # Enhanced travel/hospitality pack
│        ├─ schemas/                      # Travel-specific schemas
│        │  ├─ booking_change.json        # Booking modification schema
│        │  ├─ loyalty_update.json        # Loyalty program schema
│        │  └─ invoice_issue.json         # Invoice generation schema
│        ├─ policies/                     # Travel-specific policies
│        │  ├─ booking_controls.yaml      # Booking change controls
│        │  ├─ pii_privacy.yaml          # Privacy protection policy
│        │  └─ hitl_workflows.yaml       # HITL workflow requirements
│        ├─ fixtures/                     # Travel scenario fixtures
│        ├─ goldens/                      # Travel golden bundles
│        ├─ README.md
│        └─ pack.yaml
│
```

---

## **Enhanced Procurement Kit (v4.0)**

```
├─ kits/
│  └─ procurement/                        # Enhanced procurement materials
│     ├─ evidence/                        # NEW: organized sample evidence
│     │  ├─ data_platform/                # Data platform evidence samples
│     │  │  ├─ SAMPLE_EVIDENCE_DBT.zip
│     │  │  ├─ SAMPLE_EVIDENCE_WAREHOUSE.zip
│     │  │  └─ SAMPLE_EVIDENCE_ACTIVATION.zip
│     │  ├─ automation/                   # Automation evidence samples
│     │  │  ├─ SAMPLE_EVIDENCE_CONTRACTS.zip
│     │  │  ├─ SAMPLE_EVIDENCE_AP_AR.zip
│     │  │  ├─ SAMPLE_EVIDENCE_ETL.zip
│     │  │  └─ SAMPLE_EVIDENCE_RPA.zip
│     │  └─ industry/                     # Industry-specific evidence
│     │     ├─ SAMPLE_EVIDENCE_RETAIL.zip
│     │     ├─ SAMPLE_EVIDENCE_FINSERV.zip
│     │     └─ SAMPLE_EVIDENCE_TRAVEL.zip
│     ├─ attestations/                    # Sample attestations
│     │  ├─ data_platform/                # Data platform attestations
│     │  │  ├─ SAMPLE_ATTESTATION_SOX.pdf
│     │  │  ├─ SAMPLE_ATTESTATION_DBT.pdf
│     │  │  └─ SAMPLE_ATTESTATION_WAREHOUSE.pdf
│     │  ├─ automation/                   # Automation attestations
│     │  │  ├─ SAMPLE_ATTESTATION_CONTRACTS.pdf
│     │  │  ├─ SAMPLE_ATTESTATION_AP_AR.pdf
│     │  │  ├─ SAMPLE_ATTESTATION_ETL.pdf
│     │  │  └─ SAMPLE_ATTESTATION_RPA.pdf
│     │  ├─ compliance/                   # Compliance framework attestations
│     │  │  ├─ SAMPLE_ATTESTATION_PCI.pdf
│     │  │  ├─ SAMPLE_ATTESTATION_HIPAA.pdf
│     │  │  ├─ SAMPLE_ATTESTATION_EU_AI_ACT.pdf
│     │  │  └─ SAMPLE_ATTESTATION_NIST_RMF.pdf
│     │  └─ industry/                     # Industry-specific attestations
│     │     ├─ SAMPLE_ATTESTATION_RETAIL.pdf
│     │     ├─ SAMPLE_ATTESTATION_FINSERV.pdf
│     │     └─ SAMPLE_ATTESTATION_TRAVEL.pdf
│     ├─ documentation/                   # Enhanced documentation materials
│     │  ├─ buyer_guides/                 # Buyer guidance materials
│     │  │  ├─ data_platform_buyer_guide.md  # NEW: data platform buyer guide
│     │  │  ├─ genai_security_buyer_guide.md # NEW: GenAI security buyer guide
│     │  │  ├─ compliance_buyer_guide.md     # Enhanced compliance guide
│     │  │  └─ roi_calculator.md             # ROI calculation guidance
│     │  ├─ auditor_guides/               # Auditor guidance materials
│     │  │  ├─ verification_procedures.md    # Verification procedures
│     │  │  ├─ compliance_mapping.md         # Compliance framework mappings
│     │  │  ├─ evidence_validation.md        # Evidence validation guide
│     │  │  └─ independent_verifier.md       # Independent verifier guide
│     │  └─ implementation_guides/        # Implementation guidance
│     │     ├─ data_platform_implementation.md # NEW
│     │     ├─ genai_security_implementation.md # NEW
│     │     ├─ voice_compliance_implementation.md # NEW
│     │     └─ integration_patterns.md       # Integration patterns
│     ├─ technical/                       # Technical integration materials
│     │  ├─ kms_worm_guides.md            # Enhanced KMS and WORM guidance
│     │  ├─ siem_integration.md           # SIEM integration guide
│     │  ├─ api_reference.md              # API reference for procurement
│     │  └─ performance_benchmarks.md     # Performance benchmark data
│     ├─ legal/                           # NEW: legal and compliance materials
│     │  ├─ privacy_impact_assessment.md  # Privacy impact assessment
│     │  ├─ data_processing_agreement.md  # Data processing agreement template
│     │  ├─ compliance_certifications.md  # Compliance certification documentation
│     │  └─ audit_readiness_checklist.md  # Audit readiness checklist
│     └─ README.md                        # Enhanced procurement kit overview
│
```

---

## **Enhanced Examples & Integration (v4.0)**

```
├─ examples/                              # Enhanced integration examples
│  ├─ quickstart-compose/                 # Enhanced quickstart environment
│  │  ├─ docker-compose.yml               # Enhanced with data platform services
│  │  ├─ docker-compose.data.yml          # NEW: data platform specific services
│  │  ├─ docker-compose.genai.yml         # NEW: GenAI security services
│  │  ├─ seed.sql                         # Enhanced sample data
│  │  ├─ snowflake_setup.sql              # NEW: Snowflake setup examples
│  │  ├─ databricks_setup.py              # NEW: Databricks setup examples
│  │  └─ README.md
│  ├─ dbt-integration/                    # NEW: dbt integration examples
│  │  ├─ dbt_project.yml                  # Sample dbt project configuration
│  │  ├─ packages.yml                     # Clyra dbt package configuration
│  │  ├─ macros/                          # Clyra-specific macros
│  │  │  ├─ clyra_guards.sql              # SQL safety guard macros
│  │  │  └─ clyra_audit.sql               # Audit tracking macros
│  │  ├─ models/                          # Sample dbt models
│  │  │  ├─ staging/                      # Staging models
│  │  │  └─ marts/                        # Mart models
│  │  ├─ tests/                           # dbt tests with Clyra integration
│  │  ├─ hooks/                           # Clyra hook implementations
│  │  │  ├─ pre_run.py
│  │  │  └─ post_run.py
│  │  └─ README.md
│  ├─ warehouse-integration/              # NEW: warehouse integration examples
│  │  ├─ snowflake/                       # Snowflake integration examples
│  │  │  ├─ session_tags.sql              # Session tag examples
│  │  │  ├─ stored_procedures.sql         # Clyra guard procedures
│  │  │  ├─ resource_monitors.sql         # Resource monitor integration
│  │  │  └─ README.md
│  │  ├─ databricks/                      # Databricks integration examples
│  │  │  ├─ cluster_policies.json         # Cluster policy configurations
│  │  │  ├─ delta_integration.py          # Delta Lake integration
│  │  │  ├─ unity_catalog.py              # Unity Catalog integration
│  │  │  └─ README.md
│  │  └─ postgres/                        # PostgreSQL integration examples
│  │     ├─ wal_monitoring.sql            # WAL monitoring setup
│  │     ├─ guard_functions.sql           # SQL guard functions
│  │     └─ README.md
│  ├─ activation-flows/                   # NEW: activation/reverse-ETL examples
│  │  ├─ hightouch/                       # Hightouch integration
│  │  │  ├─ webhook_config.json
│  │  │  ├─ enforcement_setup.py
│  │  │  └─ README.md
│  │  ├─ rudderstack/                     # RudderStack integration
│  │  │  ├─ proxy_config.json
│  │  │  ├─ transformation_controls.js
│  │  │  └─ README.md
│  │  └─ census/                          # Census integration
│  │     ├─ sync_policies.yaml
│  │     ├─ audience_controls.py
│  │     └─ README.md
│  ├─ genai-security/                     # NEW: GenAI security examples
│  │  ├─ prompt_injection/                # Prompt injection examples
│  │  │  ├─ detection_examples.py
│  │  │  ├─ mitigation_strategies.py
│  │  │  └─ README.md
│  │  ├─ deepfake_detection/              # Deepfake detection examples
│  │  │  ├─ api_integration.py
│  │  │  ├─ webhook_handlers.py
│  │  │  └─ README.md
│  │  ├─ bec_prevention/                  # BEC prevention examples
│  │  │  ├─ approval_workflows.py
│  │  │  ├─ sso_integration.py
│  │  │  └─ README.md
│  │  └─ kill_switch/                     # Kill-switch examples
│  │     ├─ multi_trigger_setup.py
│  │     ├─ recovery_procedures.py
│  │     └─ README.md
│  ├─ voice-compliance/                   # NEW: voice compliance examples
│  │  ├─ tcpa_compliance/                 # TCPA compliance examples
│  │  │  ├─ disclaimer_management.py
│  │  │  ├─ consent_tracking.py
│  │  │  └─ README.md
│  │  ├─ ucaas_integration/               # UCaaS integration examples
│  │  │  ├─ teams_integration.py
│  │  │  ├─ zoom_integration.py
│  │  │  ├─ slack_integration.py
│  │  │  └─ README.md
│  │  └─ session_correlation/             # Session correlation examples
│  │     ├─ voice_to_api.py
│  │     ├─ audit_trail_linking.py
│  │     └─ README.md
│  ├─ runtime-stubs/                      # Enhanced PLG runtime starters
│  │  ├─ python-fastapi/                  # Enhanced FastAPI starter
│  │  │  ├─ app.py                        # Enhanced with GenAI security
│  │  │  ├─ requirements.txt              # Updated dependencies
│  │  │  ├─ clyra_config.py               # Clyra configuration
│  │  │  └─ README.md
│  │  ├─ node-express/                    # Enhanced Express starter
│  │  │  ├─ server.js                     # Enhanced with middleware
│  │  │  ├─ package.json                  # Updated dependencies
│  │  │  ├─ clyra-middleware.js           # Clyra middleware
│  │  │  └─ README.md
│  │  ├─ go-chi/                          # Enhanced Go Chi starter
│  │  │  ├─ main.go                       # Enhanced with middleware
│  │  │  ├─ go.mod                        # Updated dependencies
│  │  │  ├─ clyra_middleware.go           # Clyra middleware
│  │  │  └─ README.md
│  │  └─ dbt-project/                     # NEW: dbt project starter
│  │     ├─ dbt_project.yml
│  │     ├─ packages.yml
│  │     ├─ profiles.yml.example
│  │     ├─ macros/
│  │     ├─ models/
│  │     └─ README.md
│  ├─ ci-cd-integration/                  # NEW: CI/CD integration examples
│  │  ├─ github-actions/                  # GitHub Actions integration
│  │  │  ├─ evidence-verification.yml
│  │  │  ├─ policy-gates.yml
│  │  │  ├─ sox-compliance.yml
│  │  │  └─ README.md
│  │  ├─ gitlab-ci/                       # GitLab CI integration
│  │  │  ├─ .gitlab-ci.yml
│  │  │  ├─ evidence-pipeline.yml
│  │  │  └─ README.md
│  │  └─ jenkins/                         # Jenkins integration
│  │     ├─ Jenkinsfile
│  │     ├─ pipeline-library/
│  │     └─ README.md
│  ├─ servicenow-integration/             # NEW: ServiceNow setup guide
│  │  ├─ docker-compose.yml               # Local ServiceNow simulator
│  │  ├─ ticket-template.json             # Ticket format
│  │  ├─ export.sh                        # OSS stub script
│  │  └─ README.md                        # Setup instructions
│  ├─ badge-setup/                        # NEW: Badge integration
│  │  ├─ dbt_project.yml                 # Badge configuration
│  │  ├─ README.template.md               # Badge in README
│  │  ├─ ci-integration.yml               # CI/CD badge updates
│  │  └─ README.md                        # Setup guide
│  ├─ review-quickstart/                  # NEW: Listen-only demo
│  │  ├─ webhook-setup.sh                 # Webhook configuration
│  │  ├─ first-review.md                  # First daily review
│  │  ├─ progression-guide.md             # Review → Gate path
│  │  └─ README.md                        # Setup guide
│  ├─ compliance-frameworks/              # NEW: compliance framework examples
│  │  ├─ sox-itgc/                        # SOX ITGC examples
│  │  │  ├─ change_control_workflow.py
│  │  │  ├─ segregation_of_duties.py
│  │  │  └─ README.md
│  │  ├─ pci-dss/                         # PCI DSS examples
│  │  │  ├─ daily_review_automation.py
│  │  │  ├─ access_control_evidence.py
│  │  │  └─ README.md
│  │  ├─ hipaa/                           # HIPAA examples
│  │  │  ├─ audit_controls.py
│  │  │  ├─ integrity_safeguards.py
│  │  │  └─ README.md
│  │  └─ eu-ai-act/                       # EU AI Act examples
│  │     ├─ risk_documentation.py
│  │     ├─ human_oversight.py
│  │     └─ README.md
│  ├─ siem-integration/                   # Enhanced SIEM integration examples
│  │  ├─ splunk/                          # Splunk integration
│  │  │  ├─ saved_searches.json           # Enhanced with GenAI queries
│  │  │  ├─ dashboards.json               # Sample dashboards
│  │  │  ├─ alert_correlation.json        # Alert correlation rules
│  │  │  └─ README.md
│  │  ├─ datadog/                         # Datadog integration
│  │  │  ├─ custom_metrics.py             # Custom metrics integration
│  │  │  ├─ log_aggregation.py            # Log aggregation setup
│  │  │  ├─ incident_management.py        # Incident management
│  │  │  └─ README.md
│  │  ├─ elastic/                         # Elasticsearch integration
│  │  │  ├─ index_templates.json          # Index templates
│  │  │  ├─ kibana_visualizations.json    # Kibana visualizations
│  │  │  ├─ watcher_alerts.json           # Watcher alerts
│  │  │  └─ README.md
│  │  └─ generic/                         # Generic SIEM integration
│  │     ├─ otel_forwarding.py            # OpenTelemetry forwarding
│  │     ├─ fluentbit_config.yaml         # Fluent Bit configuration
│  │     └─ README.md
│  ├─ litellm-recipe/                     # Enhanced LiteLLM integration
│  │  ├─ example.py                       # Enhanced with GenAI security
│  │  ├─ genai_security.py                # GenAI security integration
│  │  ├─ threat_detection.py              # Threat detection examples
│  │  └─ README.md
│  ├─ egress/                             # Network egress control examples
│  │  ├─ iptables_sidecar.md              # iptables configuration
│  │  ├─ envoy_filter.md                  # Envoy proxy configuration
│  │  ├─ istio_policies.yaml              # Istio security policies
│  │  └─ README.md
│  └─ performance-monitoring/             # NEW: performance monitoring examples
│     ├─ k6/                              # k6 performance testing
│     │  ├─ data_platform_tests.js        # Data platform performance tests
│     │  ├─ genai_security_tests.js       # GenAI security performance tests
│     │  ├─ voice_compliance_tests.js     # Voice compliance performance tests
│     │  └─ README.md
│     ├─ otel/                            # OpenTelemetry integration
│     │  ├─ collector_config.yaml         # Collector configuration
│     │  ├─ traces_config.py              # Traces configuration
│     │  └─ README.md
│     └─ sla-monitoring/                  # SLA monitoring examples
│        ├─ sla_definitions.yaml          # SLA definitions
│        ├─ monitoring_setup.py           # Monitoring setup
│        └─ README.md
│
```

---

## **Enhanced Documentation (v4.0)**

```
├─ docs/                                  # Comprehensive documentation
│  ├─ getting-started/                    # NEW: organized getting started guides
│  │  ├─ README.md                        # Getting started overview
│  │  ├─ data-platform-quickstart.md     # NEW: data platform focused quickstart
│  │  ├─ automation-quickstart.md        # Automation focused quickstart
│  │  ├─ genai-security-quickstart.md    # NEW: GenAI security quickstart
│  │  └─ voice-compliance-quickstart.md  # NEW: voice compliance quickstart
│  ├─ installation/                       # NEW: detailed installation guides
│  │  ├─ dev_setup_mac.md                 # Enhanced macOS setup (Go 1.25.x, Node 22.x, Python 3.13)
│  │  ├─ dev_setup_linux.md               # Enhanced Linux setup
│  │  ├─ dev_setup_windows.md             # NEW: Windows setup guide
│  │  ├─ docker_setup.md                  # Docker installation guide
│  │  └─ cloud_deployment.md              # Cloud deployment guide
│  ├─ architecture/                       # Enhanced architecture documentation
│  │  ├─ overview.md                      # Architecture overview
│  │  ├─ data_platform_architecture.md   # NEW: data platform architecture
│  │  ├─ genai_security_architecture.md  # NEW: GenAI security architecture
│  │  ├─ voice_compliance_architecture.md # NEW: voice compliance architecture
│  │  ├─ c4_models/                       # C4 model diagrams
│  │  │  ├─ context_diagram.md
│  │  │  ├─ container_diagram.md
│  │  │  ├─ component_diagram.md
│  │  │  └─ code_diagram.md
│  │  ├─ runtime_flows.md                 # Enhanced runtime flows
│  │  ├─ api_cli_reference.md             # Enhanced API and CLI reference
│  │  └─ adr/                             # Architecture Decision Records
│  │     ├─ README.md                     # ADR index
│  │     ├─ 001-database-support-matrix.md
│  │     ├─ 002-evidence-format-architecture.md
│  │     ├─ 003-snapshot-strategy.md
│  │     ├─ 004-replay-isolation.md
│  │     ├─ 005-enhanced-enforcement-primitives.md
│  │     ├─ 006-data-platform-integration.md # NEW
│  │     ├─ 007-genai-security-framework.md # NEW
│  │     ├─ 008-policy-engine-architecture.md
│  │     ├─ 009-attestation-framework.md
│  │     ├─ 010-voice-conversation-compliance.md # NEW
│  │     ├─ 011-cicd-enforcement.md       # NEW
│  │     ├─ 012-evidence-bundle-cryptography.md
│  │     ├─ 013-performance-reliability-slas.md
│  │     ├─ 014-siem-integration.md
│  │     ├─ 015-shadow-mode-killswitch.md
│  │     ├─ 016-15factor-compliance.md    # NEW
│  │     ├─ 017-independent-verifier-ecosystem.md
│  │     ├─ 018-data-platform-hybrid-architecture.md # NEW
│  │     ├─ 019-retention-archival-strategy.md
│  │     └─ 020-developer-experience-automation.md # NEW
│  ├─ data-platform/                      # NEW: data platform documentation
│  │  ├─ README.md                        # Data platform overview
│  │  ├─ dbt-integration.md               # dbt integration guide
│  │  ├─ warehouse-integration/           # Warehouse integration guides
│  │  │  ├─ snowflake.md                  # Snowflake integration
│  │  │  ├─ databricks.md                 # Databricks integration
│  │  │  ├─ postgres.md                   # PostgreSQL integration
│  │  │  └─ bigquery.md                   # BigQuery integration (Phase 1.5)
│  │  ├─ activation-gateway.md            # Activation gateway guide
│  │  ├─ sql-safety-guards.md             # SQL safety guard documentation
│  │  ├─ def-format.md                    # Data Evidence Format guide
│  │  ├─ sox-compliance.md                # SOX ITGC compliance guide
│  │  └─ lineage-tracking.md              # Data lineage tracking
│  ├─ genai-security/                     # NEW: GenAI security documentation
│  │  ├─ README.md                        # GenAI security overview
│  │  ├─ threat-detection/                # Threat detection guides
│  │  │  ├─ prompt-injection.md           # Prompt injection detection
│  │  │  ├─ deepfake-detection.md         # Deepfake detection
│  │  │  ├─ bec-prevention.md             # BEC prevention
│  │  │  └─ custom-detectors.md           # Custom detector development
│  │  ├─ bec-grade-approvals.md           # BEC-grade approval certificates
│  │  ├─ kill-switch.md                   # Enhanced kill-switch documentation
│  │  ├─ shadow-mode.md                   # Shadow mode documentation
│  │  ├─ owasp-llm-mapping.md            # OWASP LLM Top 10 mapping
│  │  ├─ mitre-attack-mapping.md         # MITRE ATT&CK mapping
│  │  └─ external-detector-integration.md # External detector integration
│  ├─ voice-compliance/                   # NEW: voice compliance documentation
│  │  ├─ README.md                        # Voice compliance overview
│  │  ├─ tcpa-compliance.md               # TCPA compliance guide
│  │  ├─ session-management.md            # Voice session management
│  │  ├─ disclaimer-enforcement.md        # Disclaimer enforcement
│  │  ├─ ucaas-integration/               # UCaaS integration guides
│  │  │  ├─ microsoft-teams.md
│  │  │  ├─ zoom.md
│  │  │  ├─ slack.md
│  │  │  └─ twilio-sip.md
│  │  ├─ barge-in-capability.md          # Human interruption capability
│  │  └─ privacy-preservation.md          # Privacy preservation techniques
│  ├─ compliance/                         # Enhanced compliance documentation
│  │  ├─ README.md                        # Compliance overview
│  │  ├─ frameworks/                      # Compliance frameworks
│  │  │  ├─ sox-itgc/                     # SOX ITGC compliance
│  │  │  │  ├─ overview.md
│  │  │  │  ├─ control-mapping.md
│  │  │  │  ├─ evidence-requirements.md
│  │  │  │  └─ implementation-guide.md
│  │  │  ├─ pci-dss/                      # PCI DSS compliance
│  │  │  │  ├─ overview.md
│  │  │  │  ├─ requirement-mapping.md
│  │  │  │  ├─ daily-review.md
│  │  │  │  └─ audit-procedures.md
│  │  │  ├─ hipaa/                        # HIPAA compliance
│  │  │  │  ├─ overview.md
│  │  │  │  ├─ safeguard-mapping.md
│  │  │  │  ├─ audit-controls.md
│  │  │  │  └─ privacy-requirements.md
│  │  │  ├─ eu-ai-act/                    # EU AI Act compliance
│  │  │  │  ├─ overview.md
│  │  │  │  ├─ article-12-requirements.md
│  │  │  │  ├─ high-risk-systems.md
│  │  │  │  └─ record-keeping.md
│  │  │  ├─ nist-ai-rmf/                  # NIST AI RMF
│  │  │  │  ├─ overview.md
│  │  │  │  ├─ function-mapping.md
│  │  │  │  ├─ risk-management.md
│  │  │  │  └─ governance.md
│  │  │  └─ tcpa/                         # TCPA compliance
│  │  │     ├─ overview.md
│  │  │     ├─ consent-requirements.md
│  │  │     ├─ disclaimer-requirements.md
│  │  │     └─ opt-out-mechanisms.md
│  │  ├─ attestation-generation.md        # Attestation generation guide
│  │  ├─ evidence-validation.md           # Evidence validation procedures
│  │  ├─ audit-readiness.md               # Audit readiness guide
│  │  └─ retention-policies.md            # Retention policy guidance
│  ├─ integration/                        # Integration documentation
│  │  ├─ README.md                        # Integration overview
│  │  ├─ sdk-guides/                      # SDK integration guides
│  │  │  ├─ python-sdk.md                 # Python SDK guide
│  │  │  └─ typescript-sdk.md             # TypeScript SDK guide
│  │  ├─ api-reference/                   # API reference documentation
│  │  │  ├─ data-platform-api.md          # Data platform API
│  │  │  ├─ genai-security-api.md         # GenAI security API
│  │  │  ├─ voice-compliance-api.md       # Voice compliance API
│  │  │  └─ universal-api.md              # Universal API reference
│  │  ├─ webhook-integration.md           # Webhook integration guide
│  │  ├─ siem-integration/                # SIEM integration guides
│  │  │  ├─ splunk-integration.md
│  │  │  ├─ datadog-integration.md
│  │  │  ├─ elastic-integration.md
│  │  │  └─ generic-siem.md
│  │  ├─ ci-cd-integration/               # CI/CD integration guides
│  │  │  ├─ github-actions.md
│  │  │  ├─ gitlab-ci.md
│  │  │  └─ jenkins.md
│  │  └─ cloud-platform/                  # Cloud platform integration
│  │     ├─ aws-integration.md
│  │     ├─ azure-integration.md
│  │     └─ gcp-integration.md
│  ├─ security/                           # Enhanced security documentation
│  │  ├─ README.md                        # Security overview
│  │  ├─ security-model.md                # Security model documentation
│  │  ├─ cryptographic-standards.md       # Cryptographic standards
│  │  ├─ threat-modeling.md               # Threat modeling documentation
│  │  ├─ zero-trust-architecture.md       # Zero-trust architecture
│  │  ├─ genai-security-hardening.md      # GenAI security hardening
│  │  ├─ bec-prevention.md                # BEC prevention strategies
│  │  ├─ secure-deployment.md             # Secure deployment practices
│  │  ├─ incident-response.md             # Incident response procedures
│  │  ├─ vulnerability-management.md      # Vulnerability management
│  │  └─ security-checklists/             # Security checklists
│  │     ├─ deployment-checklist.md
│  │     ├─ configuration-checklist.md
│  │     └─ monitoring-checklist.md
│  ├─ performance/                        # Enhanced performance documentation
│  │  ├─ README.md                        # Performance overview
│  │  ├─ sla-definitions.md               # SLA definitions and requirements
│  │  ├─ performance-benchmarks.md        # Performance benchmark data
│  │  ├─ optimization-guide.md            # Performance optimization guide
│  │  ├─ monitoring-setup.md              # Performance monitoring setup
│  │  ├─ troubleshooting.md               # Performance troubleshooting
│  │  └─ capacity-planning.md             # Capacity planning guide
│  ├─ operations/                         # Operations documentation
│  │  ├─ README.md                        # Operations overview
│  │  ├─ deployment/                      # Deployment guides
│  │  │  ├─ local-development.md
│  │  │  ├─ staging-deployment.md
│  │  │  ├─ production-deployment.md
│  │  │  └─ kubernetes-deployment.md
│  │  ├─ monitoring/                      # Monitoring guides
│  │  │  ├─ telemetry-setup.md
│  │  │  ├─ alerting-configuration.md
│  │  │  ├─ dashboard-setup.md
│  │  │  └─ log-management.md
│  │  ├─ maintenance/                     # Maintenance procedures
│  │  │  ├─ backup-procedures.md
│  │  │  ├─ update-procedures.md
│  │  │  ├─ key-rotation.md
│  │  │  └─ database-maintenance.md
│  │  ├─ troubleshooting/                 # Troubleshooting guides
│  │  │  ├─ common-issues.md
│  │  │  ├─ diagnostic-procedures.md
│  │  │  ├─ error-codes.md
│  │  │  └─ support-procedures.md
│  │  └─ runbooks/                        # Operational runbooks
│  │     ├─ incident-response.md
│  │     ├─ emergency-procedures.md
│  │     ├─ escalation-procedures.md
│  │     └─ recovery-procedures.md
│  ├─ development/                        # Development documentation
│  │  ├─ README.md                        # Development overview
│  │  ├─ contributing.md                  # Contribution guidelines
│  │  ├─ coding-standards.md              # Coding standards and conventions
│  │  ├─ testing-guide.md                 # Testing guidelines
│  │  ├─ debugging-guide.md               # Debugging guide
│  │  ├─ release-process.md               # Release process documentation
│  │  └─ development-environment.md       # Development environment setup
│  ├─ compatibility/                      # Compatibility documentation
│  │  ├─ README.md                        # Compatibility overview
│  │  ├─ database-compatibility.md        # Database compatibility matrix
│  │  ├─ cloud-platform-compatibility.md # Cloud platform compatibility
│  │  ├─ language-compatibility.md        # Programming language compatibility
│  │  └─ version-support.md               # Version support policy
│  ├─ telemetry/                          # Telemetry and observability
│  │  ├─ README.md                        # Telemetry overview
│  │  ├─ metrics-reference.md             # Metrics reference
│  │  ├─ tracing-setup.md                 # Distributed tracing setup
│  │  ├─ logging-configuration.md         # Logging configuration
│  │  ├─ otel-integration.md              # OpenTelemetry integration
│  │  ├─ custom-metrics.md                # Custom metrics development
│  │  └─ correlation-ids.md               # Correlation ID management
│  ├─ reference/                          # Reference documentation
│  │  ├─ README.md                        # Reference overview
│  │  ├─ cli-reference.md                 # Comprehensive CLI reference
│  │  ├─ api-reference.md                 # Comprehensive API reference
│  │  ├─ schema-reference.md              # Schema reference
│  │  ├─ policy-reference.md              # Policy configuration reference
│  │  ├─ error-codes.md                   # Error codes reference
│  │  ├─ configuration-reference.md       # Configuration reference
│  │  └─ glossary.md                      # Glossary of terms
│  ├─ tutorials/                          # Step-by-step tutorials
│  │  ├─ README.md                        # Tutorials overview
│  │  ├─ data-platform-tutorial.md        # Data platform tutorial
│  │  ├─ genai-security-tutorial.md       # GenAI security tutorial
│  │  ├─ voice-compliance-tutorial.md     # Voice compliance tutorial
│  │  ├─ compliance-attestation-tutorial.md # Compliance attestation tutorial
│  │  ├─ siem-integration-tutorial.md     # SIEM integration tutorial
│  │  └─ custom-policy-tutorial.md        # Custom policy development tutorial
│  ├─ faq/                                # Frequently asked questions
│  │  ├─ README.md                        # FAQ overview
│  │  ├─ general-faq.md                   # General FAQ
│  │  ├─ technical-faq.md                 # Technical FAQ
│  │  ├─ compliance-faq.md                # Compliance FAQ
│  │  ├─ security-faq.md                  # Security FAQ
│  │  └─ troubleshooting-faq.md           # Troubleshooting FAQ
│  └─ changelog/                          # Detailed changelog documentation
│     ├─ README.md                        # Changelog overview
│     ├─ v4.0-migration-guide.md          # Migration guide to v4.0
│     ├─ breaking-changes.md              # Breaking changes documentation
│     └─ deprecated-features.md           # Deprecated features
│
```

---

## **Enhanced Testing Infrastructure (v4.0)**

```
├─ test/                                  # Comprehensive testing infrastructure
│  ├─ unit/                               # Unit tests (organized by component)
│  │  ├─ proxy/                           # Gateway/proxy unit tests
│  │  ├─ warehouse/                       # NEW: warehouse integration unit tests
│  │  ├─ dbt/                             # NEW: dbt integration unit tests
│  │  ├─ genai/                           # NEW: GenAI security unit tests
│  │  ├─ voice/                           # NEW: voice compliance unit tests
│  │  ├─ policy/                          # Policy engine unit tests
│  │  ├─ crypto/                          # Cryptographic unit tests
│  │  └─ common/                          # Common utility unit tests
│  ├─ integration/                        # Integration tests
│  │  ├─ data_platform/                   # NEW: data platform integration tests
│  │  │  ├─ dbt_integration_test/
│  │  │  ├─ warehouse_anchor_test/
│  │  │  ├─ activation_gateway_test/
│  │  │  └─ def_bundle_test/
│  │  ├─ genai_security/                  # NEW: GenAI security integration tests
│  │  │  ├─ threat_detection_test/
│  │  │  ├─ bec_prevention_test/
│  │  │  ├─ kill_switch_test/
│  │  │  └─ shadow_mode_test/
│  │  ├─ voice_compliance/                # NEW: voice compliance integration tests
│  │  │  ├─ session_management_test/
│  │  │  ├─ tcpa_compliance_test/
│  │  │  ├─ ucaas_integration_test/
│  │  │  └─ correlation_test/
│  │  ├─ gateway_validator/               # Enhanced gateway validation tests
│  │  ├─ canonical_merkle_parity/         # Canonicalization and Merkle tree tests
│  │  ├─ schema_matrix/                   # Schema validation matrix tests
│  │  ├─ externalization_roundtrip/       # External artifact tests
│  │  ├─ recorder_flow/                   # Recorder flow tests
│  │  ├─ enforcement_primitives/          # Enhanced enforcement primitive tests
│  │  │  ├─ idempotency_test/
│  │  │  ├─ approval_cert_test/
│  │  │  ├─ rate_limit_test/
│  │  │  ├─ tenant_fence_test/
│  │  │  └─ sql_guard_test/
│  │  └─ compliance_framework/            # NEW: compliance framework tests
│  │     ├─ sox_itgc_test/
│  │     ├─ pci_dss_test/
│  │     ├─ hipaa_test/
│  │     └─ eu_ai_act_test/
│  ├─ e2e/                                # End-to-end tests
│  │  ├─ data_platform_e2e/               # NEW: data platform E2E tests
│  │  │  ├─ dbt_full_workflow/
│  │  │  ├─ warehouse_integration_full/
│  │  │  ├─ activation_sync_full/
│  │  │  └─ sox_compliance_full/
│  │  ├─ genai_security_e2e/              # NEW: GenAI security E2E tests
│  │  │  ├─ threat_detection_full/
│  │  │  ├─ bec_prevention_full/
│  │  │  ├─ deepfake_detection_full/
│  │  │  └─ kill_switch_full/
│  │  ├─ voice_compliance_e2e/            # NEW: voice compliance E2E tests
│  │  │  ├─ tcpa_compliance_full/
│  │  │  ├─ session_correlation_full/
│  │  │  └─ ucaas_integration_full/
│  │  ├─ verify_bundle/                   # Enhanced bundle verification tests
│  │  │  ├─ def_verification/             # NEW: DEF verification tests
│  │  │  └─ pef_verification/             # Enhanced PEF verification tests
│  │  ├─ negative_vectors/                # Enhanced negative test vectors
│  │  │  ├─ genai_attack_vectors/         # NEW: GenAI attack vectors
│  │  │  ├─ voice_violation_vectors/      # NEW: voice compliance violations
│  │  │  └─ enhanced_security_vectors/    # Enhanced security test vectors
│  │  ├─ determinism/                     # Enhanced determinism tests
│  │  │  ├─ def_determinism/              # NEW: DEF determinism tests
│  │  │  ├─ pef_determinism/              # Enhanced PEF determinism tests
│  │  │  └─ replay_determinism/           # Enhanced replay determinism
│  │  ├─ compliance_attestation/          # NEW: compliance attestation E2E tests
│  │  │  ├─ sox_attestation_e2e/
│  │  │  ├─ pci_attestation_e2e/
│  │  │  ├─ hipaa_attestation_e2e/
│  │  │  └─ eu_ai_act_attestation_e2e/
│  │  ├─ recorder_contracts/              # Enhanced contract recording tests
│  │  ├─ recorder_etl/                    # Enhanced ETL recording tests
│  │  ├─ recorder_retail/                 # Enhanced retail recording tests
│  │  └─ cross_platform/                  # NEW: cross-platform compatibility tests
│  │     ├─ database_matrix/
│  │     ├─ cloud_platform_matrix/
│  │     └─ sdk_compatibility/
│  ├─ perf/                               # Enhanced performance tests
│  │  ├─ k6_scenarios/                    # k6 performance test scenarios
│  │  │  ├─ data_platform_perf.js         # NEW: data platform performance tests
│  │  │  ├─ genai_security_perf.js        # NEW: GenAI security performance tests
│  │  │  ├─ voice_compliance_perf.js      # NEW: voice compliance performance tests
│  │  │  ├─ gateway_baseline.js           # Enhanced gateway performance tests
│  │  │  ├─ recorder_baseline.js          # Enhanced recorder performance tests
│  │  │  ├─ enforcement_overhead.js       # Enforcement primitive overhead tests
│  │  │  ├─ bundle_generation_perf.js     # Bundle generation performance tests
│  │  │  ├─ verification_perf.js          # Verification performance tests
│  │  │  ├─ burst_profile.js              # Burst traffic profile tests
│  │  │  └─ sustained_load.js             # Sustained load tests
│  │  ├─ benchmarks/                      # Performance benchmarks
│  │  │  ├─ sla_validation.js             # SLA validation benchmarks
│  │  │  ├─ capacity_limits.js            # Capacity limit testing
│  │  │  └─ regression_detection.js       # Performance regression detection
│  │  └─ load_testing/                    # Load testing scenarios
│  │     ├─ scale_testing.js              # Scale testing scenarios
│  │     ├─ stress_testing.js             # Stress testing scenarios
│  │     └─ endurance_testing.js          # Endurance testing scenarios
│  ├─ security/                           # Enhanced security tests
│  │  ├─ penetration/                     # Penetration testing scenarios
│  │  │  ├─ injection_attacks/            # Injection attack tests
│  │  │  ├─ authorization_bypass/         # Authorization bypass tests
│  │  │  ├─ cryptographic_attacks/        # Cryptographic attack tests
│  │  │  └─ genai_attack_simulation/      # NEW: GenAI attack simulation
│  │  ├─ vulnerability_scanning/          # Vulnerability scanning tests
│  │  │  ├─ dependency_scanning/
│  │  │  ├─ static_analysis/
│  │  │  └─ dynamic_analysis/
│  │  ├─ compliance_scanning/             # NEW: compliance scanning tests
│  │  │  ├─ sox_compliance_scan/
│  │  │  ├─ pci_compliance_scan/
│  │  │  └─ privacy_compliance_scan/
│  │  └─ threat_modeling/                 # Threat modeling validation tests
│  │     ├─ attack_tree_validation/
│  │     ├─ threat_surface_analysis/
│  │     └─ risk_assessment_validation/
│  ├─ fuzz/                               # Enhanced fuzzing tests
│  │  ├─ canonicalization_fuzz_test.go    # Enhanced canonicalization fuzzing
│  │  ├─ schema_fuzz_test.go              # Schema validation fuzzing
│  │  ├─ policy_fuzz_test.go              # NEW: policy parsing fuzzing
│  │  ├─ genai_input_fuzz_test.go         # NEW: GenAI input fuzzing
│  │  ├─ voice_input_fuzz_test.go         # NEW: voice input fuzzing
│  │  ├─ cryptographic_fuzz_test.go       # Cryptographic operation fuzzing
│  │  └─ network_protocol_fuzz/           # Network protocol fuzzing
│  │     ├─ http_fuzz_test.go
│  │     ├─ webhook_fuzz_test.go
│  │     └─ api_fuzz_test.go
│  ├─ compatibility/                      # NEW: compatibility tests
│  │  ├─ database_compatibility/          # Database compatibility tests
│  │  │  ├─ postgres_versions/
│  │  │  ├─ snowflake_variants/
│  │  │  ├─ databricks_variants/
│  │  │  └─ cloud_providers/
│  │  ├─ sdk_compatibility/               # SDK compatibility tests
│  │  │  ├─ python_versions/
│  │  │  ├─ typescript_versions/
│  │  │  └─ dependency_matrix/
│  │  └─ platform_compatibility/          # Platform compatibility tests
│  │     ├─ operating_systems/
│  │     ├─ container_runtimes/
│  │     └─ cloud_platforms/
│  ├─ golden_vectors/                     # Enhanced golden test vectors
│  │  ├─ def_vectors/                     # NEW: DEF golden vectors
│  │  │  ├─ valid_def_bundles/
│  │  │  ├─ invalid_def_bundles/
│  │  │  └─ edge_case_def_bundles/
│  │  ├─ pef_vectors/                     # Enhanced PEF golden vectors
│  │  │  ├─ valid_pef_bundles/
│  │  │  ├─ invalid_pef_bundles/
│  │  │  └─ edge_case_pef_bundles/
│  │  ├─ genai_vectors/                   # NEW: GenAI security vectors
│  │  │  ├─ prompt_injection_vectors/
│  │  │  ├─ deepfake_detection_vectors/
│  │  │  └─ bec_prevention_vectors/
│  │  ├─ voice_vectors/                   # NEW: voice compliance vectors
│  │  │  ├─ tcpa_compliance_vectors/
│  │  │  ├─ session_management_vectors/
│  │  │  └─ correlation_vectors/
│  │  ├─ compliance_vectors/              # NEW: compliance framework vectors
│  │  │  ├─ sox_compliance_vectors/
│  │  │  ├─ pci_compliance_vectors/
│  │  │  └─ hipaa_compliance_vectors/
│  │  └─ cross_verification/              # Cross-verifier consistency vectors
│  │     ├─ go_verifier_vectors/
│  │     ├─ typescript_verifier_vectors/
│  │     └─ consistency_validation/
│  ├─ regression/                         # NEW: regression tests
│  │  ├─ performance_regression/          # Performance regression tests
│  │  ├─ security_regression/             # Security regression tests
│  │  ├─ compliance_regression/           # Compliance regression tests
│  │  └─ functional_regression/           # Functional regression tests
│  └─ tools/                              # Testing tools and utilities
│     ├─ test_data_generators/            # Test data generation tools
│     ├─ mock_services/                   # Mock service implementations
│     ├─ test_harnesses/                  # Test execution harnesses
│     └─ validation_utilities/            # Test validation utilities
│
```

---

## **Enhanced Scripts & Automation (v4.0)**

```
├─ scripts/                               # Enhanced automation scripts
│  ├─ development/                        # Development automation scripts
│  │  ├─ dev.sh                           # Enhanced development script
│  │  ├─ setup_environment.sh             # Environment setup script
│  │  ├─ reset_environment.sh             # Environment reset script
│  │  └─ update_dependencies.sh           # Dependency update script
│  ├─ performance/                        # Performance monitoring scripts
│  │  ├─ calc_perf.py                     # Enhanced performance calculation
│  │  ├─ benchmark_runner.py              # Benchmark execution script
│  │  ├─ sla_validator.py                 # SLA validation script
│  │  └─ perf_regression_detector.py      # Performance regression detection
│  ├─ security/                           # Security automation scripts
│  │  ├─ check_licenses.sh                # Enhanced license scanning
│  │  ├─ vulnerability_scan.sh            # Vulnerability scanning script
│  │  ├─ compliance_check.sh              # Compliance checking script
│  │  └─ security_audit.py                # Security audit automation
│  ├─ ci_cd/                              # CI/CD automation scripts
│  │  ├─ badge_artifact.sh                # Enhanced badge generation
│  │  ├─ release_preparation.sh           # Release preparation script
│  │  ├─ deployment_validation.sh         # Deployment validation script
│  │  └─ rollback_automation.sh           # Automated rollback script
│  ├─ data_platform/                      # NEW: data platform scripts
│  │  ├─ dbt_setup.sh                     # dbt environment setup
│  │  ├─ warehouse_doctor.py              # Warehouse health checking
│  │  ├─ lineage_validator.py             # Data lineage validation
│  │  └─ def_bundle_generator.py          # DEF bundle generation
│  ├─ genai_security/                     # NEW: GenAI security scripts
│  │  ├─ threat_detector_test.py          # Threat detector testing
│  │  ├─ attack_vector_generator.py       # Attack vector generation
│  │  ├─ bec_prevention_test.py           # BEC prevention testing
│  │  └─ genai_policy_validator.py        # GenAI policy validation
│  ├─ voice_compliance/                   # NEW: voice compliance scripts
│  │  ├─ tcpa_compliance_check.py         # TCPA compliance checking
│  │  ├─ session_correlation_test.py      # Session correlation testing
│  │  ├─ disclaimer_validator.py          # Disclaimer validation
│  │  └─ ucaas_integration_test.py        # UCaaS integration testing
│  ├─ compliance/                         # Enhanced compliance scripts
│  │  ├─ attestation_generator.py         # Enhanced attestation generation
│  │  ├─ sox_compliance_check.py          # SOX compliance checking
│  │  ├─ pci_audit_automation.py          # PCI audit automation
│  │  ├─ hipaa_privacy_check.py           # HIPAA privacy checking
│  │  └─ eu_ai_act_validator.py           # EU AI Act compliance validation
│  ├─ testing/                            # Testing automation scripts
│  │  ├─ test_runner.py                   # Enhanced test execution
│  │  ├─ golden_vector_validator.py       # Golden vector validation
│  │  ├─ cross_verifier_test.py           # Cross-verifier consistency testing
│  │  └─ regression_test_runner.py        # Regression test automation
│  ├─ deployment/                         # Deployment automation scripts
│  │  ├─ docker_build.sh                  # Docker build automation
│  │  ├─ kubernetes_deploy.sh             # Kubernetes deployment script
│  │  ├─ cloud_deployment.py              # Cloud deployment automation
│  │  └─ infrastructure_validation.py     # Infrastructure validation
│  ├─ monitoring/                         # Monitoring automation scripts
│  │  ├─ telemetry_setup.py               # Telemetry setup automation
│  │  ├─ alert_configuration.py           # Alert configuration script
│  │  ├─ dashboard_deployment.py          # Dashboard deployment automation
│  │  └─ health_check_automation.py       # Health check automation
│  └─ maintenance/                        # Maintenance automation scripts
│     ├─ key_rotation.py                  # Enhanced key rotation
│     ├─ backup_automation.sh             # Backup automation script
│     ├─ database_maintenance.py          # Database maintenance automation
│     ├─ log_rotation.sh                  # Log rotation script
│     └─ cleanup_automation.py            # Cleanup automation script
│
```

---

## **Enhanced GitHub Integration (v4.0)**

```
└─ .github/                               # Enhanced GitHub integration
   ├─ actions/                            # Enhanced GitHub Actions
   │  ├─ verify-bundle/                   # Enhanced bundle verification action
   │  │  ├─ action.yaml                   # Enhanced action definition
   │  │  ├─ README.md                     # Action documentation
   │  │  └─ dist/                         # Compiled action distribution
   │  ├─ def-verify/                      # NEW: DEF verification action
   │  │  ├─ action.yaml
   │  │  ├─ README.md
   │  │  └─ dist/
   │  ├─ genai-security-scan/             # NEW: GenAI security scanning action
   │  │  ├─ action.yaml
   │  │  ├─ README.md
   │  │  └─ dist/
   │  ├─ voice-compliance-check/          # NEW: voice compliance checking action
   │  │  ├─ action.yaml
   │  │  ├─ README.md
   │  │  └─ dist/
   │  ├─ sox-compliance-gate/             # NEW: SOX compliance gate action
   │  │  ├─ action.yaml
   │  │  ├─ README.md
   │  │  └─ dist/
   │  └─ policy-validation/               # Enhanced policy validation action
   │     ├─ action.yaml
   │     ├─ README.md
   │     └─ dist/
   ├─ ISSUE_TEMPLATE/                     # Enhanced issue templates
   │  ├─ bug_report.yaml                  # Enhanced bug report template
   │  ├─ feature_request.yaml             # Enhanced feature request template
   │  ├─ data_platform_issue.yaml         # NEW: data platform issue template
   │  ├─ genai_security_issue.yaml        # NEW: GenAI security issue template
   │  ├─ voice_compliance_issue.yaml      # NEW: voice compliance issue template
   │  ├─ compliance_question.yaml         # NEW: compliance question template
   │  └─ security_vulnerability.yaml      # Enhanced security vulnerability template
   ├─ PULL_REQUEST_TEMPLATE.md            # Enhanced PR template
   ├─ SECURITY_EXCEPTIONS.md              # Enhanced security exceptions tracking
   ├─ CODEOWNERS                          # Enhanced code ownership definitions
   └─ workflows/                          # Enhanced GitHub Actions workflows
      ├─ ci.yml                           # Enhanced CI workflow with path filtering
      ├─ data-platform-ci.yml             # NEW: data platform specific CI
      ├─ genai-security-ci.yml            # NEW: GenAI security CI
      ├─ voice-compliance-ci.yml          # NEW: voice compliance CI
      ├─ compliance-validation.yml        # NEW: compliance framework validation
      ├─ cross-verifier-consistency.yml   # NEW: cross-verifier consistency check
      ├─ performance-validation.yml       # Enhanced performance validation
      ├─ security-scanning.yml            # Enhanced security scanning
      ├─ release-please.yml               # Release automation
      ├─ release-go.yml                   # Go release workflow
      ├─ release-python.yml               # Python package release
      ├─ release-npm.yml                  # npm package release
      ├─ release-docker.yml               # NEW: Docker image release
      ├─ nightly-audit.yml                # Enhanced nightly audit workflow
      ├─ weekly-security-scan.yml         # NEW: weekly security scanning
      ├─ monthly-compliance-check.yml     # NEW: monthly compliance validation
      ├─ verifier-badge.yml               # Enhanced verifier badge generation
      ├─ traceability.yml                 # Enhanced traceability validation
      ├─ policy-contract.yml              # Enhanced policy contract validation
      ├─ perf-budgets.yml                 # Enhanced performance budget validation
      ├─ procurement-kit-smoke.yml        # Enhanced procurement kit validation
      ├─ key-rotation-reminder.yml        # Enhanced key rotation reminders
      ├─ dependency-update.yml            # NEW: automated dependency updates
      ├─ vulnerability-scanning.yml       # NEW: comprehensive vulnerability scanning
      ├─ license-compliance.yml           # NEW: license compliance checking
      └─ documentation-sync.yml           # NEW: documentation synchronization
```