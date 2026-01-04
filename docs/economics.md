[Home](index.md) | [Economics](economics.md) | [Governance](governance.md) | [Implementation](implementation.md) | [Metrics](metrics.md)

---

# Compute Unit Economics (H100)

## Core definitions
- **All-in $/GPU-hour:** amortized capex + power + networking + ops, divided by GPU-hours
- **Useful utilization:** % of H100 time running approved AI workloads
- **Compute drift:** % of H100 time consumed by unauthorized workloads OR AI misrouted to non-H100

## Inputs (fill these)
- H100 count: __
- All-in $/GPU-hour: $__  
- Current drift %: __%
- Target drift %: __%
- Current useful utilization %: __%
- Target useful utilization %: __%

## Leakage model (directional)
Monthly leakage ≈ `H100_count * 24 * 30 * ($/GPU-hour) * Drift%`

Monthly savings ≈ `Leakage_current - Leakage_target`

## Example placeholder (replace with your real numbers)
If:
- 128 H100s
- $4 / GPU-hour (all-in)
- Drift reduces 18% → 5%

Leakage_current = 128 * 720 * 4 * 0.18 ≈ **$66,355 / month**  
Leakage_target  = 128 * 720 * 4 * 0.05 ≈ **$18,432 / month**  
**Savings ≈ $47,923 / month**
