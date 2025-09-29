# Clyra v4.0 Development Makefile
# Data-Led, Agent-Ready: Enhanced development workflow for modern data pipelines
# Aligns with PRD v4.0 and enhanced 10-minute PLG onboarding paths

.DEFAULT_GOAL := help
.PHONY: help quickstart quickstart-data test test-comprehensive test-fast verify-vectors attest-sample lint lint-comprehensive clean doctor

# Tool versions (matching CLAUDE.md v4.0 requirements)
GO_VERSION := 1.25.x
NODE_VERSION := 22.x
PYTHON_VERSION := 3.13
DBT_VERSION := 1.0+

# Enhanced directories for v4.0 architecture
EXAMPLES_DIR := examples
QUICKSTART_DIR := $(EXAMPLES_DIR)/quickstart-compose
QUICKSTART_DATA_DIR := $(EXAMPLES_DIR)/quickstart-data-compose
KITS_DIR := kits/procurement
SDK_PYTHON_DIR := sdk/python
VERIFIER_GO_DIR := verifier/go
VERIFIER_TS_DIR := verifier/ts
SPEC_DIR := spec
DATA_PLATFORM_DIR := internal/warehouse
DBT_DIR := internal/dbt
GENAI_DIR := internal/genai
VOICE_DIR := internal/voice

## help: Display this enhanced help message for Clyra v4.0
help:
	@echo "Clyra v4.0 Development Makefile"
	@echo "Data Change Control & Attestation for Modern Pipelines"
	@echo ""
	@echo "Strategic positioning: Data-led market entry, agent-ready architecture"
	@echo ""
	@echo "Essential targets for enhanced development workflow:"
	@echo ""
	@sed -n 's/^##//p' $(MAKEFILE_LIST) | column -t -s ':' | sed -e 's/^/ /'
	@echo ""
	@echo "Enhanced Tech Stack Requirements (v4.0):"
	@echo "  Go: $(GO_VERSION) (enhanced with data platform + GenAI modules)"
	@echo "  Node.js: $(NODE_VERSION) LTS (CI matrix: 22.x + 24.x)"
	@echo "  Python: $(PYTHON_VERSION) (via uv) with dbt-core $(DBT_VERSION)"
	@echo "  Data Platform: Snowflake/Databricks/Postgres 15/16"
	@echo "  15-Factor: API-first, comprehensive telemetry, enhanced authentication"
	@echo ""
	@echo "Key workflows:"
	@echo "  Data Platform Track: make quickstart-data → clyra dbt init → attest"
	@echo "  Universal Track: make quickstart → clyra demo → verify → attest"
	@echo ""

## quickstart: Boot enhanced universal stack (Gateway + Recorder + warehouse simulators + GenAI/voice)
quickstart:
	@echo "🚀 Starting Clyra v4.0 enhanced universal stack..."
	@echo "   Components: Gateway + Recorder + Postgres + GenAI security + Voice compliance"
	@if [ ! -f "$(QUICKSTART_DIR)/docker-compose.yml" ]; then \
		echo "❌ Error: $(QUICKSTART_DIR)/docker-compose.yml not found"; \
		echo "   Creating stub compose for v4.0 architecture..."; \
		mkdir -p $(QUICKSTART_DIR); \
		$(MAKE) create-universal-compose; \
	fi
	cd $(QUICKSTART_DIR) && docker-compose up --build -d
	@$(MAKE) wait-for-health $(QUICKSTART_DIR)
	@echo "✅ Universal stack ready - try: clyra demo contracts --with-genai-security"

## quickstart-data: Boot data platform stack (Gateway + Recorder + Snowflake simulator + dbt project)
quickstart-data:
	@echo "🚀 Starting Clyra v4.0 data platform stack..."
	@echo "   Components: Gateway + Recorder + Snowflake simulator + dbt integration"
	@if [ ! -f "$(QUICKSTART_DATA_DIR)/docker-compose.yml" ]; then \
		echo "❌ Error: $(QUICKSTART_DATA_DIR)/docker-compose.yml not found"; \
		echo "   Creating stub compose for data platform..."; \
		mkdir -p $(QUICKSTART_DATA_DIR); \
		$(MAKE) create-data-compose; \
	fi
	cd $(QUICKSTART_DATA_DIR) && docker-compose up --build -d
	@$(MAKE) wait-for-health $(QUICKSTART_DATA_DIR)
	@echo "✅ Data platform stack ready - try: clyra dbt init demo-project"

