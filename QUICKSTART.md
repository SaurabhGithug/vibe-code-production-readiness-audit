# Quick start

This is a prompt-and-checklist toolkit. There is no scanner to install. The target is your own project, not this toolkit repository.

## Before you start

Choose the repository, release candidate, and environment. State your launch audience, important user journeys, expected workload, and what the agent may inspect. The optional [configuration template](templates/audit-config.example.md) makes this explicit. Unknown answers are fine; label them.

Start with read-only code access. Provide scoped cloud metadata access only if useful. Never paste secrets into a prompt, and do not blindly grant an agent destructive production access. Review repository scripts before authorizing builds or tests: they may write data, send email, or spend money.

## Option A — ChatGPT Agent

1. Open or attach your project using the repository access available in your environment.
2. Give the agent only the repository and cloud access necessary for your chosen scope.
3. Paste the complete [master prompt](PROMPT.md), followed by your scope/configuration.
4. Let it audit read-only first. Without runtime access, require explicit verification gaps.
5. Review P0/P1 evidence, disconfirmation attempts, and launch conditions.
6. Approve fixes and active tests separately, with a target environment and limits.

## Option B — Claude Code

1. Open a session in the target repository. Identify dirty work and other active agents.
2. Use read-only permissions for initial inspection and name off-limits resources.
3. Paste [PROMPT.md](PROMPT.md) and your scope. Attach companion files from a separate toolkit checkout if useful.
4. Request the report in chat or authorize a specific report output path.
5. Recheck serious findings against actual code/configuration. Approve remediation separately.

## Option C — Codex, Cursor, or another coding agent

1. Select the target repository and a suitable read-only/restricted mode where available.
2. Paste [PROMPT.md](PROMPT.md) with the release/environment context.
3. Have the agent discover the stack, map architecture, and trace critical flows before judging them.
4. Review findings with [REPORT_TEMPLATE.md](REPORT_TEMPLATE.md); use [CHECKLIST.md](CHECKLIST.md) to catch coverage gaps.
5. Authorize local execution, staging probes, load tests, or fixes as a separate bounded step.

Agent interfaces vary. These are workflows, not product-specific permission guarantees. When read-only enforcement is unavailable, use a disposable snapshot without production credentials and a narrow tool allowlist.

## Review the result

- Check which revision was inspected and whether it matches the intended release.
- Ask for evidence on each serious finding and what could disprove it.
- Treat unavailable production evidence as a limitation, not a clean bill of health.
- Look for MEASURED versus MODELLED — NOT VERIFIED scale statements.
- Require owners, limits, and acceptance checks for launch conditions.

A useful follow-up is: “Recheck findings F-001 and F-002 against the full call path and compensating controls. Do not change code.” After authorized fixes, rerun affected checks against the new revision and check for regressions.

Keep reports private by default. Before sharing an example publicly, remove credentials, private paths, customer information, and exploitable details about live systems. See [CONTRIBUTING.md](CONTRIBUTING.md).
