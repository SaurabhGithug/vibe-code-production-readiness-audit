# Production-readiness audit — {project}

Replace braces with evidence, not assumptions. Keep “Not assessed” where appropriate. Use [severity definitions](docs/SEVERITY_MODEL.md) and the [finding template](templates/finding-template.md).

| Audit metadata | Value |
| --- | --- |
| Project / repository | {sanitized identity} |
| Audit date/time / timezone | {timestamp} |
| Auditor / agent / reviewer | {identity; independent review or same-agent recheck} |
| Toolkit version / commit | {ref or unknown} |
| Target commit / dirty state | {SHA; changed/untracked files relevant to scope} |
| Environment / deployed artifact | {environment; revision/digest; evidence} |
| Intended launch audience / workload | {bounded scope} |
| Business goals / availability / budget | {requirements or assumptions} |
| Scope / exclusions / sampling | {components and paths inspected} |
| Access / execution authorization | {read-only sources; explicitly approved tests} |
| Limitations / freshness | {missing evidence; stale refs; production differences} |

## 1. Executive verdict

**Maturity:** {Prototype / MVP / Production-capable / Production-hardened / Scale-ready / Not determined}

{Short basis, bounded to environment, revision, workload, and evidence. No composite score. See severity guide for maturity criteria.}

## 2. Launch verdict

**Decision:** {YES / YES WITH CONDITIONS / NO} for {specific audience and load}.

{Why; confirmed/provisional blockers; critical unknowns. No confirmed P0 is not sufficient for YES.}

| Condition / blocker | Owner | Operating limit / deadline | Required evidence / acceptance check |
| --- | --- | --- | --- |
| {item or none} | {role} | {limit} | {check} |

## 3. Source-of-truth state

| Item | Observed value | Evidence / time | Gap or mismatch |
| --- | --- | --- | --- |
| Repository / remote | {sanitized} | {source} | {gap} |
| Branch / HEAD / upstream | {values} | {source} | {gap} |
| Working tree / untracked files | {metadata} | {source} | {gap} |
| Stashes / worktrees | {metadata only} | {source} | {gap} |
| Local-only / remote-only commits | {counts/refs or unknown} | {ref freshness} | {gap} |
| Release candidate / deployment branch | {refs} | {source} | {gap} |
| Production commit / deployed revision | {refs} | {runtime/release evidence} | {gap} |
| Actual image/digest / environment | {identity or not applicable} | {source} | {gap} |

## 4. Architecture map

{Text or diagram showing request/job flows, trust boundaries, tenant identity, stores, providers, and failure domains. Label inferred components.}

| Component | Technology/version | Declared / wired / deployed evidence | Role / boundary |
| --- | --- | --- | --- |
| {component} | {discovered} | {references and gaps} | {role} |

## 5–16. Subsystem verdicts

Assign status only with evidence: IMPLEMENTED / PARTIAL / MISSING / NOT NEEDED. Otherwise leave unassigned and link a gap. Evidence state is VERIFIED / INFERRED / UNVERIFIED. Each observation is scoped; do not average controls into a misleading pass.

| Section | Subsystem | Status / evidence state | Verdict and evidence | Main risk / minimum action |
| --- | --- | --- | --- | --- |
| 5 | Full stack | {status/state} | {basis} | {action} |
| 6 | System design | {status/state} | {basis} | {action} |
| 7 | Database | {status/state} | {basis} | {action} |
| 8 | Security | {status/state} | {basis} | {action} |
| 9 | Multi-tenancy | {status/state} | {basis or non-applicability} | {action} |
| 10 | DevOps | {status/state} | {basis} | {action} |
| 11 | CI/CD | {status/state} | {basis} | {action} |
| 12 | AI architecture | {status/state} | {basis or non-applicability} | {action} |
| 13 | Async/queue | {status/state} | {basis} | {action} |
| 14 | Observability | {status/state} | {basis} | {action} |
| 15 | Backup/DR | {status/state} | {basis} | {action} |
| 16 | Cost | {status/state} | {basis} | {action} |

### Recovery evidence

| Asset / dependency | Backup and retention | Restore drill / revision / date | Target RPO/RTO | Observed loss/recovery time | Gap |
| --- | --- | --- | --- | --- | --- |
| {database, objects, config, secrets, artifacts, jobs} | {evidence} | {evidence or absent} | {targets} | {results or unverified} | {gap} |

### Cost evidence

| Scenario | Successful journeys / customers | Compute / data / storage / egress | AI / media / browser / queue / email / API | Total range / unit cost | Revenue or break-even | Basis |
| --- | --- | --- | --- | --- | --- | --- |
| {usage} | {counts} | {costs} | {costs} | {currency and range} | {stated revenue or needed revenue} | {prices, date, assumptions} |

{Abuse paths, retries/failures, peak factors, idle floors, budget enforcement, and uncertainty.}

## 17. Scale verdict

**Workload assumptions:** {concurrency definition, think time, request/job rates, journey mix, payloads, dataset, quotas}.

| Concurrent users or adapted level | First bottleneck | Second bottleneck | Catastrophic failure mode | Mitigation | Evidence basis / uncertainty |
| --- | --- | --- | --- | --- | --- |
| 100 | {hypothesis} | {hypothesis} | {scenario} | {action} | {MEASURED or MODELLED — NOT VERIFIED} |
| 500 | {hypothesis} | {hypothesis} | {scenario} | {action} | {basis} |
| 5,000 | {hypothesis} | {hypothesis} | {scenario} | {action} | {basis} |
| 25,000 | {hypothesis} | {hypothesis} | {scenario} | {action} | {basis} |

