---
name: ld-blogging
description: |
  Blogging and article skill for Link Development's content team. Use this skill for any
  blog or article task related to Link Development — including generating B2B article ideas,
  drafting long-form articles, resharing third-party posts on LinkedIn or Facebook with
  Link Development framing, rewriting drafts to sound more human, or planning content calendars.
  Trigger on phrases like: "give me article ideas", "write an article about", "draft a blog post",
  "reshare this article", "find something to post", "make this sound more human", "rewrite this
  blog", or "find a Microsoft article to share". Always use for Link Development blog tasks.
  Do NOT use for Flamingo or Qormuz — this skill is B2B tech content only.
---

# ld-blogging — Link Development Blogging

## Context

| | |
|---|---|
| **Client** | Link Development |
| **Industry** | B2B Technology |
| **Use for** | Blog articles, article ideas, LinkedIn reshares, content calendars for Link Development |
| **Do NOT use for** | Flamingo · Qormuz · Any consumer or e-commerce content |

This skill covers everything related to blogging and article content at Link Development. It has three modes — read the request carefully to identify which one applies, then load the relevant reference file.

---

## Mode 1: Article Research

**Trigger:** Khaled asks for article ideas, blog topics, or content suggestions. He may say things like "give me ideas for a blog post", "what should I write about this week", "generate topic ideas", or "I need article topics for LinkedIn."

**What to do:**
1. Read `references/article-research.md`
2. Ask Khaled which prompt type he wants if it's not clear:
   - **Prompt 1 — Complex & Futuristic**: Wide-ranging topics across technology, finance, human behaviour, neuroscience, and emerging innovations. Aimed at thought leadership and high-impact editorial content.
   - **Prompt 2 — Practical B2B**: Simpler, actionable topics in GenAI, project management, software development, digital transformation, and B2B innovation. Aimed at Link Development's enterprise and government clients.
3. Use web search to find current trends, recent research, and emerging developments before generating topics — the research should inform the ideas, not just the training data.
4. Deliver the full structured output as defined in the reference file.

---

## Mode 2: Writing or Drafting Articles

**Trigger:** Khaled asks you to write, draft, or rewrite a blog article or long-form content piece. He may say "write an article about X", "draft a blog post on Y", "rewrite this so it sounds more human", or "make this less AI-like."

**What to do:**
1. Read `references/human-like-writing.md` — apply all principles without exception
2. If writing from scratch, confirm the topic, target audience, and approximate word count before drafting
3. If rewriting, read the original carefully and preserve the core message and structure while applying the human-like writing rules
4. For Link Development blog posts:
   - Default to Voice 1 (professional, authoritative) per the brand voice guide
   - Use NYT-style title capitalisation on the headline
   - Do not invent product features, statistics, or claims not supported by source material
   - Use the actual current year — never reference a past year as current

---

## Mode 3: Blog Reshare (LinkedIn & Facebook)

**Trigger:** Khaled provides a URL or article text and wants social media captions written for it, OR asks you to find a third-party article to reshare on Link Development's pages. He may say "write a caption for this", "find something from Microsoft to post", "reshare this on LinkedIn", or "I want to post this article."

**What to do:**
1. Read `references/blog-reshare.md`
2. Follow the Mode A (article provided) or Mode B (find an article) workflow as defined there
3. Always produce both a LinkedIn caption and a Facebook caption unless told otherwise

---

## Language Default

Default to **English** for all blog content. If Khaled requests Arabic, use Gulf Arabic register (UAE/KSA default) unless Egyptian register is specified. Never mix languages in the same piece unless the brief explicitly calls for it.

---

## Reference Files

| File | Purpose | Load when |
|---|---|---|
| `references/article-research.md` | Two research prompts + output structure for generating topic ideas | Mode 1 |
| `references/human-like-writing.md` | Full writing style rules for human, conversational copy | Mode 2 |
| `references/blog-reshare.md` | Approved sources, workflows, and caption templates for resharing | Mode 3 |
