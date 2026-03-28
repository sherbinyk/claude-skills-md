---
name: flamingo-performance-analysis
description: >
  E-commerce performance analysis skill for Flamingo — a cosmetics and beauty brand in Egypt.
  Use this skill whenever analyzing paid media campaigns for Flamingo or any Egyptian beauty/cosmetics
  e-commerce client. Primary platforms are Meta Ads (Facebook & Instagram) and TikTok Ads, with
  secondary support for Google Ads. Trigger when the user uploads a CSV or Excel export from Meta
  Ads Manager, TikTok Ads Manager, or Google Ads for Flamingo, or asks to analyze ROAS, CPA,
  purchase cost, creative performance, or overall campaign performance. Also trigger for casual
  requests like "how did Flamingo do this week", "check the Meta results", "review TikTok",
  "why is CPA high", or "give me the performance report". Always interprets metrics through an
  e-commerce lens. Default output language is Arabic; switch to English if the user writes in English.
---

# flamingo-performance-analysis — Flamingo (Cosmetics, Egypt)

## Context

| | |
|---|---|
| **Client** | Flamingo |
| **Industry** | Cosmetics / Beauty E-commerce |
| **Market** | Egypt (currency: EGP) |
| **Platforms** | Meta Ads — Facebook & Instagram (primary) · TikTok Ads · Google Ads |
| **Primary KPI** | ROAS · Cost per Purchase · Revenue |
| **Use for** | All paid media performance analysis for Flamingo |
| **Do NOT use for** | Link Development (use ld-performance-analysis) · Qormuz (use qormuz-performance-analysis) |

This skill analyzes paid media performance for **Flamingo** — a cosmetics and beauty brand operating in Egypt. The business model is **e-commerce**, so success metrics are purchase-focused: ROAS, CPA (cost per purchase), and revenue. Primary channel is **Meta Ads** (Facebook & Instagram), with **TikTok Ads** as a growing secondary channel, and Google Ads as tertiary.