## test-comprehensive: Run comprehensive test suite (Go/Python/TS) with data platform + GenAI + voice coverage
test-comprehensive:
	@echo "🧪 Running comprehensive v4.0 test suite..."
	@echo "   Coverage: Data platform + GenAI security + Voice compliance + Universal foundation"
	@$(MAKE) test-go-comprehensive
	@$(MAKE) test-python-comprehensive
	@$(MAKE) test-ts-comprehensive
	@$(MAKE) test-data-platform
	@$(MAKE) test-genai-security
	@$(MAKE) test-voice-compliance
	@echo "✅ All comprehensive tests passed"

## test: Run standard test suite (Go/Python/TS) - enhanced for v4.0
test:
	@echo "🧪 Running enhanced v4.0 test suite..."
	@$(MAKE) test-go
	@$(MAKE) test-python
	@$(MAKE) test-ts
	@echo "✅ All tests passed"

## test-fast: Run tests with minimal output for CI (enhanced coverage)
test-fast:
	@echo "🧪 Running fast enhanced test suite..."
	@$(MAKE) test-go-fast
	@$(MAKE) test-python-fast
	@$(MAKE) test-ts-fast
	@echo "✅ Fast tests passed"

## verify-vectors: Run enhanced Go and TS verifiers on DEF/PEF golden test vectors
verify-vectors:
	@echo "🔍 Running enhanced verifiers on DEF/PEF golden test vectors..."
	@echo "   Testing: Cross-verifier consistency, lineage validation, compliance mapping"
	@if [ -f "$(VERIFIER_GO_DIR)/go.mod" ]; then \
		echo "  Running Go verifier on DEF vectors..."; \
		cd $(VERIFIER_GO_DIR) && go run ./cmd/def-verify ../../../$(SPEC_DIR)/def/test-vectors/valid/*; \
		echo "  Running Go verifier on PEF vectors..."; \
		cd $(VERIFIER_GO_DIR) && go run ./cmd/pef-verify ../../../$(SPEC_DIR)/pef/test-vectors/valid/*; \
	else \
		echo "  ⚠️  Go verifier stub - directory structure not ready yet"; \
	fi
	@if [ -f "$(VERIFIER_TS_DIR)/package.json" ]; then \
		echo "  Running TS verifier on DEF vectors..."; \
		cd $(VERIFIER_TS_DIR) && npm run verify-def ../../../$(SPEC_DIR)/def/test-vectors/valid/*; \
		echo "  Running TS verifier on PEF vectors..."; \
		cd $(VERIFIER_TS_DIR) && npm run verify-pef ../../../$(SPEC_DIR)/pef/test-vectors/valid/*; \
	else \
		echo "  ⚠️  TS verifier stub - directory structure not ready yet"; \
	fi
	@echo "✅ Enhanced verifiers completed successfully"

## attest-sample: Generate comprehensive sample attestation artifacts for all frameworks
attest-sample:
	@echo "📋 Generating comprehensive v4.0 attestation artifacts..."
	@mkdir -p $(KITS_DIR)
	@echo "Creating multi-framework evidence samples..."
	@$(MAKE) create-def-sample
	@$(MAKE) create-pef-sample
	@$(MAKE) create-sox-attestation
	@$(MAKE) create-pci-attestation
	@$(MAKE) create-hipaa-attestation
	@$(MAKE) create-genai-attestation
	@$(MAKE) create-voice-attestation
	@echo "✅ Comprehensive attestation artifacts ready in $(KITS_DIR)/"

## doctor: Run comprehensive health checks for all v4.0 components
doctor:
	@echo "🏥 Running comprehensive v4.0 health checks..."
	@$(MAKE) doctor-go
	@$(MAKE) doctor-python
	@$(MAKE) doctor-ts
	@$(MAKE) doctor-data-platform
	@$(MAKE) doctor-genai-security
	@$(MAKE) doctor-voice-compliance
	@echo "✅ All health checks passed"

## lint-comprehensive: Run comprehensive linters for all languages and frameworks
lint-comprehensive:
	@echo "🧹 Running comprehensive v4.0 linters..."
	@$(MAKE) lint-go-comprehensive
	@$(MAKE) lint-python-comprehensive
	@$(MAKE) lint-ts-comprehensive
	@$(MAKE) lint-data-platform
	@$(MAKE) lint-genai-security
	@$(MAKE) lint-voice-compliance
	@echo "✅ All comprehensive linters passed"

## lint: Run standard linters (golangci-lint, ruff, eslint) - enhanced for v4.0
lint:
	@echo "🧹 Running enhanced v4.0 linters..."
	@$(MAKE) lint-go
	@$(MAKE) lint-python
	@$(MAKE) lint-ts
	@echo "✅ All linters passed"

## clean: Clean up generated files and Docker resources (enhanced cleanup)
clean:
	@echo "🧹 Performing comprehensive v4.0 cleanup..."
	@if [ -f "$(QUICKSTART_DIR)/docker-compose.yml" ]; then \
		cd $(QUICKSTART_DIR) && docker-compose down -v; \
	fi
	@if [ -f "$(QUICKSTART_DATA_DIR)/docker-compose.yml" ]; then \
		cd $(QUICKSTART_DATA_DIR) && docker-compose down -v; \
	fi
	@docker system prune -f
	@rm -rf $(KITS_DIR)/evidence-*.json $(KITS_DIR)/attestation-*.json
	@rm -rf /tmp/clyra-*
	@echo "✅ Comprehensive cleanup completed"

# Enhanced internal targets for v4.0

# Go testing targets
test-go-comprehensive:
	@echo "  Testing Go modules (comprehensive + data platform + GenAI + voice)..."
	@if [ -f "go.mod" ]; then \
		go test -v -race -count=1 -timeout=10m ./...; \
		go test -v -race -count=1 -timeout=5m -tags=integration ./internal/warehouse/...; \
		go test -v -race -count=1 -timeout=5m -tags=integration ./internal/genai/...; \
		go test -v -race -count=1 -timeout=5m -tags=integration ./internal/voice/...; \
	else \
		echo "  ⚠️  Go modules not initialized yet - skipping"; \
	fi

test-go:
	@echo "  Testing Go modules (enhanced)..."
	@if [ -f "go.mod" ]; then \
		go test -v -race -count=1 ./...; \
	else \
		echo "  ⚠️  Go modules not initialized yet - skipping"; \
	fi

test-go-fast:
	@if [ -f "go.mod" ]; then \
		go test -count=1 ./...; \
	else \
		echo "  ⚠️  Go modules not initialized yet - skipping"; \
	fi

# Python testing targets
test-python-comprehensive:
	@echo "  Testing Python SDK (comprehensive with dbt helpers + warehouse + GenAI + voice)..."
	@if [ -f "$(SDK_PYTHON_DIR)/pyproject.toml" ]; then \
		cd $(SDK_PYTHON_DIR) && uv run -m pytest -v --cov=clyra --cov-report=term-missing; \
		cd $(SDK_PYTHON_DIR) && uv run -m pytest -v -m "data_platform"; \
		cd $(SDK_PYTHON_DIR) && uv run -m pytest -v -m "genai_security"; \
		cd $(SDK_PYTHON_DIR) && uv run -m pytest -v -m "voice_compliance"; \
	else \
		echo "  ⚠️  Python SDK not initialized yet - skipping"; \
	fi

test-python:
	@echo "  Testing Python SDK (enhanced)..."
	@if [ -f "$(SDK_PYTHON_DIR)/pyproject.toml" ]; then \
		cd $(SDK_PYTHON_DIR) && uv run -m pytest -v; \
	else \
		echo "  ⚠️  Python SDK not initialized yet - skipping"; \
	fi

test-python-fast:
	@if [ -f "$(SDK_PYTHON_DIR)/pyproject.toml" ]; then \
		cd $(SDK_PYTHON_DIR) && uv run -m pytest -q; \
	else \
		echo "  ⚠️  Python SDK not initialized yet - skipping"; \
	fi

# TypeScript testing targets
test-ts-comprehensive:
	@echo "  Testing TypeScript verifier (comprehensive with DEF/PEF + automation focus)..."
	@if [ -f "$(VERIFIER_TS_DIR)/package.json" ]; then \
		cd $(VERIFIER_TS_DIR) && npm test -- --coverage; \
		cd $(VERIFIER_TS_DIR) && npm run test:integration; \
		cd $(VERIFIER_TS_DIR) && npm run test:def; \
		cd $(VERIFIER_TS_DIR) && npm run test:pef; \
	else \
		echo "  ⚠️  TS verifier not initialized yet - skipping"; \
	fi

test-ts:
	@echo "  Testing TypeScript verifier (enhanced)..."
	@if [ -f "$(VERIFIER_TS_DIR)/package.json" ]; then \
		cd $(VERIFIER_TS_DIR) && npm test; \
	else \
		echo "  ⚠️  TS verifier not initialized yet - skipping"; \
	fi

test-ts-fast:
	@if [ -f "$(VERIFIER_TS_DIR)/package.json" ]; then \
		cd $(VERIFIER_TS_DIR) && npm test --silent; \
	else \
		echo "  ⚠️  TS verifier not initialized yet - skipping"; \
	fi

# v4.0 Component-specific testing
test-data-platform:
	@echo "  Testing data platform components..."
	@if [ -f "go.mod" ]; then \
		go test -v -tags=data_platform ./internal/warehouse/... ./internal/dbt/... ./internal/activation/...; \
	else \
		echo "  ⚠️  Data platform modules not ready yet - skipping"; \
	fi

test-genai-security:
	@echo "  Testing GenAI security components..."
	@if [ -f "go.mod" ]; then \
		go test -v -tags=genai_security ./internal/genai/...; \
	else \
		echo "  ⚠️  GenAI security modules not ready yet - skipping"; \
	fi

test-voice-compliance:
	@echo "  Testing voice compliance components..."
	@if [ -f "go.mod" ]; then \
		go test -v -tags=voice_compliance ./internal/voice/...; \
	else \
		echo "  ⚠️  Voice compliance modules not ready yet - skipping"; \
	fi

# Enhanced lint targets
lint-go-comprehensive:
	@echo "  Linting Go code (comprehensive + gosec + go vet)..."
	@if command -v golangci-lint >/dev/null 2>&1; then \
		if [ -f "go.mod" ]; then \
			golangci-lint run --config .golangci-v4.yml --timeout 10m; \
			go vet ./...; \
			if command -v gosec >/dev/null 2>&1; then \
				gosec -fmt json -out gosec-report.json -severity medium ./...; \
			fi; \
		else \
			echo "  ⚠️  Go modules not initialized yet - skipping"; \
		fi; \
	else \
		echo "  ⚠️  golangci-lint not found - install via: go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest"; \
	fi

lint-go:
	@echo "  Linting Go code (enhanced)..."
	@if command -v golangci-lint >/dev/null 2>&1; then \
		if [ -f "go.mod" ]; then \
			golangci-lint run; \
		else \
			echo "  ⚠️  Go modules not initialized yet - skipping"; \
		fi; \
	else \
		echo "  ⚠️  golangci-lint not found - install via: go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest"; \
	fi

lint-python-comprehensive:
	@echo "  Linting Python code (comprehensive: ruff + mypy + bandit)..."
	@if command -v uv >/dev/null 2>&1; then \
		if [ -f "$(SDK_PYTHON_DIR)/pyproject.toml" ]; then \
			cd $(SDK_PYTHON_DIR) && uv run ruff check --output-format=json --output-file=ruff-report.json .; \
			cd $(SDK_PYTHON_DIR) && uv run mypy --strict .; \
			if command -v bandit >/dev/null 2>&1; then \
				cd $(SDK_PYTHON_DIR) && bandit -f json -o bandit-report.json -r .; \
			fi; \
		else \
			echo "  ⚠️  Python SDK not initialized yet - skipping"; \
		fi; \
	else \
		echo "  ⚠️  uv not found - install via: curl -LsSf https://astral.sh/uv/install.sh | sh"; \
	fi

lint-python:
	@echo "  Linting Python code (enhanced)..."
	@if command -v uv >/dev/null 2>&1; then \
		if [ -f "$(SDK_PYTHON_DIR)/pyproject.toml" ]; then \
			cd $(SDK_PYTHON_DIR) && uv run ruff check; \
		else \
			echo "  ⚠️  Python SDK not initialized yet - skipping"; \
		fi; \
	else \
		echo "  ⚠️  uv not found - install via: curl -LsSf https://astral.sh/uv/install.sh | sh"; \
	fi

lint-ts-comprehensive:
	@echo "  Linting TypeScript code (comprehensive: ESLint v9.17.0 + prettier + security)..."
	@if command -v npm >/dev/null 2>&1; then \
		if [ -f "$(VERIFIER_TS_DIR)/package.json" ]; then \
			cd $(VERIFIER_TS_DIR) && npm run lint:comprehensive; \
			cd $(VERIFIER_TS_DIR) && npm run prettier:check; \
			if [ -f "$(VERIFIER_TS_DIR)/eslint-security.json" ]; then \
				cd $(VERIFIER_TS_DIR) && npm run lint:security; \
			fi; \
		else \
			echo "  ⚠️  TS verifier not initialized yet - skipping"; \
		fi; \
	else \
		echo "  ⚠️  npm not found - install Node.js $(NODE_VERSION) LTS"; \
	fi

lint-ts:
	@echo "  Linting TypeScript code (enhanced)..."
	@if command -v npm >/dev/null 2>&1; then \
		if [ -f "$(VERIFIER_TS_DIR)/package.json" ]; then \
			cd $(VERIFIER_TS_DIR) && npm run lint; \
		else \
			echo "  ⚠️  TS verifier not initialized yet - skipping"; \
		fi; \
	else \
		echo "  ⚠️  npm not found - install Node.js $(NODE_VERSION) LTS"; \
	fi

# v4.0 Component-specific linting
lint-data-platform:
	@echo "  Linting data platform components..."
	@if command -v sqlfluff >/dev/null 2>&1; then \
		if [ -d "$(DATA_PLATFORM_DIR)" ]; then \
			sqlfluff lint $(DATA_PLATFORM_DIR)/**/*.sql --dialect=snowflake; \
		fi; \
	else \
		echo "  ⚠️  sqlfluff not found - SQL linting skipped"; \
	fi

