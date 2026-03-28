---
name: ld-content-creator
description: >
  Content creation skill for Link Development — a B2B technology company. Use this skill
  whenever writing, drafting, creating, or improving marketing content for Link Development,
  including social media posts (LinkedIn, Instagram, X), ad copy (Meta, Google, Snapchat,
  TikTok), email campaigns, blog posts, or website copy. Trigger for casual requests like
  "write me a caption", "I need ad copy", "draft an email", or "rewrite this for LinkedIn"
  — as long as the context is Link Development or its products. In English or Arabic.
  Do NOT use this skill for Flamingo (cosmetics) or Qormuz (fashion) — those clients have
  their own dedicated skills.
---

# ld-content-creator — Link Development Content

## Context

| | |
|---|---|
| **Client** | Link Development |
| **Industry** | B2B Technology / Digital Transformation |
| **Use for** | All content for Link Development: social posts, ad copy, emails, website copy, content briefs |
| **Do NOT use for** | Flamingo · Qormuz · Any e-commerce or consumer brand |

A specialized skill for writing high-quality marketing content across all digital channels.
Produces platform-native, persuasive, on-brand copy tailored to performance marketing goals.
Covers ad copy, social media, email, blogs, and website content — in English and Arabic.

---

## Workflow Overview

1. **Identify content type and platform** from the user's request
2. **Select brand voice and audience** — read reference files and match to context
3. **Gather missing context** — ask ONE targeted question if critical info is missing
4. **Apply the platform-specific framework** for tone, length, and format
5. **Write the content** with variations where useful
6. **Deliver in the requested format** (chat, Word doc, Excel content calendar, etc.)

---

## Step 1: Brand Voice & Audience Selection

Before writing, read the reference files and apply the right voice and audience profile:

- **Brand voices** → `references/brand-voices.md`
- **Audience profiles** → `references/audiences.md`
- **Products & services** → `/sessions/fervent-practical-goldberg/mnt/Link Development/products.md`

> **Product rule:** If the user mentions any Link Development product by name (CountBig, Project360, Strategy360, ServeBig, TeamBeats, PatientFirst, Globby, SellBig, ServeStream, Digital Courts, Retail Hub, CitizenEver, EventEX, InspAction, Meeting360, VisitStream, Survey Management, On-Prem Connector, Open for Investments), read `products.md` immediately to get the correct tagline, description, target audience, and messaging angle before writing anything. Never guess product descriptions — always read the reference first.

### How to select the voice
- If the user mentions **Link Development** or **linkdevelopment.com** → use **Voice 1** (professional, clear, authoritative)
- If the user asks for **bold, inspirational, or community-driven** content → use **Voice 2** (Funky Fresh, Tech Savvy & Bold)
- If no voice is specified, default to **Voice 1** for B2B/professional content, and ask if unsure

### How to select the audience
- If content targets **tech leaders, C-suite, VPs, or enterprise decision makers** → apply the **Technology Leadership & Decision Makers** profile from `references/audiences.md`
- Use the audience's power phrases, proof point preferences, and objection handling when relevant
- If a new audience is described by the user, apply it as given and note assumptions

### What to confirm before writing
| Input | Why it matters |
|---|---|
| **Product/Service** | What are you promoting? |
| **Target audience** | Who are you talking to? |
| **Brand voice** | Which voice applies? |
| **Goal / CTA** | What should the reader do? |
| **Platform** | Tone and format depend on this |
| **Language** | English, Arabic, or both? |

If the user doesn't provide all of this, use what's available and make reasonable assumptions —
briefly state them at the top of the output. Only ask if something is truly unworkable without it.

---

## Step 2: Platform Frameworks

### 2.1 Ad Copy

#### Meta Ads (Facebook & Instagram)

**Structure:**
- **Primary text**: 125 characters ideal (first line is the hook — must stop the scroll)
- **Headline**: 40 characters max — punchy, benefit-led
- **Description**: 30 characters — supporting detail or CTA

**Principles:**
- Lead with the problem or desire, not the product
- Use social proof when possible ("Join 10,000+ customers…")
- One clear CTA per ad
- For Arabic: right-to-left layout — keep sentences short and punchy

**Formats to deliver** (always give 2–3 variations):
```
--- Variation 1 ---
Primary text: [text]
Headline: [text]
Description: [text]
CTA button: [Shop Now / Learn More / Sign Up / etc.]

--- Variation 2 ---
...
```

#### Google Ads (Search)

**Structure (RSA — Responsive Search Ad):**
- **Headlines**: 15 options × 30 characters max (Google mixes and matches)
- **Descriptions**: 4 options × 90 characters max

**Principles:**
- Include the primary keyword in at least 3 headlines
- Mix benefit headlines, feature headlines, and CTA headlines
- Use all 15 headline slots — more variety = better optimization
- Pin headline 1 only if brand name is required in position 1
- Descriptions should expand on the best 2 headlines, include CTA

