---
name: review-deck
description: Review an investor pitch deck from multiple VC perspectives. Use when asked to review, critique, or give feedback on a pitch deck or investor presentation.
argument-hint: <file> [--firm NAME] [--fund NAME] [--stage STAGE]
allowed-tools: Read, Bash, Grep, Glob
---

# Pitch Deck Review

You review investor pitch decks from VC firm perspectives.

## Step 1: Parse Arguments

Parse the arguments from `$ARGUMENTS`. Extract:
- **file**: The path to the deck file (PDF or PPTX) — the first positional argument
- **--firm**: A specific VC firm name (e.g. `a16z`, `sequoia`). **If not specified, run a comparative review across ALL available firms** (see Step 5a).
- **--fund**: Fund/sector within the firm, e.g. `apps`, `infra`, `crypto` (default: `apps`). Only applies when `--firm` is specified and the firm has fund subdirectories.
- **--stage**: Funding stage, e.g. `seed`, `series-a`. **If not specified, auto-detect from the deck** (see Step 3).

## Step 2: Read the Deck

Use the Read tool to read the pitch deck file **before** loading perspective files. For PDFs, read all pages. For large PDFs (>10 pages), read in chunks of 20 pages.

## Step 3: Detect Stage (if not explicitly provided)

If `--stage` was not specified, infer the stage from the deck content using a simple rule:

- **Seed** = the product is **pre-launch** (not yet live with real users/customers paying for it)
- **Series A** = the product is **post-launch** (live in market with real users or paying customers)

Look for evidence of launch status: revenue from the product being pitched, paying customers, live deployments, active users. Note: revenue or traction from the founder's *other* companies does not count — only the company being pitched matters.

State which stage you detected and why.

## Step 4: Discover and Load Perspective Files

First, discover all available firms by listing directories under `${CLAUDE_SKILL_DIR}/perspectives/firms/` (exclude `_template`).

Then load perspective files:

1. **Always load**: `${CLAUDE_SKILL_DIR}/base-review.md`
2. **Always load**: `${CLAUDE_SKILL_DIR}/output-format.md`

**If `--firm` is specified (single-firm deep review):**
3. Load `{firm}/overview.md`
4. Stage criteria — resolve in order:
   a. If `--fund` is specified: `{firm}/{fund}/{stage}.md`
   b. If that doesn't exist, or no fund: `{firm}/{stage}.md`
   c. If neither exists, use only firm overview + base review

**If `--firm` is NOT specified (comparative review across all firms):**
3. For each discovered firm, load:
   - `{firm}/overview.md`
   - Stage file: try `{firm}/{default-fund}/{stage}.md`, then `{firm}/{stage}.md`
   - For a16z, default fund is `apps`

Use the Read tool to load each file. Skip gracefully if a file doesn't exist.

## Step 5: Evaluate and Output

### Step 5a: Comparative Review (default — no `--firm` specified)

Evaluate the deck against ALL loaded firm perspectives, then output a **comparative summary**:

```
## Comparative Deck Review: [Company Name]

**Deck length:** [X slides]
**Detected stage:** [Stage] — [1-sentence rationale]

---

### Quick Verdicts

| Firm | Verdict | Key Reason |
|------|---------|------------|
| [firm] | [Pass / Soft Pass / Take the Meeting / Strong Interest] | [1-sentence reason] |
| ... | ... | ... |

---

### Where Firms Agree

Bullet points on feedback that is consistent across all firm perspectives. These are the highest-priority fixes — every investor would flag them.

---

### Where Firms Diverge

Bullet points on where firm perspectives lead to different evaluations. Explain WHY each firm sees it differently based on their specific criteria. This is the most valuable section — it shows how the same deck lands differently depending on who's reading it.

---

### Deck Strengths (Universal)

Bulleted list of what works across all perspectives.

---

### Top 5 Changes That Move the Needle Everywhere

Numbered, prioritized list. Each item should be specific and actionable — not generic advice. Reference which firms' criteria each change addresses.

---

> **Want a deeper review from a specific firm?** Run:
> `/timetobuild <file> --firm a16z` or `/timetobuild <file> --firm sequoia`
> Available firms: [list all discovered firms]
```

### Step 5b: Single-Firm Deep Review (when `--firm` is specified)

Evaluate the deck against the specific firm's perspective. Your review must be:

- **Specific**: Reference actual slide content, not generic advice
- **Opinionated**: Channel the firm's actual investment thesis and evaluation style
- **Constructive**: Every criticism should come with a specific suggestion
- **Honest**: If the deck wouldn't get a meeting at this firm, say so and explain why

For **seed-stage reviews**, weight founder signals heavily — what does the deck reveal about the founder's depth, conviction, and capability? Use the firm's founder assessment criteria.

For **Series A+ reviews**, weight metrics and proof of PMF — traction data, unit economics, and evidence of repeatable growth.

Format using the structure in `output-format.md`. Specify which perspective was used, including the detected stage and why.

End every single-firm review with:

```
> **Want to see how other firms would evaluate this deck?** Run:
> `/timetobuild <file>` (comparative review across all firms)
> Or try a different firm: `/timetobuild <file> --firm [other firm]`
> Available firms: [list all discovered firms]
```
