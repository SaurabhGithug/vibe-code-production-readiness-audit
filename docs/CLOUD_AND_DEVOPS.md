# Cloud, delivery, and recovery

Follow one release from Git to the running artifact. Match branch/ref, commit, build inputs, immutable artifact identity, environment configuration, schema, and deployed revision. A deployment dashboard and a local checkout may describe different systems.

## Delivery and infrastructure

| Area | Verify | Failure to investigate |
| --- | --- | --- |
| Git and CI gates | Required checks, review policy, protected deployment permissions | Untested or unreviewed changes reach production |
| Build | Locked inputs, reproducible process, dependency/image provenance | Same commit produces a different or untrusted artifact |
| Untrusted PRs | Minimal token permissions and no privileged secret execution | Contributor-controlled code gains deployment credentials |
| Environments | Separate credentials/data, deliberate configuration, migration order | Staging writes production or secrets drift |
| Runtime | Appropriate non-root/container limits where used, health/readiness checks | Unhealthy instance receives traffic or exhausts shared resources |
| Release | Draining, compatibility, rollback ownership and evidence | Old code cannot run against a new schema |
| IAM/network/storage | Least privilege, service account scopes, intended exposure | A low-trust component reaches privileged data |
| Configuration | Infrastructure as code plus recorded manual state | Production cannot be recreated |
| Regions/quotas | Placement, latency, provider ceilings, autoscaling caps | Cross-region latency or scaling exhausts another resource |
| Schedulers | Timezone, overlap prevention, catch-up, missed-run alerts | Duplicate or silently skipped critical work |

Review Docker/Kubernetes controls only where used. Managed services, VMs, serverless platforms, and simple monoliths can all be appropriate. Recommend operational complexity only with a demonstrated requirement.

## Async and workload boundaries

Trace durable job acceptance, database/enqueue gaps, acknowledgment, lease expiry, retry/dead-letter behavior, idempotent side effects, and recovery ownership. Consider process death, scale-down, release interruption, and a 10,000-job burst.

Check CPU, memory, disk, database connections, browser sessions, FFmpeg/media tasks, AI concurrency, and cron contention. Bounded admission or a small worker service may solve a problem without a large distributed architecture.

## Smallest useful operational view

Start with availability, throughput, p50/p95/p99 latency, error rate, resource/connection saturation, queue oldest age/depth, failed jobs, provider errors/quotas/spend, scheduled-task freshness, and backup freshness where relevant.

Each alert needs a source, actionable threshold or baseline, owner, and response. Check delivery evidence. Correlate requests and jobs without logging tokens, customer content, or unbounded metric labels.

## Recovery is a procedure with evidence

Inventory database, objects, configuration, secrets, deployable artifacts, queues/in-flight jobs, and integrations. Establish RPO (maximum acceptable data-loss window) and RTO (maximum acceptable service-restoration time). Keep business targets separate from observed drill results.

Inspect backup existence, retention, access separation, alerts, and restoration instructions. A successful backup job does not prove restoration. Propose an approved isolated drill that restores a representative snapshot, starts compatible application code, validates golden flows and object references, reconciles pending work, and measures actual loss/time.

Check whether keys and secrets can be recovered securely when the primary account or region is unavailable. Recovering a container image is not recovering its data. Do not restore over production or change live infrastructure during the audit.

## Failure and load plans

Plan controlled database/cache/queue/provider/storage/network failures, 429s, timeouts, corrupt files, worker crashes, and deployment during a job. Define expected containment, user-visible response, data integrity, observability, recovery, stop conditions, and cleanup.

Load plans belong in isolated staging with realistic user journeys, synthetic data, resource limits, and a spend cap. Merely reading configuration does not verify runtime recovery. See [scale guidance](SCALE_MODEL.md) and the [report template](../REPORT_TEMPLATE.md).
