
[🏠 Return to Strategy Memo](index.md)

---

# Governance Model

Treating H100s as Capital Assets requires a change in permissioning.

## Access Tiers

| Tier | Workload Type | Access Policy |
| :--- | :--- | :--- |
| **Tier 1** | Large Model Training (LLM), Prod Inference | **Guaranteed.** Uses "Shield + Magnet". |
| **Tier 2** | Interactive Notebooks, Debugging | **Blocked.** Must use A10G, T4, or CPU. |
| **Tier 3** | Data Pre-processing | **Blocked.** Must use CPU nodes. |

## Exception Process
If a team needs H100s for interactive work (e.g., debugging a specific kernel):
1.  Request "Break-glass" access via Infra Ticket.
2.  Time-bound lease (Max 4 hours).
3.  Auto-revocation of tolerations after lease expiry.

---
[🏠 Return to Strategy Memo](index.md)
