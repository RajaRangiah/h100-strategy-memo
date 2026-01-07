[🏠 Return to Strategy Memo](index.md)

---

# Compute Unit Economics

## The Cost of "Drift"
When a generic workload runs on an H100, we are not just wasting capacity; we are paying a premium for performance we don't use.

### Tier-1 vs. Tier-2 Cost Structure
* **H100 Node Cost:** ~$XX/hour (approx. market rate)
* **Standard CPU Node Cost:** ~$X/hour
* **Price Premium:** ~10x-20x

### The "Silent Leak" Calculation
If 30% of a 100-GPU fleet is running CPU-bound tasks (data prep, idle notebooks):
* **Daily Waste:** 30 GPUs * 24 hours * $Cost_Diff
* **Annual Waste:** > $10M+ depending on reserved instance pricing.

## Target Unit Economics
By enforcing the "Shield + Magnet" policy, we aim to shift:
1.  **Cost per Training Flop:** Decrease by ensuring H100s never idle.
2.  **Effective Utilization:** Shift from "Allocated" (vanity) to "Tensor Core Active" (reality).

---
[🏠 Return to Strategy Memo](index.md)