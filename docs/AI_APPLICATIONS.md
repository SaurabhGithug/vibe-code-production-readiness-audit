# AI and agentic application review

Apply this guide when the project uses models or agents. Discover LLMs, image/video generation, TTS, ASR, embeddings, search, scrapers, browser automation, and tools. Inventory each call site, including workers, cron, fallback providers, and direct SDK calls.

The [OWASP GenAI risk reference](https://genai.owasp.org/llm-top-10/) provides additional context for model-specific threats. Use current provider documentation for pricing and data-handling claims; record dates and assumptions.

## Follow the whole generation

Trace identity → tenant authorization → budget reservation → provider request → streaming/job lifecycle → persisted result → usage reconciliation → optional external action.

| Control | Evidence to seek | Failure pattern |
| --- | --- | --- |
| Authentication and keys | Server-side credential storage and scoped access | Public endpoint or client bundle exposes paid capability |
| Budgets/quotas | Atomic reservation before work, bounded reconciliation after work | Concurrent requests all pass the same remaining-budget check |
| Retries/fallbacks | Shared spend budget, attempt ceiling, timeout/cancellation | Each fallback silently starts another full-price request |
| Cost tracking | Provider/model, billed units, tenant, request/job ID, failed work | Successful responses tracked but aborted streams omitted |
| Retrieval | Authorization before search and on results, deletion propagation | Another tenant's material enters model context |
| Structured output | Schema/business-rule validation and safe rendering | Model text becomes executable code, SQL, or trusted HTML |
| Tools | Server-side allowlists, argument validation, user/tenant permission checks | Model chooses a tool or object it has no authority to use |
| External actions | Explicit user intent, scope, idempotency, confirmation when consequential | Retrieved text triggers publishing, payments, deletion, or messages |
| Quality | Representative evaluations, uncertainty handling, grounded citations where needed | Plausible output is treated as verified fact |
| Data lifecycle | Minimization, retention, provider boundaries, deletion behavior | Sensitive prompts persist beyond the product's policy |

Provider calls should not bypass the same guard through a different route, worker, SDK, or emergency fallback. Search reachable call sites and compare their enforcement. A central wrapper existing does not establish coverage.

## Untrusted content remains data

Web pages, documents, emails, social posts, comments, and retrieved context can contain instructions. Those instructions must not grant tool permissions, change tenant scope, reveal secrets, or override user intent. Prompt wording alone is not a security boundary: enforce authority in application code and restrict tool credentials.

Use synthetic malicious documents to test the boundary in an approved environment. Prefer inert tools or dry-run effects. Do not let a test send real messages or invoke paid models without explicit scope.

## Bound cost and work

Check global and tenant limits, maximum input/output sizes, tool-loop iterations, browser lifetime, media duration/resolution, concurrent jobs, retry budgets, and cancellation cleanup. Distinguish spend alerts from hard admission controls. Record behavior when usage data is delayed or the billing service fails.

Do not require an elaborate agent platform when a bounded single-model call meets the need. See [cost and scale reporting](../REPORT_TEMPLATE.md) for consistent evidence.
