# Integrate

When the user reads, watches, or listens to something new, scan their knowledge base to find related content and suggest how to weave the new material into their existing knowledge — both as a standalone summary and as part of a broader topic page.

## Goal

The wiki should have two layers:
1. **Source summaries** - One file per article/book/video. Detailed enough to recall the original in 5 years. Created using the `summarize` skill.
2. **Topic pages** - One file per topic that synthesizes learnings from multiple sources into a single reference. These are the pages you actually go back to. They link to individual source summaries for deeper reading.

## Steps

### 1. Scan the knowledge base

First discover the current wiki structure instead of assuming one:
- Confirm the wiki root from user input or infer it from provided file paths
- Find `index.md` files and section directories (for example: source collections, topics, notes)
- Read existing summaries and topic pages to understand what topics are covered
- Identify where topic pages currently live, and treat that as canonical unless the user wants to change it

### 2. Find related content

When the user shares new content (article, video, book, etc.), identify what in their existing wiki is related:
- Direct topic matches (e.g., new article about 1-on-1 meetings + existing 1-on-1 notes)
- Overlapping concepts (e.g., new article about feedback + existing notes on radical candor)
- Complementary or opposing viewpoints

### 3. Report what you found

Tell the user clearly:

**Related content in your wiki:**
- List each related file with its path and a one-line description of how it connects
- Note if sources agree, disagree, or complement each other

### 4. Suggest an action plan

Based on what exists, suggest one of these paths:

**Path A: First source on a new topic**
- Create a source summary (using the `summarize` skill format)
- No topic page yet — one source is not enough to synthesize

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

<The synthesized knowledge from all sources, organized by theme — not by source. Write it as if you are explaining the topic to yourself in 5 years. Use bullet points. Be direct.>

### <Theme 1>
- <Learning point>
- <Learning point>

### <Theme 2>
- <Learning point>
- <Learning point>

<As many themes as needed>

## Where sources disagree

<If different sources contradict each other or offer different perspectives, note that here. This is valuable — it shows you the full picture, not just one take. Skip this section if all sources align.>

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
6. **Preserve attribution** - When a specific insight comes from a specific source, note it (e.g., "per [Source Title], ...") so you can trace ideas back.
7. **Follow the wiki's existing structure** - Detect current section layout and index conventions; do not assume fixed folders like `Articles/` or `Books/`.
8. **Keep topics source-agnostic** - Topic pages should live in a dedicated topics section (for example `Topics/`), not inside a source-type folder.
9. **Treat path changes as migrations** - For rename/move operations, update inbound links and keep aliases aligned with old names.
