# How I Built a LinkedIn Content Generation Skill Using Claude Code — And Why It Changed My Content Strategy Forever

Most people use AI to write one post at a time.

I built a system that writes for me, remembers what works, and gets smarter every single time I use it.

---

## The Problem I Was Trying to Solve

I was spending 3-4 hours a week writing LinkedIn content.

Not because I didn't have ideas. Because I kept starting from scratch — every single time.

No system. No memory of what worked. No way to scale what was already resonating with my audience.

I knew AI could help. But every tool I tried gave me generic content that sounded nothing like me. It didn't know my niche. It didn't know my tone. It had zero memory of my wins.

So I built my own.

---

## What I Built — The LinkedIn Content Generation Skill

I built a **Claude Code Skill** — a custom set of Python scripts and AI instructions that plug directly into my coding assistant.

The result: 7 slash commands that give me professional, SEO-optimised LinkedIn content in under 60 seconds.

| Command | What it does |
|---|---|
| `/generate-post` | Ready-to-publish post with hook, body, CTA, and hashtags |
| `/generate-carousel` | Full slide-by-slide carousel content |
| `/generate-newsletter` | Long-form newsletter edition |
| `/generate-calendar` | 30-day content calendar with hooks and CTAs |
| `/feedback` | Saves what worked into a learning memory |
| `/show-memory` | Shows everything the skill knows about you |
| `/clear-memory` | Resets back to defaults |

But the part I'm most proud of isn't the commands.

It's the **reinforcement learning loop** built into the core.

---

## The Architecture — How It Actually Works

Here's the thing most AI content tools miss: **they have no memory.**

Every session starts from zero. They don't know your tone. They don't know your best-performing hook style. They don't know your niche.

I fixed that with a file called `memory.md`.

### The Three-Layer Architecture

**Layer 1 — The SKILL.md Files (Agent Instructions)**

Each command lives in `.claude/skills/<command-name>/SKILL.md`. This is a markdown file with YAML frontmatter that Claude Code natively reads and registers as a real slash command.

```markdown
---
description: Generate a LinkedIn post. Usage: /generate-post <topic>
allowed-tools: Bash
---
## Step 1 — Parse Arguments
...
## Step 2 — Run the Script
\`\`\`bash
python3 scripts/generate_post.py --topic "..." --niche "..."
\`\`\`
```

When you type `/generate-post`, Claude Code reads this file, executes the Python script, reads the output, and uses it as its system prompt.

**Layer 2 — The Python Prompt Builders (The Brain)**

The Python scripts don't call any external API. They don't need an OpenAI key.

Instead, they do two things:
1. Load the user's personal `memory.md`
2. Build a richly-engineered prompt combining LinkedIn SEO rules + the user's historical preferences

That prompt gets printed to stdout. Claude Code reads it. Claude — using its own built-in intelligence — generates the final content based on those exact instructions.

```python
def get_base_prompt_context(niche: str, content_type: str) -> str:
    memory_context = read_memory()
    return f"""<SYSTEM_INSTRUCTION>
You are an elite LinkedIn Content Strategist...
{LINKEDIN_SEO_RULES}
<MEMORY>{memory_context}</MEMORY>
</SYSTEM_INSTRUCTION>"""
```

**Layer 3 — The Memory Manager (Reinforcement Learning)**

`memory_manager.py` handles reading, writing, and clearing `memory.md`. When I tell the skill what worked, it runs:

```bash
python3 scripts/memory_manager.py add \
  --id "contrarian-ai-post" \
  --feedback "Bold contrarian hook got 3x impressions" \
  --tags "hook,contrarian"
```

A timestamped entry gets appended to `memory.md`. Every future generation reads it.

The more I use it, the more it sounds like me.

---

## The LinkedIn SEO Engine — What Makes the Content Actually Perform

Generic AI content gets ignored on LinkedIn. Here's why mine doesn't.

Inside `scripts/utils.py`, I built a comprehensive SEO ruleset injected into every single prompt:

### Hook Engineering (The Most Critical Part)

The first two lines of any LinkedIn post determine 80% of its performance. I defined four proven hook formulas the skill must choose from:

- **Contrarian:** *"Most LinkedIn advice is wrong. Here's why."*
- **Statistic:** *"95% of posts get fewer than 100 views. Here's the 5% secret."*
- **Question:** *"What if everything you knew about personal branding was backwards?"*
- **Story:** *"3 years ago, I had 47 followers. Here's what changed."*

The skill is hardcoded to **never** use openers like "In today's fast-paced world..." or "I'm excited to share..."

### Structure Rules

Every post follows a strict framework:

`Hook → Context → Core Value → Takeaway → CTA → Hashtags (max 5)`

### Tone Options

The `/generate-post` command accepts `--tone` flags: `professional`, `storytelling`, `controversial`, `educational`, `motivational`. Each maps to a specific writing instruction injected into the prompt.

---

## The Folder Structure — Built for Portability

The entire skill is open-source and GitHub-ready. Anyone can clone it and use it in 5 minutes.

```
linkedin-content-skill/
├── README.md
├── scripts/                  ← Visible, editable Python files
│   ├── generate_post.py
│   ├── generate_carousel.py
│   ├── generate_newsletter.py
│   ├── generate_calendar.py
│   ├── memory_manager.py
│   ├── utils.py
│   └── memory.md             ← Your personal RL database
└── .claude/
    └── skills/               ← Claude Code reads this automatically
        ├── generate-post/SKILL.md
        ├── generate-carousel/SKILL.md
        └── ... (7 total)
```

The design decision I'm most proud of: **Python scripts in a visible folder, skill definitions in a hidden folder.**

The scripts you edit frequently (`memory.md`, `utils.py`) are right in front of you. The Claude Code plumbing stays out of your way.

---

## How to Install It in 60 Seconds

```bash
# Clone the repo
git clone https://github.com/sarveshtalele/linkedin-content-skill.git

# Copy into your project
cp -r linkedin-content-skill/.claude your-project/
cp -r linkedin-content-skill/scripts your-project/

# Launch Claude Code
cd your-project && claude
```

Type `/` — all 7 commands appear instantly.

---

## Key Takeaways

- **Platform-agnostic by design.** Uses Claude Code's built-in AI — no API keys, no paid services, no external dependencies.
- **The memory loop is the real product.** Commands are just the interface. The compounding personalization from `memory.md` is what makes this genuinely useful over time.
- **Prompt engineering > model switching.** Quality of output is determined almost entirely by the richness of the system prompt, not which model you use.
- **Open-source = extensible.** Add new tones, new commands, new SEO rules — without touching the skill definitions.
- **Structure beats creativity.** The LinkedIn SEO rules do more for post performance than any amount of "writing better."

---

## Your Action Step This Week

Clone the repo. Set your niche in `scripts/memory.md`. Run `/generate-post` on your next topic.

Then post it on LinkedIn. Watch what happens. Come back and run `/feedback` with what worked.

After 5 feedback entries, you'll notice the content starting to genuinely sound like you.

**[→ Get the skill on GitHub](https://github.com/sarveshtalele/linkedin-content-skill)**

---

## One Question for You

**What's the single biggest bottleneck in your current LinkedIn content workflow?**

Drop it in the comments — I read every reply and I'll tell you exactly which command in this skill would solve it.

---

*#AI #ClaudeCode #LinkedInMarketing #ContentStrategy #AITools*
