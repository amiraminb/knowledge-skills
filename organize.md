# Organize

Audit and maintain the structure of a personal wiki. Keep indexes accurate, links consistent, and the knowledge base easy to navigate as it grows.

Start by detecting the wiki root and current structure from the user's paths and existing files. Do not assume fixed directory names.

## When to use

- After adding new content (summaries, topic pages, notes)
- Periodically as a health check
- When the user feels the wiki is getting messy

## What to audit

Run these checks against the wiki and report findings grouped by severity.

### 1. Orphaned files

Files that exist in the wiki but are not linked from any index or other file.

- Scan all `.md` files (excluding `.git/`)
- For each file, check if it appears as a wiki-link (`[[...]]`) or markdown link in at least one other file
- Report any file that is not referenced anywhere
- **Suggestion:** Add it to the appropriate index, or ask the user if it should be removed

### 2. Broken links

Links in index files or other pages that point to files that don't exist.

- Scan all wiki-links (`[[path|label]]` and `[[path]]`) across all `.md` files
- Resolve each link to an actual file (handle both with and without `.md` extension)
- Report any link whose target file does not exist
- **Suggestion:** Create the missing file, fix the link path, or remove the dead link

### 3. Index completeness

Every directory that contains `.md` content files should have an `index.md` that links to all files in that directory.

- For each directory with an `index.md`, list files in the directory that are not linked from the index
- For directories without an `index.md` that contain 2+ content files, suggest creating one
- **Suggestion:** Add missing entries to the index

### 4. Link format consistency

Wiki-links should use a consistent format throughout the wiki.

- Check if links mix `.md` extensions and bare names (e.g., `[[file.md|label]]` vs `[[file|label]]`)
- Report the dominant style and any deviations
- **Suggestion:** Normalize to the dominant style

### 5. Frontmatter consistency

Every content `.md` file should have frontmatter with at minimum: `id`, `tags`, `review`.

- Report files missing frontmatter entirely
- Report files with incomplete frontmatter (missing required fields)
- **Suggestion:** Add missing frontmatter fields

### 6. Empty or stub files

Files that have frontmatter but no real content (e.g., just a title or a link with no summary).

- Report files with fewer than 5 lines of content after frontmatter
- **Suggestion:** Flag as "needs content" — the user may want to fill these in or remove them

### 7. Root-level structure

Check that the root `index.md` accurately reflects the current top-level directories and their index files.

- Compare directories listed in the root `index.md` against actual directories
- Report any directory that exists but isn't linked from root index
- Report any link in root index pointing to a nonexistent directory or file

### 8. Canonical paths and rename drift

Detect pages that were likely renamed or moved, but links and references were not fully migrated.

- Find links still pointing to old paths when a canonical page now exists elsewhere
- Report files with overlapping identities (same `id`, same title, or alias collisions)
- Flag probable duplicates that should be merged into one canonical page
- **Suggestion:** Pick one canonical path, update all inbound links, and keep aliases/frontmatter aligned

## Output format

Present findings as a structured report:

```
## Wiki Health Report

### Critical (broken things)
- [ ] Broken link: `Teams/index.md` links to `[[Teams/Notes/auth-demo]]` but file does not exist
- [ ] ...

### Warnings (inconsistencies)
- [ ] Orphaned file: `Sources/some-file.md` not linked from any index
- [ ] Stub file: `Sources/estimating-software-projects.md` has no content beyond title
- [ ] ...

### Suggestions (improvements)
- [ ] Directory `Ben/` at wiki root appears to duplicate `Mentorship/Ben/` — consider consolidating
- [ ] Link format: 73% of links omit `.md`, 27% include it — normalize to omit `.md`
- [ ] ...

### Summary
- X files total
- X orphaned files
- X broken links
- X stubs needing content
- X index entries missing
```

## Actions

After presenting the report, ask the user which issues they want to fix. Then:

1. **Fix broken links** — correct the path or remove the link
2. **Update indexes** — add missing file entries to the appropriate index
3. **Normalize link format** — rewrite links to use the dominant style
4. **Add frontmatter** — add missing fields to files that need them
5. **Flag stubs** — mark empty files with a `<!-- TODO: add content -->` comment or remove them per user preference
6. **Canonicalize renamed pages** — migrate links to canonical paths and resolve duplicate identities

Never delete files or remove content without explicit user confirmation. When in doubt, ask.

## Conventions to enforce

These are the wiki's structural conventions. The organize skill enforces them:

1. **Every directory with content needs an `index.md`** that serves as the entry point
2. **Root `index.md`** links to all top-level sections
3. **Section indexes** link to all files within that section
4. **Topic pages** (from the `integrate` skill) live in a dedicated topics section and are linked from that section's index
5. **Source summaries** live in source-specific sections (for example articles/books/videos) and are linked from their respective index
6. **Wiki-links use consistent format** — pick one style (with or without `.md`) and stick to it
7. **Frontmatter is always present** on content files with at least `id`, `tags`, `review`
8. **Canonical path per page identity** — each knowledge page has one canonical file path; aliases and old names should redirect via links/frontmatter, not duplicate pages