For MEASURED rows attach revision, environment, duration, workload, throughput, latency, errors, resource/connection use, queue growth, provider limits, and cost. Explain differences from production. For models show calculations and sensitivity; unknown ordering is acceptable.

## 18. Top 10 risks

Use fewer than ten if warranted. Include critical unknowns without presenting them as confirmed defects.

| Rank | Finding / gap ID | Risk and business impact | Severity / confidence | Immediate decision |
| --- | --- | --- | --- | --- |
| {rank} | {ID} | {impact/preconditions} | {P0–P3 or critical unknown} | {action} |

## 19. P0 — Launch blockers

| ID | Finding | Confirmed / provisional | Evidence / disconfirmation | Impact / preconditions | Fix / acceptance check |
| --- | --- | --- | --- | --- | --- |
| {ID or none found within scope} | {title} | {state} | {references} | {impact} | {action/check} |

{Detailed finding records using the finding template. “None found” must state coverage limits.}

## 20. P1 — Before scale

| ID | Finding | Confirmed / provisional | Evidence / disconfirmation | Pilot limits / owner | Fix / acceptance check |
| --- | --- | --- | --- | --- | --- |
| {ID or none found within scope} | {title} | {state} | {references} | {mitigation} | {action/check} |

## 21. P2 — Important; P3 — Later

| ID | Severity | Finding / evidence | Impact | Action / acceptance check |
| --- | --- | --- | --- | --- |
| {ID} | {P2/P3} | {title/reference} | {impact} | {action/check} |

## 22. Course / fundamentals matrix

Expand relevant concepts; do not mark unknown controls NOT NEEDED. IMPLEMENTED requires existence, wiring, reasonable tests, and architectural fit.

| Foundation | Concept / requirement | Status | Evidence state / reference | Gap / next action |
| --- | --- | --- | --- | --- |
| Full Stack Development | Boundary validation, contracts, sessions, accessibility | {per-concept rows} | {state/ref} | {action} |
| Full Stack Development | Transactions, concurrency, golden flows | {per-concept rows} | {state/ref} | {action} |
| System Design | Capacity, caching, retries, idempotency, failure isolation | {per-concept rows} | {state/ref} | {action} |
| DevOps / Cloud Engineering | CI/CD, least privilege, rollout/rollback, observability, recovery | {per-concept rows} | {state/ref} | {action} |
| Cybersecurity | Authorization, tenancy, injection, secrets, supply chain | {per-concept rows} | {state/ref} | {action} |

### Evidence-gap register

| Gap ID | Unknown | Why it matters | What resolves it / owner | Effect on launch decision |
| --- | --- | --- | --- | --- |
| {G-001} | {unknown} | {risk} | {access, test, or document} | {effect} |

## 23. What is NOT needed yet

| Mechanism / technology | Current reason | Revisit trigger |
| --- | --- | --- |
| {item} | {requirement-based rationale} | {measurable change} |

## 24. Exact order of work

Suggested sequencing, not delivery promises. Put blockers before optional architecture work.

| When | Ordered action / finding IDs | Dependency | Owner / effort / uncertainty | Acceptance criteria |
| --- | --- | --- | --- | --- |
| NOW | {action} | {dependency} | {role/estimate} | {check} |
| WEEK 1 | {action} | {dependency} | {role/estimate} | {check} |
| WEEK 2 | {action} | {dependency} | {role/estimate} | {check} |
| WEEK 3 | {action} | {dependency} | {role/estimate} | {check} |
| LATER | {action} | {trigger} | {role/estimate} | {check} |

## 25. Final answers

- **What is genuinely complete?** {scoped evidence}
- **Can this project safely launch?** {decision and limits}
- **What fails first under growth?** {measurement or model}
- **What prevents major scale?** {constraint}
- **What is being overengineered?** {unnecessary complexity}
- **What is underengineered?** {gap}
- **What is the minimum work before launch?** {ordered items}
- **What is the minimum work before scaling?** {ordered items}
- **If responsible for production, what would you do next?** {concrete next action}

## Appendix — Verification and operating plans

### Checks performed

| Check / command | Inspected / executed / skipped / proposed | Authorization and environment | Revision / result / evidence | Limitation |
| --- | --- | --- | --- | --- |
| {check} | {state} | {scope} | {result} | {gap} |

### Failure and load plans

| Scenario / realistic journey | Synthetic setup / target | Expected containment and recovery | Limits / stop thresholds / cost cap | Owner / approval / cleanup | Metrics / result |
| --- | --- | --- | --- | --- | --- |
| {failure or ramp stage} | {setup} | {expectation} | {limits} | {scope} | {observed or proposed} |

### Smallest useful dashboard

| Signal | Data source / dimensions | Threshold / baseline | Owner / response | Delivery verified? |
| --- | --- | --- | --- | --- |
| {availability, latency, errors, saturation, queues, providers, cron, spend, backups} | {source} | {threshold} | {response} | {evidence or gap} |

**Remaining decisions/access needed:** {items}. This report is a scoped second opinion, not a security or compliance certification.
