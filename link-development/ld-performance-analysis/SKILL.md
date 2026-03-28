---
name: ld-performance-analysis
description: >
  Lead generation performance analysis skill for Link Development's digital marketing team.
  Use this skill whenever analyzing paid media campaigns focused on B2B lead generation —
  primarily LinkedIn Ads and Google Search Ads, with secondary support for Meta Ads and X (Twitter) Ads.
  Trigger when the user uploads a CSV or Excel export from LinkedIn Campaign Manager, Google Ads,
  Meta Ads, or X Ads, or asks to analyze CPL, MQL quality, lead volume, funnel performance,
  or campaign ROI for any B2B or lead gen campaign. Also trigger for casual requests like
  "how did the LinkedIn campaign do", "check our CPL this month", "why are leads expensive",
  "review our Google Search results", or "compare platforms". Always interprets metrics through
  a lead generation lens — never e-commerce or ROAS-first.
---

# ld-performance-analysis — Link Development (Lead Gen)

## Context

| | |
|---|---|
| **Client** | Link Development |
| **Industry** | B2B Technology |
| **Platforms** | LinkedIn Ads (primary) · Google Search Ads (primary) · Meta Ads · X Ads |
| **Primary KPI** | CPL (Cost per Lead) · Lead Volume · MQL Quality |
| **Use for** | All paid media analysis for Link Development campaigns |
| **Do NOT use for** | Qormuz (use qormuz-performance-analysis) · Flamingo (use flamingo-performance-analysis) · Any e-commerce ROAS analysis |

This skill analyzes paid media performance for **B2B lead generation** campaigns. Primary platforms are **LinkedIn Ads** and **Google Search Ads**. Meta Ads and X Ads are secondary investments — analyzed with the same rigor but with adjusted expectations.

The goal of every analysis is to answer: *Are we generating quality leads at an efficient cost, and where should we optimize next?*

---

## Workflow Overview

1. **Identify the platform** from the file or user context
2. **Parse and clean the data** — use pandas for CSV, xlsx skill for Excel
3. **Map columns** to the standard schema using the reference below
4. **Analyze** using the lead gen framework
5. **Output** in the format requested

---

## Step 1: File Intake

- Check file extension: `.csv` → pandas; `.xlsx` → read xlsx skill at `.claude/skills/xlsx/SKILL.md`
- If platform is unclear, infer from column signatures (see Column Maps section below)
- Ask for **reporting period** if not in the file
- Ask for **campaign objective** only if ambiguous (lead form vs. website conversion vs. awareness)

---

## Step 2: Column Maps

### LinkedIn Campaign Manager Export

| Standard Name   | LinkedIn Column Name(s)                          |
|-----------------|--------------------------------------------------|
| `campaign_name` | `Campaign name`                                  |
| `adset_name`    | `Ad group name`                                  |
| `ad_name`       | `Creative name` / `Ad name`                      |
| `spend`         | `Amount spent` / `Total spent`                   |
| `impressions`   | `Impressions`                                    |
| `clicks`        | `Clicks`                                         |
| `ctr`           | `Click-through rate (CTR)` / `Average CTR`       |
| `cpc`           | `Average CPC` / `Cost per click`                 |
| `leads`         | `Leads` / `Lead form opens` / `One-click leads`  |
| `cpl`           | `Cost per lead` / `Cost per one-click lead`      |
| `conversions`   | `Conversions` / `Website conversions`            |
| `cpa`           | `Cost per conversion`                            |
| `conv_rate`     | `Conversion rate`                                |
| `video_views`   | `Video views` (video campaigns only)             |
| `follows`       | `Follows` (follower campaigns only)              |

**Detection signal:** Columns like `Lead form opens`, `One-click leads`, or `Cost per one-click lead` uniquely identify LinkedIn exports.

---

### Google Ads Export (Search / Demand Gen)

| Standard Name   | Google Ads Column Name(s)              |
|-----------------|----------------------------------------|
| `campaign_name` | `Campaign`                             |
| `adset_name`    | `Ad group`                             |
| `ad_name`       | `Ad` / `Responsive search ad`          |
| `spend`         | `Cost` / `Cost (USD)`                  |
| `impressions`   | `Impr.` / `Impressions`                |
| `clicks`        | `Clicks`                               |
| `ctr`           | `CTR`                                  |
| `cpc`           | `Avg. CPC`                             |
| `conversions`   | `Conversions` / `Conv.`                |
| `cpa`           | `Cost / conv.`                         |
| `conv_rate`     | `Conv. rate`                           |
| `impr_share`    | `Search Impr. share`                   |
| `quality_score` | `Quality Score` (keyword level)        |

---

### Meta Ads Export (Lead Gen Objective)

| Standard Name   | Meta Column Name(s)                               |
|-----------------|---------------------------------------------------|
| `campaign_name` | `Campaign name`                                   |
| `adset_name`    | `Ad Set Name`                                     |
| `ad_name`       | `Ad Name`                                         |
| `spend`         | `Amount spent (USD)` / `Amount spent`             |
| `impressions`   | `Impressions`                                     |
| `clicks`        | `Link clicks`                                     |
| `ctr`           | `CTR (link click-through rate)`                   |
| `cpc`           | `CPC (cost per link click)`                       |
| `leads`         | `Leads` / `On-Facebook leads` / `Website leads`   |
| `cpl`           | `Cost per lead` / `Cost per result`               |
| `frequency`     | `Frequency`                                       |

---

### X (Twitter) Ads Export

