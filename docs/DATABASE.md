# Database review

Begin with the actual storage model and workload. Relational, document, embedded, key-value, and vector stores have different integrity and concurrency mechanisms. The question is whether the chosen mechanism protects the application's invariants.

| Area | Evidence to inspect | Failure to investigate |
| --- | --- | --- |
| Schema and integrity | Models, constraints, validation, ownership keys | Orphans, invalid states, tenant-crossing references |
| Query shape | Real call paths, pagination, query plans, slow-query telemetry | N+1 work, scans, unstable ordering, large payloads |
| Indexes | Filters, joins, sort order, cardinality, write rate | Missing useful indexes or excessive write amplification |
| Transactions | Multi-step mutations, isolation, uniqueness, locks | Lost updates, overselling, duplicate side effects |
| Connections | App/worker pools, replica ceilings, reserved capacity | Autoscaling exhausts database connections |
| Migrations | History, deployed schema metadata, compatible rollout | Drift, partial migration, old code unable to run |
| Lifecycle | Retention, deletion, cascades, archive/recovery policy | Unbounded tables or accidental deletion fan-out |
| Replication | Lag, read routing, failover assumptions | Stale reads after writes, unsafe promotion |
| Vectors/documents | Ownership filters, index updates, deletion propagation | Cross-tenant retrieval or stale sensitive records |
| Recovery | Backup metadata and isolated restore drill | Backup exists but cannot restore a usable application |

Foreign keys do not universally create indexes on referencing columns. Check the selected engine and relevant access/deletion paths; do not recommend an index on every FK without considering workload. JSON and denormalization are choices to evaluate, not automatic defects.

## Trace a critical mutation

Follow validation → authorization → reads → writes → external side effects. Identify the invariant, concurrent contenders, crash points, and retry behavior. A database transaction cannot automatically roll back an email or payment. Check idempotency keys, uniqueness, durable handoff, and reconciliation where needed.

## Inspect without harming production

Prefer schema metadata, existing telemetry, sampled/redacted plans, and a representative staging dataset. Bound every live query. Execution-producing plan analysis can run writes or expensive work; it requires explicit approval. Do not scan private records merely to prove access.

Review timeouts, lock waits, long transactions, pooling mode compatibility, and maximum connection budgets. Compare migration and application behavior across old/new revisions before recommending rollback.

## Choose infrastructure deliberately

A familiar database is not automatically wrong, and a new managed platform is not automatically better. For any stay/migrate recommendation, state the measured constraint, cost, operational capacity, data movement, outage risk, compatibility, and rollback path.

See [scale modelling](SCALE_MODEL.md) and [cloud/recovery guidance](CLOUD_AND_DEVOPS.md). Report missing access separately from missing controls.
