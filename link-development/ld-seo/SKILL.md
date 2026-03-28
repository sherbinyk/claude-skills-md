---
name: ld-seo
description: >
  SEO analysis skill for Link Development — a B2B technology company. Use this skill whenever
  analyzing organic search performance, running keyword research, or auditing SEO for Link
  Development or its clients. Trigger when the user uploads a GSC, Ahrefs, SEMrush, or Moz
  export, or asks to review rankings, traffic drops, content SEO, or technical SEO issues.
  Also trigger for casual requests like "check my GSC data", "what keywords should I target",
  "audit this page for SEO", or "why is my traffic dropping". Applies in English or Arabic.
  Do NOT use for Flamingo or Qormuz e-commerce SEO — this skill is tuned for B2B tech content
  and lead generation, not product or e-commerce SEO.
---

# ld-seo — Link Development SEO

## Context

| | |
|---|---|
| **Client** | Link Development |
| **Industry** | B2B Technology |
| **Use for** | SEO analysis, keyword research, GSC/Ahrefs/SEMrush reports for Link Development |
| **Do NOT use for** | Flamingo · Qormuz · Any e-commerce or consumer product SEO |

## Workflow Overview

1. **Identify the task type** — keyword analysis, content audit, technical SEO, or reporting
2. **Parse any uploaded files** using pandas (CSV) or the xlsx skill (Excel)
3. **Map columns** to the standard schema (see reference below)
4. **Run the analysis** following the relevant framework
5. **Generate output** in the format requested (chat analysis, Word report, Excel, or slides)

---

## Step 1: Task Identification

When the user initiates an SEO task, first identify which of these four modes applies:

| Mode | Trigger |
|---|---|
| **Keyword Analysis** | File with keyword/volume/difficulty data, or "what keywords should I target" |
| **Content SEO Audit** | URL, page text, or doc uploaded for SEO review |
| **Technical SEO** | Questions about crawling, indexing, page speed, Core Web Vitals, site structure |
| **SEO Reporting** | Request for a rankings summary, traffic report, or visibility overview |

If the task is unclear, ask one targeted question to clarify — don't ask multiple.

---

## Step 2: File Intake & Parsing

When a file is provided:
- `.csv` → use pandas
- `.xlsx` / `.xls` → use the xlsx skill

```python
import pandas as pd

# CSV
df = pd.read_csv('/path/to/file.csv')

# Excel
df = pd.read_excel('/path/to/file.xlsx')

# Clean column names
df.columns = df.columns.str.strip()

# Convert numeric strings
for col in df.select_dtypes(include='object').columns:
    try:
        df[col] = pd.to_numeric(
            df[col].str.replace(',', '').str.replace('%', ''), errors='ignore'
        )
    except:
        pass
```

### Column Name Mappings

→ See `references/column-maps.md` for GSC, Ahrefs, and SEMrush column mappings.

---

## Step 3: Analysis Frameworks

### 3.1 Keyword Research & Analysis

When analyzing keyword data:

**Opportunity scoring** — Classify each keyword:
- 🟢 **Quick Win**: Position 4–15, difficulty < 40, volume > 100 → already ranking, push to page 1
- 🔵 **High Value**: Volume > 500, difficulty < 60 → worth targeting
- 🟡 **Long-term**: High volume, high difficulty → content investment needed
- ⚪ **Informational**: Question-based, low CPC → good for blogs/content

**Key calculations:**
```python
# Estimated traffic potential (if not provided)
# Rough CTR by position: P1=28%, P2=15%, P3=11%, P4=8%, P5=7%
ctr_by_pos = {1: 0.28, 2: 0.15, 3: 0.11, 4: 0.08, 5: 0.07}
df['est_traffic'] = df.apply(
    lambda r: r['search_volume'] * ctr_by_pos.get(int(r['avg_position']), 0.02)
    if pd.notna(r['avg_position']) else 0, axis=1
)
```

**What to surface:**
- Top 10 quick-win keywords (best opportunity per effort)
- Keyword gaps (high volume keywords not yet ranking)
- Cannibalization risks (multiple URLs ranking for same keyword)
- Branded vs. non-branded split (if identifiable)

### 3.2 Content SEO Audit

When given a URL, page text, or document to audit:

**Check these elements in order:**

