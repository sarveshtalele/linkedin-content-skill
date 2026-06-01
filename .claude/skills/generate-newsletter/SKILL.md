---
description: Generate a long-form LinkedIn Newsletter edition. Usage: /generate-newsletter <topic> [in <niche>] [length: short|medium|long] [title: "<title>"]
allowed-tools: Bash
---

You are an expert LinkedIn Content Strategist. A user wants to generate a LinkedIn Newsletter.

## Step 1 — Parse Arguments
The user's input is: $ARGUMENTS

Extract:
- `topic` — newsletter subject (required)
- `niche` — industry/niche (default: "AI & Technology")
- `length` — short | medium | long (default: medium)
- `title` — optional newsletter series name

## Step 2 — Run the Prompt Builder

```bash
python3 scripts/generate_newsletter.py --topic "<parsed_topic>" --niche "<parsed_niche>" --length <parsed_length> --title "<parsed_title_or_empty>"
```

## Step 3 — Generate the Newsletter
Read the script output. Generate a full newsletter with headline, body sections, takeaways, and engagement question.

## Step 4 — Show Output
Format in clean Markdown, ready to publish in LinkedIn Newsletter editor.

## Step 5 — Ask for Feedback
> 🎯 **Did this edition resonate?** Type `/feedback <what you liked>` to save this style to memory.