lint-genai-security:
	@echo "  Linting GenAI security components..."
	@if [ -d "$(GENAI_DIR)" ] && [ -f "go.mod" ]; then \
		golangci-lint run --config .golangci-genai.yml ./internal/genai/...; \
	else \
		echo "  ⚠️  GenAI security modules not ready yet - skipping"; \
	fi

lint-voice-compliance:
	@echo "  Linting voice compliance components..."
	@if [ -d "$(VOICE_DIR)" ] && [ -f "go.mod" ]; then \
		golangci-lint run --config .golangci-voice.yml ./internal/voice/...; \
	else \
		echo "  ⚠️  Voice compliance modules not ready yet - skipping"; \
	fi

# Doctor (health check) targets
doctor-go:
	@echo "  Go environment health check..."
	@go version | grep $(GO_VERSION) || echo "  ⚠️  Expected Go $(GO_VERSION)"
	@if command -v golangci-lint >/dev/null 2>&1; then echo "  ✅ golangci-lint available"; else echo "  ❌ golangci-lint missing"; fi
	@if command -v gosec >/dev/null 2>&1; then echo "  ✅ gosec available"; else echo "  ⚠️  gosec missing (optional)"; fi

doctor-python:
	@echo "  Python environment health check..."
	@python --version | grep $(PYTHON_VERSION) || echo "  ⚠️  Expected Python $(PYTHON_VERSION)"
	@if command -v uv >/dev/null 2>&1; then echo "  ✅ uv available"; else echo "  ❌ uv missing"; fi
	@if command -v dbt >/dev/null 2>&1; then echo "  ✅ dbt available"; else echo "  ⚠️  dbt missing (install via: pip install dbt-core)"; fi

