# outcomes-setup

Set up a personal Intended Outcomes tracking site from the outcomes-tracker template.
Trigger: "set up my outcomes tracker", "set up outcomes-tracker for me", or when someone
points you at github.com/karissagenovese/outcomes-tracker and asks you to run it.

## What this does

Clones the outcomes-tracker template, fills in the CONFIG block interactively,
and deploys a personal quick site — no manual file editing required.

## Prerequisites check

Before starting, verify:
- `git` is available: `git --version`
- `quick` CLI is available: `quick --version`

If either is missing, stop and tell the user what's needed.

## Step 1 — Gather information

Ask the user these questions. You can ask them all at once or one at a time.
If you have Vault access, pre-fill what you can (name, email, team) and confirm.

**Required:**
1. **Name** — full name (or pull from Vault profile)
2. **Email** — Shopify email (or pull from Vault)
3. **Discipline** — one of: `TPM` | `SWE` | `Product` | `Design` | `PMM` | `ProdOps` | `Marketing` | `Custom`
   - If manager track: use `Custom` and note they'll paste M-track skills from os.shopify.io
4. **Current level** — e.g. `C6`, `C7`, `M4`, `M5`
5. **Team / org name** — e.g. "Retail Hardware & Payments"
6. **Intended Outcomes** — their 2–4 IOs for this cycle. If they don't have them yet,
   use placeholder text and tell them to fill it in later.

**Optional (ask, but okay to skip):**
7. **Target level** — one level above current, only if actively working toward scope change
8. **Manager's email** — to add to the allowlist (restricts site to owner + manager only).
   Default: leave allowlist empty (any Shopifolk with the URL can view)
9. **GitHub handle** — for PR tracking. Can be added later.
10. **Site name** — the URL slug, e.g. `alex-outcomes-2026`. Default: `{firstname}-outcomes-{year}`

## Step 2 — Clone the template

```bash
cd ~
git clone https://github.com/karissagenovese/outcomes-tracker {site-name}
cd {site-name}
```

Use the site name they chose (or the default) as the directory name.

## Step 3 — Fill in the CONFIG block

Use Python to make targeted replacements in `index.html`.
Do NOT rewrite the whole file — make precise substitutions only.

```python
import re

with open('index.html', 'r') as f:
    html = f.read()

# Identity
html = html.replace("name: null,", f"name: '{name}',")
html = html.replace("email: null,", f"email: '{email}',")

# Discipline and level
html = html.replace("discipline: 'TPM',", f"discipline: '{discipline}',")
html = html.replace("level: 'C7',", f"level: '{level}',")

# Target level — keep or remove
if target_level:
    html = html.replace("targetLevel: 'C8',", f"targetLevel: '{target_level}',")
else:
    html = html.replace("  targetLevel: 'C8',        // optional — shows \"C7 → C8\" in header\n", "")

# Org
html = html.replace("org: 'Your Team',", f"org: '{org}',")

# Allowlist
if manager_email:
    html = html.replace("allowlist: [],", f"allowlist: ['{manager_email}'],")

# GitHub handle
if github_handle:
    html = html.replace("handle: null,", f"handle: '{github_handle}',")

with open('index.html', 'w') as f:
    f.write(html)
```

## Step 4 — Fill in Intended Outcomes

Each IO in the CONFIG block looks like:
```js
{
  title: 'Your first intended outcome',
  outcome: 'Describe the full scope...',
  success: 'Specific, measurable deliverables...',
  why: 'Why does this matter...',
  ...
}
```

Replace the placeholder IOs with the user's actual IOs using targeted Python substitution.
If they gave you their IOs as free text, parse them into the right fields:
- `title` — short name for the IO
- `outcome` — what they own / full scope
- `success` — what done looks like, metrics, deadlines
- `why` — why it matters at the Shopify strategy level

If they don't have IOs yet, leave the placeholders and tell them to fill in later.

## Step 5 — Deploy

```bash
quick deploy . {site-name} --force
```

Confirm the URL: `{site-name}.quick.shopify.io`

## Step 6 — Confirm and summarize

Tell the user:
- Their site URL: `{site-name}.quick.shopify.io`
- Who can view it (owner only, or owner + manager if allowlist was set)
- How to update it: edit `index.html`, run `quick deploy . {site-name} --force`
- How to run the evidence scan: open `SCAN-PROMPT.md`, fill in their info, paste into any LLM

## Step 7 — Offer to run the scan

Ask: "Want me to run the evidence scan now to pull your first batch of entries from Vault, Slack, and Fellow?"

If yes, run the `outcomes-scan` skill from this repo.

## Notes

- The `cycle` field auto-detects from the current date — don't set it manually
- Skills shown are filtered to their current level only (+ target level if set)
- The site saves state to `quick.db` — works across devices automatically
- To add someone to the allowlist later: edit `index.html`, add their email to `allowlist: []`, redeploy
- Manager track (M4, M5, etc.): set discipline to `Custom` and paste M-track skills from os.shopify.io into the placeholder fields
