# Magnet + Authorization: Affinity + Toleration (Golden Spec)

This page is the **only** authoritative source for Kubernetes scheduling controls targeting **H100-class nodes**.  
Everything here is copy/paste safe.

---

## 1) Required node labeling and tainting (bash)

```bash
NODE="h100-node-01"

# Label the node to advertise GPU family
kubectl label nodes "$NODE" nvidia.com/gpu.family=h100 --overwrite

# Taint the node to repel non-authorized workloads
kubectl taint nodes "$NODE" hardware=h100:NoSchedule --overwrite
```

## 2) Workload deployment (Kubernetes YAML)


```yaml
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
```
