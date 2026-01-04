# Infrastructure Strategy: H100 Fleet Optimization (H1 2026)
**To:** Executive Leadership Team  
**Objective:** Maximizing Compute Unit Economics via Advanced K8s Scheduling

---

## 1. The Economic Problem
Our H100 fleet is our most expensive asset. Currently, we face **"Compute Drift"** where:
* Standard CPU tasks occupy high-cost GPU nodes.
* AI models accidentally run on legacy A100/CPU hardware, increasing latency and cost-per-inference.

## 2. The Solution: The "Shield & Magnet" Architecture
To protect our margins, we are implementing a mandatory dual-layer scheduling policy.

### Layer 1: The Shield (Taints)
We "Taint" the H100 nodes to repel unauthorized workloads.
* **Action:** `kubectl taint nodes <node> hardware=h100:NoSchedule`
* **Business Value:** Prevents $0.10/hr tasks from blocking $4.00/hr hardware slots.

### Layer 2: The Magnet (Node Affinity)
We use "Node Affinity" to pull AI workloads specifically to the H100s.
* **Business Value:** Ensures we get the 3x performance boost we paid for by guaranteeing the right hardware is used.

---

## 3. Implementation Code (The Golden Spec)
This configuration ensures the workload finds the H100 (Affinity) and is allowed to stay there (Toleration).

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: h100-optimized-service
spec:
  template:
    spec:
      # THE MAGNET: Specifically targets H100 hardware
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: "[nvidia.com/gpu.family](https://nvidia.com/gpu.family)"
                operator: In
                values:
                - "h100"

      # THE SHIELD: Authorized "Key" to bypass the H100 Taint
      tolerations:
      - key: "hardware"
        operator: "Equal"
        value: "h100"
        effect: "NoSchedule"

      containers:
      - name: ai-engine
        image: "internal-registry/llama3:latest"