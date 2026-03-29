# Platform Column Maps

This file maps each platform's native export columns to the unified schema.
Reference this whenever normalizing raw exports.

---

## Facebook (Meta Business Suite — Post Export)

**File format:** CSV
**Rows:** One row per post, lifetime metrics
**Identifying headers:** `Page ID`, `Page name`, `Reactions, Comments and Shares`, `Caption type`

### Column Mapping

| Unified Column | Facebook Source Column | Notes |
|---|---|---|
| `Publish Date` | `Publish time` | Strip time, keep date only |
| `Content Text` | `Title` | Caption text; truncate at 200 chars |
| `Permalink` | `Permalink` | |
| `Content Type` | `Post type` | See normalization table below |
| `Organic / Paid` | *(not in export)* | Set to "Organic" — FB post export = organic |
| `Impressions` | `Views` | Total times post appeared in feeds |
| `Reach` | `Reach` | Unique accounts |
| `Likes` | `Reactions` | Includes all emoji reaction types |
| `Comments` | `Comments` | |
| `Shares / Reposts` | `Shares` | |
| `Follows` | *(not in export)* | Leave blank — FB post export doesn't include this |
| `Clicks` | `Total clicks` | Includes all click types |
| `Saves` | *(not in export)* | Leave blank — not tracked by FB native analytics |
| `Engagements` | Calculated | `Reactions + Comments + Shares` |
| `Engagement Rate` | Calculated | `Engagements / Views` |

### Facebook-Only Columns (keep in Facebook sheet, exclude from unified)

| Column | Description |
|---|---|
| `Post ID` | Internal FB identifier |
| `Page ID` | Page identifier |
| `Link Clicks` | Subset of Total clicks — clicks on links only |
| `Other Clicks` | Clicks not on links or photos |
| `Matched Audience Targeting Consumption (Photo Click)` | Photo/image clicks |
| `Seconds viewed` | Total seconds video was watched |
| `Average Seconds viewed` | Average watch time per view |
| `Estimated earnings (USD)` | Monetization (usually empty for brand pages) |
| `Ad CPM (USD)` | Paid only — usually empty in organic export |
| `Ad impressions` | Paid only |
| `Negative feedback from users: Hide all` | Negative signals |
| `Negative feedback from users: Hide` | Negative signals |
| `Reactions, Comments and Shares` | Pre-summed total — recalculate for consistency |
| `Is crosspost` | Boolean |
| `Is share` | Boolean |

### Facebook Content Type Normalization

| Facebook `Post type` | Unified `Content Type` |
|---|---|
| Photos | Image |
| Videos | Video |
| Links | Link |
| Reels | Reel |
| Stories | Story |

---

## Instagram (Meta Business Suite — Post Export)

**File format:** CSV
**Rows:** One row per post, lifetime metrics
**Identifying headers:** `Account username`, `Saves`, `Post type` starting with "IG"

### Column Mapping

| Unified Column | Instagram Source Column | Notes |
|---|---|---|
| `Publish Date` | `Publish time` | Strip time, keep date only |
| `Content Text` | `Description` | Caption text; truncate at 200 chars |
| `Permalink` | `Permalink` | |
| `Content Type` | `Post type` | See normalization table below |
| `Organic / Paid` | *(not in export)* | Set to "Organic" |
| `Impressions` | `Views` | Total views for all content types |
| `Reach` | `Reach` | Unique accounts |
| `Likes` | `Likes` | |
| `Comments` | `Comments` | |
| `Shares / Reposts` | `Shares` | |
| `Follows` | `Follows` | New follows attributed to this post |
| `Clicks` | *(not in export)* | **IG does not export clicks — leave blank** |
| `Saves` | `Saves` | IG-exclusive; important signal of content quality |
| `Engagements` | Calculated | `Likes + Comments + Shares` |
| `Engagement Rate` | Calculated | `Engagements / Views` |

### Instagram-Only Columns (keep in Instagram sheet, exclude from unified)

| Column | Description |
|---|---|
| `Post ID` | Internal IG identifier |
| `Account ID` | Account identifier |
| `Account username` | Handle (e.g. linkdevelopment) |
| `Duration (sec)` | For Reels — video duration |

### Instagram Content Type Normalization

| Instagram `Post type` | Unified `Content Type` |
|---|---|
| IG image | Image |
| IG reel | Reel |
| IG carousel | Carousel |
| IG video | Video |
| IG story | Story |

