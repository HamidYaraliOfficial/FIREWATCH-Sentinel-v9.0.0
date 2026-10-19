# FIREWATCH Sentinel v9.0.0 Release Checklist

## Reproducible build gates

- [x] `VERSION`, `backend/app/version.py`, `backend/pyproject.toml`, README, manifest and UI show `9.0.0` / FIREWATCH Sentinel.
- [x] `python -m pytest backend/tests -q` passes all collected tests (5,931 cases across 60 modules).
- [x] Eight staged coverage shards pass with one unchanged test-collection fingerprint; combined Python statement coverage is 85.81% (80% minimum).
- [x] `python -m compileall -q backend/app backend/tests demo_target scripts` passes.
- [x] `python scripts/repo_hygiene.py` passes.
- [x] Assessment catalog, test manifest/matrix, and declared dependency inventory regenerate successfully.
- [ ] Demo scan generates HTML/JSON/CSV/Markdown/SARIF and completed status only after report records are safely published.
- [x] Report path escape/symlink tests and response body caps pass.
- [x] Sample report bundle is validated by `python scripts/verify_report_bundle.py examples/demo_scan/report-bundle.zip`.
- [x] `node --check frontend/static/app.js` and `bash -n scripts/publish_to_github.sh` pass locally.
- [ ] Bandit and `pip-audit` pass in a network/tool-enabled environment.
- [x] `docker-compose.yml` parses as YAML locally.
- [ ] Docker CLI Compose validation and actual image build pass in a Docker-enabled environment.
- [ ] Hosted GitHub Actions and CodeQL are green before a public release.
- [ ] SBOM is resolved from locked dependencies and provenance/release artifacts are signed before making supply-chain authenticity claims.

## Security and operations gates before multi-customer production

- [ ] Implement and independently test OIDC/SSO, per-tenant RBAC/ABAC, and resource-level access control.
- [ ] Add network egress enforcement and resolved-IP pinning/protection against DNS rebinding.
- [ ] Add versioned database migrations, backup/restore drills, worker lease/heartbeat recovery and graceful shutdown tests.
- [ ] Integrate and test KMS/secret-manager key management and rotation.
- [ ] Complete real ZAP execution/alert ingestion if advertised as an integration.
- [ ] Complete load/stress/soak tests and define operational alerts, retention and incident response.
- [ ] Obtain independent security review and penetration testing.

Unexecuted or unverified checks must remain marked as such; do not mark missing tools as a pass.
