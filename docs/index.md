# Infrastructure Strategy: H100 Fleet Optimization (H1 2026)

To: Executive Leadership Team  
Decision Needed: Approve enforcement of H100 scheduling governance + reporting cadence  
Objective: Improve H100 ROI by reducing compute drift and increasing useful utilization

---

## 1) Economic Problem: Compute Drift

H100s are Tier-1 capital assets. Today we experience **Compute Drift**:

- Non-GPU workloads consume H100 nodes (waste high-cost capacity)
- AI workloads run on A100/CPU, increasing latency and cost-per-inference

Impact: drift silently raises inference COGS and delays H100 breakeven.

---

## 2) Expected Economic Impact (Directional)

| Metric | Current | Target (Post-Policy) |
|---|---:|---:|
| Useful H100 utilization | __% | __% |
| Drift rate (wrong workloads on H100) | __% | __% |
| Effective $/useful GPU-hour | $__ | $__ |
| Estimated monthly leakage | $__ | $__ |

Model + assumptions: **Economics**

---

## 3) Policy: “Shield & Magnet”

We will enforce a mandatory dual-layer scheduling policy:

- **Shield**: block unauthorized workloads from H100 nodes (hard control)
- **Magnet**: place approved AI workloads on H100 nodes (correct placement)

Engineering details: **Implementation**

---

## 4) Governance (Controls, Ownership, Exceptions)

- H100 nodes classified as Tier-1 Capital Assets
- Enforcement is hard-block at scheduling time
- Exceptions require Infra + FinOps approval with expiry

Details: **Governance**

---

## 5) Decision Ask

Approve:
1) Mandatory enforcement across clusters  
2) Monthly executive reporting on utilization, drift, and compute ROI (**Metrics**)