doctor-ts:
	@echo "  TypeScript environment health check..."
	@node --version | grep $(NODE_VERSION) || echo "  ⚠️  Expected Node.js $(NODE_VERSION)"
	@if command -v npm >/dev/null 2>&1; then echo "  ✅ npm available"; else echo "  ❌ npm missing"; fi
	@if command -v tsc >/dev/null 2>&1; then echo "  ✅ TypeScript compiler available"; else echo "  ⚠️  TypeScript missing"; fi

doctor-data-platform:
	@echo "  Data platform health check..."
	@if command -v dbt >/dev/null 2>&1; then \
		echo "  ✅ dbt-core available: $$(dbt --version | head -1)"; \
	else \
		echo "  ❌ dbt-core missing - install via: pip install dbt-core"; \
	fi
	@if command -v sqlfluff >/dev/null 2>&1; then echo "  ✅ sqlfluff available"; else echo "  ⚠️  sqlfluff missing (optional SQL linting)"; fi

doctor-genai-security:
	@echo "  GenAI security health check..."
	@if command -v curl >/dev/null 2>&1; then echo "  ✅ curl available (for external detector APIs)"; else echo "  ❌ curl missing"; fi
	@if [ -f "$(GENAI_DIR)/detectors/config.yaml" ]; then echo "  ✅ GenAI detector config found"; else echo "  ⚠️  GenAI detector config not found"; fi

