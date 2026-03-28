---
name: Skills Navigation
description: >
  Master navigation map for all available skills and reference files. Read this first before
  loading any other skill. Use it to locate the correct SKILL.md or reference file without
  exploring the folder structure. Trigger whenever a task involves multiple skills, or when
  Claude needs to know what skills and references are available.
---

# Skills Navigation Map

> Read this file first. Use it to locate the right skill or reference file without exploring the folder structure.

> **Path note:** All skills are installed to `.claude/skills/[skill-name]/SKILL.md` within the active session mount. Full path format: `/sessions/[session-id]/mnt/.claude/skills/[skill-name]/SKILL.md`. Reference files for `products.md` and `services.md` live in the Link Development project folder, not inside the skill.

---

## Link Development Skills

Skills for Khaled's main company — B2B technology, lead generation focus.

| Skill | SKILL.md | Reference Files | Use For |
|---|---|---|---|
| content-creator | `.claude/skills/content-creator/SKILL.md` | `references/audiences.md`, `references/brand-voices.md`, `references/email-ready-format.md` + `products.md` / `services.md` from LD project folder | Social posts, ad copy, emails, blog content for LD |
| blogging | `.claude/skills/blogging/SKILL.md` | `references/article-research.md`, `references/human-like-writing.md`, `references/blog-reshare.md` | Blog articles, article ideas, LinkedIn reshares |
| seo-analyst | `.claude/skills/seo-analyst/SKILL.md` | `references/column-maps.md` + `semrush-mcp.md` from LD project folder | SEO analysis, keyword research, GSC/Ahrefs/SEMrush reports |
| performance-analysis-ld | `.claude/skills/performance-analysis-ld/SKILL.md` | `references/ld-analysis-templates.md` | Lead gen campaign analysis — LinkedIn, Google, Meta, X |
| ads-copy-ld | `.claude/skills/ads-copy-ld/SKILL.md` | — | B2B English ad copy — LinkedIn Ads, Google Search RSA |

---

## Freelance Skills — Qormuz

Skills for Qormuz — fashion e-commerce, Saudi Arabia.

| Skill | SKILL.md | Reference Files | Use For |
|---|---|---|---|
| performance-analysis | `.claude/skills/performance-analysis/SKILL.md` | `references/platform-column-maps.md`, `references/Analysis templates.md` | E-commerce campaign analysis — Meta, Google, Snapchat |
| google-ads-content-ar | `.claude/skills/google-ads-content-ar/SKILL.md` | — | Arabic Google Ads copy — RSA, PMax, Display, Shopping |

---

## Freelance Skills — Flamingo

Skills for Flamingo — cosmetics e-commerce, Egypt.

| Skill | SKILL.md | Reference Files | Use For |
|---|---|---|---|
| performance-analysis-flamingo | `.claude/skills/performance-analysis-flamingo/SKILL.md` | `references/flamingo-templates.md` | E-commerce campaign analysis — Meta, TikTok, Google (EGP, Arabic default) |

---

## Core Skills (Universal)

General-purpose document and file creation tools — apply across all clients and contexts.

| Skill | SKILL.md | Use For |
|---|---|---|
| docx | `.claude/skills/docx/SKILL.md` | Creating or editing Word documents |
| xlsx | `.claude/skills/xlsx/SKILL.md` | Creating or editing Excel spreadsheets |
| pptx | `.claude/skills/pptx/SKILL.md` | Creating or editing PowerPoint presentations |
| pdf | `.claude/skills/pdf/SKILL.md` | Reading, creating, merging, or filling PDF files |
| schedule | `.claude/skills/schedule/SKILL.md` | Creating scheduled or recurring tasks |

---

## System Skills

Skills that operate on the skill system itself — not client-facing.

| Skill | SKILL.md | Use For |
|---|---|---|
| skill-creator | `.claude/skills/skill-creator/SKILL.md` | Building, editing, testing, and packaging skills |
| skills-navigation | `.claude/skills/skills-navigation/SKILL.md` | This file — navigating the skill library |

---

## Quick Decision Guide

| If the task involves... | Use this skill |
|---|---|
| LinkedIn or Google campaign analysis for Link Development | `performance-analysis-ld` |
| LinkedIn or Google ad copy (English, B2B) | `ads-copy-ld` |
| Arabic Google Ads copy (any client) | `google-ads-content-ar` |
| Meta / Google / Snapchat analysis for Qormuz | `performance-analysis` |
| Meta / TikTok / Google analysis for Flamingo | `performance-analysis-flamingo` |
| Blog post, article, or LinkedIn reshare for LD | `blogging` |
| Social post, email, or ad copy for LD | `content-creator` |
| SEO report, keyword research | `seo-analyst` |
| Word document | `docx` |
| Excel spreadsheet | `xlsx` |
| PowerPoint presentation | `pptx` |
| PDF creation or extraction | `pdf` |
| Building or improving a skill | `skill-creator` |