**Format to deliver:**
```
Headlines (30 chars max each):
1. [headline]
2. [headline]
...
15. [headline]

Descriptions (90 chars max each):
1. [description]
2. [description]
3. [description]
4. [description]
```

#### Snapchat Ads

**Structure:**
- **Headline**: 34 characters
- **Brand name**: 25 characters
- **CTA**: Standard snap CTAs (Shop Now, Swipe Up, etc.)
- **Body** (for Story ads): 90 characters

**Principles:**
- Snapchat audience skews young — casual, energetic tone
- Visual-first: copy supports the creative, doesn't carry the full message
- Use urgency ("Today only", "Limited drop")
- Emojis acceptable and often effective

#### TikTok Ads

**Structure:**
- **Ad text**: 100 characters
- Script/hook (first 3 seconds is everything)

**Principles:**
- Hook must be in the first 1–3 seconds — state the tension or payoff immediately
- Use conversational, native-feeling language
- Trending language and formats help (but avoid forced trends)
- Recommend a visual direction alongside the copy

---

### 2.2 Social Media Content

#### Instagram

| Format | Length | Notes |
|---|---|---|
| Feed caption | 125–150 chars visible, up to 2,200 total | Hook in first line (before "more") |
| Story | Very short, direct | Usually paired with a visual prompt |
| Reel caption | 150–300 chars | Hook + context + CTA |

**Caption structure:**
1. Hook (first line — must work without expanding)
2. Body (story, value, or insight — 3–5 lines)
3. CTA (comment, share, save, link in bio)
4. Hashtags (5–10, relevant — at the end or first comment)

#### LinkedIn

| Format | Length | Notes |
|---|---|---|
| Standard post | 150–300 words | Professional but personal — share insight, not just news |
| Long-form | 500–1,000 words | Story-based, lesson-driven |

**Post structure:**
1. Hook (1–2 lines — provoke, challenge, or intrigue)
2. Context or story (3–5 short paragraphs)
3. Lesson or takeaway
4. Question or CTA (invite comments)

LinkedIn tone: Thought-leadership, professional, authentic. Avoid overly corporate language.

**Standard deliverables for every LinkedIn post (always include all three — no exceptions):**

- **Post copy** — structured per the framework above
- **Text on Visual (TOV)** — short, punchy overlay text for the creative, designed to stop the scroll without needing the caption. Format: bold tension/hook line → resolution line → brand/product tagline. Keep it to 2–3 lines max. Example:
  ```
  "Your vision deserves more than a spreadsheet."
  Build. Measure. Optimize.
  [Product Name] — [Brand]
  ```
- **Post type label** — identify the content role on a single line: Promotional · Informative · Engaging · Thought Leadership · Inspirational · Social Proof · Awareness (can be a combination, e.g., "Informative + Promotional")

#### Twitter / X

- Max 280 characters
- Threads: 5–10 tweets, each self-contained but building on the previous
- Tone: Direct, opinionated, conversational
- Hook tweet must stand alone

---

### 2.3 Email Campaigns

#### Single email structure:
```
Subject line: [primary — 40–50 chars]
Preview text: [secondary — 85–100 chars, no repeat of subject]

[Opening line — personalized or curiosity-driven]
[Body — 2–3 short paragraphs, max 200 words total]
[CTA button text — 3–5 words]
[P.S. — optional, great for urgency or second CTA]
```

**Subject line principles:**
- Be specific, not clever — "You left something behind" < "Your cart expires tonight"
- Use numbers when possible ("3 things…", "Save 20%…")
- Avoid spam trigger words: FREE, URGENT, CLICK HERE (all caps)
- Personalization ([First Name]) improves open rates when used naturally

**Sequences:** When writing a multi-email sequence, always clarify:
- How many emails and over what period?
- What's the journey goal (conversion, re-engagement, nurture)?
- Suggest: Welcome (Day 0) → Value/Education (Day 2) → Social Proof (Day 5) → Offer (Day 7) → Urgency (Day 10)

#### Deliver subject lines in sets:
```
Subject line options:
A: [direct benefit]
B: [curiosity/question]
C: [urgency/scarcity]
D: [personalized/data-driven]
```

---

### 2.4 Blog Posts & Articles

**Structure:**
1. **Title** — SEO-optimized (primary keyword near front), 50–60 chars
2. **Introduction** (100–150 words) — Hook, frame the problem, preview the solution
3. **Body sections** — H2 headings, 200–400 words each, one idea per section
4. **Conclusion** (80–100 words) — Summary + CTA or next step
5. **Meta description** — 140–160 chars, include keyword, end with action

**SEO integration:**
- Primary keyword in: title, first 100 words, at least one H2, meta description
- Secondary keywords naturally throughout body
- Internal link suggestions (prompt the user if known URLs exist)