The Egyptian market context matters: currency is EGP, the audience is predominantly female, Instagram and TikTok drive strong product discovery for beauty, and seasonal peaks (Ramadan, Eid, back-to-school, Mother's Day) significantly shift benchmarks.

---

## Workflow Overview

1. **Identify the platform** from the file or user context
2. **Parse and clean the data** — pandas for CSV, xlsx skill for Excel
3. **Map columns** to the standard schema below
4. **Analyze** using the e-commerce framework
5. **Output** in requested format and language

---

## Step 1: File Intake

- Check file extension: `.csv` → pandas; `.xlsx` → read xlsx skill
- Infer platform from column signatures if not stated (see Auto-Detection below)
- Ask for **reporting period** if not in the file
- Ask for **campaign objective** if ambiguous — for Flamingo this is almost always Purchases/Conversions, but occasionally Traffic or Awareness

---

## Step 2: Column Maps

### Meta Ads Export

| Standard Name   | Meta Column Name(s)                                   |
|-----------------|-------------------------------------------------------|
| `campaign_name` | `Campaign name`                                       |
| `adset_name`    | `Ad Set Name`                                         |
| `ad_name`       | `Ad Name`                                             |
| `spend`         | `Amount spent (EGP)` / `Amount spent`                 |
| `impressions`   | `Impressions`                                         |
| `clicks`        | `Link clicks`                                         |
| `ctr`           | `CTR (link click-through rate)`                       |
| `cpc`           | `CPC (cost per link click)`                           |
| `cpm`           | `CPM (cost per 1,000 impressions)`                    |
| `conversions`   | `Purchases` / `Results`                               |
| `revenue`       | `Purchase conversion value`                           |
| `cpa`           | `Cost per result` / `Cost per purchase`               |
| `roas`          | `Website purchase ROAS` / `Purchase ROAS`             |
| `frequency`     | `Frequency`                                           |
| `add_to_cart`   | `Adds to cart` (optional — use if available)          |
| `initiate_checkout` | `Checkouts initiated` (optional)                 |

---

### TikTok Ads Export

| Standard Name   | TikTok Ads Column Name(s)                             |
|-----------------|-------------------------------------------------------|
| `campaign_name` | `Campaign Name`                                       |
| `adset_name`    | `Ad Group Name`                                       |
| `ad_name`       | `Ad Name`                                             |
| `spend`         | `Cost` / `Amount Spent`                               |
| `impressions`   | `Impressions`                                         |
| `clicks`        | `Clicks`                                              |
| `ctr`           | `CTR` / `Click-Through Rate`                          |
| `cpc`           | `CPC` / `Cost Per Click`                              |
| `cpm`           | `CPM` / `Cost Per 1000 Impressions`                   |
| `conversions`   | `Complete Payment` / `Conversions` / `Purchases`      |
| `revenue`       | `Total Complete Payment Value` / `Revenue`            |
| `cpa`           | `Cost Per Complete Payment` / `Cost Per Conversion`   |
| `roas`          | `ROAS` / `Return on Ad Spend`                         |
| `video_views`   | `Video Views`                                         |
| `video_vtr`     | `Video Views at 100%` / `Video Completion Rate`       |

**Detection signal:** `Complete Payment`, `Ad Group Name`, or `Video Views at 100%` uniquely identify TikTok exports.

---

### Google Ads Export

| Standard Name   | Google Ads Column Name(s)          |
|-----------------|------------------------------------|
| `campaign_name` | `Campaign`                         |
| `adset_name`    | `Ad group`                         |
| `ad_name`       | `Ad`                               |
| `spend`         | `Cost`                             |
| `impressions`   | `Impr.`                            |
| `clicks`        | `Clicks`                           |
| `ctr`           | `CTR`                              |
| `cpc`           | `Avg. CPC`                         |
| `conversions`   | `Conversions`                      |
| `revenue`       | `Conv. value`                      |
| `cpa`           | `Cost / conv.`                     |
| `roas`          | `Conv. value / cost`               |

---

### Auto-Detection

| Platform | Unique Signal Columns                                          |
|----------|----------------------------------------------------------------|
| Meta     | `Frequency`, `CPM (cost per 1,000 impressions)`, `Ad Set Name` |
| TikTok   | `Complete Payment`, `Ad Group Name`, `Video Views at 100%`     |
| Google   | `Impr.`, `Avg. CPC`, `Conv. value / cost`, `Ad group`          |

---

## Step 3: Analysis Framework

### 3.1 Top-Line Summary

Compute totals and averages:
- Total Spend, Impressions, Clicks, Purchases, Revenue
- Blended CTR, CPC, CPM, CPA (Cost per Purchase), ROAS
- Add-to-cart rate and checkout completion rate (if data available) — these reveal funnel drop-off points
- Flag: ROAS < 1.0 → spending more than earning; zero purchases with spend > 10% budget → urgent

### 3.2 Platform Comparison (when multi-platform data)

| Platform | Spend | Purchases | CPA  | ROAS | CTR  |
|----------|-------|-----------|------|------|------|
| Meta     |       |           |      |      |      |
| TikTok   |       |           |      |      |      |
| Google   |       |           |      |      |      |

Flag which platform delivers the best ROAS and recommend budget reallocation if the gap is >30%.

### 3.3 Performance Segmentation

For **purchase/conversion campaigns**, rank by ROAS descending, then CPA ascending.

Label each row:
- 🟢 **Top Performer** — ROAS above campaign average by >20%, or CPA below average by >20%
- 🟡 **On Target** — within ±20% of campaign average
- 🔴 **Underperformer** — ROAS below average by >20%, or CPA above average by >20%

### 3.4 Anomaly Detection

| Signal | Threshold | Meaning |
|--------|-----------|---------|
| CTR (Meta/TikTok) | < 0.5% | Creative fatigue or wrong audience |
| CTR (Google) | < 2.0% | Weak copy or keyword mismatch |
| Frequency (Meta) | > 3.5 | Audience saturation — refresh creative |
| ROAS | < 1.0 | Losing money — pause and investigate |
| CPA | > 2× campaign average | Budget drain |
| Zero purchases | Spend > 10% budget | Urgent — check pixel, landing page, or audience |
| VTR (TikTok) | < 15% | Creative is not holding attention past 3 seconds |

### 3.5 Creative Analysis (Ad Level)

When ad-level data is available:
- Identify top 3 and bottom 3 by ROAS (or CPA if ROAS unavailable)
- For TikTok: include Video View Rate (VTR) — a low VTR with good CTR means the thumbnail works but the video doesn't hold
- Note patterns: video vs. static, user-generated content (UGC) vs. produced, discount-led vs. product-showcase
- Flag creative fatigue: CTR declining week-over-week, or frequency > 3.5 on Meta

### 3.6 Funnel Analysis (when add-to-cart and checkout data available)

| Stage                  | Volume | Drop-off Rate |
|------------------------|--------|---------------|
| Clicks                 |        |               |
| Add to Cart            |        | % of clicks   |
| Checkout Initiated     |        | % of ATC      |
| Purchases              |        | % of checkout |

High click → low ATC: landing page issue
High ATC → low checkout: price sensitivity or friction
High checkout → low purchase: payment failure or trust issue

---

## Step 4: Egyptian Market Benchmarks

Benchmarks in **EGP**. Adjust during Ramadan (CPM spikes 30–50%, ROAS can improve with right offers) and major sale events.

| Metric       | Meta (Egypt) | TikTok (Egypt) | Google (Egypt) |
|--------------|--------------|----------------|----------------|
| CTR          | 0.8–2.5%     | 0.6–2.0%       | 2–5%           |
| CPC          | EGP 1–5      | EGP 0.8–4      | EGP 2–8        |
| CPM          | EGP 15–45    | EGP 10–35      | N/A (Search)   |
| CPA (beauty) | EGP 50–200   | EGP 60–250     | EGP 80–300     |
| ROAS (beauty)| 2.0–5.0×     | 1.5–4.0×       | 2.5–5.5×       |
| Frequency    | ≤ 3.5        | N/A            | N/A            |
| VTR (TikTok) | N/A          | 15–35%         | N/A            |

> **Cosmetics note:** ROAS benchmarks for beauty in Egypt tend to be higher during gifting seasons (Eid, Mother's Day, Valentine's). Lower ROAS during off-peak is normal — flag only if it falls below 1.5× sustained.

---

## Step 5: Output Formats

### Format A — Plain Analysis (default)

```
## تحليل الأداء — [المنصة] | [الفترة]

### 📊 ملخص الأداء
[جدول المؤشرات الرئيسية]

### 🏆 أفضل الحملات أداءً
[القائمة مع ROAS وCPA والإنفاق]

### ⚠️ المشكلات والتنبيهات
[القائمة مع التشخيص]

### 🔍 الملاحظات الرئيسية
[3–5 نقاط]

### ✅ التوصيات
[3–5 إجراءات محددة وقابلة للتنفيذ]
```

### Format B — Excel Report

Read xlsx skill first. Sheets:
1. **Summary** — KPIs, period, platform
2. **Platform Comparison** (if applicable)
3. **Campaign View** — with performance labels
4. **Ad View** — top/bottom performers
5. **Funnel View** — ATC → checkout → purchase (if data available)
6. **Recommendations**

### Format C — PowerPoint Deck

Read pptx skill first. Slides:
1. Cover — Flamingo, Platform(s), Period
2. Executive Summary — top KPIs, one-line verdict
3. Platform Comparison (if applicable)
4. Campaign & Ad Performance
5. Creative Insights
6. Issues & Recommendations

---

## Step 6: Language

- **Default:** Arabic — all labels, insights, and recommendations in Arabic
- **Switch to English** if the user writes in English or requests English output
- Do not mix languages in the same report unless the user asks for a bilingual output
- For numbers: use Arabic-Indic numerals only if user prefers; default to Western numerals (0–9) for tables

---

## Reference Files

- `references/flamingo-templates.md` — Report templates pre-formatted for Flamingo
