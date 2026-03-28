---
name: qormuz-performance-analysis
description: >
  E-commerce performance analysis skill for Qormuz — a fashion brand in Saudi Arabia.
  Use this skill whenever analyzing paid media campaigns for Qormuz across Meta Ads,
  Google Ads, or Snapchat Ads. Trigger when the user uploads a CSV or Excel export from
  any of these platforms for Qormuz, or asks about ROAS, CPA, CTR, CPC, or creative
  performance. Also trigger for casual requests like "how did Qormuz do", "check the Meta
  results", "what's going wrong", or "give me the numbers". Always interprets metrics
  through an e-commerce lens (ROAS-first, purchase CPA). In English or Arabic.
  Do NOT use for Link Development (use ld-performance-analysis — it's lead gen, not e-commerce)
  or for Flamingo (use flamingo-performance-analysis — different market and platforms).
---

# qormuz-performance-analysis — Qormuz (Fashion, Saudi Arabia)

## Context

| | |
|---|---|
| **Client** | Qormuz |
| **Industry** | Fashion E-commerce |
| **Market** | Saudi Arabia |
| **Platforms** | Meta Ads (primary) · Google Ads · Snapchat Ads |
| **Primary KPI** | ROAS · Cost per Purchase |
| **Use for** | All paid media performance analysis for Qormuz |
| **Do NOT use for** | Link Development (use ld-performance-analysis) · Flamingo (use flamingo-performance-analysis) |

## Workflow Overview

1. **Identify the platform** from the file or user context
2. **Parse and clean the data** using the xlsx skill (for Excel) or pandas (for CSV)
3. **Map columns** to standard metrics using the platform column map → `references/platform-column-maps.md`
4. **Run the analysis** following the framework below
5. **Generate output** in the format requested (plain analysis, structured report, or Excel)

---

## Step 1: File Intake

When a file is uploaded:

- Check the file extension: `.csv` → use pandas; `.xlsx` / `.xls` → read the xlsx skill at `/mnt/.skills/skills/xlsx/SKILL.md`
- If the platform is not stated, infer it from column headers (see `references/platform-column-maps.md`)
- Ask the user to clarify the **reporting period** if not present in the file or conversation
- Ask for **campaign objective** if ambiguous (Conversions vs. Lead Generation) — this affects how you weight metrics

---

## Step 2: Data Parsing

```python
import pandas as pd

# For CSV
df = pd.read_csv('/mnt/user-data/uploads/filename.csv')

# For Excel - use xlsx skill; or fallback:
df = pd.read_excel('/mnt/user-data/uploads/filename.xlsx')

# Clean: strip whitespace from column names
df.columns = df.columns.str.strip()

# Convert numeric columns (remove commas, currency symbols)
for col in df.select_dtypes(include='object').columns:
    try:
        df[col] = pd.to_numeric(df[col].str.replace(',', '').str.replace('$', '').str.replace('%', ''), errors='ignore')
    except:
        pass
```

Refer to `references/platform-column-maps.md` to rename columns into the standard schema below.

### Standard Internal Schema

| Standard Name   | Description                                    |
| --------------- | ---------------------------------------------- |
| `campaign_name` | Campaign identifier                            |
| `adset_name`    | Ad set / Ad group name                         |
| `ad_name`       | Individual ad name                             |
| `spend`         | Total amount spent                             |
| `impressions`   | Total impressions                              |
| `clicks`        | Total link clicks                              |
| `conversions`   | Purchase / Lead events                         |
| `revenue`       | Conversion value (if available)                |
| `ctr`           | Click-through rate (%)                         |
| `cpc`           | Cost per click                                 |
| `cpm`           | Cost per 1,000 impressions                     |
| `cpa`           | Cost per acquisition/lead                      |
| `roas`          | Return on ad spend                             |
| `frequency`     | Avg. times an impression was shown (Meta/Snap) |

---

## Step 3: Analysis Framework

Always analyze at **three levels** when data allows: Campaign → Ad Set → Ad.

### 3.1 Top-Line Summary

Compute totals and averages:

- Total Spend, Total Impressions, Total Clicks, Total Conversions
- Blended CTR, Blended CPC, Blended CPA, Blended ROAS (if revenue available)
- Flag if spend is 0 or conversions are 0 — do not divide; note as "insufficient data"

### 3.2 Performance Segmentation

Rank campaigns / ad sets / ads by primary KPI:

- **Conversions campaigns** → sort by ROAS desc, then CPA asc
- **Lead gen campaigns** → sort by CPL asc, then CTR desc

Label each row:

- 🟢 **Top Performer** — ROAS above average OR CPA below average by >20%
- 🟡 **Average** — within ±20% of average
- 🔴 **Underperformer** — ROAS below average OR CPA above average by >20%

### 3.3 Anomaly Detection

Flag these automatically:

- CTR < 0.5% → creative fatigue or poor targeting
- Frequency > 3.5 (Meta/Snap) → audience saturation
- CPA > 2× campaign average → budget drain
- Zero conversions with spend > 10% of total budget → urgent issue
- ROAS < 1.0 → spending more than earning

### 3.4 Creative Analysis (Ad Level)

When ad-level data is available:

- Identify top 3 and bottom 3 ads by primary KPI
- Note patterns in ad names if structured (e.g., "Video_v1", "Static_Offer") — infer creative type
- Flag creative fatigue using CTR trend or frequency

### 3.5 Benchmarks Reference

Use these as directional benchmarks, not hard rules. Adjust based on vertical if known.

|Metric|Meta|Google Search|Snapchat|
|---|---|---|---|
|CTR|0.9–2.5%|3–8%|0.5–1.5%|
|CPC|$0.5–$1.5|$1–$4|$0.3–$1.0|
|CPM|$7–$15|n/a|$3–$8|
|ROAS (ecom)|2.0–4.0×|3.0–6.0×|1.5–3.0×|
|Frequency cap|≤3.5|n/a|≤3.0|

Note: Benchmarks are in USD. If data is in AED or other currencies, flag and convert mentally or ask user.

---

## Step 4: Output Formats

### Format A — Plain Analysis (default for chat)

Use this when no file output is requested. Structure as:

```
## Performance Analysis — [Platform] | [Period]

### 📊 Top-Line Summary
[Table or bullet list of blended metrics]

### 🏆 Top Performers
[List with metrics]

### ⚠️ Underperformers & Issues
[List with diagnosis]

### 🔍 Key Observations
[3–5 bullet insights]

### ✅ Recommendations
[3–5 prioritized, specific, actionable recommendations]
```

### Format B — Structured Excel Report

Use when user asks for a file, spreadsheet, or downloadable report. → Read `/mnt/.skills/skills/xlsx/SKILL.md` before generating.

Structure the Excel with these sheets:

1. **Summary** — blended KPIs, period, platform
2. **Campaign View** — campaign-level metrics with performance labels
3. **Ad Set View** — ad set breakdown
4. **Ad View** — ad-level breakdown with top/bottom flags (if data available)
5. **Recommendations** — plain text action items

### Format C — PowerPoint Slide Deck

Use when user asks for a presentation or slides. → Read `/mnt/.skills/skills/pptx/SKILL.md` before generating.

Slide structure:

1. Cover — Campaign Name, Platform, Period
2. Executive Summary — 3 KPIs, 1-line verdict
3. Performance Breakdown — chart or table
4. Top & Bottom Performers
5. Key Issues
6. Recommendations

---

## Step 5: Tone & Language

- **Internal stakeholder reports**: Direct, data-forward, include raw numbers
- **Client-facing reports**: Lead with insights and outcomes, soften issues as "optimization opportunities", include recommendations framed as next steps
- **Language**: Default to English. If user writes in Arabic or asks for Arabic output, switch fully — including labels, column headers, and insights. Do not mix languages in the same output unless asked.

### Audience-Aware Reporting

For **Technology Leadership & Decision Makers**: lead with business impact (growth, ROI, efficiency), frame issues as optimization opportunities, keep executive summaries to 3–5 outcome-first bullets. See full audience profile in `references/audiences.md` (content-creator skill folder) if needed.

---

## Edge Cases

- **Missing conversion data**: Analyze efficiency metrics only (CTR, CPC, CPM). Note that ROAS/CPA cannot be computed.
- **Multiple platforms in one file**: Split by platform column if present, or ask user to confirm.
- **Very large files (>10k rows)**: Aggregate to campaign or ad-set level first, then analyze.
- **Currency**: Note the currency from the file. Do not convert unless asked. Flag if mixed currencies are detected.

---

## Reference Files

- `references/platform-column-maps.md` — Column name mappings for Meta, Google, Snapchat exports
- `references/Analysis templates.md` — Copy-paste output templates for common report types