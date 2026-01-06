# Infrastructure Strategy: H100 Fleet Optimization (H1 2026)

To: Executive Leadership Team  
Decision Needed: Approve enforcement of H100 scheduling governance + reporting cadence  
Objective: Improve H100 ROI by reducing compute drift and increasing useful utilization

---

## 1) Economic Problem: Compute Drift

H100 GPUs are Tier-1 capital assets. Today, we experience **Compute Drift**:
- Non-GPU workloads occupy H100 nodes, wasting high-cost capacity
- AI workloads run on A100 or CPU hardware, increasing latency and cost-per-inference

Business impact: compute drift silently raises inference COGS, degrades performance, and delays breakeven on H100 capital expenditure.

---

## 2) Expected Economic Impact (Directional)

| Metric | Current | Target (Post-Policy) |
|---|---:|---:|
| Useful H100 utilization | __% | __% |
| Drift rate (wrong workloads on H100) | __% | __% |
| Effective $/useful GPU-hour | $__ | $__ |
| Estimated monthly leakage | $__ | $__ |

Model and assumptions: [Compute Unit Economics](economics.md)

---

## 3) Policy: “Shield & Magnet” Scheduling

We will enforce a mandatory dual-layer scheduling policy:
- **Shield**: Unauthorized workloads are blocked from H100 nodes (hard enforcement)
- **Magnet**: Approved AI workloads are explicitly placed on H100 hardware

Engineering specification: [Implementation](implementation.md)

---

## 4) Infrastructure Governance

- H100 nodes are classified as Tier-1 Capital Assets
- Enforcement occurs at scheduling time (no best-effort placement)
- Exceptions require Infra + FinOps approval, with scope and expiry

Governance details: [Governance Model](governance.md)

---

## 5) Measurement & Accountability

Effectiveness will be tracked via:
- Useful H100 utilization
- Compute drift rate
- Mis-routing of AI workloads
- Effective $/useful GPU-hour

Reporting cadence and KPIs: [Metrics](metrics.md)

---

## 6) Decision Ask

Approve:
1. Mandatory enforcement of the H100 scheduling policy across clusters
2. Monthly executive reporting on utilization, drift, and compute ROI