# Vibe Code Production Readiness Audit

Your AI coding agent can build features quickly. This toolkit helps another agent check what might have been missed.

An agent-driven production-readiness audit for software built fast — especially with AI. Copy the [master prompt](PROMPT.md) into a capable coding agent to examine your project's engineering foundations, collect evidence, and prioritize the work before launch or growth.

## Start here

1. Open the **project you want to audit** in your agent, or provide a repository snapshot.
2. Set the scope with the optional [audit configuration](templates/audit-config.example.md).
3. Paste [PROMPT.md](PROMPT.md). Begin with read-only repository access; add scoped infrastructure access only when needed.
4. Review the report, independently recheck P0/P1 findings, and authorize fixes separately.

No installation or particular stack is required. Use ChatGPT Agent, Claude Code, Codex, Cursor, Windsurf, Copilot, or another agent with suitable repository tools. Available tools and permissions determine what can actually be verified. See [QUICKSTART.md](QUICKSTART.md), or use the [human checklist](CHECKLIST.md) without an agent.

## Why I made this

I created this after repeatedly auditing a large application I had built with AI coding agents. Features were working and thousands of tests were passing, yet deeper independent reviews still uncovered issues involving permissions, tenant isolation, background work, deployment safety, and scalability.

AI-assisted development worked extremely well. Its speed made it easy to focus on visible features while assuming the invisible engineering foundations had also been handled. So I turned the questions I kept asking into a reusable audit framework. [Read the origin story](docs/WHY_THIS_EXISTS.md).

## What it audits

| Foundation | Questions it investigates |
| --- | --- |
| Full stack development | Do real user flows work across UI, APIs, authorization, and data? |
| System design & scalability | What fails under concurrency, backlog, or dependency failure? |
| DevOps & cloud engineering | Can you deploy, observe, roll back, and recover the actual system? |
| Cybersecurity | Can someone cross a trust boundary, access another tenant, or abuse a privileged operation? |

When relevant, it also examines AI/LLM engineering, cost controls, queues and background jobs, browser automation, media processing, multi-tenancy, observability, and disaster recovery. It discovers your stack before choosing checks: a small monolith, mobile backend, SaaS product, internal tool, and enterprise service need different answers.

## Sample output

Fictional excerpt, not a verdict on any real project:

| Check | Status | Evidence and implication |
| --- | --- | --- |
| Rate limiting | PARTIAL | Redis client exists; deployment uses per-instance memory. Limits multiply with replicas. |
| Backups | PARTIAL | Backup jobs succeed; no restore drill evidence is available. Recovery remains unverified. |
| Kubernetes | NOT NEEDED | Present workload fits a managed service; orchestration adds no demonstrated benefit. |

> Launch: YES WITH CONDITIONS — controlled pilot only, with named owners and limits.
> Scale: MODELLED — NOT VERIFIED. No representative load test has run.

The complete [report template](REPORT_TEMPLATE.md) includes source-of-truth state, architecture, evidence, P0–P3 findings, a fundamentals matrix, and an ordered remediation plan. See more [fictional examples](docs/EXAMPLES.md).

## Principles

- Audit what exists: source, wiring, configuration, tests, and accessible runtime evidence.
- Verify claims and actively try to disprove serious findings.
- Distinguish IMPLEMENTED, PARTIAL, MISSING, and NOT NEEDED. Record evidence gaps separately.
- Separate measured capacity from assumptions. Never turn a model into a capacity claim.
- Recommend the simplest design that meets the requirements.
- Protect live systems. Read-only comes first; fixes and active tests need their own scope.

For deeper review, see the [methodology](docs/AUDIT_METHODOLOGY.md), [severity model](docs/SEVERITY_MODEL.md), [scale model](docs/SCALE_MODEL.md), [database](docs/DATABASE.md), [security](docs/SECURITY.md), [AI applications](docs/AI_APPLICATIONS.md), and [cloud/DevOps](docs/CLOUD_AND_DEVOPS.md) guides.

## Limits and contributions

This framework is a systematic second opinion, not a substitute for professional security audits, penetration testing, compliance reviews or experienced engineering judgment. A clean report is not a security guarantee. Missing access, incomplete sampling, and agent mistakes can hide real problems; critical unknowns can prevent a launch recommendation.

Builders, students, solo founders, startups, agencies, and engineering teams are welcome to [contribute](CONTRIBUTING.md). Every new check should catch a realistic failure mode. Challenge unnecessary complexity as readily as missing controls.

Licensed under [MIT](LICENSE). Reuse and adapt it.
