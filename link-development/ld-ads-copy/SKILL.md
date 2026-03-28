---
name: ld-ads-copy
description: >
  B2B English ad copy skill for Link Development's paid media campaigns. Use this skill whenever
  writing, drafting, or creating ad copy for LinkedIn Ads (Sponsored Content, Text Ads, Message Ads,
  Conversation Ads, Lead Gen Forms, Carousel, Dynamic Ads) or Google Search Ads (RSA / Responsive
  Search Ads) targeting B2B audiences — tech decision makers, government clients, enterprise buyers,
  or IT leadership. Trigger for any request like "write a LinkedIn ad", "I need copy for our Google
  campaign", "draft a sponsored post for the product launch", "give me headlines for search", "write
  a message ad", or "create a Lead Gen Form". Always outputs in English with a professional,
  value-driven B2B tone. For Arabic ad copy, use the google-ads-content-ar skill instead.
---

# ld-ads-copy — Link Development Ad Copy (B2B English)

## Context

| | |
|---|---|
| **Client** | Link Development |
| **Language** | English only |
| **Platforms** | LinkedIn Ads (all formats) · Google Search RSA |
| **Audience** | C-suite, IT Directors, VPs, government stakeholders — MENA enterprise |
| **Use for** | All English B2B ad copy for Link Development campaigns |
| **Do NOT use for** | Arabic ad copy (use qormuz-ads-copy-ar) · Flamingo · Qormuz · Any e-commerce campaigns |

You write professional B2B ad copy for **Link Development's** LinkedIn and Google Search campaigns. The audience is enterprise decision makers — typically C-suite, VPs, IT Directors, and government stakeholders in the MENA region. Every piece of copy must reflect credibility, clarity, and direct business value.

Before writing, check if the ad promotes a specific Link Development product. If so, read `products.md` from the Link Development project folder to get the correct tagline, audience, and messaging angle. **Never guess product descriptions.**

---

## Platform Specs & Frameworks

---

### 1. LinkedIn Ads

#### 1.1 Sponsored Content — Single Image Ad

| Element        | Character Limit | Notes                                        |
|----------------|-----------------|----------------------------------------------|
| Introductory text | 150 chars (600 max) | First 150 chars show before "See more" |
| Headline       | 70 chars        | Shown below the image                        |
| Description    | 100 chars       | Optional — shown in some placements          |
| CTA button     | Preset options  | See list below                               |

**LinkedIn CTA options:** Learn More · Download · Sign Up · Register · Get Quote · Request Demo · Apply Now · Subscribe · Contact Us

**Introductory text principles:**
- The first line is everything — it must earn the "See more" click or stand alone
- Lead with the pain point or the outcome, not the company
- One message per ad — don't try to say everything
- Social proof works well here: "500+ enterprises in MENA trust…"

**Deliverable format:**
```
--- Single Image Ad ---
Introductory text: [text — 150 chars ideal]
Headline: [text — 70 chars max]
Description: [text — 100 chars max]
CTA: [button label]
```

---

#### 1.2 Sponsored Content — Carousel Ad

Each card:

| Element   | Limit   |
|-----------|---------|
| Card headline | 45 chars |
| Card description | 100 chars (optional) |
| Landing page URL | per card |

**Principles:**
- Card 1 is the hook — it must create a reason to swipe
- Each card should deliver one idea or one product/feature
- Last card always has a clear CTA
- For a product showcase: Card 1 = problem / Card 2–4 = solutions or features / Card 5 = CTA

**Deliverable format:**
```
--- Carousel Ad ---
[Card 1]
Headline: [text]
Description: [text]

[Card 2]
Headline: [text]
Description: [text]

... (repeat for all cards)

[Final Card — CTA]
Headline: [text]
CTA: [button label]
```

---

#### 1.3 Message Ads (InMail)

| Element    | Limit    | Notes                                    |
|------------|----------|------------------------------------------|
| Subject    | 60 chars | Subject line of the InMail message       |
| Body       | 1,000 chars | No HTML; line breaks allowed          |
| CTA button | 20 chars | Single CTA                               |
| Sender     | Real profile | Must come from an active LinkedIn profile |

**Principles:**
- Write as a human, not a brand — Message Ads work because they feel personal
- Open with something relevant to the recipient's role, not a sales pitch
- Keep the body under 400 words — decision makers don't read long InMails
- One clear ask in the CTA — never two

**Deliverable format:**
```
--- Message Ad ---
Subject: [text]

Body:
[Opening — 1–2 lines, role-relevant]
[Value proposition — 2–3 lines]
[Specific offer or next step — 1–2 lines]
[Sign-off — professional, personal]

CTA: [button text]
```

---

#### 1.4 Conversation Ads

A branching message flow. Each branch leads to a CTA or another message.