| Standard Name   | X Ads Column Name(s)                      |
|-----------------|-------------------------------------------|
| `campaign_name` | `Campaign name`                           |
| `adset_name`    | `Ad group name`                           |
| `ad_name`       | `Card name` / `Ad name`                   |
| `spend`         | `Spend` / `Billed charge`                 |
| `impressions`   | `Impressions`                             |
| `clicks`        | `Link clicks` / `URL clicks`              |
| `engagements`   | `Engagements`                             |
| `ctr`           | `CTR`                                     |
| `cpc`           | `Cost per link click`                     |
| `leads`         | `Leads` / `Lead form submissions`         |
| `cpl`           | `Cost per lead`                           |

---

## Step 3: Analysis Framework

Always analyze at **three levels** when data allows: Campaign → Ad Group → Ad.

### 3.1 Top-Line Summary

Compute totals and averages:
- Total Spend, Total Impressions, Total Clicks, Total Leads/Conversions
- Blended CTR, Blended CPC, Blended CPL/CPA
- Lead volume per platform (where multi-platform data exists)
- Flag: zero conversions with spend > 10% of budget → urgent issue

### 3.2 Platform Comparison (when multiple platforms in scope)

When Link Development is running LinkedIn + Google + Meta + X simultaneously, always produce a cross-platform view:

| Platform  | Spend | Leads | CPL  | CTR  | CPC  |
|-----------|-------|-------|------|------|------|
| LinkedIn  |       |       |      |      |      |
| Google    |       |       |      |      |      |
| Meta      |       |       |      |      |      |
| X         |       |       |      |      |      |

Flag the most efficient platform by CPL and recommend budget reallocation if the gap is significant (>30% CPL difference).

### 3.3 Performance Segmentation

Rank campaigns / ad groups by primary KPI: **CPL ascending**, then **CTR descending**.

Label each row:
- 🟢 **Efficient** — CPL below blended average by >20%
- 🟡 **On target** — CPL within ±20% of blended average
- 🔴 **Expensive** — CPL above blended average by >20%

### 3.4 Anomaly Detection

Flag these automatically:

| Signal | Threshold | Meaning |
|--------|-----------|---------|
| CTR (LinkedIn) | < 0.3% | Poor creative or targeting match |
| CTR (Google Search) | < 2.0% | Weak copy or keyword mismatch |
| CTR (Meta) | < 0.4% | Creative fatigue or wrong audience |
| Frequency (Meta/LinkedIn) | > 3.5 | Audience saturation |
| CPL | > 2× campaign average | Budget drain |
| Zero leads | Spend > 10% budget | Urgent — pause or investigate |
| Impression Share (Google) | < 40% | Budget or Quality Score limiting reach |

### 3.5 Creative Analysis (Ad Level)

When ad-level data is available:
- Identify top 3 and bottom 3 ads by CPL
- Note patterns across top performers (format, message angle, audience)
- Flag creative fatigue: CTR declining week-over-week or frequency > 3.5

---

## Step 4: Lead Gen Benchmarks

Use as directional benchmarks. B2B tech/enterprise benchmarks in the MENA region tend toward the higher end.

| Metric         | LinkedIn (B2B) | Google Search (B2B) | Meta (B2B Lead Gen) | X (B2B)    |
|----------------|----------------|----------------------|----------------------|------------|
| CTR            | 0.35–0.65%     | 3–8%                 | 0.5–1.5%             | 0.5–1.0%   |
| CPC            | $8–$20         | $3–$12               | $1–$4                | $1–$5      |
| CPL            | $40–$150       | $20–$80              | $15–$60              | $20–$100   |
| Conv. Rate     | 5–15% (LGF)    | 2–6%                 | 1–4%                 | 1–3%       |
| Frequency cap  | ≤ 3.5          | N/A                  | ≤ 3.5                | N/A        |

> **Note:** LinkedIn Lead Gen Form (LGF) completion rates (5–15%) are typically higher than website landing page conversions because friction is lower. Always distinguish between LGF leads and website form submissions in the analysis.

> **Currency:** If data is in AED or EGP, note it. Do not convert unless asked.

---

## Step 5: Output Formats

### Format A — Plain Analysis (default)

```
## Performance Analysis — [Platform(s)] | [Period]

### 📊 Top-Line Summary
[Key metrics table]

### 🏆 Top Performers
[List with CPL, CTR, spend]

### ⚠️ Issues & Anomalies
[List with diagnosis]

### 🔍 Key Observations
[3–5 insight bullets]

### ✅ Recommendations
[3–5 prioritized, specific, actionable items]
```

### Format B — Excel Report

Read xlsx skill before generating. Structure:
1. **Summary** — blended KPIs, period, platforms
2. **Platform Comparison** — cross-platform view (if applicable)
3. **Campaign View** — campaign-level metrics with labels
4. **Ad Group View** — ad group breakdown
5. **Ad View** — ad-level data with top/bottom flags
6. **Recommendations** — plain text action items

### Format C — PowerPoint Deck

Read pptx skill before generating. Slides:
1. Cover — Campaign Name, Platform(s), Period
2. Executive Summary — top 3 KPIs, one-line verdict
3. Platform Comparison (if applicable)
4. Campaign Breakdown
5. Top & Bottom Performers
6. Issues & Recommendations

---

## Step 6: Tone & Language

- **Internal (Link Development team)**: Direct, data-forward, include raw numbers. No softening.
- **Client-facing**: Lead with outcomes, frame issues as "optimization opportunities", include forward-looking recommendations.
- **Language**: Default to English. Switch fully to Arabic if the user writes in Arabic or requests it — including labels, column headers, and insights.

---

## Reference Files

- `references/ld-analysis-templates.md` — Report templates pre-formatted for Link Development context
