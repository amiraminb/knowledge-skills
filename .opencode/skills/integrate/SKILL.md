---
name: integrate
description: Connect new sources to existing wiki knowledge and recommend the right synthesis path.
license: MIT
compatibility: opencode
metadata:
  audience: personal-knowledge-wiki
  workflow: source-to-topic-integration
---

When the user reads, watches, or listens to something new, or asks for a wiki-wide integration pass, find related content and suggest how to weave notes together with Obsidian wiki-links.

Scope is intentionally limited to the user's "Knowledge is Power" area in `~/wiki/index.md` (or the wiki root `index.md` if `~/wiki/index.md` is not present). Treat only notes reachable from that section as in-scope for integration.

## Goal

The wiki should have two layers:
1. **Source summaries** - One file per article/book/video. Detailed enough to recall the original in 5 years. Created using the `summarize` skill.
2. **Topic pages** - One file per topic that synthesizes learnings from multiple sources into a single reference. These are the pages you actually go back to. They link to individual source summaries for deeper reading.

And one ongoing practice:
3. **Relationship linking** - Existing notes (source summaries, topic pages, evergreen notes, chapter notes) should be cross-linked when they meaningfully relate.

## Steps

### 1. Scan only the "Knowledge is Power" scope

First discover the current wiki structure instead of assuming one:
- Confirm the wiki root from user input or infer it from provided file paths
- Read `~/wiki/index.md` (or `<wiki-root>/index.md`) and locate the `## Knowledge is Power` header
- Build the candidate set from links listed under that header (for example `Articles/index`, `Books/index`, `Mentorship/index`) and notes reachable from those indexes
- Read existing summaries and topic pages within this scope to understand what topics are covered
- Identify where topic pages currently live within this scope, and treat that as canonical unless the user wants to change it
- Exclude notes outside this scope, even if they are topically related

### 2. Find related content across in-scope notes

For each in-scope candidate note, identify what other in-scope notes are related:
- Direct topic matches (for example, new article about 1-on-1 meetings + existing 1-on-1 notes)
- Overlapping concepts (for example, new article about feedback + existing notes on radical candor)
- Complementary or opposing viewpoints
- Source-to-source relationships (for example, a book chapter and an article covering the same mechanism)
- Source-to-topic relationships (for example, chapter supports an existing synthesis page)
- Topic-to-topic relationships (for example, adjacent concepts that should cross-reference)
- Prerequisite, example, and contrast relationships (for example, "foundation for", "case study for", "alternative to")

Prioritize high-signal links:
- Prefer links that improve retrieval and synthesis later
- Avoid weak keyword-only matches
- Skip links that would create clutter

### 3. Report proposed links before writing

Tell the user clearly:

**Related content in your wiki:**
- List each related file pair/group with paths and a one-line description of how they connect
- Note if sources agree, disagree, complement, or provide prerequisite context

**Proposed link actions:**
- For each proposed edit, show:
  - Source file path
  - Target note to link
  - Anchor text to use
  - Where to insert (section/paragraph)
  - Why this link is useful

Do not write files yet. Present this as a reviewable plan.

### 4. Suggest an action plan

Based on what exists, suggest one of these paths:

**Path A: First source on a new topic**
- Create a source summary (using the `summarize` skill format)
- No topic page yet - one source is not enough to synthesize

**Path B: Multiple sources exist, no topic page yet**
- Create a source summary for the new content
- Create a new topic page that synthesizes learnings from all related sources (existing + new)
- Update the relevant source index to link to the new source summary
- Add the new topic page to the topic index

**Path C: Topic page already exists**
- Create a source summary for the new content
- Update the existing topic page with new learnings from this source
- Add a link to the new source summary in the topic page's sources section
- Ensure the topic index links to the topic page

### 5. Canonical path and renames

Before creating a new topic page, check for existing topic pages that may already cover the same concept under a different filename or path.

- If a likely duplicate exists, propose consolidation instead of creating a second page
- If the canonical location has changed, propose a rename/move plan before writing
- For approved renames/moves, update links across the wiki to the new canonical path
- Preserve discoverability by keeping frontmatter aliases accurate after rename/move

Always ask the user which path they want before writing files.

### 6. User approval gate and linking execution

After presenting proposed links, ask for explicit approval.

- If user approves all: apply all proposed link edits
- If user approves a subset: apply only selected links
- If user requests changes: revise proposals and re-present
- If user rejects: do not write changes

When applying approved links:
- Use Obsidian wiki-links (`[[Note Name]]` or `[[path/to/note|Label]]`) consistent with existing wiki style
- Preserve note meaning; do not rewrite large sections just to inject links
- Keep edits minimal and local to relevant lines
- Avoid duplicate links to the same target in the same short section unless justified

After applying links, report:
- Files changed
- Links added per file
- Any skipped candidates and why

## Topic page format

```markdown
---
id: <kebab-case-topic>
aliases:
  - <Human readable topic name>
tags: []
review: false
---

# <Topic Name>

## Why this matters

<2-3 sentences on why this topic is worth having a dedicated page. What problem does understanding this solve?>

## Key learnings

<The synthesized knowledge from all sources, organized by theme - not by source. Write it as if you are explaining the topic to yourself in 5 years. Use bullet points. Be direct.>

### <Theme 1>
- <Learning point>
- <Learning point>

### <Theme 2>
- <Learning point>
- <Learning point>

<As many themes as needed>

## Where sources disagree

<If different sources contradict each other or offer different perspectives, note that here. This is valuable - it shows you the full picture, not just one take. Skip this section if all sources align.>

## Sources

<Link to each individual source summary. Use wiki-links for internal files.>

- [[source-summary-1|Source Title 1]] - one-line note on what this source specifically contributes
- [[source-summary-2|Source Title 2]] - one-line note on what this source specifically contributes
```

## Rules

1. **Synthesize, don't concatenate** - A topic page is not a list of summaries glued together. It extracts the best ideas from each source and organizes them by theme.
2. **Source summaries stay independent** - Each source summary should stand on its own. Don't remove content from a source summary just because it's also on the topic page.
3. **Topic pages are living documents** - They grow as more sources are added. New learnings get woven into the existing structure, not appended at the bottom.
4. **Link both ways** - Topic pages link to source summaries. Source summaries don't need to link back (they're standalone), but can if it helps.
5. **Don't force topic pages** - One source on a topic doesn't need a topic page. Wait until there are at least 2-3 sources that share a theme.
6. **Preserve attribution** - When a specific insight comes from a specific source, note it (for example, "per [Source Title], ...") so you can trace ideas back.
7. **Follow the wiki's existing structure** - Detect current section layout and index conventions; do not assume fixed folders like `Articles/` or `Books/`.
8. **Keep topics source-agnostic** - Topic pages should live in a dedicated topics section (for example `Topics/`), not inside a source-type folder.
9. **Treat path changes as migrations** - For rename/move operations, update inbound links and keep aliases aligned with old names.
10. **Propose first, edit second** - Relationship links must be proposed and approved before writing.
11. **Scoped-wiki mindset** - Integration is not only for a new source; it also includes discovering missing links among existing notes within the "Knowledge is Power" scope.
12. **High-value links only** - Prefer semantically meaningful links over dense cross-linking.
13. **Respect scope boundaries** - Do not include or propose links to notes outside the `## Knowledge is Power` section of the wiki index unless the user explicitly overrides this rule.
