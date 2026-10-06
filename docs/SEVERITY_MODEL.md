# Severity and readiness

Severity describes the consequences of a problem in the stated launch context. It is independent of implementation status and confidence. An isolated pilot and a public service handling sensitive data have different requirements.

| Priority | Meaning | Typical examples | Decision |
| --- | --- | --- | --- |
| P0 — LAUNCH BLOCKER | Unacceptable exposure for the intended launch | Cross-tenant leakage, serious auth bypass, destructive data-loss path, public unbounded paid-provider access | Resolve or demonstrably contain before launch |
| P1 — BEFORE SCALE | Risk tolerable only under explicit bounded pilot conditions | Connection exhaustion at planned growth, fragile background processing with a safe manual fallback | Owner, mitigation, workload ceiling, and deadline before growth |
| P2 — IMPORTANT | Meaningful quality or reliability problem | Poor failure diagnostics, inefficient noncritical query, missing lower-risk contract coverage | Prioritize by impact and effort |
| P3 — LATER | Low-impact cleanup or optimization | Unreachable legacy duplication with documented ownership | Backlog with revisit trigger |

Confirmed tenant leaks generally receive P0. If an exception is proposed, explain data sensitivity, exposure, compensating controls, and why launch remains acceptable. A recovery gap can be P0 when losing the data is unacceptable; it is not automatically P1 because it involves operations. P1 never means “safe by definition.”

## Calibrate a finding

Record affected actors/data, prerequisites, reachability, blast radius, reversibility, frequency, detection, and mitigations. Evaluate current usage and credible near-term growth separately. Avoid multiplying arbitrary numbers into a false precision score.

For P0/P1, trace the full path and attempt disconfirmation before confirming severity. A missing helper call may be covered by a gateway or lower layer. If that cannot be checked, use “provisional P0/P1” and name the missing evidence. A plausible urgent risk still belongs in the launch discussion.

Confidence may be high, medium, or low with an explanation. VERIFIED means a named observation was checked; it does not certify the whole control. A scanner alert alone rarely establishes exploitability.

## Executive maturity

| Verdict | Minimum basis within stated scope |
| --- | --- |
| Prototype | Feasibility demonstrated; engineering and operating safeguards incomplete |
| MVP | Core value journeys work; release/operating limitations remain explicit |
| Production-capable | Critical flows and safeguards demonstrated for a bounded workload and environment |
| Production-hardened | Recovery, deployment, monitoring, and failure safeguards have been exercised with operational ownership |
| Scale-ready | Representative capacity tests meet stated throughput/latency/error/cost targets, with headroom and operating plans |

Use **Not determined** when evidence is insufficient. A product can have mature deployment practices and a launch-blocking authorization defect; these labels are not substitutes for findings.

## Launch decision

- **YES:** evidence supports the specified release scope; no unresolved blockers or critical unknowns undermine it.
- **YES WITH CONDITIONS:** a bounded launch has explicit enforceable limits, owners, monitoring, and acceptance criteria. This does not waive P0 issues.
- **NO:** confirmed or credible unresolved blockers, or missing critical evidence, prevent a defensible launch recommendation.

State audience, environment, workload, and expiration/revisit trigger. No confirmed P0 is not proof of readiness. Avoid unconditional “secure,” “compliant,” or “supports millions” language.
