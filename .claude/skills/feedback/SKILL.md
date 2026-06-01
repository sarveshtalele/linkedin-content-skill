---
description: Save positive feedback to memory for reinforcement learning. Usage: /feedback <what worked well about this content>
allowed-tools: Bash
---

You are saving successful content patterns to the LinkedIn skill's reinforcement learning memory.

## Step 1 — Parse Arguments
The user's feedback is: $ARGUMENTS

Extract:
- What specifically worked (tone, hook type, format, topic, structure)
- Generate a short `content_id` slug (e.g. "contrarian-ai-hook", "storytelling-carousel")
- Identify relevant tags (e.g. hook, carousel, storytelling, data-driven)

## Step 2 — Save to Memory

```bash
python3 scripts/memory_manager.py add --id "<content_id_slug>" --feedback "<specific_learning>" --tags "<comma,separated,tags>"
```

## Step 3 — Confirm
After the script runs:

✅ **Memory updated!** Saved: *"<what was saved>"*

Future posts, carousels, and calendars will now reflect this preference automatically.

> 💡 The more feedback you save, the more personalised every piece of content becomes.
