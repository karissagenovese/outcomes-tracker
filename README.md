# Intended Outcomes Tracker — Quick Site Template

A self-updating evidence site for Shopify employees to track their Intended Outcomes and OS skills continuously — not just at review time. Works for any discipline: TPM, SWE, Product, Design, Marketing, and more.

## What this does

- Tracks evidence against your Intended Outcomes (IOs) and OS skills continuously — not just at review time
- Scans Vault, Slack, Fellow transcripts, GitHub PRs, Gmail, and Google Sheets/Drive — paste the included prompt into any LLM
- Filters out baseline expectations — only additive, concrete contributions
- Caps at ~8 entries per skill to demonstrate consistency, not volume
- Includes a context blurb for newer managers who don't have your historical background
- Saves state to `quick.db` (cross-device) with localStorage fallback

## Auto-scan

Open `SCAN-PROMPT.md`, fill in your name, IOs, OS skills, and what to scan, then paste it into any LLM — MANA, Claude, Copilot, whatever you use. It will scan your sources and return evidence entries you can paste into your site or keep in a doc.

For your OS skills: go to [os.shopify.io](https://os.shopify.io) → find your discipline → copy the skills for your level → paste them into the prompt. LLMs with Vault access (MANA, Claude, Pi) can pull them automatically.

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

Open `SCAN-PROMPT.md`, fill in your info, paste into any LLM. Done.

If you use Pi, an `outcomes-scan` skill is included — copy it to your skills directory and run `/outcomes-scan` for a fully automated scan.

### 5. Connect GitHub (optional)

Click "Connect GitHub" in the PR section. You'll need a Personal Access Token with `read:org` + `repo` scope. Create one at [github.com/settings/tokens](https://github.com/settings/tokens). Saved to `quick.db` — set once, works everywhere.

## Skills frameworks

The site auto-loads the right OS skills based on your discipline:
- **TPM** — direct from `vault.shopify.io/disciplines/351-Technical-Program-Management`
- **SWE** — direct from `vault.shopify.io/disciplines/145-Software-Engineering`
- **Product** — direct from `vault.shopify.io/disciplines/Product-Management`

Skills at and above your level are shown — you can track stretch signals before you're formally there.

## Privacy — controlling who can see your site

Quick sites are already Shopifolk-only (Shopify SSO required — not accessible to the public internet). But any Shopify employee who has your URL can open it.

To restrict access to specific people, set `allowlist` in CONFIG:

```js
allowlist: ['manager@shopify.com', 'skip@shopify.com'],
```

- **You are always allowed** — no need to add yourself.
- Anyone not on the list sees a lock screen with no content.
- Set `allowlist: []` (the default) to allow any Shopifolk with the URL.

To add someone later (e.g. before a calibration conversation):
1. Edit `allowlist` in `index.html`
2. Run `quick deploy . your-site-name --force`

Common patterns:
- **Just you and your manager**: `['manager@shopify.com']`
- **Manager + skip**: `['manager@shopify.com', 'skip@shopify.com']`
- **Open to your whole team**: `[]`

## Sharing

Share this GitHub link with colleagues — they clone it and set up their own. Your personal site URL stays private.

`https://github.com/karissagenovese/outcomes-tracker`

## Questions

Open an issue in the repo.
