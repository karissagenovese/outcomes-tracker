# Intended Outcomes Scan — Universal Prompt

**Works with any LLM: MANA, Claude, Pi, Copilot, or anything else.**

Copy everything below the line, paste it into your LLM of choice, fill in the `[ ]` fields, and send it. The LLM will scan your sources and return evidence entries you can paste into your outcomes quicksite (or just keep in a doc).

---

```
You are helping me track evidence of my contributions against my Intended Outcomes
and Shopify OS skills. Scan the sources I list below and return concrete, specific
evidence entries I can use for my performance review.

════════════════════════════════════════════
ABOUT ME
════════════════════════════════════════════
Name: [Your Name]
Discipline: [TPM / Software Engineering / Product Management / UX Design / Marketing / Data Science / etc.]
Level: [e.g. C7]
Target level: [e.g. C8, or leave blank]
Team / org: [e.g. Retail Hardware & Payments]
Review cycle: [e.g. May–Oct 2026]

════════════════════════════════════════════
MY INTENDED OUTCOMES
════════════════════════════════════════════
These are the 2–4 outcomes I agreed with my manager at the start of this cycle.

IO 1: [Paste your first intended outcome here]
IO 2: [Paste your second intended outcome here]
IO 3: [Paste your third intended outcome here — often craft/AI growth]

════════════════════════════════════════════
MY OS SKILLS
════════════════════════════════════════════
Go to os.shopify.io → find your discipline → copy the skills for your level.
Paste them here so the LLM knows exactly what to map evidence to.

If your LLM has access to Vault, ask it to run:
  vault_get_discipline("[Your discipline]") 
and it will pull the skills automatically.

[PASTE YOUR OS SKILLS HERE — or delete this block and ask the LLM to pull them from Vault]

Example format:
  Craft: Be obsessed with making cross-team mission shipping smooth and easy
  Craft: Be self-reliant and do it yourself first  
  Craft: Use AI to multiply your craft
  Responsibilities: Identify dependencies and gaps, drive decisions and unblock issues
  Responsibilities: Drive cross-functional stakeholder alignment
  Ambition: Inspire your product area / domain

════════════════════════════════════════════
WHAT TO SCAN — [last N days, default: 7]
════════════════════════════════════════════
Scan ALL of the following sources. Do not skip any.

Slack:
  - My handle: [e.g. karissa.genovese]
  - Channels: [list the channel names or IDs, e.g. #retail-hardware-slt-connect, #shared-shopify-verifone]
  - Search: everything I posted in the last [7] days + any direct feedback sent to me

Vault projects:
  - [Paste Vault project URLs or IDs, e.g. vault.shopify.io/gsd/projects/48932]
  - Look for: status changes, milestones, decisions, blockers resolved, PRs, reviews

Fellow / meeting transcripts:
  - Scan my meetings from the last [7] days
  - Look for: decisions I drove, pushbacks I gave, risks I surfaced, quotes about my impact

GitHub:
  - My handle: [e.g. karissagenovese]
  - Org: Shopify
  - Look for: PRs authored, PRs reviewed, issues commented on

Gmail / email:
  - Scan sent mail from last [7] days
  - Look for: external partner comms, decisions communicated, feedback received

Google Drive / Sheets:
  - [Optional: paste Drive file IDs or names of sheets you contribute to]
  - Look for: files I edited, docs I authored, comments I left

Other keywords to search across all sources:
  - [e.g. your project name, product name, partner name]

════════════════════════════════════════════
RULES FOR WHAT TO INCLUDE
════════════════════════════════════════════
ONLY include entries that are additive — things beyond baseline expectations.

SKIP these (baseline — not worth capturing):
- "Ran a meeting" without specifying what was decided or driven
- "Provided an update" without noting what changed because of it  
- "Coordinated with team" — too vague
- Anything every person at this level does every day

KEEP these (concrete, specific, additive):
- A decision that wouldn't have happened without me
- A blocker I unblocked with specifics on how
- A risk I surfaced before anyone else named it
- A pushback I gave — and what the outcome was
- Cross-team alignment I created that didn't exist before
- Direct quotes from colleagues about my impact (include their name, role, date, source)
- A program or milestone that shipped — with my specific contribution named
- Something I built that others now use (tool, framework, artifact)
- A gap I identified and closed before it became a problem

Cap at 8–9 entries per skill. If I already have many examples of one skill, only add
something if it's materially stronger or more recent than what's already there.

Rate each entry:
- SOLID: clear, specific, concrete — you can point to an outcome that changed
- [Next level] signal: clear evidence toward my target level
- [Early foundation]: directionally right but needs more evidence

════════════════════════════════════════════
OUTPUT FORMAT
════════════════════════════════════════════
Return two things:

1. HUMAN-READABLE SUMMARY
Group by IO. For each entry show:
  [DATE] [RATING] [OS SKILL]
  One paragraph: what I did, what was specific about it, what changed because of it.

Also include a "Stakeholder quotes" section with any direct feedback captured,
and a "Skipped (baseline)" list so I know what was filtered out.

2. JSON FOR IMPORT
After the summary, output this JSON block so I can paste it into my outcomes quicksite:

[
  {
    "skill": "[exact OS skill id or short label]",
    "io": "io1",
    "date": "YYYY-MM-DD",
    "signal": "SOLID",
    "text": "Specific description of what happened and what changed...",
    "source": "slack / fellow / vault / github / gmail / drive",
    "sourceRef": "link or reference"
  }
]

If you find any risks or blockers worth surfacing to leadership, flag them separately
at the end under ⚠ RISKS SURFACED.

════════════════════════════════════════════
IMPORTANT NOTES
════════════════════════════════════════════
- Do not fabricate. If you can't find evidence for a skill, say so.
- Do not list something as my contribution if it was the team's — be precise about
  my specific role (what I drove, decided, unblocked, or built).
- If a source isn't accessible to you, tell me and I'll paste the content in.
- Prefer primary sources (transcripts, Slack messages, Vault decisions) over summaries.
- The most recent source wins if there's a conflict.
```
