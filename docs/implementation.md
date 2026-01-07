[🏠 Return to Strategy Memo](index.md)

---

# Implementation Specification: Shield & Magnet

To stop compute drift, we move from "Best Effort" scheduling to "Enforced" scheduling using Kubernetes primitives.

## 1. The Shield (Taints)
We apply a "NoSchedule" taint to all H100 nodes. This repels any pod that does not explicitly ask for these expensive resources.

**Command:**
```bash
kubectl taint nodes <node-name> sku=h100:NoSchedule
```

## 2. The Magnet (Tolerations & Affinity)
Legitimate training workloads must contain a specific toleration to bypass the shield, AND a node affinity to be attracted to the H100s.

Pod Spec Requirement:

```yaml
tolerations:
- key: "sku"
  operator: "Equal"
  value: "h100"
  effect: "NoSchedule"
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: gpu-type
          operator: In
          values:
          - nvidia-h100
```

## 3. Migration Plan
Phase 1 (Audit): Tag all current H100 workloads.

Phase 2 (Soft Enforce): Warn owners of non-compliant pods.

Phase 3 (Hard Enforce): Apply Taints. Non-compliant pods will remain Pending until moved to CPU nodes.

[🏠 Return to Strategy Memo](index.md)