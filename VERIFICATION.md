# FIREWATCH Sentinel v9.0.0 — Verification Record

## Local test and coverage results

- Pytest collection: **5,931 test cases across 60 modules** (`docs/TEST_MANIFEST_V9.json`).
- Full regression suite without Coverage instrumentation: **passed**, zero failures/errors/skips reported.
- Combined Python statement coverage: **85.81%**, measured with 8 deterministic shards; all shards were run against the same collected-test fingerprint. The configured minimum gate is 80%.
- New hardening tests cover bounded streamed response bodies, unexpected content encodings, invalid body-size configuration, report paths outside the scan directory, path traversal/symlink escape, download size ceilings, and Production API-docs configuration.
- Existing API integration tests verify that in-scope reports remain downloadable and bundles include matching SHA-256/size manifests. The standalone report-bundle verifier validates archive paths, manifest/file agreement, lengths and hashes.
- Catalogue validation: 67 selected standards/framework references, 32 domains, and 469 curated checklist control objectives. All references map to at least one control; generated JSON/CSV/Markdown, assessment plan, Test Manifest/Matrix, and declared dependency inventory regenerated successfully.
- Assessment plan exports 79 cases: 22 passive automated observations, 13 review candidates requiring validation, 38 requiring manual/test-account context, and 6 requiring specialist tools.
- Python compilation, JavaScript syntax, publisher shell syntax, Docker Compose YAML parsing, repository hygiene, generated inventories and report-bundle verification passed locally.

## Not run / not independently verified

Bandit, `pip-audit`, Docker CLI/image build, hosted GitHub Actions and hosted CodeQL were not executed in this environment. Playwright's real Chromium browser may need installation in the deployment environment. The generated dependency inventory is based on declared requirements and constraints; it is **not** a resolved SBOM and is **not** a vulnerability audit. The report manifest hashes provide integrity relative to the manifest but are not a digital signature or proof of publisher identity.

## Known industrial deployment blockers

- The shared API-key gate is not multi-tenant identity or resource-level authorization. `project_key` in the standards module partitions checklist state but is not a security boundary.
- Scope checks resolve hostnames but do not pin the validated IP address to the final network socket. Use an egress firewall/proxy and independent network policy to mitigate DNS rebinding/SSRF exposure.
- The ZAP adapter generates a passive Automation Framework plan and checks service reachability; it does not automatically execute a full ZAP scan or import ZAP alerts into findings.
- The database uses `create_all()` and has no versioned Alembic migration framework. Production upgrades need a separately rehearsed migration and rollback process.
- Worker lease/heartbeat-based crash recovery and stale-job reassignment are not complete. External-worker production deployments need supervision and operational recovery procedures.
- TLS termination, secret-manager/KMS integration, key rotation, backup/restore drills, observability/alerting, incident response and independent penetration testing remain deployment/release gates.

The project should be described as a hardened, scope-controlled security assessment tool—not defect-free, clause-complete, certified, or capable of proving that a website contains no vulnerabilities. A lack of findings is not proof of security or standards compliance.