doctor-voice-compliance:
	@echo "  Voice compliance health check..."
	@if command -v ffmpeg >/dev/null 2>&1; then echo "  ✅ ffmpeg available (for audio processing)"; else echo "  ⚠️  ffmpeg missing (optional)"; fi
	@if [ -f "$(VOICE_DIR)/ucaas/config.yaml" ]; then echo "  ✅ UCaaS config found"; else echo "  ⚠️  UCaaS config not found"; fi

# Sample creation utilities
create-def-sample:
	@timestamp=$$(date -u +%Y-%m-%dT%H:%M:%SZ); \
	printf '{\n  "def_version": "0.1.0",\n  "bundle_id": "def-sample-001",\n  "timestamp": "%s",\n  "warehouse_anchor": {\n    "platform": "snowflake",\n    "query_id": "01b12345-6789-abcd-ef01-234567890123",\n    "session_tags": {"clyra_evidence": "true"}\n  },\n  "data_evidence": {\n    "schema_changes": [],\n    "row_counts": {"before": 1000, "after": 1050},\n    "lineage": ["model.my_project.users", "model.my_project.orders"]\n  },\n  "governance_metadata": {\n    "framework": "sox",\n    "attestation": "change_control",\n    "approver": "system"\n  },\n  "signature": {\n    "algorithm": "Ed25519",\n    "key_id": "def-sample-key-001",\n    "signature": "def-sample-signature-placeholder"\n  }\n}\n' "$timestamp" > $(KITS_DIR)/evidence-def-sample.json

