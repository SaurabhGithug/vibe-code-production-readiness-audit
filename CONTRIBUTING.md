# Contributing

Thanks for helping make this a useful second engineering review. Contributions can be small: a clearer question, a missed failure mode, or removal of an unnecessarily strict recommendation.

We welcome real-world findings, new failure patterns, better security checks, stack examples, scale models, cloud-specific guidance, corrections, and simplification.

## Every check needs a reason

**Every new check should catch a realistic failure mode.**

Explain:

1. What can go wrong, and for whom?
2. Which architecture or requirement makes the check relevant?
3. What evidence confirms or disproves it?
4. How can it be investigated safely?
5. What is the simplest remediation, and when is it NOT NEEDED?

Avoid adding fashionable technology requirements. A contribution about queues should identify durability, retry, or backpressure behavior; it should not require every project to adopt a particular broker.

## Choose the right place

- Agent instructions: [PROMPT.md](PROMPT.md).
- Compact human review: [CHECKLIST.md](CHECKLIST.md).
- Output fields: [REPORT_TEMPLATE.md](REPORT_TEMPLATE.md) and [templates](templates/finding-template.md).
- Rationale and depth: [methodology](docs/AUDIT_METHODOLOGY.md) and focused guides in docs.
- Teaching examples: [EXAMPLES.md](docs/EXAMPLES.md), clearly fictional or safely sanitized.

Keep shared terms consistent: IMPLEMENTED / PARTIAL / MISSING / NOT NEEDED, evidence state, severity, and MEASURED versus MODELLED — NOT VERIFIED. When changing the methodology, update prompt, checklist, and report fields where relevant.

## Submit a change

Open an issue for a toolkit bug, audit gap, or improvement, or send a focused pull request. Describe the failure mode and the final behavior. Explain any added complexity. Keep the README concise and move depth into focused guides.

Before submitting:

- Read the change as a first-time user and remove repetition or unsupported guarantees.
- Verify relative Markdown links and any external references you changed.
- Run `git diff --check` and inspect the complete diff.
- Check for private application names, machine paths, credentials, connection strings, customer data, and live exploit details.
- If demonstrating a workflow, state which steps were actually exercised and which were only reasoned about.

Use available Markdown/spelling tools if practical; there is no required runtime or dependency installation for this documentation repository.

## Share failures responsibly

Do not post credentials, proprietary source, customer information, or exploitable details about a live third-party system. Report vulnerabilities to the affected project's private security channel. For this toolkit, a synthetic minimal example usually explains the methodology problem without exposing anyone.

Challenge assumptions respectfully. The goal is useful engineering decisions, including decisions to keep a system simple.

Contributions are provided under the repository's [MIT license](LICENSE).
