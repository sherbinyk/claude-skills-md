---
name: skills-navigation
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
| ld-content-creator | `.claude/skills/ld-content-creator/SKILL.md` | `references/audiences.md`, `references/brand-voices.md`, `references/email-ready-format.md` + `products.md` / `services.md` from LD project folder | Social posts, ad copy, emails, blog content for LD |
| ld-blogging | `.claude/skills/ld-blogging/SKILL.md` | `references/article-research.md`, `references/human-like-writing.md`, `references/blog-reshare.md` | Blog articles, article ideas, LinkedIn reshares |
| ld-seo | `.claude/skills/ld-seo/SKILL.md` | `references/column-maps.md` + `semrush-mcp.md` from LD project folder | SEO analysis, keyword research, GSC/Ahrefs/SEMrush reports |
| ld-performance-analysis | `.claude/skills/ld-performance-analysis/SKILL.md` | `references/ld-analysis-templates.md` | Lead gen campaign analysis — LinkedIn, Google, Meta, X |
| ld-ads-copy | `.claude/skills/ld-ads-copy/SKILL.md` | — | B2B English ad copy — LinkedIn Ads, Google Search RSA |

---

## Freelance Skills — Qormuz

Skills for Qormuz — fashion e-commerce, Saudi Arabia.

| Skill | SKILL.md | Reference Files | Use For |
|---|---|---|---|
| qormuz-performance-analysis | `.claude/skills/qormuz-performance-analysis/SKILL.md` | `references/platform-column-maps.md`, `references/Analysis templates.md` | E-commerce campaign analysis — Meta, Google, Snapchat |
| qormuz-ads-copy-ar | `.claude/skills/qormuz-ads-copy-ar/SKILL.md` | — | Arabic Google Ads copy — RSA, PMax, Display, Shopping |

---

## Freelance Skills — Flamingo

Skills for Flamingo — cosmetics e-commerce, Egypt.

| Skill | SKILL.md | Reference Files | Use For |
|---|---|---|---|
| flamingo-performance-analysis | `.claude/skills/flamingo-performance-analysis/SKILL.md` | `references/flamingo-templates.md` | E-commerce campaign analysis — Meta, TikTok, Google (EGP, Arabic default) |

---

## Cross-Client Skills

Skills that work across all clients — not tied to a single brand.

| Skill | SKILL.md | Reference Files | Use For |
|---|---|---|---|
| social-analysis | `.claude/skills/social-analysis/SKILL.md` | `references/platform-column-maps.md`, `references/analysis-output-template.md` | Organic social media performance — Facebook, Instagram, LinkedIn, TikTok, Snapchat, Threads, X (native analytics exports, NOT Ads Manager) |

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
| LinkedIn or Google campaign analysis for Link Development | `ld-performance-analysis` |
| LinkedIn or Google ad copy (English, B2B) | `ld-ads-copy` |
| Arabic Google Ads copy (any client) | `qormuz-ads-copy-ar` |
| Meta / Google / Snapchat analysis for Qormuz | `qormuz-performance-analysis` |
| Meta / TikTok / Google analysis for Flamingo | `flamingo-performance-analysis` |
| Organic social media analytics (any client, native exports) | `social-analysis` |
| Blog post, article, or LinkedIn reshare for LD | `ld-blogging` |
| Social post, email, or ad copy for LD | `ld-content-creator` |
| SEO report, keyword research | `ld-seo` |
| Word document | `docx` |
| Excel spreadsheet | `xlsx` |
| PowerPoint presentation | `pptx` |
| PDF creation or extraction | `pdf` |
| Building or improving a skill | `skill-creator` |