### ⚠️ Instagram Data Gaps

- **No clicks data** — Instagram native analytics does not export link clicks, profile clicks, or
  any click metrics at post level. This is a hard platform limitation, not a missing column.
- **Saves** are available on Instagram but not on Facebook or LinkedIn.
- The `Date` column in the export always shows "Lifetime" — the actual publish date is in
  `Publish time`.

---

## LinkedIn (LinkedIn Page Analytics Export)

**File format:** XLS (Excel) with two sheets
**Identifying headers:** Sheet names `Metrics` and `All posts`; columns include `Posted by`, `Reposts`

### Sheet: All Posts (post-level data)

| Unified Column | LinkedIn Source Column | Notes |
|---|---|---|
| `Publish Date` | `Created date` | Format: MM/DD/YYYY |
| `Content Text` | `Post title` | Post caption; truncate at 200 chars |
| `Permalink` | `Post link` | Full LinkedIn activity URL |
| `Content Type` | `Content Type` | "Video" or blank — see normalization below |
| `Organic / Paid` | `Post type` | "Organic" or "Sponsored" |
| `Impressions` | `Impressions` | Total impressions |
| `Reach` | *(not in post export)* | **Not available at post level — leave blank** |
| `Likes` | `Likes` | |
| `Comments` | `Comments` | |
| `Shares / Reposts` | `Reposts` | |
| `Follows` | `Follows` | New follows attributed to this post |
| `Clicks` | `Clicks` | All clicks on the post |
| `Saves` | *(not available)* | LinkedIn does not export saves |
| `Engagements` | Calculated | `Likes + Comments + Reposts` |
| `Engagement Rate` | Calculated | Use calculated value OR `Engagement rate` column |

### LinkedIn-Only Columns (keep in LinkedIn Posts sheet, exclude from unified)

| Column | Description |
|---|---|
| `Campaign name` | For sponsored posts |
| `Posted by` | Person who published (e.g., Hidy Rostom) |
| `Campaign start date` | For sponsored posts |
| `Campaign end date` | For sponsored posts |
| `Audience` | Target audience label |
| `Views` | Video views (only populated for video posts) |
| `Offsite Views` | Views from outside LinkedIn |
| `Click through rate (CTR)` | LinkedIn-calculated CTR |
| `Unique impressions (organic)` | Only in Metrics sheet |

### LinkedIn Content Type Normalization

| LinkedIn `Content Type` | Unified `Content Type` |
|---|---|
| Video | Video |
| *(blank)* | Image/Text |
| Document | Document |
| Article | Article |

### Sheet: Metrics (daily page-level data)

This sheet should be preserved as a separate "LinkedIn Daily Metrics" sheet in the output workbook.
It is NOT merged into the unified All Platforms sheet. Use it for:
- Organic vs. sponsored impression breakdown
- Day-by-day trend analysis
- Unique impressions (available here but not in post-level export)

| Metrics Column | Description |
|---|---|
| `Date` | Day (MM/DD/YYYY) |
| `Impressions (organic/sponsored/total)` | Split by distribution type |
| `Unique impressions (organic)` | Unique accounts — only available here |
| `Clicks (organic/sponsored/total)` | |
| `Reactions (organic/sponsored/total)` | |
| `Comments (organic/sponsored/total)` | |
| `Reposts (organic/sponsored/total)` | |
| `Engagement rate (organic/sponsored/total)` | LinkedIn-calculated |

### ⚠️ LinkedIn Data Gaps

- **No reach at post level** — Reach (unique impressions) is only in the daily Metrics sheet.
- **Content Type is sparse** — only "Video" is labeled; other content types are blank.
- **No saves** — LinkedIn does not track or export saves/bookmarks.

---

## Threads (Meta Threads Insights Export)

**File format:** CSV
**Status:** Limited — Threads analytics are still maturing as of early 2026

### Column Mapping (when available)

| Unified Column | Threads Source Column |
|---|---|
| `Publish Date` | `Published` or `Date` |
| `Content Text` | `Post text` or `Caption` |
| `Permalink` | `Post URL` |
| `Content Type` | Inferred (Image / Video / Text) |
| `Impressions` | `Views` |
| `Reach` | *(usually not available)* |
| `Likes` | `Likes` |
| `Comments` | `Replies` |
| `Shares / Reposts` | `Reposts` or `Quotes` |

### ⚠️ Threads Note

