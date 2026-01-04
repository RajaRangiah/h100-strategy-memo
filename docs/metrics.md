
---

## `docs/metrics.md`

```md
# Metrics: Measuring Drift, Utilization, and ROI

## Executive KPIs

- **Useful H100 utilization (%)**: time spent on approved AI workloads
- **Compute drift (%)**: time H100 capacity is consumed by unauthorized workloads
- **Misroute rate (%)**: AI workloads running on A100/CPU when H100 available
- **Effective $/useful GPU-hour**
- **Cost per inference (sampled)**

---

## Operational metrics (for Infra + FinOps)

- **Top offenders (namespaces / deployments / users)** consuming H100 without authorization
- **Queue pressure**: pending GPU pods vs available H100 capacity
- **Time-to-schedule (P50/P95)** for approved workloads
- **Exception inventory**: who has exceptions, expiry dates, and actual usage
- **Utilization split**: training vs inference vs “other”

---

## Reporting cadence

- **Weekly**: Infra + FinOps internal review
- **Monthly**: executive summary (trend + offenders + savings estimate)

---

## Outputs (what the report must contain)

- KPI trend lines (last 4–8 weeks)
- Drift breakdown by offender (top 10)
- “Savings estimate” vs baseline month
- Action list: enforcement gaps, expiring exceptions, and planned remediations
