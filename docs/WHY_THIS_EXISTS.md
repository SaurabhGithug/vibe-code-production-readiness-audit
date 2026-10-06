# Why this exists

I enjoy building with AI. The speed is extraordinary: I can try ideas, connect systems, and build useful features far faster than before.

While building a large project, I repeatedly discovered that feature completeness and production readiness are different things. The UI worked. Thousands of tests passed. Yet deeper reviews still found gaps in permissions, tenant boundaries, background work, deployment safety, and scalability.

A feature can work while authorization is incomplete, rate limiting is instance-local, or background work disappears when a process stops. A system can have backups nobody has restored, cost controls some provider calls bypass, a database across a regional boundary, an unsigned webhook, or one heavy job that starves the web server. These are failure patterns worth checking, not claims that every project has every problem. A cross-region database may be deliberate; its latency and failure implications still need to be understood.

None of that is obvious from a polished UI. Passing tests help, but their value depends on which real boundaries they exercise.

I wanted the questions I kept asking to be available earlier, before a launch decision or a growth spike. So I created the framework I wished I had at the beginning: discover the actual system, trace important flows, collect evidence, challenge the findings, and recommend the minimum useful work.

This is not an argument against vibe coding. AI-assisted development is extremely powerful. Faster development increases the importance of systematic verification. An independent review gives that speed a stronger engineering foundation.

I am sharing this because other builders are probably facing the same problem, from students and solo founders to established teams. You should be able to use it without adopting my stack or buying into a particular architecture.

Please open issues, challenge assumptions, submit PRs, add missing checks, improve the prompts, contribute fictional or sanitized examples, and share failures the audit helped catch. Do not publish private project evidence or live vulnerability details in an issue.

**This is a living checklist. If something is wrong, incomplete, outdated or unnecessarily strict, please open an issue or PR.**

Start with the [master prompt](../PROMPT.md), or help improve it through [contributing](../CONTRIBUTING.md).