**Tone:** Match to brand — inform before selling; for performance-driven blogs, end with a clear next step.

---

### 2.5 Website Copy

**Landing pages:**
- **Hero headline**: Benefit-led, 6–10 words, primary keyword
- **Subheadline**: Expand the promise, add specificity, 1–2 sentences
- **Body sections**: Feature → Benefit → Evidence (repeat per section)
- **CTA**: Action verb + specific outcome ("Start your free trial" > "Submit")
- **Social proof**: Placement near CTA or below hero

**Product descriptions:**
- Lead with the outcome the product creates, not the specs
- Use sensory language when relevant (texture, experience, result)
- End with urgency or reassurance (return policy, reviews)

---

## Step 3: Writing Principles (Applies to All Content)

1. **Lead with the benefit, not the feature.** "Saves you 3 hours a week" > "Automated scheduling."
2. **One message per piece.** Every sentence should serve the same goal.
3. **Match the platform's native voice.** LinkedIn sounds different from TikTok.
4. **Use active voice.** "We build brands" > "Brands are built by us."
5. **CTA clarity.** Tell the reader exactly what to do and why right now.
6. **Shorter sentences perform better** in ads and social. Blogs can breathe more.
7. **Never hard-code a year.** If content references "the current year" or a recent timeframe, use the actual current year from the system date — never assume or write a past year. A reference to "2025" in copy published in 2026 immediately reads as outdated.
8. **Use NYT-style title capitalisation** for all titles and headlines in Link Development and Beyon Solutions content (blog titles, article headings, email subject lines, TOV lines, and any headline-style copy). Rules:
   - **Always capitalise:** first word, last word, all words ≥4 letters, nouns, pronouns, verbs, "No/Nor/Not/Off/Out/So/Up," prepositions <4 letters used adverbially/adjectivally, "For" when it means to advocate
   - **Always lowercase:** a, and, as, at, but, by, en, for, if, in, of, on, or, the, to, v., vs., via; "to" in infinitives; prepositions <4 letters used as prepositions
   - **Hyphenated compounds:** capitalise both words unless the prefix is 2–3 letters and separates doubled vowels (e.g. "Re-enter" stays lowercase on the second part; "Self-Aware" capitalises both)

---

## Step 4: Output Formats

| Requested Output | Action |
|---|---|
| Chat | Deliver content directly, structured per platform framework |
| Word document | Read docx skill → `/mnt/skills/public/docx/SKILL.md` |
| Content calendar (Excel) | Read xlsx skill → `/mnt/skills/public/xlsx/SKILL.md` |
| Presentation | Read pptx skill → `/mnt/skills/public/pptx/SKILL.md` |

**When delivering multiple variations** (always do this for ads, subject lines, and social captions):
- Clearly label each variation (A, B, C or Variation 1, 2, 3)
- Note what's different about each (tone, angle, length)
- Recommend the strongest variation and briefly explain why

---

## Step 5: Tone & Language

- **Brand voice**: Always apply the selected voice from `references/brand-voices.md`. The voice determines word choice, sentence structure, formality level, and CTA style — not just the "vibe."
- **Default fallback**: English, professional-but-approachable, performance-oriented (Voice 1 principles)
- **Arabic output**: If the user writes in Arabic or requests Arabic content, write fully in Arabic — including all labels, copy, and notes. Use natural, colloquial marketing Arabic (not MSA/formal unless specifically requested). Be mindful of:
  - Gulf vs. Levantine vs. Egyptian register — ask if it matters for the brand
  - Right-to-left formatting considerations in ad specs
  - Local idioms and cultural references that resonate in the target market
  - When writing in Arabic for the Technology Leadership audience, maintain the professional, data-driven tone — avoid casualness even in Arabic
- **Do not mix languages** in the same content piece unless the brief calls for it (e.g., a bilingual ad).

---

## Edge Cases

- **No brand/product info**: Ask one question — "What product or service is this for?" — before writing.
- **Rewrite request**: If the user pastes existing copy to improve, identify what's weak about it first (hook, CTA, clarity, length), then rewrite aligned with the correct brand voice.
- **Compliance-sensitive industries** (finance, healthcare, supplements): Flag claims that may need legal review. Write the copy but add a note: "⚠️ Recommend legal/compliance review before publishing."
- **Content brief only**: If the user wants a brief rather than the content itself, produce a structured brief with: objective, audience, brand voice, key message, format, length, keywords (if SEO), deadline placeholder.
- **Technology Leadership audience**: Before finalizing content for this audience, run through the Content Refinement Checklist in `references/audiences.md` — verify technical accuracy, audience alignment, and engagement elements are all present.
- **New client or brand**: If the user introduces a client not yet in the references, ask for their brand voice and target audience before writing. Offer to save it to the reference files for future use.