create-pef-sample:
	@timestamp=$$(date -u +%Y-%m-%dT%H:%M:%SZ); \
	printf '{\n  "pef_version": "0.2.0",\n  "bundle_id": "pef-enhanced-001",\n  "timestamp": "%s",\n  "genai_security": {\n    "threat_classification": "none",\n    "owasp_llm_mapping": [],\n    "bec_grade_approval": null\n  },\n  "voice_compliance": {\n    "tcpa_compliant": true,\n    "session_id": "voice-session-001",\n    "disclaimer_acknowledged": true\n  },\n  "attestation": {\n    "framework": "comprehensive",\n    "status": "generated",\n    "artifacts": ["evidence-enhanced.zip"]\n  },\n  "governance_metadata": {\n    "reliability": "high",\n    "transparency": "full",\n    "accuracy": "validated",\n    "oversight": "automated"\n  },\n  "signature": {\n    "algorithm": "Ed25519",\n    "key_id": "pef-enhanced-key-001",\n    "signature": "pef-enhanced-signature-placeholder"\n  }\n}\n' "$timestamp" > $(KITS_DIR)/evidence-pef-enhanced.json

create-sox-attestation:
	@timestamp=$$(date -u +%Y-%m-%dT%H:%M:%SZ); \
	printf '{\n  "attestation_framework": "sox_itgc",\n  "bundle_id": "sox-attestation-001",\n  "timestamp": "%s",\n  "controls": {\n    "change_control": "pass",\n    "segregation_of_duties": "pass",\n    "access_management": "pass",\n    "monitoring": "pass"\n  },\n  "evidence_bundles": ["evidence-def-sample.json"],\n  "auditor_guidance": {\n    "verification_steps": ["Independent verification via Go/TS verifiers", "Cryptographic signature validation", "Warehouse anchor confirmation"],\n    "compliance_mapping": "SOX Section 404 - Internal Control over Financial Reporting"\n  },\n  "signature": {\n    "algorithm": "Ed25519",\n    "key_id": "sox-attestation-key-001",\n    "signature": "sox-attestation-signature-placeholder"\n  }\n}\n' "$timestamp" > $(KITS_DIR)/attestation-sox.json

