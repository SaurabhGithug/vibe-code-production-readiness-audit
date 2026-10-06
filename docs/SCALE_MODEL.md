# Model scale before claiming it

Capacity depends on a workload, configuration, dataset, and service-level target. Start with 100, 500, 5,000, and 25,000 concurrent users, then adapt these levels to the product. A batch processor may need jobs/hour; a mobile backend may need sync bursts.

## Define demand

Record active sessions, journey mix, requests/journey, think time, response time, background jobs/journey, payload and object sizes, cache behavior, database size, and provider quotas. Include peak-to-average ratios and tenant skew.

Useful approximations under stable conditions:

- Closed interactive workload: throughput ≈ concurrent active users / (think time + response time), when each cycle makes one request. Account explicitly for multi-request journeys.
- Little's Law: in-flight work ≈ arrival rate × average time in system. State units and avoid applying steady-state reasoning to an unbounded growing queue.
- Worker service capacity ≈ workers × concurrent slots per worker / mean job duration. Sustainable arrivals need headroom below this value.
- Connection ceiling ≥ application replicas × pool size + workers × worker pool size + migration/admin/reserved connections.

These are models, not proof. Retries, cold starts, lock contention, tail latency, autoscaling delays, and nonuniform tenants can change the outcome substantially.

## Fictional worked example

Assume each active user sends one request per ten seconds. Eight worker slots each complete a job in four seconds. Ten percent of requests enqueue one job. Ignore bursts and retries only for this illustration.

| Concurrent users | Requests/second | Jobs/second | Worker capacity | Implication |
| --- | --- | --- | --- | --- |
| 100 | 10 | 1 | 2 jobs/s | Average demand fits; tails and other components remain untested |
| 500 | 50 | 5 | 2 jobs/s | Queue grows by about 3 jobs/s |
| 5,000 | 500 | 50 | 2 jobs/s | Queue grows by about 48 jobs/s |
| 25,000 | 2,500 | 250 | 2 jobs/s | Admission control or capacity changes needed |

**MODELLED — NOT VERIFIED.** These assumptions say nothing about the capacity of a real application. They expose a worker constraint; without query and provider measurements they cannot establish the first bottleneck in the whole system.

For every level, fill the [report's scale table](../REPORT_TEMPLATE.md): first bottleneck, second bottleneck, catastrophic failure, mitigation, evidence, and uncertainty. “Ordering unknown; measure database saturation and provider quota headroom” is better than invented precision.

## Cover the resource envelope

Check CPU, memory, network/egress, database query cost and connections, queue depth/oldest age, worker slots, external quotas, storage throughput/capacity, cron overlap, cache effectiveness, browser sessions, and media processing. Model a slow provider and a retry burst. Consider recovery time after demand falls, not just peak throughput.

Try simple mitigations first: query/index changes, pagination, bounded concurrency, timeouts, admission control, and a suitably sized instance. Separate workers or add infrastructure when the failure model supports it.

## Staging-only verification plan

1. Record approval, isolated target, revision, production differences, synthetic tenants/data, spend cap, and owner.
2. Choose realistic golden journeys and warm/cold paths. Stub external paid actions unless explicitly approved.
3. Establish a baseline; ramp gradually; hold representative steady demand; exercise an approved burst; observe recovery.
4. Set numeric stop thresholds for errors, p95/p99 latency, memory, connections, queue age, and spend before execution.
5. Capture throughput, latency distributions, resource use, queries, queues, quotas, and cost. Preserve sanitized results and clean up approved test data.

Use **MEASURED** only with environment, workload, duration, revision, and results. A passing staging test applies to its tested configuration. Extrapolation remains MODELLED — NOT VERIFIED.
