# Skills MD

Extracted and readable versions of all `.skill` files, organized to mirror the original folder structure.

---

## Structure

```
claude-skills-md/
├── system/
│   ├── skills-navigation/        # Master navigation map across all skills
│   │   └── SKILL.md
│   └── skill-creator/            # Build, test, and improve skills
│       └── SKILL.md
│
├── core/                         # Universal skills — apply across all clients
│   ├── docx/                     # Word document creation and editing
│   ├── xlsx/                     # Excel spreadsheet creation and editing
│   ├── pptx/                     # PowerPoint presentation creation and editing
│   ├── pdf/                      # PDF reading, creation, merging, and forms
│   └── schedule/                 # Scheduled and recurring task creation
│
├── universal/                    # Multi-client skills (work across all brands)
│   └── social-analysis/          # Organic social media performance analysis
│       ├── SKILL.md
│       └── references/
│           ├── platform-column-maps.md
│           └── analysis-output-template.md
│
├── link-development/             # Skills for the primary employer (B2B tech)
│   ├── ld-ads-copy/              # Paid ad copy — LinkedIn & Google Search
│   ├── ld-blogging/              # Blog articles, reshares, long-form content
│   │   └── references/
│   │       ├── article-research.md
│   │       ├── human-like-writing.md
│   │       └── blog-reshare.md
│   ├── ld-content-creator/       # Social posts, emails, landing pages, general copy
│   │   └── references/
│   │       ├── audiences.md
│   │       ├── brand-voices.md
│   │       └── email-ready-format.md
│   ├── ld-performance-analysis/  # Campaign analysis — LinkedIn, Google, Meta, X
│   │   └── references/
│   │       └── ld-analysis-templates.md
│   └── ld-seo/                   # SEO audits, keyword research, organic performance
│       └── references/
│           └── column-maps.md
│
└── freelance/
    └── clients/                  # Freelance client skills
        ├── flamingo/             # Cosmetics e-commerce, Egypt — Meta & TikTok Ads
        │   └── flamingo-performance-analysis/
        │       ├── SKILL.md
        │       └── references/
        │           └── flamingo-templates.md
        └── qormuz/               # Fashion e-commerce, Saudi Arabia — Meta, Google & Snapchat
            ├── qormuz-performance-analysis/
            │   ├── SKILL.md
            │   └── references/
            │       ├── Analysis templates.md
            │       └── platform-column-maps.md
            └── qormuz-ads-copy-ar/
                └── SKILL.md
```

---

## Skill Types

| Type | Description |
|---|---|
| `SKILL.md` | Core instructions — the main brain of the skill |
| `references/` | Supporting knowledge files Claude reads before acting |

---

## Skill Index

### System

| Skill | Purpose |
|---|---|
| `skills-navigation` | Master map for locating all skills and reference files |
| `skill-creator` | Build, test, iterate, and package new skills |

### Core (Universal)

| Skill | Purpose |
|---|---|
| `docx` | Word document creation, editing, and XML-level manipulation |
| `xlsx` | Excel spreadsheet creation, editing, formulas, and formatting |
| `pptx` | PowerPoint deck creation, editing, and visual QA |
| `pdf` | PDF reading, extraction, merging, splitting, forms, and creation |
| `schedule` | Create scheduled or recurring tasks |

### Universal (Multi-Client)

| Skill | Purpose |
|---|---|
| `social-analysis` | Organic social performance analysis — Facebook, Instagram, LinkedIn, TikTok, Snapchat, Threads, X |

### Link Development

| Skill | Purpose |
|---|---|
| `ld-content-creator` | Social posts, emails, ad copy, web content for Link Development |
| `ld-ads-copy` | B2B English ad copy for LinkedIn Ads and Google Search Ads |
| `ld-blogging` | Blog articles, reshares, long-form B2B content |
| `ld-performance-analysis` | Lead gen campaign analysis — LinkedIn, Google, Meta, X |
| `ld-seo` | SEO audits, keyword research, organic performance reports |

### Freelance — Flamingo

| Skill | Purpose |
|---|---|
| `flamingo-performance-analysis` | E-commerce campaign analysis — Meta, TikTok, Google (Egypt, Arabic default) |

### Freelance — Qormuz

| Skill | Purpose |
|---|---|
| `qormuz-performance-analysis` | E-commerce campaign analysis — Meta, Google, Snapchat (Saudi Arabia) |
| `qormuz-ads-copy-ar` | Arabic Google Ads copy — RSA, PMax, Display, Shopping, and more |

---

## How to Use

Each skill folder contains a `SKILL.md` with the full instructions, and optionally a `references/` subfolder with domain-specific knowledge files (brand voices, templates, column maps, etc.).

To apply a skill, reference the relevant `SKILL.md` and any files under its `references/` folder.
