# Platform Column Maps

Use these mappings to rename raw export columns into the standard internal schema. After renaming, all analysis logic in SKILL.md applies uniformly regardless of platform.

---

## Meta Ads (Facebook Ads Manager Export)

|Standard Name|Meta Column Name(s)|
|---|---|
|`campaign_name`|`Campaign name`|
|`adset_name`|`Ad Set Name`|
|`ad_name`|`Ad Name`|
|`spend`|`Amount spent (USD)` / `Amount spent`|
|`impressions`|`Impressions`|
|`clicks`|`Link clicks` / `Clicks (all)`|
|`conversions`|`Purchases` / `Leads` / `Results`|
|`revenue`|`Purchase conversion value` / `Website purchase ROAS` × spend|
|`ctr`|`CTR (link click-through rate)`|
|`cpc`|`CPC (cost per link click)`|
|`cpm`|`CPM (cost per 1,000 impressions)`|
|`cpa`|`Cost per result`|
|`roas`|`Website purchase ROAS` / `Purchase ROAS`|
|`frequency`|`Frequency`|

**Notes:**

- Meta exports may include both "Link clicks" and "Clicks (all)" — always prefer `Link clicks` for CTR and CPC
- ROAS in Meta is already computed; Revenue = ROAS × Spend if not directly exported
- "Results" column maps to either Purchases or Leads depending on campaign objective — confirm with user if ambiguous
- Breakdown columns (Age, Gender, Placement) may appear — aggregate before analysis unless user wants segmented view

---

## Google Ads Export (Standard Campaign Report)

|Standard Name|Google Ads Column Name(s)|
|---|---|
|`campaign_name`|`Campaign`|
|`adset_name`|`Ad group`|
|`ad_name`|`Ad` / `Responsive search ad`|
|`spend`|`Cost` / `Cost (USD)`|
|`impressions`|`Impr.` / `Impressions`|
|`clicks`|`Clicks`|
|`conversions`|`Conversions` / `Conv.`|
|`revenue`|`Conv. value` / `All conv. value`|
|`ctr`|`CTR`|
|`cpc`|`Avg. CPC`|
|`cpm`|`Avg. CPM` (Display/YouTube only)|
|`cpa`|`Cost / conv.`|
|`roas`|`Conv. value / cost`|
|`frequency`|N/A (not available in Search)|

**Notes:**

- Google exports use abbreviations: `Impr.`, `Conv.`, `Avg. CPC` — handle both abbreviated and full forms
- `Conv. value / cost` = ROAS (already a ratio, not a percentage)
- For Search campaigns, CPM is not meaningful — skip it
- If exporting YouTube or Display, CPM and View Rate will be present — include in analysis
- "All conversions" vs "Conversions" — prefer `Conversions` unless user specifies otherwise

---

## Snapchat Ads (Ads Manager Export)

|Standard Name|Snapchat Column Name(s)|
|---|---|
|`campaign_name`|`Campaign Name`|
|`adset_name`|`Ad Set Name`|
|`ad_name`|`Ad Name` / `Creative Name`|
|`spend`|`Spend` / `Amount Spent`|
|`impressions`|`Impressions`|
|`clicks`|`Swipe Ups` / `Click-Through`|
|`conversions`|`Purchases` / `Sign Ups` / `App Installs`|
|`revenue`|`Purchase Value` / `Revenue`|
|`ctr`|`Swipe Up Rate` / `CTR`|
|`cpc`|`Cost Per Swipe Up` / `CPC`|
|`cpm`|`eCPM` / `CPM`|
|`cpa`|`Cost Per Purchase` / `Cost Per Sign Up`|
|`roas`|`ROAS` (if available) or compute: Revenue ÷ Spend|
|`frequency`|`Frequency`|

**Notes:**

- Snapchat uses "Swipe Up" instead of Click — treat as equivalent to Link Click
- `eCPM` = effective CPM; treat as CPM
- ROAS may not always be exported directly — compute if Revenue column is present
- Snapchat exports sometimes include Story vs. Non-Story breakdowns — aggregate unless user requests split

---

## Auto-Detection Logic

If the platform is not stated, infer from these unique column signatures:

|Platform|Unique Signal Columns|
|---|---|
|Meta|`Frequency`, `CPM (cost per 1,000 impressions)`, `Ad Set Name`|
|Google|`Impr.`, `Avg. CPC`, `Conv. value / cost`, `Ad group`|
|Snapchat|`Swipe Ups`, `Swipe Up Rate`, `eCPM`|

If detection is ambiguous, ask the user: _"Which platform did this export come from — Meta, Google, or Snapchat?"_