# Human production-readiness checklist

Use without an agent. Tick a box when the review is completed, **not when the control passes**. Record IMPLEMENTED / PARTIAL / MISSING / NOT NEEDED, evidence, and finding ID beside it or in the [report](REPORT_TEMPLATE.md). Leave status unassigned if unknown. Explain non-applicability. Default to read-only; active tests require authorization and isolated synthetic data.

## Git / source of truth

- [ ] Identify repository, branch, HEAD, upstream, sanitized remote, and ref freshness.
- [ ] Record dirty/untracked work, stashes, worktrees, and local-only/remote-only commits without changing them.
- [ ] Reconcile release candidate, deployment branch, production commit, and deployed artifact/environment.
- [ ] Define scope, allowed actions, evidence gaps, and active-agent boundaries.

## Architecture

- [ ] Discover actual frontend/backend, data stores, auth, providers, and deployment components.
- [ ] Trace golden journeys and mark trust boundaries, data ownership, and synchronous/async work.
- [ ] Distinguish declared dependencies, wired code, and deployed behavior.
- [ ] Rank duplicate/dead systems by reachable failure or maintenance impact.

## Full stack

- [ ] Review client/server boundaries, API contracts/versioning, validation, and error semantics.
- [ ] Trace authentication, sessions, authorization, and negative cases through each critical flow.
- [ ] Check pagination, state/data fetching, caching, transactions, races, and idempotency.
- [ ] Review uploads/media limits, accessibility basics, production builds, and E2E coverage.
- [ ] Find silent errors, fake fallbacks, unsafe casts, hardcoded paths, partial migrations, and unwired code.

## Database

- [ ] Check schema/integrity, query-shaped indexes, FK index needs, JSON/documents, and N+1 paths.
- [ ] Inspect transactions, locks, pooling, connection ceilings, query timeouts, and slow-query evidence.
- [ ] Check migration drift, backward compatibility, retention, deletion, cascades, and growth.
- [ ] Assess vectors/replication where used; justify current platform or migration by evidence.

## Security

- [ ] Trace IDOR/BOLA, privilege escalation, admin/debug routes, sessions, and brute-force controls.
- [ ] Examine injection, XSS, CSRF, SSRF, path traversal, redirects, CORS, and security headers.
- [ ] Review OAuth, webhook signature/replay protection, uploads, and decompression limits.
- [ ] Check secrets, sensitive logging, PII handling, account deletion, dependencies, and CI supply chain.
- [ ] Attempt to disprove serious findings and distinguish confirmed from provisional results.

## Tenancy

- [ ] Establish tenancy model and actor/resource/action ownership rules, or justify NOT NEEDED.
- [ ] Review cross-tenant READ, MODIFY, DELETE, PUBLISH, and TRIGGER WORK paths.
- [ ] Include batch/nested IDs, workers, caches, storage, signed URLs, exports, billing, and vector search.
- [ ] Plan or execute authorized synthetic A/B tenant tests and check absence of side effects.

## AI

- [ ] Inventory models, agents, tools, embeddings, scrapers, and all provider call sites.
- [ ] Trace auth, key isolation, quotas, atomic budgets, retries/fallbacks, and cost reconciliation.
- [ ] Check prompt/tool injection, retrieval isolation, structured outputs, and use-case evaluations.
- [ ] Ensure untrusted content cannot authorize tools or consequential external actions.

## Async

- [ ] Verify durable acceptance, retries, acknowledgment, leases, dead letters, and cancellation.
- [ ] Check duplicate delivery, idempotency, database/enqueue gaps, and reconciliation.
- [ ] Analyze request end, crash, deploy, scale-down, and 10,000-job burst behavior.
- [ ] Check heavy-work isolation and cleanup of browsers, subprocesses, and temporary files.

## Scale

- [ ] Define concurrency, journey mix, request/job rates, data volume, and workload assumptions.
- [ ] Model 100 / 500 / 5,000 / 25,000 concurrent users or justify different levels.
- [ ] Identify first/second bottlenecks, catastrophic failure, and mitigation for each level.
- [ ] Include CPU, memory, connections, network, workers, APIs, storage, cron, cache, browsers, and media.
- [ ] Separate MEASURED results from MODELLED — NOT VERIFIED; do not invent capacity.

## DevOps

- [ ] Trace commit → CI → artifact → deployment; review gates and reproducibility.
- [ ] Check environment separation, migrations, health checks, draining, and code/schema rollback.
- [ ] Verify scheduler overlap behavior and release ownership/runbooks.

## Cloud

- [ ] Inspect IAM/service accounts, network/storage exposure, DNS/TLS, and secret access.
- [ ] Reconcile infrastructure as code with accessible deployed settings and manual drift.
- [ ] Check autoscaling ceilings, regions, quotas, and shared resource failure domains.
- [ ] Determine whether production can be recreated without undocumented manual state.

## Observability

- [ ] Verify availability, throughput, p50/p95/p99 latency, errors, and resource saturation evidence.
- [ ] Inspect queue depth/age, job failures, provider health/spend, and scheduled-task freshness.
- [ ] Check trace correlation, redaction, actionable alerts, owner, and delivery evidence.
- [ ] Propose the smallest useful dashboard and response instructions.

## Backup

- [ ] Verify database/object/configuration/secret recovery coverage and retention.
- [ ] Record backup success separately from isolated restore drill evidence.
- [ ] Compare RPO/RTO targets with measured recovery and check artifact rollback.
- [ ] Account for in-flight jobs, missing objects, integrations, and post-restore reconciliation.

## Testing

- [ ] Classify unit, integration, API, contract, E2E, security, tenancy, load, failure, and deployment tests.
- [ ] Identify critical golden flows and mocking that hides real boundaries.
- [ ] Plan safe database/cache/queue/provider/storage/network failure cases and recovery checks.
- [ ] Define staging-only realistic load stages, spend limits, stop thresholds, and cleanup.
- [ ] Separate inspected, executed, skipped, and proposed tests with revision/environment evidence.

## Cost

- [ ] Model compute, data, storage, egress, AI, media, browsers, queues, email, and APIs.
- [ ] Include retries, failures, idle floors, retention, current price sources, and uncertainty.
- [ ] Calculate cost per successful flow/customer and break-even or COST > REVENUE conditions.
- [ ] Review abuse paths and distinguish budget alerts from enforceable spending controls.

## Release readiness

- [ ] Assign scoped maturity and YES / YES WITH CONDITIONS / NO with evidence.
- [ ] Independently recheck P0/P1 premises; unresolved critical unknowns remain visible.
- [ ] Complete the four-foundation matrix and explain what is NOT NEEDED yet.
- [ ] Order NOW / WEEK 1 / WEEK 2 / WEEK 3 / LATER with owners and acceptance checks.
- [ ] Keep fixes separately authorized and redact reports before sharing.
