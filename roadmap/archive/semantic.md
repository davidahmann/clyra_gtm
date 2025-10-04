Open Control Plane – MVP (v0.1)

📖 Description

Clyra Open Control Plane is an open-source, neutral semantics + policy layer for multi-engine data estates. It unifies metric definitions and access policies across Snowflake, Databricks, Trino, and Iceberg catalogs, and produces auditable evidence receipts for every enforcement decision.

It is not a new catalog, BI tool, or discovery crawler. Instead, it sits above existing catalogs and engines, compiling policies and semantics into native artifacts, and logging tamper-proof receipts auditors can verify.

⸻

💡 Value Proposition
 • For engineers: One spec (semantics.yaml, policy.yaml) defines metrics and access once, enforced everywhere. No more drift between Snowflake, Trino, and Databricks. Lightweight adapters and OSS tooling fit directly into dbt, CI/CD, and data engineering workflows.
 • For CISOs/CDOs: A unified policy plane across all engines, with enforcement mapped to regulatory frameworks (SOX, PCI, HIPAA, EU AI Act). Every decision generates a signed receipt → fewer audit exceptions, faster compliance prep.
 • For auditors/finance: Evidence bundles tie policies, semantics, and execution context into verifiable, signed artifacts. “One metric, one policy, consistent everywhere” with proof you can file.
 • For AI agents/LLMs: A safe “semantic API” endpoint provides agents with metric definitions + policy-scoped SQL, ensuring agent queries are safe-by-construction.

⸻

🛠️ MVP Scope (v0.1)

Specs (OSS-first)
 • semantics.yaml: entities, metrics, dimensional grains, constraints.
 • Bridge to dbt Semantic Layer to avoid reinvention.
 • policy.yaml: subjects, attributes, masking rules, row filters, purpose tags.
 • Includes control mappings (SOX, PCI DSS, HIPAA, EU AI Act).

Adapters (read/write)
 • Catalogs: Polaris (Iceberg REST, OSS baseline), Unity Catalog (read), Nessie (read).
 • Engines:
 • Snowflake: compile to Dynamic Data Masking + Row Access Policies.
 • Databricks/Spark: Unity views + column masking UDFs.
 • Trino/Starburst: SQL rewriter + connector-level row/column filters.

Enforcement + Identity
 • Identity bridge: OIDC groups → engine roles, attribute resolver for dept/region/purpose.
 • Approvals: lightweight TTL-based exceptions (Slack/Jira integration optional).

Evidence Journal
 • Append-only, signed decision logs:
 • decision_id, policy_id, semantic_version, engine target + artifact, identity, timestamp.
 • Regulatory control tags (SOX/PCI/etc.).
 • Verifier CLI: offline check of receipts → JSON + human-readable SOX-mapped PDF.

Agent Endpoint (read-only, minimal)
 • API to resolve metric definitions and return policy-scoped SQL queries → safe for LLM/agent use.

⸻

🚫 Non-Goals (v0.1)
 • No new catalog (bind to Polaris/Unity/Nessie).
 • No BI tool integration (Power BI/Tableau can come later).
 • No full discovery crawler (leave that to Collibra/Alation/Atlan).
 • No Cedar backend yet (OPA/Rego only).

⸻

🎯 Killer Demo (MVP narrative)
 • Stack: Iceberg tables in S3, Polaris catalog, Snowflake + Trino attached.
 • Define once: “Active Customer” metric in semantics.yaml + PII masking in policy.yaml.
 • Run: query from Trino client + Snowflake console → identical metric values, masking enforced.
 • Prove: download an evidence bundle showing SOX tags, compiled artifacts, and signed receipts.

⸻

👉 This way, the MVP delivers engineer adoption hooks (OSS specs + adapters) and executive/auditor value (receipts tied to controls) from day one.