1. **Title tag** — Is it 50–60 characters? Does it include the primary keyword near the front?
2. **Meta description** — Is it 140–160 characters? Is it compelling with a CTA?
3. **H1** — One H1 only, contains primary keyword
4. **Headings structure** — Logical H2/H3 hierarchy, secondary keywords in H2s
5. **Keyword usage** — Primary keyword in first 100 words, used naturally throughout
6. **Content depth** — Word count appropriate for intent (informational: 800+, pillar: 1500+)
7. **Internal links** — Are there at least 2–3 relevant internal links?
8. **Image alt text** — Are images present? Do alt texts include keywords?
9. **URL slug** — Short, contains keyword, no stop words
10. **Page speed / CWV** — Flag if the user has data; otherwise note as "requires manual check"

**Output format for content audit:**
```
## SEO Audit — [Page Title / URL]

### ✅ Passing
[List of elements that are well-optimized]

### ⚠️ Needs Improvement
[Specific issue + exact fix recommended]

### ❌ Critical Issues
[High-impact problems — fix immediately]

### 📝 Rewrite Suggestions
[Specific copy rewrites for title, meta, H1 if needed]
```

### 3.3 Technical SEO

When the user asks about technical issues, structure your response around these areas:

**Crawlability & Indexing**
- robots.txt blocking key pages?
- Canonical tags correct?
- noindex accidentally applied?
- XML sitemap up to date and submitted?

**Core Web Vitals**
- LCP (Largest Contentful Paint): target < 2.5s
- FID/INP (Interactivity): target < 100ms
- CLS (Cumulative Layout Shift): target < 0.1
- Flag which CWV is failing and what typically causes it

**Site Structure**
- Is crawl depth > 3 clicks from homepage for important pages?
- Orphan pages (no internal links pointing to them)?
- Redirect chains (301 → 301 → destination)?

**Mobile & International**
- Mobile-first indexing: is the mobile version complete?
- hreflang tags present and correct for Arabic/English content?

Always explain the business impact of each technical issue (why it matters for rankings/traffic), not just the issue itself.

### 3.4 SEO Reporting

When generating an SEO report, always include:

**Standard report structure:**

```
## SEO Report — [Client/Brand] | [Period]

### 📊 Executive Summary
[3–5 key takeaways — written for a non-technical audience]

### 📈 Organic Traffic Overview
- Sessions / Clicks (vs. previous period)
- Impressions
- Average CTR
- Average Position

### 🏆 Top Performing Keywords
[Top 10 by clicks or traffic, with position]

### 📉 Declining Keywords / Pages
[Keywords or pages that dropped — with possible reasons]

### 🔍 Opportunities Identified
[Quick wins, content gaps, technical issues]

### ✅ Recommendations
[3–5 prioritized, actionable next steps]
```

For client-facing reports: lead with outcomes and opportunities, frame declines as "areas for optimization."
For internal reports: be direct, include raw numbers, flag urgency clearly.

---

## Step 4: Output Formats

| Requested Output | Action |
|---|---|
| Chat analysis | Use plain analysis format from relevant framework above |
| Word document / report | Read the docx skill first → `/mnt/.skills/skills/docx/SKILL.md` |
| Excel file | Read the xlsx skill first → `/mnt/.skills/skills/xlsx/SKILL.md` |
| Presentation / slides | Read the pptx skill first → `/mnt/.skills/skills/pptx/SKILL.md` |

---

## Step 5: Tone & Language

- **Default**: English, professional, data-driven
- **Arabic output**: If the user writes in Arabic or requests Arabic output, switch fully — all labels, headings, insights, and recommendations. Use proper marketing/SEO terminology in Arabic (e.g., كثافة الكلمات المفتاحية، الظهور العضوي، معدل النقر).
- **Do not mix languages** in the same output unless explicitly asked.
- **Client-facing**: Lead with insights, frame problems as opportunities, include next steps
- **Internal**: Direct language, include all data, flag critical issues clearly

---

## Edge Cases

- **No file provided**: Ask the user to share data or a URL. If they describe the situation verbally, work with what's given and note what would be needed for a full analysis.
- **GSC data with no conversions**: Focus on clicks, impressions, CTR, and position. Note that revenue impact cannot be computed without linking to GA4 or CRM data.
- **Arabic keyword data**: Be aware that search volumes for Arabic keywords are often lower — adjust opportunity thresholds accordingly (volume > 50 can be high-value in Arabic markets).
- **Large files (>5,000 rows)**: Aggregate to keyword or URL level first, then analyze top/bottom performers.
- **Competitor data included**: If Ahrefs/SEMrush export includes competitor columns, surface competitor gaps as additional opportunities.
