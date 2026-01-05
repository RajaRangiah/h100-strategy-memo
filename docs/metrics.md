

```markdown
# Metrics (Scoreboard)

This page defines the operational scoreboard for the H100 strategy: capacity, cost, latency, reliability, and quality.

---

## 1) North Star Metrics

| Metric | Definition | Target |
|---|---|---:|
| GPU Utilization (SM%) | Avg Streaming Multiprocessor utilization across H100 fleet | __% |
| MFU (Model FLOPs Utilization) | Achieved FLOPs / theoretical FLOPs (model + hardware) | __% |
| P95 End-to-End Latency | Prompt-in → last token out | __ ms |
| Cost per 1M Output Tokens | Fully loaded cost / output tokens (by tier) | $__ |
| SLO Compliance | % requests meeting latency + error budgets | __% |

---

## 2) Capacity & Fleet Health

### 2.1 GPU Availability

| Metric | Definition | Target |
|---|---|---:|
| GPU Ready Rate | % GPUs healthy + schedulable | __% |
| Node Ready Rate | % nodes healthy + schedulable | __% |
| Drain/Repair MTTR | Mean time to repair failed nodes | __ hrs |

### 2.2 Scheduler Signal

| Metric | Definition | Target |
|---|---|---:|
| Pending Pods (H100 queue) | Count of pods pending due to GPU constraints | __ |
| Time-to-Schedule (P95) | P95 time from create → scheduled | __ sec |
| Preemption Events | Count/day (by namespace) | __ |

---

## 3) Performance (Serving)

### 3.1 Latency

| Metric | Definition | Target |
|---|---|---:|
| TTFT (P50 / P95) | Time to first token | __ / __ ms |
| TPOT (P50 / P95) | Time per output token | __ / __ ms |
| E2E (P50 / P95) | End-to-end request latency | __ / __ ms |

### 3.2 Throughput

| Metric | Definition | Target |
|---|---|---:|
| Tokens/sec/GPU | Output tokens per second per GPU | __ |
| Req/sec/GPU | Requests per second per GPU (by endpoint) | __ |
| Effective Batch Size | Actual batch size after dynamic batching | __ |

---

## 4) GPU Efficiency (Compute + Memory)

### 4.1 Utilization

| Metric | Definition | Target |
|---|---|---:|
| SM Utilization | GPU compute utilization | __% |
| HBM Bandwidth Utilization | Memory bandwidth used / peak | __% |
| Power Utilization | Avg GPU power draw / TDP | __% |

### 4.2 Memory

| Metric | Definition | Target |
|---|---|---:|
| HBM Used (P95) | P95 HBM used per GPU | __ GB |
| KV Cache Hit Rate | Cache hits / total lookups | __% |
| KV Evictions | Evictions/sec (or per req) | __ |

---

## 5) MFU Definition (use consistently)

```text
MFU = achieved_FLOPs_per_second / theoretical_peak_FLOPs_per_second

```