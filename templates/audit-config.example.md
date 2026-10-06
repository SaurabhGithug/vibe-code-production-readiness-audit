# Audit configuration — {project}

Optional: fill in what you know and paste after the master prompt. This file documents scope; it does not configure or enforce agent permissions. Do not include credentials, connection strings, private machine paths, or customer data.

## Target and purpose

- Repository: {sanitized identity}
- Release candidate / branch / commit: {ref or unknown; agent must verify}
- Intended environment / deployed revision: {identity or unknown}
- Intended launch audience: {internal / controlled pilot / public; details}
- Critical user journeys: {three to five concrete flows}
- Sensitive data / tenancy model: {categories, no records}
- Stack hints: {optional; agent must discover and verify}
- Active work / other agents: {boundaries to preserve}

## Requirements and assumptions

- Current and target workload: {concurrent users or appropriate workload units}
- Journey mix / think time / request and job rates: {known values or unknown}
- Dataset / file sizes / retention: {ranges}
- Latency / error / availability goals: {targets}
- RPO / RTO: {acceptable loss and restoration time, or unknown}
- Monthly budget / currency / revenue assumptions: {optional; unknown is valid}
- Regulatory or contractual constraints: {requirements for qualified review}
- Audit time budget / priority areas: {optional; require explicit coverage limits}

## Access and authorization

- Read-only sources available: {repository, deployment metadata, redacted telemetry, etc.}
- Sources unavailable / off-limits: {list}
- Default execution: **inspect only; do not run repository code or active tests**.
- Approved local execution, if any: {exact commands/categories, disposable target, no production credentials}
- Approved staging/security/load/failure tests, if any: {explicit actions, synthetic accounts, target, owner}
- Spend cap / numeric stop thresholds / time window: {only for approved active tests}
- Cleanup permitted: {specific synthetic resources only}
- Report destination: **chat**, unless a specific output file is authorized.
- Fixes / deployments / production changes: **not authorized by this configuration unless explicitly listed with scope**.

The agent must continue useful safe inspection when access is missing and record gaps. Existing credentials do not expand permission. Do not infer authorization from an unfilled placeholder.

## Deliverable

Use [REPORT_TEMPLATE.md](../REPORT_TEMPLATE.md), including evidence references, disconfirmation of P0/P1 findings, measured versus modelled scale, critical unknowns, and minimum work before launch/scaling.
