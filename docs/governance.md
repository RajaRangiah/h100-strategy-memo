[Home](index.md) | [Economics](economics.md) | [Governance](governance.md) | [Implementation](implementation.md) | [Metrics](metrics.md)

---

# Infrastructure Governance: H100 as a Controlled Asset

## Controls (what is enforced)
1) **Enforcement Control (Shield / Hard Block)**
   - H100 nodes are tainted
   - Only workloads with approved tolerations can schedule

2) **Placement Control (Magnet / Correct Hardware)**
   - Approved AI workloads must specify H100 affinity
   - Prevents silent performance/cost regression

3) **Exception Control**
   - Exceptions require Infra + FinOps approval
   - Exceptions must include: business justification, cost center, expiry date, max replicas

## Ownership
- **Infra Platform:** cluster policy + enforcement
- **FinOps:** chargeback/showback and ROI reporting
- **Service owners:** correct labels/affinity/tolerations, SLO compliance

## Auditability
- Monthly report: useful utilization %, drift %, top offenders by namespace/workload
