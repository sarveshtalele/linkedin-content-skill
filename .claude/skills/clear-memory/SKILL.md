---
description: Reset your LinkedIn content memory back to defaults. Usage: /clear-memory
allowed-tools: Bash
---

## Step 1 — Confirm
Ask the user to confirm first:
> ⚠️ **Are you sure?** This will erase all your saved feedback from memory. Type "yes" to confirm.

Wait for confirmation before running anything.

## Step 2 — Clear (only after "yes")

```bash
python3 scripts/memory_manager.py clear
```

## Step 3 — Confirm
✅ **Memory cleared.** Reset to defaults. Use `/feedback` to start building new learnings.
