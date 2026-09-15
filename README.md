# Intended Outcomes Tracker — Quick Site Template

A self-updating performance evidence site for Shopify employees. Works for any discipline (TPM, SWE, Product, Design). Built by Karissa Genovese as a C8 craft-sharing artifact — as Julia Kranjac put it: "You're going to have one more thing for leading the evolution of your craft."

## What this does

- Tracks evidence against your Intended Outcomes (IOs) and OS skills continuously — not just at review time
- Auto-scans Vault, Slack, Fellow transcripts, GitHub PRs, Gmail, and Google Sheets/Drive weekly via the Pi `outcomes-scan` skill
- Filters out baseline expectations — only additive, concrete contributions
- Caps at ~8 entries per skill to demonstrate consistency, not volume
- Includes a context blurb for newer managers who don't have your historical background
- Saves state to `quick.db` (cross-device) with localStorage fallback

## Auto-scan — works with any LLM

You don't need Pi. Open `SCAN-PROMPT.md`, fill in your name, IOs, OS skills, and what to scan, then paste the whole thing into **MANA, Claude, Pi, or any LLM you use**. It will scan your sources and return evidence entries you can paste into your site or keep in a doc.

For your OS skills: go to [os.shopify.io](https://os.shopify.io) → find your discipline → copy the skills for your level → paste them into the prompt. If you're using Pi or MANA with Vault access, the LLM can pull them automatically.

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

### 4. Run the scan weekly

**Option A — any LLM (MANA, Claude, Pi, Copilot):**
Open `SCAN-PROMPT.md`, fill in your info, paste into whatever LLM you use. Done.

**Option B — Pi users:**
The `outcomes-scan` skill in this repo is pre-configured for Pi. Copy it to your skills directory and run `/outcomes-scan`.

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
