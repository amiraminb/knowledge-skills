# Knowledge Skills

Portable AI prompt files for managing a personal knowledge wiki. Works with any AI tool (Claude Code, OpenCode, etc.) — just reference the skill file as a prompt or system instruction.

## Usage

Point your AI tool at a skill file and provide your input. For example:

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

## Using with OpenCode

Use the same pattern: tell OpenCode to follow one of the skill files, then provide the content to process.

Example:

```
Use /Users/amir/dev/knowledge-skills/organize.md to audit my wiki and report issues.
```

You can swap in any skill file:
- `summarize.md` for source summaries
- `integrate.md` for relating new content to existing notes
- `organize.md` for structure and link hygiene