If native export is not available, the user may log post metrics manually into a sheet.
Treat manually logged data the same as an export — normalize to unified schema.
Flag in the Notes column: "Manual entry".

---

## X / Twitter (X Analytics Export)

**File format:** CSV
**Identifying headers:** `Tweet id`, `impressions`, `engagements`, `url clicks`, `retweets`

### Column Mapping

| Unified Column | X Source Column | Notes |
|---|---|---|
| `Publish Date` | `time` | Parse date only |
| `Content Text` | `Tweet text` | |
| `Permalink` | Construct from Tweet id: `https://x.com/i/web/status/<Tweet id>` |
| `Content Type` | Inferred from media in tweet | Image / Video / Text / Link |
| `Impressions` | `impressions` | |
| `Reach` | *(not available)* | X does not export reach |
| `Likes` | `likes` | |
| `Comments` | `replies` | |
| `Shares / Reposts` | `retweets` | |
| `Clicks` | `url clicks` | |

### X-Only Columns

| Column | Description |
|---|---|
| `engagements` | Pre-summed total (use for reference) |
| `engagement rate` | X-calculated |
| `media views` | Video/image views |
| `media engagements` | Clicks on media |
| `profile clicks` | Clicks on profile from tweet |
| `detail expands` | Tweet expanded to full view |

---

## Engagement Rate — Consistent Formula

Use this formula consistently across ALL platforms to allow fair comparison:

```
Engagement Rate = (Likes + Comments + Shares) / Impressions
```

Do NOT use platform-provided engagement rate calculations — they use different denominators.
LinkedIn's native ER includes clicks; Facebook's does not. Using the formula above ensures
all platforms are on the same basis.

**Exception:** When reporting LinkedIn ER to the user *specifically for LinkedIn*
(not cross-platform), you may also show the platform-calculated rate alongside.

---

## Followers Reports — Column Maps

Followers exports are separate from post exports. They contain daily new-follower counts
and (for LinkedIn) demographic breakdowns of the cumulative follower base.

---

### Facebook — New Followers (Meta Business Suite)

**File format:** CSV, UTF-16-LE encoded with BOM + `sep=,` header line
**Row 1:** `sep=,`
**Row 2:** `"Facebook follows"` (platform label — skip)
**Row 3:** Header: `"Date","Primary"`
**Data:** One row per day, only days where follows > 0 are included

| Unified Column | Facebook Source | Notes |
|---|---|---|
| `date` | `Date` | ISO format: `2026-01-01T00:00:00` — strip to date only |
| `new_follows` | `Primary` | Daily new page follows |

---

### Instagram — New Followers (Meta Business Suite)

**File format:** CSV, UTF-16-LE encoded with BOM + `sep=,` header line
**Row 1:** `sep=,`
**Row 2:** `"Instagram follows"` (platform label — skip)
**Row 3:** Header: `"Date","Primary"`
**Data:** One row per day — only days with ≥1 new follow are logged (sparse — days with 0 are missing)

| Unified Column | Instagram Source | Notes |
|---|---|---|
| `date` | `Date` | ISO format — strip to date only |
| `new_follows` | `Primary` | Daily new account follows |

**⚠️ Encoding note:** Both FB and IG follows CSVs are UTF-16-LE encoded, not UTF-8.
Use `open(path, 'rb')` and decode with `utf-16-le`. The `decode_meta_csv()` helper in
`build_unified.py` handles this automatically.

---

### LinkedIn — Followers (LinkedIn Page Analytics Export)

**File format:** XLS with 6 sheets

#### Sheet: New followers (daily growth)

| Unified Column | LinkedIn Source | Notes |
|---|---|---|
| `date` | `Date` | MM/DD/YYYY |
| `organic_follows` | `Organic followers` | Organic new followers per day |
| `sponsored_follows` | `Sponsored followers` | Paid/sponsored new followers per day |
| `auto_invited_follows` | `Auto-invited followers` | Auto-invite new followers |
| `total_follows` | `Total followers` | Sum of all types |

#### Sheet: Location
Columns: `Location`, `Total followers` — cumulative follower count by city/region.

#### Sheet: Job function
Columns: `Job function`, `Total followers` — cumulative follower count by job function.

#### Sheet: Seniority
Columns: `Seniority`, `Total followers` — cumulative follower count by seniority level.

#### Sheet: Industry
Columns: `Industry`, `Total followers` — cumulative follower count by industry.

