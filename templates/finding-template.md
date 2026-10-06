# {F-001}: {specific failure and affected flow}

| Field | Value |
| --- | --- |
| Severity | {P0 / P1 / P2 / P3; rationale tied to launch scope} |
| Finding state | {confirmed / provisional / dismissed after recheck} |
| Control status | {IMPLEMENTED / PARTIAL / MISSING / NOT NEEDED, or unassigned} |
| Evidence state / confidence | {VERIFIED / INFERRED / UNVERIFIED; high/medium/low and why} |
| Component / affected actors | {flow, role, tenant boundary} |
| Environment / revision / time | {exact scope, dirty state if relevant} |
| Owner | {person or responsible role} |

## Observed behavior

{What happens, where, and under which conditions. Separate direct observations from inference.}

## Expected invariant

{Requirement the behavior violates, such as “only members of the owning tenant can read this object.”}

## Evidence and safe reproduction

- Source: {repository-relative file and verified line, or sanitized runtime artifact}
- Setup: {synthetic data, target, authorization, prerequisites}
- Method: {executed steps or static reasoning; clearly label which}
- Result: {redacted observation; no credentials or customer payloads}
- Coverage limit: {uninspected routes, configuration, or production differences}

## Impact

{Reachability, exposure, affected data/actions, blast radius, likelihood, reversibility, and launch/scale consequence.}

## Attempt to disprove

{Alternative explanation or compensating control checked; method, result, reviewer identity/role. Distinguish same-agent recheck from independent review. If blocked, state confirmation/dismissal criteria.}

## Minimum remediation

{Smallest effective change, tradeoffs, dependencies, and why additional infrastructure is or is not needed. Do not apply it during the audit.}

## Acceptance and follow-up

{Positive and negative checks, side-effect assertions, regression scope, target environment, owner, and required evidence.}

- Related findings / deduplicated root cause: {IDs}
- Recheck revision / result: {to be filled after authorized remediation}
- Remaining uncertainty: {gap IDs}
