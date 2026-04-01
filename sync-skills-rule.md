# Rule: Sync Skills to Markdown

## What This Rule Does

Whenever `.skills` files inside the `Skills` folder are updated, this rule performs a full sync across two locations:

1. Generates or updates a `.md` file inside `claude-skills-md` that lists all current `.skills` files — their names and any relevant metadata
2. Checks and updates key `.md` files inside the Projects folder for Link Development

## Important Constraint

**Never perform this action automatically.**
Only execute this rule when the user explicitly requests it using one of the trigger phrases below.

---

## Trigger Phrases

Any of the following phrases (or close variations) should activate this rule:

- "Sync my skills"
- "Update the skills list"
- "Refresh the skills markdown"
- "List all my skills"
- "Generate the skills index"
- "Rebuild the skills file"
- "Update the skills md"
- "Sync skills to markdown"
- "Show me all skills in a file"
- "Export skills list"

---

## Behavior When Triggered

### Step 1 — Sync Skills to claude-skills-md

1. Scan the `Skills` folder for all `.skills` files
2. Read each file and extract relevant metadata (name, description, etc.)
3. Generate or overwrite a `.md` listing file in `claude-skills-md`

### Step 2 — Update the Link Development Projects Folder

After Step 1 is complete, check and update the following files inside:
`C:\Users\khaled.elsherbiny\Documents\Claude\Projects\Link Development`

- **CLAUDE.md** — Update with any new or changed skills that are relevant to Link Development workflows
- **memory.md** — Refresh any skill references or context stored in memory
- **skills-navigation** SKILL.md — Update the navigation map to reflect the current skills list accurately

### Step 3 — Confirm

Confirm to the user that the full sync is complete, and provide links to all updated files.

---

## File Paths Reference

| Location | Path |
|---|---|
| Skills source folder | `skills/` (mounted) |
| Skills markdown output | `claude-skills-md/` (mounted) |
| Skills navigation | `claude-skills-md/system/skills-navigation/SKILL.md` |
| Link Development Project | `C:\Users\khaled.elsherbiny\Documents\Claude\Projects\Link Development` |