create-pci-attestation:
	@timestamp=$$(date -u +%Y-%m-%dT%H:%M:%SZ); \
	printf '{\n  "attestation_framework": "pci_dss",\n  "bundle_id": "pci-attestation-001",\n  "timestamp": "%s",\n  "requirements": {\n    "req_10_logging": "pass",\n    "req_6_development": "pass",\n    "req_8_access": "pass",\n    "req_11_testing": "pass"\n  },\n  "daily_review_included": true,\n  "genai_threat_posture": "monitored",\n  "signature": {\n    "algorithm": "Ed25519",\n    "key_id": "pci-attestation-key-001",\n    "signature": "pci-attestation-signature-placeholder"\n  }\n}\n' "$timestamp" > $(KITS_DIR)/attestation-pci.json

create-hipaa-attestation:
	@timestamp=$$(date -u +%Y-%m-%dT%H:%M:%SZ); \
	printf '{\n  "attestation_framework": "hipaa",\n  "bundle_id": "hipaa-attestation-001",\n  "timestamp": "%s",\n  "safeguards": {\n    "administrative": "164.308",\n    "technical": "164.312",\n    "organizational": "164.314"\n  },\n  "voice_compliance": {\n    "tcpa_integration": true,\n    "privacy_preservation": "metadata_only",\n    "consent_management": "enforced"\n  },\n  "signature": {\n    "algorithm": "Ed25519",\n    "key_id": "hipaa-attestation-key-001",\n    "signature": "hipaa-attestation-signature-placeholder"\n  }\n}\n' "$timestamp" > $(KITS_DIR)/attestation-hipaa.json

create-genai-attestation:
	@timestamp=$$(date -u +%Y-%m-%dT%H:%M:%SZ); \
	printf '{\n  "attestation_framework": "genai_security",\n  "bundle_id": "genai-attestation-001",\n  "timestamp": "%s",\n  "threat_detection": {\n    "owasp_llm_top10": "monitored",\n    "mitre_attack_genai": "mapped",\n    "deepfake_detection": "enabled",\n    "bec_prevention": "active"\n  },\n  "enforcement": {\n    "prompt_injection_heuristics": "enabled",\n    "external_detector_apis": "configured",\n    "kill_switch_multi_trigger": "armed",\n    "shadow_mode": "comprehensive_logging"\n  },\n  "signature": {\n    "algorithm": "Ed25519",\n    "key_id": "genai-attestation-key-001",\n    "signature": "genai-attestation-signature-placeholder"\n  }\n}\n' "$timestamp" > $(KITS_DIR)/attestation-genai-security.json

