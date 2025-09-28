Execution order: 0 → 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10 → 11 → 12 → 13
(then Phase 1.5, Phase 2, Phase 3)
***Epic 0 — Foundations (Repo, CI/CD, Security, OSS Hygiene)
Goal: Monorepo-lite scaffold, Warp-first dev, path-filtered CI/CD, traceability gate, supply-chain hardening, architecture/ADR bases.
Stories & repo_paths (with acceptance)
0.1 Repo scaffold & OSS hygiene
Paths: /README.md, /LICENSE, /CODE_OF_CONDUCT.md, /CONTRIBUTING.md, /SECURITY.md, /SUPPORT.md, /.editorconfig, /.gitignore, /.gitattributes, /CODEOWNERS, /CHANGELOG.md, top-level dirs per structure.
✅ OSS headers present; CHANGELOG wired to release-please.
0.2 Dev setup (Warp-first) & Make targets
Paths: /Makefile, /.pre-commit-config.yaml, /.warp/workflows.yaml, /docs/dev_setup_mac.md, /docs/dev_setup_linux.md, /examples/quickstart-compose/*, /kits/procurement/README.md.
✅ make quickstart works <10 min; pre-commit runs locally.
0.3 Language workspaces
Paths: /go.mod, /go.work, /package.json, /sdk/python/pyproject.toml.
✅ go work sync clean; npm -w verifier/ts test runs.
0.4 CI/CD automation
Paths: /.github/workflows/ci.yml, release-please.yml, release-go.yml, publish-python.yml, publish-npm.yml, /release-please-config.json, /.github/actions/verify-bundle/*.
✅ PR CI green on new repo; release-please opens version PRs.
0.5 Security & provenance (SBOM, Grype, cosign, Scorecard, OSV, ZAP Baseline, CodeQL).”
Paths: /.github/workflows/ci.yml (ZAP baseline), /.github/workflows/nightly-audit.yml (Scorecard, OSV, CodeQL).
✅ Signed artifacts on tag; exceptions file enforced.
0.6 Traceability & PR review agent (SKIPPED)
0.7 Architecture & ADR base
Paths: /docs/arch/architecture.md, /docs/arch/runtime_flows.md, /docs/arch/api_cli_reference.md, /docs/ADR_INDEX.md, /docs/arch/adr/0001-technical-foundations.md, 0002-pef-v0-core-decisions.md.
✅ Diagrams render; ADR index links valid.
***Epic 1 — Core Evidence & Spec Compliance (PEF v0 + Vectors)
Goal: PEF v0 spec, canonicalization, Merkle, externalization, signatures, vectors, verifiers wired in CI.
Stories & repo_paths
1.1 PEF spec & schemas
Paths: /spec/pef/SPEC.md, /spec/pef/VERSIONING.md, /spec/pef/schemas/{manifest.json,receipt.json,replay_certificate.json,journal_event.json}.
✅ Schemas validate with ajv/Go tests.
1.2 Canonicalization & Merkle
Paths: /internal/bundle/{canonical.go,merkle.go}.
✅ Same input ⇒ identical bytes; Merkle root stable.
1.3 Externalization
Paths: /internal/bundle/externalization.go.
✅ >25MB artifacts referenced with sha256.
1.4 Signature object & agility
Paths: /internal/crypto/signature.go, /spec/pef/schemas/manifest.json.
✅ Ed25519 default; others optional; key_id present.
1.5 Golden vectors
Paths: /spec/pef/test-vectors/{valid,forged,truncated}/.
✅ Verifiers pass/fail as expected; vectors immutable after publish.
1.6 Verifier CI & action
Paths: /.github/actions/verify-bundle/*, /.github/workflows/ci.yml.
✅ Composite action works with both verifiers.
1.7 Governance & automation metadata
Paths: update schemas/spec & /docs/compliance/*.
✅ Optional {job_id,service_id,pipeline_id} accepted.
1.8 Conformance & implementers
Paths: /docs/{conformance.md,implementers_guide.md}.
✅ Clear “do/don’t”, examples compile.
1.9 License scan
Paths: /scripts/check_licenses.sh, docs.
✅ CI gate passes, flags disallowed licenses.
***Epic 2 — Gateway (SchemaLock + Firewall)
Goal: Streaming JSON validator (repair-once), signed receipts with OWASP/threat_class/mitre_id, bypass detection, per-run hash chain, SSE notarization, CSV validator, spill→503, ECS/OCSF NDJSON, detector framework.
Stories & repo_paths
2.1 Streaming validator + repair-once
/internal/proxy/validator.go, /internal/policy/loader.go.
✅ Repair once then block; perf budget held.
2.2 Receipts & schema hashes
/internal/proxy/receipts.go, /spec/pef/schemas/receipt.json.
✅ Required fields present & signed.
2.3 Bypass & hash chain
/internal/proxy/{bypass.go,hashchain.go}.
✅ Hash chain continuous; bypass events logged.
2.4 SSE notarization
/internal/proxy/sse_notarization.go.
✅ Notary evidence in bundle.
2.5 CSV minimal validator
/internal/proxy/csv_validator.go.
✅ Blocks malformed CSV.
2.6 Spill policy
/internal/proxy/queue.go.
✅ Backpressure → 503 with metrics.
2.7 NDJSON + saved searches
/internal/proxy/ndjson.go, /docs/siem/{mapping.md,splunk_queries.json,datadog_queries.json}.
✅ Import templates work in Splunk/Datadog.
2.8 Detectors
/internal/proxy/{detectors.go,ext_detectors.go}.
✅ Timeouts/quotas; async tap path.
***Epic 3 — Recorder (Flight Data Recorder)
Goal: HMAC capture, metadata snapshots (REPEATABLE READ; WAL LSN; DSN hash; reject replicas), deterministic diff, offline replay (scratch schema) + signed Replay Certificate; Cloud PG matrix doc.
Stories & repo_paths
3.1 Capture & body_storage
/internal/proxy/{hmac.go,body_storage.go,hashchain.go}, /internal/bundle/journal_append.go.
✅ Privacy by default; HMAC enforced.
3.2 Snapshot engine & manifest
/internal/snapshot/{snapshot.go,manifest.go,errors.go}.
✅ Failure codes: PRE_FAIL|LSN_MISSING|POST_TIMEOUT|REPLICA_LAG|POLICY_SKIP.
3.3 Deterministic diff
/internal/diff/diff.go.
✅ Stable ordering; checksums consistent.
3.4 Replay + certificate
/internal/replay/{replay.go,denylist.go}, /spec/pef/schemas/replay_certificate.json.
✅ Status {success|partial|failed} + codes.
3.5 Cloud PG matrix
/docs/compatibility/cloud_postgres_matrix.md.
✅ 15/16 supported; 13/14 best-effort warnings.
***Epic 4 — Unified Policy Surface
Goal: Canonical policy.yaml with policy_hash; schemas, validators, lineage, HITL, body_storage, threat_map, cost caps, version metadata; plus v3.0 enforcement primitives contract.
Stories & repo_paths
4.1 Loader/validator & canonicalization
/internal/policy/loader.go, /spec/pef/schemas/policy.schema.json.
✅ Policy validates against schema.
4.2 Lineage matchers
/internal/lineage/lineage.go.
✅ Trusted write hints linked.
4.3 HITL checkpoints
/internal/policy/loader.go, /cmd/clyra/*.
✅ Pause/resume points respected.
4.4 Privacy & body_storage
/internal/proxy/body_storage.go.
✅ Deny by default; explicit redaction.
4.5 Threat map
/internal/policy/threat_map.go, schema updates.
✅ OWASP/MITRE → threat_class mapping.
4.6 Cost/Quota caps
/internal/policy/cost_caps.go, metrics.
✅ Caps enforced & metered.
4.7 Version fingerprints
bundle metrics + policy.
✅ agent/runtime/schema versions recorded.
4.8 Two-person promotion guard (docs)
/docs/sop/change-mgmt.md.
✅ Process documented & referenced by CI labels.
4.9 Automation context plumbed
schemas/manifest updated.
✅ Optional context present in bundles.
***Epic 5 — Attestation v0 (+ Overlays)
Goal: clyra attest → signed JSON (source of truth) + PDF referencing digest; PCI/HIPAA pass/fail; EU AI Act/NIST overlays only; chain-of-custody & WORM pointers; procurement samples.
Stories & repo_paths
5.1 Generator & CLI
/cmd/clyra/attest.go, /internal/bundle/*, /docs/attestation.md.
✅ JSON signed; PDF includes JSON digest reference.
5.2 Framework overlays
/docs/compliance/{pci_mappings.md,hipaa_mappings.md,eu_ai_act_art12.md,nist_ai_rmf.md}.
✅ EU/NIST show mappings w/o pass/fail.
5.3 Procurement kit
/kits/procurement/* (sample evidence + attest PDFs + buyer/auditor one-pagers).
✅ Kit verifies & attests in CI.
***Epic 6 — Shadow Mode
Goal: Dry-run secondary policies; log shadow_verdict=true; optional SIEM forwarding.
Stories & repo_paths
6.1 Shadow execution
/internal/proxy/, /internal/policy/, /cmd/clyra/*.
✅ Overhead ≤1ms; no blocking.
6.2 Evidence & NDJSON
/internal/proxy/ndjson.go, bundle metrics.
✅ Shadow verdicts visible in SIEM.
6.3 Docs
/docs/*.
✅ Example config included.
***Epic 7 — SDKs & LiteLLM (MVP)
Goal: Python SDK (headers, decorators, LiteLLM middleware, small retry helper); example recipes.
Stories & repo_paths
7.1 Python SDK
/sdk/python/clyra_sdk/{headers.py,decorators.py,litellm_middleware.py,retry.py}, /sdk/python/tests/.
✅ Works against quickstart.
7.2 Examples
/examples/litellm-recipe/example.py.
✅ Demonstrates vendor-agnostic use.
7.3 Docs
/README.md, /docs/*.
✅ Usage copied into docs.
***Epic 8 — Packs & Service Templates
Goal: Contracts, AP/AR, ETL, RPA packs; Frontline “Service” (Retail/FinServ/Travel) production-lean templates; goldens; kit updates.
Stories & repo_paths
8.1 Contracts
/packs/contracts/{schemas,policies,fixtures,goldens,pack.yaml,README.md}.
✅ Policy passes contract tests.
8.2 AP/AR
/packs/ap_ar/... ✅
8.3 ETL
/packs/etl/... ✅
8.4 RPA
/packs/rpa/... ✅
8.5 Frontline Service Packs
/packs/service/{retail,finserv,travel}/... with schemas (order_update/refund_request/etc.), HITL defaults, PII redaction.
✅ Goldens included; docs explain hardening.
8.6 Procurement kit additions
/kits/procurement/* (retail assets if included).
✅ CI smoke verifies kit outputs.
***Epic 9 — SOPs, KMS & WORM, Egress
Goal: Runbooks for incidents/changes/keys; doctor checks for PG; egress controls examples.
Stories & repo_paths
9.1 SOPs
/docs/sop/{incident.md,change-mgmt.md,kms.md,rotation.md}.
✅ Linked by docs & CI notes.
9.2 Doctor checks
/cmd/clyra/doctor.go, /docs/compatibility/cloud_postgres_matrix.md.
✅ Warns on PG 13/14; exits non-zero on enforce unless flag.
9.3 Egress examples
/examples/egress/{iptables_sidecar.md,envoy_filter.md}.
✅ Copy-pasteable recipes.
***Epic 10 — Quickstart, Demos, Procurement, Success Digest
Goal: 10-minute PLG; clyra demo contracts|etl; success digest; verifier badge; doctor suggest-fixes; one-zip procurement kit.
Stories & repo_paths
10.1 Quickstart
/cmd/clyra/quickstart.go, /examples/quickstart-compose/{docker-compose.yml,seed.sql}.
✅ One command up.
10.2 Demos (contracts, etl)
/cmd/clyra/demo/{contracts.go,etl.go}, /examples/etl-demo/{dataset.sql,pipeline_config.yaml,README.md}, /packs/etl/*.
✅ Produces bundles.
10.3 Success digest & badge
/cmd/clyra/report.go, /scripts/badge_artifact.sh, /.github/actions/verify-bundle/*.
✅ Digest includes Merkle root, blocks, replay result, badge link.
10.4 Doctor suggest-fixes
/cmd/clyra/doctor.go.
✅ Prints shell/SQL remediations.
10.5 Kit one-zip
/kits/procurement/*.
✅ End-to-end verify/attest via CI workflow.
10.6 PLG docs & success digest (hello_bundle.md, success_digest.md
Paths: /docs/plg/*.
***Epic 11 — Independent Verifiers & Action
Goal: Neutral Go & TS verifiers; composite GH Action.
Stories & repo_paths
11.1 Go verifier
/verifier/go/{go.mod,cmd/pef-verify/main.go,pkg/verifier/verifier.go}.
✅ Only imports /spec/pef/*.
11.2 TS verifier
/verifier/ts/{package.json,tsconfig.json,src/index.ts}.
✅ npx @clyra/pef-verifier works.
11.3 GH Action
/.github/actions/verify-bundle/*.
✅ Usable by external repos.
***Epic 12 — Performance & Reliability SLOs
Goal: Gateway p95 ≤15ms (+≤2ms enforcement), Recorder p95 ≤20ms, Snapshot ≤50ms (≤100 tables), Diff <2s (demo), k6 gates, metrics.
Stories & repo_paths
12.1 k6 scenarios & perf budgets
/test/perf/k6_scenarios.js, /.github/workflows/perf-budgets.yml, ci/perf_budgets.yml, /docs/perf.md.
✅ CI reads thresholds from YAML; PRs fail on regression. k6 scenarios + nightly perf audit: explicitly list Scorecard, OSV, ZAP Full, CodeQL scans in nightly-audit.yml.
12.2 Metrics in manifest
/internal/bundle/performance_metrics.go, /spec/pef/schemas/manifest.json.
✅ Proxy p95, snapshot lag, blocks recorded.
12.3 Perf calc script
/scripts/calc_perf.py.
✅ Generates curves for weekly audit.
12.4 Fuzz/negative spec tests
/test/fuzz/{canonicalization_fuzz_test.go,schema_negative/*}.
✅ Guards canonicalization code.
***Epic 13 — Release Integrity & Community Posture
Goal: Signed releases w/ SBOM & provenance; issue/PR templates; non-root images guidance; samples cover AI & non-AI.
Stories & repo_paths
13.1 Signed releases
/.github/workflows/release-go.yml, /goreleaser.yaml, /.cosign.pub.
✅ Cosign + SLSA attestations published.
13.2 Templates & labels
/.github/ISSUE_TEMPLATE/*, /.github/PULL_REQUEST_TEMPLATE.md, /docs/labels.md.
✅ Triage labels applied.
13.3 Non-root images guidance
/docs/security.md, CI checks in ci.yml.
✅ Container user != root.
13.4 Samples parity
/spec/pef/test-vectors/valid/* (include ETL/RPA), /kits/procurement/*.
✅ Examples stay current via procurement-kit-smoke.yml.
13.5 OSS labels & triage docs
Paths: /docs/labels.md.
***CI Workflows (non-code deliverables)
/.github/workflows/ci.yml — build, unit/integration, lint (Go/Py/TS), Semgrep, Gitleaks, ZAP Baseline, verifier action.
/.github/workflows/nightly-audit.yml — k6 perf, ZAP Full, CodeQL, SBOM+Grype, OSV, OpenSSF Scorecard; exports perf curves.
/.github/workflows/release-please.yml — versioning & changelog PRs.
/.github/workflows/release-go.yml — GoReleaser, cosign, SLSA provenance.
/.github/workflows/publish-python.yml / publish-npm.yml — SDK/verifier releases.
/.github/workflows/verifier-badge.yml — builds & uploads badge artifact.
/.github/workflows/traceability.yml — PRD/Task/paths gate.
/.github/workflows/policy-contract.yml — validate all policies vs policy.schema.json; check golden receipts/attestations exist.
/.github/workflows/perf-budgets.yml — read thresholds from ci/perf_budgets.yml, run k6, fail on regressions.
/.github/workflows/procurement-kit-smoke.yml — verify/attest kit samples; create PDF referencing JSON digest.
/.github/workflows/key-rotation-reminder.yml — open rotation issues every 180d.
***Test Matrix & Examples (where tests live)
Integration: /test/integration/{gateway_validator,canonical_merkle_parity,schema_matrix,externalization_roundtrip,recorder_flow}
E2E: /test/e2e/{verify_bundle,negative_vectors,determinism,recorder_contracts,recorder_etl,recorder_retail}
Perf: /test/perf/k6_scenarios.js
Fuzz: /test/fuzz/{canonicalization_fuzz_test.go,schema_negative/*}
Examples used by tests: /examples/quickstart-compose, /examples/etl-demo, /examples/litellm-recipe, /examples/egress/*
***Phase 1.5 (Fast-Follow after MVP)
TS SDK: /sdk/ts/* + publish workflow
K8s/Istio/Helm: /deploy/helm/*, enrich /examples/egress/envoy_filter.md
Packaged SIEM dashboards: /integrations/siem/{splunk,datadog}/*
Diff-Agent CLI: /cmd/clyra/, /internal/diff/
Rollback manifest pointer: /internal/bundle/*
Redis rate/idempotency store: plug into /internal/proxy/{ratelimit,idempotency}
Phase 2
Self-hosted control plane (RBAC, registry, BYOK): /control-plane/{api,ui,db}/*
Advanced compliance packs: /packs/-advanced/
Phase 3
UI/Dashboard (/ui/web/) and SaaS packaging (/saas/)