#### Sheet: Company size
Columns: `Company size`, `Total followers` — cumulative follower count by company size band.

All demographic sheets show the **total cumulative audience** at the time of export,
not new followers for the period. Use them for audience profile analysis, not growth analysis.

---

## TikTok (TikTok Creator Center / Business Center Export)

**File format:** CSV
**Identifying headers:** `Video ID`, `Video Title`, `Video Views`, `Average Watch Time`, `Shares`
**Note:** TikTok export column names vary between Creator Center and Business Center versions.
The script tries multiple column name variants automatically.

### Column Mapping

| Unified Column | TikTok Source Column | Notes |
|---|---|---|
| `Publish Date` | `Video Publish Time` or `Date` | Strip time |
| `Content Text` | `Video Title` or `Caption` or `Description` | Truncate to 200 chars |
| `Permalink` | `Video Link` or `URL` | |
| `Content Type` | Always `Reel` | All TikTok content is short-form video |
| `Organic / Paid` | `Organic` | Native analytics = organic |
| `Impressions` | `Video Views` or `Views` | Total video plays |
| `Reach` | `Reach` | Not always available — blank if absent |
| `Likes` | `Likes` or `Hearts` | |
| `Comments` | `Comments` | |
| `Shares / Reposts` | `Shares` | |
| `Follows` | `New Followers` or `Follows` | |
| `Clicks` | `Profile Clicks` or `Clicks` | |
| `Saves` | `Saved` | |
| `Engagements` | Calculated | Likes + Comments + Shares |
| `Engagement Rate` | Calculated | Engagements / Video Views |

### TikTok-Only Columns (keep in TikTok sheet only)

| Column | Description |
|---|---|
| `Avg Watch Time (s)` | Average seconds watched — key TikTok-specific metric |
| `Total Watch Time` | Total seconds watched across all views |
| `Completion Rate` | % of viewers who watched to the end |

### ⚠️ TikTok Data Gaps

- TikTok's export is inconsistent across creator vs. business accounts.
- Reach is not always available — treat Views as the impressions proxy when Reach is absent.
- Watch time and completion rate are TikTok-exclusive and have no equivalent on other platforms.
- TikTok does not export post-level click data unless the post has a link in bio or ad attribution.

---

## Snapchat (Snapchat Story Insights Export)

**File format:** CSV
**Identifying headers:** `Snap ID`, `Story Views`, `Swipe Ups`, `Screenshots`, `Story Date`
**Note:** Snapchat exports are story-based (not individual snap/post level like other platforms).

### Column Mapping

| Unified Column | Snapchat Source Column | Notes |
|---|---|---|
| `Publish Date` | `Story Date` or `Publish Date` or `Date` | |
| `Content Text` | `Story Title` or `Caption` or `Description` | |
| `Permalink` | `Story URL` or `URL` | |
| `Content Type` | Always `Story` | Snapchat content is stories |
| `Organic / Paid` | `Organic` | Native analytics = organic |
| `Impressions` | `Story Views` or `Views` or `Impressions` | Total story views |
| `Reach` | `Unique Viewers` or `Reach` | |
| `Likes` | Not available | **Snapchat has no likes metric** |
| `Comments` | `Replies` | |
| `Shares / Reposts` | `Shares` | |
| `Follows` | `New Subscribers` | New account follows from this story |
| `Clicks` | `Swipe Ups` or `Swipe-Ups` | Swipe-up = link click equivalent |
| `Saves` | `Screenshots` | Screenshots = closest proxy for saves |
| `Engagements` | Calculated | Comments + Shares + Swipe-Ups |
| `Engagement Rate` | Calculated | Engagements / Story Views |

### Snapchat-Only Columns (keep in Snapchat sheet only)

| Column | Description |
|---|---|
| `Swipe-Ups (Clicks)` | Number of swipe-ups (link engagement) |
| `Screenshots (Saves)` | Number of screenshots taken |
| `Completion Rate` | % of viewers who completed the story |

### ⚠️ Snapchat Data Gaps

- **No likes** — Snapchat has no likes/reactions. ER = (Comments + Shares + Swipe-Ups) / Views.
- Swipe-Ups (mapped to Clicks) require a link to be attached to the story.
- Screenshots (mapped to Saves) are a rough proxy — not a perfect equivalent to Instagram Saves.
- Story-level exports may group multiple snaps into one story row.