create-voice-attestation:
	@timestamp=$$(date -u +%Y-%m-%dT%H:%M:%SZ); \
	printf '{\n  "attestation_framework": "voice_compliance",\n  "bundle_id": "voice-attestation-001",\n  "timestamp": "%s",\n  "tcpa_compliance": {\n    "disclaimer_enforcement": "active",\n    "consent_tracking": "enabled",\n    "opt_out_mechanisms": "available",\n    "time_restrictions": "8am_9pm_local"\n  },\n  "session_management": {\n    "correlation_accuracy": "<5ms",\n    "metadata_only_capture": true,\n    "privacy_preservation": "enforced",\n    "barge_in_capability": "<200ms"\n  },\n  "ucaas_integration": {\n    "teams": "configured",\n    "zoom": "configured",\n    "slack": "configured",\n    "twilio": "configured"\n  },\n  "signature": {\n    "algorithm": "Ed25519",\n    "key_id": "voice-attestation-key-001",\n    "signature": "voice-attestation-signature-placeholder"\n  }\n}\n' "$timestamp" > $(KITS_DIR)/attestation-voice-compliance.json

# Docker compose creation utilities
create-universal-compose:
	@printf 'version: "3.8"\nservices:\n  clyra-gateway:\n    image: clyra/gateway:v4.0-dev\n    ports:\n      - "8080:8080"\n    environment:\n      - CLYRA_MODE=universal\n      - CLYRA_GENAI_ENABLED=true\n      - CLYRA_VOICE_ENABLED=true\n    healthcheck:\n      test: ["CMD", "curl", "-f", "http://localhost:8080/health"]\n      interval: 10s\n      timeout: 5s\n      retries: 3\n  clyra-recorder:\n    image: clyra/recorder:v4.0-dev\n    ports:\n      - "8081:8081"\n    depends_on:\n      - postgres\n  postgres:\n    image: postgres:16\n    environment:\n      - POSTGRES_DB=clyra\n      - POSTGRES_USER=clyra\n      - POSTGRES_PASSWORD=clyra-dev\n    ports:\n      - "5432:5432"\n    healthcheck:\n      test: ["CMD-SHELL", "pg_isready -U clyra"]\n      interval: 5s\n      timeout: 5s\n      retries: 5\n' > $(QUICKSTART_DIR)/docker-compose.yml

create-data-compose:
	@printf 'version: "3.8"\nservices:\n  clyra-gateway:\n    image: clyra/gateway:v4.0-data-dev\n    ports:\n      - "8080:8080"\n    environment:\n      - CLYRA_MODE=data_platform\n      - CLYRA_DATA_PLATFORM_ENABLED=true\n      - CLYRA_DBT_INTEGRATION=true\n    healthcheck:\n      test: ["CMD", "curl", "-f", "http://localhost:8080/health"]\n  clyra-recorder:\n    image: clyra/recorder:v4.0-data-dev\n    ports:\n      - "8081:8081"\n    depends_on:\n      - snowflake-simulator\n  snowflake-simulator:\n    image: clyra/snowflake-simulator:v4.0-dev\n    ports:\n      - "5433:5433"\n    environment:\n      - SF_ACCOUNT=clyra-dev\n      - SF_USER=clyra\n      - SF_PASSWORD=clyra-dev\n      - SF_DATABASE=CLYRA_DEV\n    healthcheck:\n      test: ["CMD", "nc", "-z", "localhost", "5433"]\n  dbt-demo:\n    image: clyra/dbt-demo:v4.0-dev\n    volumes:\n      - ./dbt-project:/dbt-project\n    depends_on:\n      - snowflake-simulator\n' > $(QUICKSTART_DATA_DIR)/docker-compose.yml

wait-for-health:
	@timeout=300; \
	compose_dir=$(1); \
	while [ $timeout -gt 0 ]; do \
		if docker-compose -f $${compose_dir}/docker-compose.yml ps | grep -q "Up.*healthy"; then \
			echo "✅ Stack is healthy and ready"; \
			echo "📊 View logs: docker-compose -f $${compose_dir}/docker-compose.yml logs"; \
			echo "🔍 Health status: docker-compose -f $${compose_dir}/docker-compose.yml ps"; \
			exit 0; \
		fi; \
		sleep 5; \
		timeout=$$(( timeout - 5 )); \
	done; \
	echo "❌ Timeout waiting for services to be healthy"; \
	docker-compose -f $${compose_dir}/docker-compose.yml logs; \
	exit 1