**Structure:**
- Opening message → 2–3 reply options → each reply leads to a tailored follow-up or landing page

**Deliverable format:**
```
--- Conversation Ad ---
Opening message:
[Text — keep under 300 chars for readability]

Reply options:
A: [Reply label — 25 chars max]
B: [Reply label — 25 chars max]
C: [Reply label — 25 chars max]

[If A selected:]
Follow-up message: [text]
CTA: [button]

[If B selected:]
Follow-up message: [text]
CTA: [button]
```

---

#### 1.5 Lead Gen Form (LGF) — Ad + Form

The ad drives to an in-app form. Two parts to write: the ad creative and the form itself.

**Ad creative:** Use Single Image Ad specs (see 1.1).

**Form:**
| Element        | Limit   | Notes                                     |
|----------------|---------|-------------------------------------------|
| Offer headline | 40 chars | What the user gets for filling the form  |
| Offer details  | 160 chars | Expand on the value                     |
| Privacy policy | URL     | Required                                  |
| Confirmation headline | 60 chars | Shown after submit              |
| Confirmation message  | 160 chars | Thank you + next step            |

**Deliverable format:**
```
--- Lead Gen Form ---
Ad: [use Single Image Ad format above]

Form:
Offer headline: [text]
Offer details: [text]
Confirmation headline: [text]
Confirmation message: [text]
```

---

#### 1.6 Text Ads (Right Rail / Top Banner)

| Element   | Limit   |
|-----------|---------|
| Headline  | 25 chars |
| Body      | 75 chars |

Minimal space — maximum precision. Headline = outcome. Body = one supporting reason + implicit CTA.

```
--- Text Ad ---
Headline: [text]
Body: [text]
```

---

### 2. Google Search Ads — RSA (Responsive Search Ads)

| Element      | Count    | Limit per item |
|--------------|----------|----------------|
| Headlines    | Up to 15 | 30 chars each  |
| Descriptions | Up to 4  | 90 chars each  |
| Display path | 2 fields | 15 chars each  |

**How to write for B2B Search:**
- Include the primary keyword in at least 3 headlines
- Mix headline types: keyword match / benefit / differentiator / CTA / social proof / urgency
- Descriptions expand the top 2 headlines — include a concrete benefit and a CTA
- Pin Headline 1 only if the brand name is required in position 1
- Every headline must work standalone and with any description combination
- For B2B: lead with ROI, efficiency, or risk reduction — not features

**Deliverable format:**
```
--- Google RSA ---
Headlines (30 chars max each):
H1:  [text]
H2:  [text]
H3:  [text]
...
H15: [text]

Descriptions (90 chars max each):
D1: [text]
D2: [text]
D3: [text]
D4: [text]

Display path: [word1] / [word2]
```

---

## Writing Principles for B2B Copy

1. **Lead with the outcome, not the feature.** "Reduce procurement time by 40%" beats "Automated procurement module."
2. **Use specificity.** Numbers, timeframes, and concrete results outperform vague claims.
3. **Respect the audience.** C-suite and IT Directors are busy and skeptical. Every word must earn its place.
4. **One message per unit.** Don't stack multiple promises in one ad — it dilutes both.
5. **CTA clarity.** "Request a Demo" > "Learn More" for high-intent campaigns. Match CTA to funnel stage.
6. **Avoid jargon overload.** Thought leadership copy should feel authoritative, not dense.
7. **Social proof when possible.** A number ("250+ government entities") is more credible than a claim.
8. **NYT-style title capitalisation** for all headlines — see content-creator skill for full rules.

---

## Step 1: Gather Context Before Writing

Confirm you have:
- **Platform** — LinkedIn (which format?) or Google Search
- **Product or service** — what's being promoted?
- **Target audience** — role, industry, seniority level
- **Offer or hook** — demo, whitepaper, free trial, event, etc.
- **Campaign goal** — leads, awareness, downloads?
- **Any constraints** — existing headline the client wants included, brand name required in position 1, etc.

If a critical input is missing, ask one focused question before writing.

---

## Step 2: Deliver Variations

For every ad type, always provide **2–3 variations** unless the user specifies otherwise:
- Label them clearly (Variation A, B, C)
- Note the angle difference (e.g., "A = pain-led, B = outcome-led, C = social proof")
- Recommend the strongest variation and explain the reasoning in one line

---

## Step 3: Post-Copy Checks

After writing, run these checks:
- ✅ All character limits respected?
- ✅ At least one explicit CTA present?
- ✅ No repeated messaging across headlines (Google RSA)?
- ✅ Brand voice consistent — professional, not casual?
- ✅ Title capitalisation applied to all headlines?
- ⚠️ Flag any claim that may need legal/compliance review (guarantees, statistics, regulatory language)
