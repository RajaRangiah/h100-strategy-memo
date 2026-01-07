[🏠 Return to Strategy Memo](index.md)

---

These metrics directly back the economic recovery modeled in docs/economics.md.
Each KPI exists to prevent a specific dollar-denominated failure mode.


# Metrics & KPIs

We are moving away from "Allocated Memory" as a success metric.

## Primary KPIs (The "Real" Numbers)

### 1. Useful Utilization (SM Active)
* **Definition:** % of time Tensor Cores are active > 0%.
* **Goal:** > 60% fleet-wide.
* **Why:** High memory allocation with 0% compute means the GPU is just holding data, not training.

### 2. Drift Rate
* **Definition:** % of H100 hours consumed by pods *without* the "Magnet" toleration (during transition) or strictly Tier-2 workloads.
* **Goal:** < 5%.

### 3. Cost Per Training Hour
* **Definition:** Total H100 Spend / Total Training Hours.
* **Goal:** Normalize this metric to detect efficiency regressions.

## Reporting Cadence
* **Weekly:** Engineering View (Drift hotspots).
* **Monthly:** Executive View (Total Waste Avoided vs. Previous Month).

---
[🏠 Return to Strategy Memo](index.md)