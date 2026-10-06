# Security review

Start with assets, actors, trust boundaries, and reachable entry points. Apply checks to the discovered architecture. A local utility and an internet-facing multi-tenant service do not have the same exposure.

Use the [OWASP Top 10](https://owasp.org/projects/top-ten) and [OWASP API Security project](https://owasp.org/API-Security/) as reference material. Record the edition consulted when using specific categories. This toolkit is not an OWASP certification or an exhaustive security standard.

## Trace controls, not names

| Surface | Review question | Useful evidence |
| --- | --- | --- |
| Authentication/sessions | Can tokens, sessions, or reset flows be replayed or confused? | Lifecycle, expiry/revocation, cookie flags, negative tests |
| Authorization / IDOR / BOLA | Does the current actor own or have permission for every supplied object? | Complete call path and actor/resource/action matrix |
| Browser/API boundary | Are XSS, CSRF, CORS, redirects, and unsafe rendering addressed for the actual flow? | Encoding, framework behavior, origin checks, headers |
| Injection | Can input reach SQL, shell, templates, or executable expressions unsafely? | Parameterization and sink tracing |
| SSRF / paths | Can a user reach internal networks or escape an allowed storage path? | URL/path validation, redirect/DNS behavior, network limits |
| Files | Are size, type, decompression, parsing, and access bounded? | Upload/processing pipeline and isolated negative fixtures |
| OAuth/webhooks | Are state, redirect binding, signatures, time windows, and duplicates handled? | Verified flow, signed raw bytes, replay/idempotency tests |
| Abuse | Can anonymous or low-privilege callers exhaust resources or spend money? | Distributed limits, quotas, authorization, spend enforcement |
| Privileged endpoints | Are admin/debug routes exposed or protected inconsistently? | Route inventory, role checks, deployed routing |
| Data lifecycle | Are secrets/PII logged or retained after deletion? | Redacted log schemas, retention and deletion propagation |
| Infrastructure/supply chain | Can broad credentials or untrusted build input reach production? | IAM, storage/network access, CI permissions, dependency/artifact provenance |

Rate limits need a stated scope: process, replica, tenant, account, or global. A single-process limiter may be sufficient for a bounded deployment; do not demand shared infrastructure without examining the threat and scaling model.

## Multi-tenant verification

Use synthetic tenants A and B and an explicit permissions matrix. Cover READ, MODIFY, DELETE, PUBLISH, and TRIGGER WORK for workspace, organization, project, asset, file, billing, and integration identifiers. Include batch and nested routes, caches, storage URLs, exports, background jobs, search, and vector retrieval.

Approved active tests must assert both rejection and absence of side effects. A denied response after a job was already enqueued is still a boundary failure. Never attempt writes against real customer resources. Without an isolated test environment, trace statically and record the unresolved verification.

Confirmed cross-tenant leaks generally warrant P0. Try to disprove the finding through the complete path and compensating controls before confirming it; retain urgent unverified risks as provisional.

## Handling evidence

Do not print secret values or customer data to prove a leak. Use redacted metadata or synthetic markers. Do not publish live vulnerability details in this toolkit's issues. Follow the affected project's private disclosure process.

This is a systematic second opinion, not a penetration test or compliance review. See [severity guidance](SEVERITY_MODEL.md) for launch decisions and [AI guidance](AI_APPLICATIONS.md) for model/tool boundaries.
