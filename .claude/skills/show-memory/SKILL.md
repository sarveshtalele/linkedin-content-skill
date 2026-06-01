---
description: Display your current LinkedIn content memory and preferences. Usage: /show-memory
allowed-tools: Bash
---

## Read Memory

```bash
python3 scripts/memory_manager.py read
```

Display the memory contents cleanly. At the top summarise:
- How many feedback entries exist in the log
- What the current primary niche is set to
- What tone/style is configured

Then show the full memory content.

At the bottom remind the user:
> 💡 Edit `memory.md` in `.claude/skills/scripts/` to set your niche and tone. Use `/feedback` to add new learnings.
