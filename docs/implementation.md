[Home](index.md) | [Economics](economics.md) | [Governance](governance.md) | [Implementation](implementation.md) | [Metrics](metrics.md)

---

# Implementation Spec: Shield & Magnet Scheduling

## Shield: Taint H100 nodes
```bash
kubectl taint nodes <node-name> hardware=h100:NoSchedule


apiVersion: apps/v1
kind: Deployment
metadata:
  name: h100-optimized-service
spec:
  template:
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
              - matchExpressions:
                  - key: "nvidia.com/gpu.family"
                    operator: In
                    values: ["h100"]

      tolerations:
        - key: "hardware"
          operator: "Equal"
          value: "h100"
          effect: "NoSchedule"

      containers:
        - name: ai-engine
          image: "internal-registry/llama3:latest"

kubectl label node <node-name> nvidia.com/gpu.family=h100
