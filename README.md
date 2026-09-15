# Intended Outcomes Tracker — Quick Site Template

A self-updating evidence site for Shopify employees to track their Intended Outcomes and OS skills continuously — not just at review time. Works for any discipline: TPM, SWE, Product, Design, Marketing, and more.

## What this does

- Tracks evidence against your Intended Outcomes (IOs) and OS skills continuously — not just at review time
- Scans Vault, Slack, Fellow transcripts, GitHub PRs, Gmail, and Google Sheets/Drive — paste the included prompt into any LLM
- Filters out baseline expectations — only additive, concrete contributions
- Caps at ~8 entries per skill to demonstrate consistency, not volume
- Includes a context blurb for newer managers who don't have your historical background
- Saves state to `quick.db` (cross-device) with localStorage fallback

## What this doesn't do — be honest about this

**This tool lowers the cost of not forgetting. It doesn't write your review.**

- **It doesn't generate impact.** The scan finds work you did — PRs merged, decisions made, risks surfaced. If the impact of that work isn't documented somewhere (PR description, Slack post, Vault update), the scan can't infer it. Quantitative metrics (latency reduced by 20%, conversion up 15%) only surface if you wrote them down somewhere.

- **It doesn't write the narrative.** The tool collects evidence. You still have to connect it to outcomes, articulate what changed because of your work, and explain why it mattered. That's the individual's job. The manager's job is to understand the impact — the tool gives you both better raw material.

- **The scan is manual.** You run it every few weeks. If you set up the site and never run the scan, nothing accumulates. The value compounds with consistent use, not from a one-time setup.

- **LLM access determines scan quality.** If your LLM can search Slack, read Fellow transcripts, and query GitHub directly, you get a full scan automatically. If it can't reach those sources, you paste content in manually or skip those sources. Pi works end-to-end. MANA depends on what tools are enabled.

- **Private conversations are invisible.** Work done in Slack DMs, verbal feedback in 1:1s, or decisions made in unrecorded calls won't be captured unless someone wrote them down somewhere. High-trust, low-paper-trail work is systematically underrepresented.

- **Good IOs are a prerequisite.** The scan is only as good as how clearly your IOs are written. Vague IOs return vague evidence. If you and your manager haven't aligned on specific, measurable outcomes, fix that first.

**The honest use case:** run the scan every 2–4 weeks, review what it surfaces, add the entries that are genuinely additive, and write a sentence or two of context for each. By end of cycle you have a curated body of evidence instead of scrambling to remember six months of work.

## Auto-scan

Open `SCAN-PROMPT.md`, fill in your name, IOs, OS skills, and what to scan, then paste it into any LLM — MANA, Claude, Copilot, whatever you use. It will scan your sources and return evidence entries you can paste into your site or keep in a doc.

For your OS skills: go to [os.shopify.io](https://os.shopify.io) → find your discipline → copy the skills for your level → paste them into the prompt. LLMs with Vault access (MANA, Claude, Pi) can pull them automatically.

## Setup

### Option A — Let an LLM do it (easiest)

If you use Pi, Claude, or MANA with tool access, just say:

> “Set up the outcomes tracker for me: github.com/karissagenovese/outcomes-tracker”

Tell it your discipline, level, team, and IOs. It clones the repo, fills in your CONFIG, and deploys your site. Done.

The `.pi/skills/outcomes-setup/SKILL.md` in this repo has the full instructions for the LLM.

### Option B — Do it yourself (5 minutes)

#### 1. Clone the template

```bash
git clone https://github.com/karissagenovese/outcomes-tracker
cd outcomes-tracker
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
quick deploy . your-name-outcomes-2026
```

Your site is live at `your-name-outcomes-2026.quick.shopify.io`.

### 4. Run the scan weekly

Open `SCAN-PROMPT.md`, fill in your info, paste into any LLM. Done.

If you use Pi, an `outcomes-scan` skill is included — copy it to your skills directory and run `/outcomes-scan` for a fully automated scan.

### 5. Connect GitHub (optional)

Click "Connect GitHub" in the PR section. You'll need a Personal Access Token with `read:org` + `repo` scope. Create one at [github.com/settings/tokens](https://github.com/settings/tokens). Saved to `quick.db` — set once, works everywhere.

## Skills frameworks

Skills are baked in from [os.shopify.io](https://os.shopify.io) for these disciplines:
- **TPM** — Technical Program Management
- **SWE** — Software Engineering
- **Product** — Product Management
- **Design** — Product Design
- **Marketing** — Growth Marketing
- **Custom** — paste in your own skills from [os.shopify.io](https://os.shopify.io) if your discipline isn't listed

By default only your current level's skills are shown. Set `targetLevel` to one level above to also see those skills (dimmed) — useful if you're working toward a scope change.

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
