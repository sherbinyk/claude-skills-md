---
name: social-analysis
description: >
  Organic social media performance analysis across any client or brand. Use this skill whenever
  the user uploads CSV or XLS exports from Facebook, Instagram, LinkedIn, TikTok, Snapchat,
  Threads, or X native analytics — NOT from Ads Manager. Trigger on phrases like "analyze my
  social media", "check post performance", "how did our posts do", "cross-platform social report",
  "Facebook and Instagram results", "LinkedIn organic performance", "TikTok performance",
  "Snapchat results", or any time the user uploads files that look like native platform analytics
  exports. This skill identifies the client, detects which platforms were uploaded, normalizes
  all data into a unified schema, builds a structured Excel workbook, and delivers a written
  performance analysis in the appropriate language. Do NOT use for paid campaign analysis.
---

# social-analysis

Organic social media performance analysis — works across all clients (Link Development, Flamingo,
Qormuz, or any other brand) and all major platforms (Facebook, Instagram, LinkedIn, TikTok,
Snapchat, Threads, X).

---

## Step 0 — Before you start

Read `references/platform-column-maps.md` for exact column names from each platform's native
export, how to map them to the unified schema, and known data gaps per platform.

---

## Step 1 — Identify the client and language

Before touching the files, determine:

**Which client is this for?**

| Client | Platforms typically active | Output language | Arabic register |
|---|---|---|---|
| Link Development | Facebook, Instagram, LinkedIn | English | — |
| Flamingo | Facebook, Instagram, TikTok | Arabic | Egyptian |
| Qormuz | Facebook, Instagram, Snapchat | Arabic | Gulf (KSA) |
| Other / unknown | Ask | Ask | Ask |

If the client is not clear from context, ask before proceeding. Language and tone differ
significantly — do not default to English for Flamingo or Qormuz.

**Output language rule:** Match the language of the written analysis to the client's default.
If the user themselves writes in a different language than the client default, follow the user.
The Excel workbook title should include the client name regardless of language.

---

## Step 2 — Identify the uploaded files

Identify each file's platform by inspecting headers or filename patterns:

| Platform | Key identifying columns / signals |
|---|---|
| **Facebook** | `Page ID`, `Page name`, `Reactions, Comments and Shares`, `Caption type` |
| **Instagram** | `Account username`, `Account name`, `Saves`, `Post type` starting with "IG" |
| **LinkedIn** | `.xls` with sheets `Metrics` and `All posts`; headers include `Posted by`, `Reposts` |
| **TikTok** | `Video ID`, `Video Title`, `Video Views`, `Average Watch Time`, `Shares` |
| **Snapchat** | `Snap ID`, `Story Views`, `Swipe Ups`, `Screenshots`, `Story Date` |
| **Threads** | `Post ID`, `Views`, `Replies`, `Reposts`, `Quotes` (no reach column) |
| **X (Twitter)** | `Tweet id`, `impressions`, `engagements`, `url clicks`, `retweets` |
| **FB/IG Follows** | UTF-16 CSV with `sep=,` header + `"Facebook follows"` or `"Instagram follows"` label |
| **LinkedIn Followers** | `.xls` with sheets `New followers`, `Location`, `Job function`, `Seniority`, etc. |

If a file's platform is ambiguous, check the permalink/URL column — the domain confirms it.

---

## Step 3 — Run the build script

Use `scripts/build_unified.py`:

```bash
python scripts/build_unified.py \
  --client "Flamingo" \
  --facebook  <fb_posts.csv> \
  --instagram <ig_posts.csv> \
  --linkedin  <li_posts.xls> \
  --tiktok    <tiktok_posts.csv> \
  --snapchat  <snapchat_posts.csv> \
  --fb-follows   <fb_follows.csv> \
  --ig-follows   <ig_follows.csv> \
  --li-follows   <li_followers.xls> \
  --output    <output_path.xlsx> \
  --period    "Jan – Mar 2026"
```

