# FIREWATCH Sentinel v9.0.0 — Remaining industrialization roadmap

The current package is a hardened local release candidate. The following work is intentionally not represented as complete because it needs architecture changes and/or independent infrastructure verification.

## P0 — Required before hosting mutually untrusted customers

- Implement OIDC/SSO and tenant-level RBAC/ABAC with a resource-level authorization policy on every scan, report, asset, evidence, and standards route.
- Enforce outbound network scope outside the application using an egress proxy/firewall; design DNS resolution pinning and rebinding resistance.
- Introduce versioned Alembic migrations and rehearse rollback across real PostgreSQL versions.
- Add worker leases/heartbeats, stale-job recovery, retry ceilings, idempotent artifact publication and supervised shutdown.
- Add production secret-manager/KMS integration and rotation without breaking scans already queued.

## P1 — Required before claiming full DAST integration

- Execute ZAP Automation Framework plans in an isolated, authenticated service; constrain context/include/exclude paths and spider behavior; ingest and normalize alerts; test cancellation and timeouts. Current adapter only writes the passive plan and checks reachability.
- Add benchmark fixtures for known-positive/known-negative vulnerabilities; track precision/recall and false-positive rates per rule.
- Expand authenticated browser journeys, object-level authorization test matrices, business-logic workflows and specialist protocol modules with safe, explicit engagement controls.

## P2 — Enterprise operation and supply-chain assurance

- Generate a resolved CycloneDX/SPDX SBOM, run Bandit and `pip-audit`, build/scan OCI images, sign release artifacts and publish verifiable provenance.
- Add metrics, structured event correlation, alerting, retention policy, backup/restore drills, incident response exercises and performance/soak tests.
- Complete external architecture review and independent penetration test; close all critical/high findings before public production deployment.

A green unit test suite and 85.81% code coverage are software quality indicators—not vulnerability detection accuracy, conformance certification, or evidence that the service is safe under every deployment configuration.
