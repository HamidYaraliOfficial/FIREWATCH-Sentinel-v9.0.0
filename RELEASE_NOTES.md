# FIREWATCH Sentinel v9.0.0 — Final Release

FIREWATCH Sentinel is an evidence-driven, scope-controlled platform for authorized web application security assessment. This release keeps the existing v9 Standards & Assurance workspace and adds release hardening for response capture, report downloads, production API documentation, and scan completion semantics.

## Final-release hardening

- **Bounded HTTP response capture:** the HTTP client streams raw bytes and caps the amount retained for parsing (`MAX_RESPONSE_BODY_BYTES`, default 2,000,000; accepted configuration range 1,024–25,000,000). Unexpected compressed responses are not decompressed or parsed; affected body coverage is called out as inconclusive.
- **Report path confinement:** report file downloads resolve the stored path and require it to remain beneath `REPORT_DIR/<scan-id>/`; symlink/path escape attempts are rejected. Single-report size is capped at 32 MiB; bundle uncompressed and final archive sizes are capped at 64 MiB.
- **Atomic completion/report publication:** report files are rendered before the terminal status transition. Report records and `completed` state are committed in a guarded transaction; a concurrent cancellation wins the compare-and-swap and orphaned output is cleaned.
- **Production documentation gate:** interactive Swagger, ReDoc, and OpenAPI endpoints are disabled when `ENVIRONMENT=production` or `prod`.
- **Report access log:** successful single-report and bundle download requests emit a structured log with scan ID, format, and access type; no target URL, API key, or credential value is logged.
- **Final product branding:** product display name is FIREWATCH Sentinel; repository URL remains `HamidYaraliOfficial/FIREWATCH-WebSec-Agent` for backward-compatible publishing.

## Included platform features

- Bounded crawler, scope/host/port/path policy, robots/sitemap guidance, JavaScript route heuristics, optional same-scope Playwright inventory, OpenAPI/Swagger and GraphQL discovery.
- Passive and low-impact read-only rules for HTTP security headers, TLS, cookies, CORS, caching, information disclosure and selected query-parameter reflection candidates.
- Encrypted-at-rest authentication configuration, root-origin credential isolation, evidence redaction, finding deduplication and confidence/risk scoring.
- HTML, JSON, CSV, Markdown and SARIF 2.1.0 reports; report ZIP with SHA-256 integrity manifest and independent verifier.
- Standards & Assurance module: 67 selected references, 32 domains and 469 paraphrased control objectives, plus JSON/CSV/Markdown and Excel assets.
- FastAPI dashboard/API, local demo target, Docker Compose configuration, GitHub Actions/CodeQL definitions, publishing helpers and operational documentation.

## Local verification record

- Pytest collection: **5,931 tests across 60 modules**.
- Full regression suite: **passed**, zero failures/errors/skips reported.
- Combined Python statement coverage: **85.81%**, using 8 deterministic shards with the same collection fingerprint; minimum gate is 80%.
- New response-limit, report-path traversal/symlink, report-size policy and production docs-option tests pass.
- Repository hygiene, Python compilation, JS syntax, shell syntax, Docker Compose YAML parsing, assessment/test-manifest/dependency-inventory generation and report-bundle integrity verification passed locally.

## Explicit limits and not-yet-verified checks

This is a final local release candidate, not a claim of defect-free or fully certified software. The current common API-key model and checklist `project_key` are **not** tenant-level RBAC/ABAC; do not host mutually untrusted customers without adding and independently testing identity and per-resource authorization. DNS answers are checked but not pinned to the connected socket; deploy an outbound firewall/proxy and do not rely on application checks alone against DNS rebinding/SSRF. The ZAP adapter currently writes a passive Automation Framework plan and checks reachability; it does not execute a complete ZAP scan. The database has no Alembic migration framework, so existing deployments require an explicit migration plan before upgrades. Worker crash recovery/lease-based reassignment is not complete.

Bandit, `pip-audit`, Docker image build, hosted GitHub Actions and hosted CodeQL are unverified in the build environment. The dependency inventory lists declared constraints and is not a resolved SBOM or vulnerability audit. A zero-finding scan is not proof of security; authorization, business logic, exploitability, test-account workflows and conditional standards controls may require manual validation.
