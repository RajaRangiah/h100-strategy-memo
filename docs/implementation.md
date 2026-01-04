# Magnet + Authorization: Affinity + Toleration (Golden Spec)

This page is the **only** place engineers should copy/paste Kubernetes scheduling controls for H100.

---

## 1) Required node labeling (bash)

```bash
NODE="h100-node-01"
kubectl label nodes "$NODE" nvidia.com/gpu.family=h100 --overwrite

NODE="h100-node-01"
kubectl taint nodes "$NODE" hardware=h100:NoSchedule --overwrite

apiVersion: apps/v1
kind: Deployment
metadata:
  name: h100-optimized-service
spec:
  replicas: 1
  selector:
    matchLabels:
      app: h100-optimized-service
  template:
    metadata:
      labels:
        app: h100-optimized-service
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
              - matchExpressions:
                  - key: nvidia.com/gpu.family
                    operator: In
                    values:
                      - h100
      tolerations:
        - key: hardware
          operator: Equal
          value: h100
          effect: NoSchedule
      containers:
        - name: ai-engine
          image: internal-registry/llama3:latest
