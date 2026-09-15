# Intended Outcomes Tracker — Quick Site Template

A self-updating performance evidence site for Shopify employees. Works for any discipline (TPM, SWE, Product, Design). Built by Karissa Genovese as a C8 craft-sharing artifact — as Julia Kranjac put it: "You're going to have one more thing for leading the evolution of your craft."

## What this does

- Tracks evidence against your Intended Outcomes (IOs) and OS skills continuously — not just at review time
- Auto-scans Vault, Slack, Fellow transcripts, GitHub PRs, Gmail, and Google Sheets/Drive weekly via the Pi `outcomes-scan` skill
- Filters out baseline expectations — only additive, concrete contributions
- Caps at ~8 entries per skill to demonstrate consistency, not volume
- Includes a context blurb for newer managers who don't have your historical background
- Saves state to `quick.db` (cross-device) with localStorage fallback

## Setup — 5 minutes

### 1. Clone the template

```bash
quick remix outcomes-tracker my-outcomes-2026
```

Or clone the repo and deploy:
```bash
git clone https://github.com/Shopify/outcomes-tracker
cd outcomes-tracker
quick deploy my-outcomes-2026
```

### 2. Edit `index.html` — the CONFIG block at the top

Open `index.html` and fill in the `CONFIG` object. It's clearly marked. The fields:

- `name`, `email` — your identity (auto-filled from `quick.id` if left null)
- `discipline` — `'TPM'` | `'SWE'` | `'Product'` — loads the right OS skills framework
- `level` / `targetLevel` — e.g. `'C7'` / `'C8'`
- `cycle` — e.g. `'May–Oct 2026'`
- `context` — a blurb for your manager: tenure, past roles, hiring history, domain expertise
- `intendedOutcomes` — your 2–4 IOs, as agreed with your manager
- `github.handle` — your GitHub username (for PR tracking)
- `sheets` — optional: Google Drive file IDs of sheets you contribute to
- `scan` — Vault project IDs, Slack channels, and keywords for the auto-scan

### 3. Deploy

```bash
quick deploy
```

Your site is live at `my-outcomes-2026.quick.shopify.io`.

### 4. Set up the auto-scan Pi skill

The `outcomes-scan` Pi skill scans all your sources weekly and produces evidence entries to paste in.

Copy the skill to your Pi skills directory:
```bash
cp -r outcomes-scan-skill ~/.claude/skills/outcomes-scan
# or for Pi:
cp -r outcomes-scan-skill ~/.pi/agent/skills/outcomes-scan
```

Run it weekly with `/outcomes-scan` in Pi. It will:
1. Read your CONFIG from the site (or a local `~/.outcomes-config.json`)
2. Scan Vault, Slack, Fellow, GitHub, Gmail, Google Sheets/Drive
3. Map findings to your IOs and OS skills
4. Filter out baseline expectations
5. Output formatted evidence entries + JSON you can import via the site's Import button

### 5. Connect GitHub (optional)

Click "Connect GitHub" in the PR section. You'll need a Personal Access Token with `read:org` + `repo` scope. Create one at [github.com/settings/tokens](https://github.com/settings/tokens). Saved to `quick.db` — set once, works everywhere.

## Skills frameworks

The site auto-loads the right OS skills based on your discipline:
- **TPM** — direct from `vault.shopify.io/disciplines/351-Technical-Program-Management`
- **SWE** — direct from `vault.shopify.io/disciplines/145-Software-Engineering`
- **Product** — direct from `vault.shopify.io/disciplines/Product-Management`

Skills beyond your level are shown but marked clearly so you can track C8 signals before you're there.

## Sharing

Keep your personal site link private — it has your performance data. Share *this template repo* with colleagues so they can build their own.

## Questions

Reach out to Karissa Genovese or open an issue in the repo.
