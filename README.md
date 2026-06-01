# LinkedIn Content Generation — Claude Code Skill

> A production-ready Claude Code skill that turns your AI assistant into a personal LinkedIn Content Strategist. Generate SEO-optimised posts, carousels, newsletters, and content calendars — with a reinforcement learning memory that gets smarter every time you use it.

![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet?style=flat-square)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-macOS%20%7C%20Linux%20%7C%20Windows-lightgrey?style=flat-square)
[![Forks][forks-shield][forks-url]
[![Stargazers][stars-shield]][stars-url]


## ✨ What This Skill Does

Once installed, type a slash command in Claude Code and get professional LinkedIn content in seconds:

| Command | Output |
|---|---|
| `/generate-post` | A ready-to-publish LinkedIn post with hook, body, CTA, and hashtags |
| `/generate-carousel` | Numbered slide-by-slide carousel content + LinkedIn caption |
| `/generate-newsletter` | A full long-form newsletter edition in Markdown |
| `/generate-calendar` | A 30-day content calendar table with hooks and CTAs |
| `/feedback` | Saves what worked to memory for smarter future content |
| `/show-memory` | Displays your current preferences and learning history |
| `/clear-memory` | Resets memory back to defaults |

**Reinforcement Learning built-in:** Every time you tell the skill what worked, it updates `memory.md`. Every future generation reads that memory and adapts to your personal voice, tone, and style — automatically.



## 📁 Folder Structure

```
linkedin-content-skill/
│
├── README.md                        ← You are here
│
├── scripts/                         ← Python scripts (visible & editable)
│   ├── generate_post.py             ← Post prompt builder
│   ├── generate_carousel.py         ← Carousel prompt builder
│   ├── generate_newsletter.py       ← Newsletter prompt builder
│   ├── generate_calendar.py         ← Calendar prompt builder
│   ├── memory_manager.py            ← Read/write/clear memory.md
│   ├── utils.py                     ← Shared LinkedIn SEO prompt engine
│   └── memory.md                    ← Your RL database (edit this!)
│
└── .claude/                         ← Hidden folder (Claude Code reads this)
    └── skills/
        ├── generate-post/SKILL.md
        ├── generate-carousel/SKILL.md
        ├── generate-newsletter/SKILL.md
        ├── generate-calendar/SKILL.md
        ├── feedback/SKILL.md
        ├── show-memory/SKILL.md
        └── clear-memory/SKILL.md
```

> **Note:** The `.claude/` folder is hidden on macOS by default. Press `⌘ Cmd + Shift + .` in Finder to reveal hidden files.



## 🚀 Installation — Step by Step

### Prerequisites
- [Claude Code](https://claude.ai/code) installed (`npm install -g @anthropic-ai/claude-code`)
- Python 3.8 or higher (`python3 --version` to check)
- A Claude Pro or Team account



### Option A — Install as a Project-Level Skill

Use this if you want the skill available **only inside a specific project folder**.

**Step 1: Download this repository**

```bash
# Clone via git
git clone https://github.com/yourusername/linkedin-content-skill.git

# OR download the ZIP from GitHub and unzip it
```

**Step 2: Copy the skill into your project**

```bash
# Navigate to your existing project (or create a new folder)
mkdir ~/my-project && cd ~/my-project

# Copy the .claude folder and scripts folder into your project root
cp -r /path/to/linkedin-content-skill/.claude .
cp -r /path/to/linkedin-content-skill/scripts .
```

Your project should now look like:

```
my-project/
├── .claude/
│   └── skills/
│       ├── generate-post/SKILL.md
│       └── ... (all 7 skills)
└── scripts/
    ├── generate_post.py
    └── ... (all scripts + memory.md)
```

**Step 3: Launch Claude Code**

```bash
cd ~/my-project
claude
```

**Step 4: Verify installation**

Type `/` in the Claude Code prompt. You should see all 7 LinkedIn commands in the autocomplete list.



### Option B — Install as a Global User-Level Skill

Use this if you want the skill available **in every project** you open with Claude Code.

**Step 1: Download this repository**

```bash
git clone https://github.com/yourusername/linkedin-content-skill.git
```

**Step 2: Copy skills to your global Claude directory**

```bash
# Create the global skills directory if it doesn't exist
mkdir -p ~/.claude/skills

# Copy all skill definitions globally
cp -r /path/to/linkedin-content-skill/.claude/skills/* ~/.claude/skills/

# Create a permanent home for the scripts (recommended: ~/.claude/linkedin-scripts)
mkdir -p ~/.claude/linkedin-scripts
cp -r /path/to/linkedin-content-skill/scripts/* ~/.claude/linkedin-scripts/
```

**Step 3: Update script paths in each SKILL.md**

Because the scripts now live at `~/.claude/linkedin-scripts/`, update the bash commands in each `.claude/skills/*/SKILL.md` file. Replace:

```bash
# Old path
python3 scripts/generate_post.py

# New path (use the full absolute path)
python3 ~/.claude/linkedin-scripts/generate_post.py
```

Repeat for all 7 `SKILL.md` files.

**Step 4: Launch Claude Code from any folder**

```bash
claude
```
Type `/` — your LinkedIn commands are now available globally in every project.



## Personalising the Skill

### Step 1: Set Your Niche and Tone (Do This First)

Open `scripts/memory.md` in any text editor and update the top section:

```markdown
## 🧠 Core Identity & Tone
- **Primary Niche:** AI & Technology        ← Change this to your niche
- **Tone:** Professional and story-driven   ← Change this to your style
- **Voice:** First-person, confident        ← Describe your writing voice
```

This is the most important personalisation step. Every script reads this file before generating.

### Step 2: Start Using and Giving Feedback

The skill learns from you over time. After generating content you love:

```
/feedback The contrarian hook about AI replacing developers got 500+ reactions. Save this.
```

Claude Code will automatically run `memory_manager.py` and store the learning. Future content will reflect it.


## 🛠️ How to Modify & Extend the Skill

### To change how a command works — edit the SKILL.md file

Each command's behaviour is defined in its `SKILL.md`:

| What you want to change | File to edit |
|---|---|
| How Claude interprets `/generate-post` | `.claude/skills/generate-post/SKILL.md` |
| How Claude interprets `/generate-carousel` | `.claude/skills/generate-carousel/SKILL.md` |
| How Claude interprets `/generate-newsletter` | `.claude/skills/generate-newsletter/SKILL.md` |
| How Claude interprets `/generate-calendar` | `.claude/skills/generate-calendar/SKILL.md` |
| How Claude saves feedback | `.claude/skills/feedback/SKILL.md` |

**Example:** To make `/generate-post` always ask for the niche before running, open `.claude/skills/generate-post/SKILL.md` and add to Step 1:
```markdown
If `niche` is not specified, ALWAYS ask the user before proceeding.
```



### To change the content quality and SEO rules — edit `utils.py`

`scripts/utils.py` is the brain of the skill. It contains all the LinkedIn SEO rules injected into every prompt:

- **Hook formulas** — Edit `LINKEDIN_SEO_RULES` to add new hook patterns
- **Structure rules** — Change the post structure (Hook → Body → CTA)
- **Hashtag limits** — Adjust the hashtag count or strategy
- **Tone rules** — Add new writing style guidance

---

### To add new tone or style options — edit the generator scripts

For example, to add a `"humorous"` tone to `/generate-post`:

Open `scripts/generate_post.py` and add to `TONE_GUIDE`:

```python
TONE_GUIDE = {
    ...
    "humorous": "Use wit and light humour. Keep it professional but make the reader smile.",
}
```

Then update `.claude/skills/generate-post/SKILL.md` to include `humorous` as an option.


### To add a brand new command

1. Create a new folder: `.claude/skills/your-command-name/`
2. Create `SKILL.md` inside it with the format:
   ```markdown
   ---
   description: What this command does. Usage: /your-command-name <args>
   allowed-tools: Bash
   ---
   ## Step 1 — Parse Arguments
   ...
   ## Step 2 — Run Script
   ```bash
   python3 scripts/your_script.py --arg "$ARGUMENTS"
   ```
   ```
3. Create `scripts/your_script.py` with your logic
4. Restart Claude Code — the command is live immediately


## 💡 Usage Examples

```
# Generate a controversial post about AI in the tech niche
/generate-post AI agents replacing junior developers in tech, tone: controversial

# Create a 10-slide carousel about LinkedIn growth hacks
/generate-carousel 10 LinkedIn growth hacks nobody tells you, 10 slides, listicle style

# Plan a full month of content with a lead generation goal
/generate-calendar AI & Technology niche, 30 days, goal: leads, 4 times a week

# Write a deep-dive newsletter edition
/generate-newsletter The state of AI agents in 2025, long format, niche: Technology

# Save what worked to memory
/feedback That storytelling post about my first startup failure got 800 reactions — save the narrative hook style

# Check what the skill remembers about you
/show-memory
```



## 🔄 Reinforcement Learning — How It Works

```
You generate a post
        ↓
You post it on LinkedIn
        ↓
It performs well
        ↓
You run: /feedback <what worked>
        ↓
Claude runs: python3 scripts/memory_manager.py add ...
        ↓
memory.md is updated with a timestamped entry
        ↓
Every future generation reads memory.md
        ↓
Content becomes more aligned with YOUR voice over time
```

The `memory.md` file grows richer with every piece of feedback. After 10-20 feedback entries, the skill generates content that sounds genuinely like you.



## Script Reference

### `scripts/generate_post.py`
```bash
python3 scripts/generate_post.py --topic "<topic>" --niche "<niche>" [--tone <tone>] [--style <style>]
```
| Flag | Options | Default |
|---|---|---|
| `--tone` | `professional` `storytelling` `controversial` `educational` `motivational` | `professional` |
| `--style` | `list-based` `text-only` `data-driven` `contrarian` `storytelling` | `list-based` |

### `scripts/generate_carousel.py`
```bash
python3 scripts/generate_carousel.py --topic "<topic>" --niche "<niche>" [--slides <n>] [--style <style>]
```
| Flag | Options | Default |
|---|---|---|
| `--slides` | Integer 3–12 | `7` |
| `--style` | `how-to` `listicle` `myth-busting` `framework` `story-arc` | `listicle` |

### `scripts/generate_newsletter.py`
```bash
python3 scripts/generate_newsletter.py --topic "<topic>" --niche "<niche>" [--length <length>] [--title "<title>"]
```
| Flag | Options | Default |
|---|---|---|
| `--length` | `short` (~700w) `medium` (~1200w) `long` (~2000w) | `medium` |

### `scripts/generate_calendar.py`
```bash
python3 scripts/generate_calendar.py --niche "<niche>" [--days <n>] [--frequency "<freq>"] [--goal <goal>]
```
| Flag | Options | Default |
|---|---|---|
| `--days` | Any integer | `30` |
| `--frequency` | e.g. `"daily"` `"3 times a week"` | `"3 times a week"` |
| `--goal` | `awareness` `engagement` `leads` `authority` `growth` | `growth` |

### `scripts/memory_manager.py`
```bash
python3 scripts/memory_manager.py add --id "<id>" --feedback "<text>" [--tags "<tags>"]
python3 scripts/memory_manager.py read
python3 scripts/memory_manager.py clear
```


## Platform Compatibility

| Platform | Support |
|---|---|
| **Claude Code (CLI)** | ✅ Full native support — slash commands auto-register |
| **Claude Projects (Web)** | ⚠️ Partial — paste `SKILL.md` contents into Custom Instructions; upload `memory.md` to Knowledge |
| **GitHub Copilot** | ⚠️ Partial — add `SKILL.md` content to `.github/copilot-instructions.md` |
| **Cursor** | ⚠️ Partial — add `SKILL.md` content to `.cursorrules` |



## Contributing

Contributions are welcome. To add a new command or improve an existing one:

1. Fork this repository
2. Create a branch: `git checkout -b feature/new-command`
3. Make your changes following the structure above
4. Submit a Pull Request with a description of what you changed



## 📄 License

MIT License — free to use, modify, and distribute. See [LICENSE](LICENSE) for details.



*Built for LinkedIn creators who want AI that learns their voice, not generic content.*