Pass only the files uploaded. All flags except `--output` are optional.
`--client` sets the workbook title — use the brand name exactly.

**What the script produces:**
- One sheet per platform (cleaned, renamed)
- `All Platforms` — unified normalized sheet, one row per post
- `LinkedIn Daily Metrics` — if LinkedIn XLS uploaded (page-level daily data)
- `Followers — Daily Growth` — if any follows files uploaded
- `LinkedIn Follower Demographics` — if LinkedIn followers XLS uploaded
- `Data Quality` — accuracy score + issues list
- `Schema & Notes` — column definitions

**If the script fails**, fall back to the manual normalization in
`references/platform-column-maps.md` and build the workbook using openpyxl directly.

---

## Step 4 — Unified schema (All Platforms sheet)

Every row must have these columns:

| Column | Notes |
|---|---|
| `Platform` | Facebook / Instagram / LinkedIn / TikTok / Snapchat / Threads / X |
| `Publish Date` | MM/DD/YYYY, time stripped |
| `Content Text` | First 200 chars of caption, newlines removed |
| `Permalink` | Direct URL to post |
| `Content Type` | Image / Video / Reel / Carousel / Link / Story / Image-Text |
| `Organic / Paid` | Always Organic for native analytics |
| `Impressions` | Total times post displayed |
| `Reach` | Unique accounts (blank where not exported) |
| `Likes` | All positive reactions |
| `Comments` | |
| `Shares / Reposts` | Platform-specific label normalized |
| `Follows` | New follows attributed to post (where available) |
| `Clicks` | Total clicks (blank where not exported) |
| `Saves` | IG-exclusive; blank for all others |
| `Engagements` | Likes + Comments + Shares |
| `Engagement Rate` | Engagements / Impressions |
| `Notes` | Platform-specific caveats |

**Content type normalization:**

| Raw label | Unified |
|---|---|
| Photos, IG image | Image |
| Videos, IG video, TikTok video | Video |
| IG reel, TikTok | Reel |
| IG carousel | Carousel |
| Links | Link |
| Stories, Snap | Story |
| LI blank content type | Image/Text |

---

## Step 5 — Produce the analysis

Read `references/analysis-output-template.md` for the full structure. Cover:

1. **Overall performance summary** — totals and averages across all platforms
2. **Platform comparison** — ranked performance with explanation
3. **Content type performance** — which formats drive the most engagement
4. **Top 3 posts per platform** — by engagement rate
5. **Cross-posted content** — same post on multiple platforms, ER compared (if applicable)
6. **Follower growth** — totals, averages, peak dates (only if follows data uploaded)
7. **LinkedIn audience demographics** — 1-sentence snapshot (if LI demographic data uploaded)
8. **Recommendations** — specific, data-backed, actionable
9. **Data Completeness score** — mandatory, always last

**Language:**
- Link Development → English
- Flamingo → Arabic (Egyptian register)
- Qormuz → Arabic (Gulf / KSA register)
- Other → match user's language, or ask

**Tone:** Executive-ready. Lead with outcomes, not numbers.
Keep the written analysis under 700 words — the Excel file has all the detail.

---

## Step 6 — Deliver

1. Save the Excel workbook to the workspace folder
2. Share using a `computer://` path link
3. Write the analysis in the conversation — not in the Excel file
4. End with the Data Completeness score section (see template)

---

## Platform-specific caveats (always flag when relevant)

- **Instagram**: No click data in native exports — Clicks column blank.
- **TikTok**: No reach column — Impressions (Views) is used instead. Watch time is TikTok-exclusive.
- **Snapchat**: Swipe-ups = clicks equivalent. No likes. Story-based (not feed posts).
- **LinkedIn (post-level)**: No reach — only in the Daily Metrics sheet. Content Type sparse.
- **Facebook**: "Reactions" includes all emoji types.
- **FB/IG Follows CSVs**: UTF-16-LE encoded — standard CSV readers will fail. Script handles this.
- **IG follows**: Only days with ≥1 new follow are logged — zero-follow days are absent.
