# Fictional audit examples

All projects, paths, evidence, and outcomes below are invented for illustration. Do not interpret them as findings about a real application or as universal severities.

## “Redis dependency exists”

**PARTIAL.** The manifest includes a Redis client, but deployment metadata shows no shared limiter configured. The active path falls back to per-instance memory. With multiple replicas, an account can exceed the intended aggregate limit.

Recheck: verify whether the ingress already enforces that exact account limit. If not, choose a shared limiter or a bounded deployment policy justified by the threat model. A missing Redis service alone is not the finding.

## “Backups enabled”

**PARTIAL.** Backup metadata confirms snapshots and retention, but no restore drill has been performed. Recovery remains UNVERIFIED.

Minimum action: restore synthetic or approved data into an isolated environment, validate application/object consistency, and compare observed recovery with RPO/RTO targets. Severity depends on the consequence of data loss and launch requirements.

## “Kubernetes missing”

**NOT NEEDED.** A small service's current load and operating requirements fit its managed platform. No measured constraint justifies cluster operations.

Revisit if deployment isolation, platform limits, or organizational requirements create a concrete need. The absence of a fashionable tool is not a defect.

## “Authentication exists”

**PARTIAL.** Several reachable API routes establish identity but bypass object-level authorization. In an approved synthetic test, tenant A can read tenant B's asset by ID.

**P0, confirmed in the test environment.** The reviewer checked for an upstream ownership guard and found none on that path. The test does not by itself prove which revision is deployed. Fix the shared ownership boundary and test all affected read/write/job paths before launch.

## “1,000 tests pass”

Useful signal, not a readiness verdict. The tests mock the database, queue, and provider and never exercise deployment behavior. Classify their scope accurately; the test-quality control is **PARTIAL** if critical boundaries remain untested.

Minimum action: add a small number of realistic integration, negative authorization, and deployment smoke checks rather than increasing the count for its own sake.

## “No cloud access”

**Status unassigned; evidence UNVERIFIED.** Source declares backups and private storage, but deployed configuration is inaccessible. Record an evidence gap with the metadata or drill needed to resolve it. Do not mark the controls MISSING or NOT NEEDED.

## “A queue will solve it”

**PARTIAL.** Enqueue is durable, but the worker acknowledges before persisting completion and repeats a paid side effect after a crash. Adding another broker does not address the invariant.

Minimum action: define the business idempotency key, acknowledgment/retry semantics, and reconciliation behavior. Verify crash boundaries with inert synthetic effects in approved staging.

## Stack adaptation

| Fictional project | Focus | Likely unnecessary unless requirements change |
| --- | --- | --- |
| Django + PostgreSQL internal tool | Role boundaries, migrations, restore, scheduled work | Multi-region and sharding |
| Go API + MongoDB mobile backend | Document ownership, offline replay, idempotency, connection limits | Relational FK checks applied literally |
| .NET service on VMs with SQL Server | Service identity, patch/release process, transaction and recovery behavior | Mandatory Kubernetes migration |
| Serverless TypeScript + object storage + AI provider | Request lifetime, durable tasks, signed URLs, cost enforcement | Dedicated cache without evidence |
| Rust desktop utility using SQLite | File safety, local persistence, upgrade/backup behavior | Web CORS or tenant tests when no such boundaries exist |

These are starting questions, not prescriptive architecture. Use the [master prompt](../PROMPT.md) to discover the actual system.
