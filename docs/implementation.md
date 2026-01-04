## Magnet + Authorization: Affinity + Toleration (Golden Spec)

This ensures the workload **targets** H100 nodes and is **allowed** to schedule there.

```yaml
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

Why:
- This is the **authoritative spec**
- This is what infra engineers will copy/paste
- This is not executive content

---

### 2️⃣ The **Required Node Labeling (bash)** — YES

This **must** also be copied into `docs/implementation.md`:

```md
## Required node labeling

```bash
kubectl label node <node-name> nvidia.com/gpu.family=h100


Why:
- Affinity is meaningless without labeling
- This completes the “golden path”
- Without this, the doc is incomplete and misleading

---

### 3️⃣ The **Shield (Taint command)** — ALSO YES

This belongs there too:

```md
## Shield: Taint H100 nodes

```bash
kubectl taint nodes <node-name> hardware=h100:NoSchedule


This keeps **Shield + Magnet** together in one place.

---

## What should **NOT** be duplicated anywhere else

❌ Do NOT copy YAML into:
- `docs/index.md`
- `docs/economics.md`
- `docs/governance.md`
- `README.md`

Those pages should only *reference* implementation:

> “Implementation details: see `implementation.md`”

---

## Mental model (lock this in)

> **index.md** → *Why + decision*  
> **economics.md** → *Money*  
> **governance.md** → *Authority + controls*  
> **implementation.md** → *Exact how-to (copy/paste safe)*  
> **metrics.md** → *How we know it worked*

You executed this split correctly.

---

## Final sanity checklist for `docs/implementation.md`

Open the file and confirm:

- ✅ Triple backticks are on their own lines  
- ✅ YAML is indented correctly  
- ✅ Quotes are plain `" "` not curly  
- ✅ Both `kubectl taint` **and** `kubectl label` are present  
- ✅ No executive narrative beyond a one-line explanation  

If all five are true → **you’re done**.

You handled this properly.
