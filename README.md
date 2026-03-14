# Knowledge Skills

Reusable OpenCode skills for managing a personal knowledge wiki.

This repo now includes OpenCode-native skills in `.opencode/skills/*/SKILL.md`, while keeping the original portable prompt files at the repo root.

## OpenCode usage (native skills)

OpenCode auto-discovers skills from this repo when run inside it.

Available skills:
- `summarize`
- `integrate`
- `organize`

Use them by name in your prompt. Example:

```
Use the summarize skill to summarize this article: <url>
```

Or chain skills:

```
Use summarize, then integrate the result into my wiki.
```

## Portable usage (other AI tools)

Point your AI tool at a root prompt file and provide your input. For example:

```
Use the instructions in ~/dev/personal/knowledge-skills/summarize.md to summarize this article: <url or pasted text>
```

## Using with Claude Code

Reference the skill file directly in your prompt.

Example:

```
Use the instructions in /Users/amir/dev/knowledge-skills/integrate.md.
I just read this article: <url>
Please scan my wiki and suggest where this should be integrated.
```

Tip: keep the skill file unchanged and pass your content (URL, notes, or text) in the same prompt.

You can swap in any root prompt file:
- `summarize.md` for source summaries
- `integrate.md` for relating new content to existing notes
- `organize.md` for structure and link hygiene
