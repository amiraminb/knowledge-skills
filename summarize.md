# Summarize

Create a structured summary of content (article, book, book chapter, video, podcast, talk, etc.) for a personal knowledge wiki. The summary must be written so that re-reading it in 5 years brings the material back to life - not just the gist, but the important details, arguments, and examples. The summary should not be too long. It should be simple to read and to the point.

## Input

The user will provide one or more of:
- Pasted text or notes
- A URL (fetch and read it)
- A file path (read the file)
- Verbal description of what they watched/read

The user will also specify (or you should ask):
1. **Source type**: article, book, book-chapter, video, podcast, talk, paper
2. **Title**
3. **Author / Speaker** (if known)
4. **Source link** (if available)

## Output format

Write the summary as a Markdown file.

### For articles, videos, podcasts, talks

```markdown
---
id: <kebab-case-title>
aliases: []
tags: []
review: false
---

<source link if available>

# <Title>

## One sentence to remember

<A single sentence that captures the core message. If you had to tattoo one idea from this content, this is it.>

**<A bold 2-3 sentence TL;DR that covers the full argument, not just the topic.>**

## The big idea

<What is the central thesis or argument? Why does the author/speaker think this matters? Write it so someone with zero context can follow.>

## Key points

<Break into logical sections with descriptive headings. Each section should cover one major point or argument. Use bullet points for supporting details, examples, and evidence. Preserve specific numbers, names, frameworks, analogies, and stories — these are what trigger memory years later.>

### <Point 1 heading>
- ...

### <Point 2 heading>
- ...

<Add as many sections as the content warrants. Don't pad, don't skip.>

## Practical takeaways

<What should the reader actually do differently? Concrete actions, habits, or mental models. Skip this section if the content is purely informational with no actionable angle.>

## Memorable quotes or examples

<Pull out 2-5 specific quotes, stories, analogies, or examples that make the ideas stick. These are recall anchors.>
```

### For books (full book summary)

```markdown
---
id: <kebab-case-title>
aliases:
  - <Human readable title>
tags: []
review: false
---

# <Book Title>

## Chapter <N> - <Chapter Title or Theme>
* The big idea of the chapter is: **<one sentence>**
* <Key concepts, arguments, and details as bullet points>
* Memory hook: **<a short phrase that encodes the chapter's pattern>**
* <Important frameworks, models, or terminology — explained, not just named>
* <Specific examples, stories, or data that support the main points>
* <Warnings, counterarguments, or nuances the author raises>

> The key takeaway: **<one paragraph summary of the chapter's most important lesson>**

<Repeat for each chapter>

---

# Whole Book in One Screen
* <Bullet-point synthesis of the entire book — the ideas that matter most, compressed into a single scrollable section>
* <Key frameworks and how they connect>
* <The book's ultimate argument or lesson>
```

## Quality rules

1. **No fluff** - Every sentence must earn its place. Cut filler words and generic statements.
2. **Preserve specifics** - Names, numbers, dates, framework names, technical terms, story details. These are what make a summary useful years later. A summary that says "the author gives an example" is useless — say what the example is.
3. **Explain, don't just name** - Don't write "The author introduces the XYZ framework." Write what the XYZ framework is and how it works.
4. **Use memory hooks** - For each major section or chapter, include a short bold phrase that encodes the pattern. These work like mnemonics.
5. **Keep the author's structure when it's good** - If the original has a clear logical flow, follow it. Don't reorganize for the sake of reorganizing.
6. **Capture counterarguments and nuance** - If the author addresses objections or edge cases, include them. Real understanding includes knowing the limits.
7. **Write in plain direct language** - Short sentences. Active voice. No academic hedging.
8. **Blockquote key takeaways** - Use `>` blockquotes for chapter/section takeaways to make them visually scannable.
9. **Length should match depth** - A 5-minute article gets a focused summary. A 400-page book gets a thorough one. Don't compress a complex book into a page, and don't inflate a simple article into an essay.

## File naming

- Use underscores for book titles: `The_Pragmatic_Programmer.md`
- Use kebab-case for articles/videos: `arts-of-reading-the-docs.md`

