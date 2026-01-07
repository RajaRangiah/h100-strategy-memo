[🏠 Return to Strategy Memo](index.md)

---

# Compute Unit Economics

This section quantifies the hidden capital loss caused by scheduler drift in large H100 fleets and frames scheduling governance as a first-order capital allocation decision.

---

## The Cost of “Drift”

When a generic or CPU-bound workload runs on an H100, the loss is not just underutilization — it is **paying a premium for performance that is never exercised**.

This loss is largely invisible in standard utilization dashboards and compounds as fleets scale.

---

## Tier-1 vs. Tier-2 Cost Structure

Representative, conservative economics:

- **H100 GPU (fully loaded cost):**  
  **$30,000–$40,000 per GPU per year**  
  (hardware, power, cooling, networking, support, depreciation)

- **Effective hourly cost (amortized):**  
  ~$3.50–$4.50 / GPU / hour

- **CPU / general-purpose node cost:**  
  ~10×–20× cheaper for non-accelerated workloads

**Key observation:**  
Running CPU-bound or idle workloads on H100s is not “inefficient” — it is **capital destruction**.

---

## The “Silent Leak” (Fleet-Scale)

In mixed production environments, observed patterns are consistent:

- Nominal GPU utilization: **60–70%**
- *Effective* utilization (tensor-core-productive work): **40–50%**
- Silent misplacement loss: **15–25% of total GPU time**

This loss does **not** trigger alerts.  
It shows up months later as:
- Missed training deadlines
- Inference starvation
- Emergency GPU purchase requests

---

## Dollar Impact (Conservative)

Assume:
- **Cost per H100 per year:** $35,000
- **Silent waste:** 20%

➡ **$7,000 lost per GPU per year**

| Fleet Size | Annual GPU Spend | Silent Waste (20%) |
|----------|------------------|--------------------|
| 1,000 GPUs | $35M | **$7M / year** |
| 10,000 GPUs | $350M | **$70M / year** |
| 50,000 GPUs | $1.75B | **$350M / year** |

This loss scales **linearly with fleet growth**.

---

## What Shield + Magnet Recovers

The Shield + Magnet policy does **not** attempt to reach 100% utilization.

Its objective is **placement correctness**:
- H100s run only workloads that exercise tensor cores
- Low-value or bursty workloads are displaced immediately
- High-priority training and inference are shielded from interference

Conservative, observed recovery:

- **30–40% of previously wasted capacity**
- Net effective utilization gain: **+8–12 percentage points**

---

## Recovered Capital (10,000-GPU Example)

- Silent waste: **$70M / year**
- Recovery at 35%: **$24.5M / year**

That is:
- ~$2M per month
- No new hardware
- No model changes
- No developer productivity tax

This is **pure governance arbitrage**.

---

## Why Buying More GPUs Makes This Worse

Without placement governance:
- Additional GPUs amplify the same misallocation
- Utilization dashboards improve
- Capital efficiency degrades

Buying more GPUs before fixing scheduling policy **scales the loss faster than the capacity**.

---

## Decision Framing

This is not an infrastructure optimization.

It is a choice between:
- **Recovering $25–40M per year** in existing capital  
**or**
- Accelerating the next GPU purchase cycle to compensate for silent waste

The scheduler is already making decisions.  
Shield + Magnet simply ensures those decisions reflect **economic intent**.

---

[🏠 Return to Strategy Memo](index.md)
