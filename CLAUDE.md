# timetobuild

A Claude Code skill that reviews investor pitch decks from VC firm perspectives.

## What it does

- Reviews pitch deck PDFs from the perspective of top VC firms (a16z, Sequoia, more coming)
- **Default mode (no --firm):** Comparative review across all firms — quick verdicts table, where firms agree/diverge, top 5 changes
- **Deep dive (--firm a16z):** Single-firm review with slide-by-slide feedback, founder signal read, narrative arc suggestions, calibrated verdict
- **Auto-detects stage:** Pre-launch = seed, post-launch = Series A. Can be overridden with --stage.

## Invocation

```
/timetobuild <file>                                    # Comparative review (all firms)
/timetobuild <file> --firm a16z                        # Deep dive: a16z apps seed
/timetobuild <file> --firm sequoia --stage series-a    # Deep dive: Sequoia Series A
/timetobuild <file> --firm a16z --fund apps --stage seed  # Fully explicit
```

## Repo structure

```
SKILL.md                              # Main skill — orchestrates the review
base-review.md                        # Universal deck evaluation framework
output-format.md                      # Standardized review output template
perspectives/
  firms/
    a16z/
      overview.md                     # Shared a16z philosophy (founding essays, thesis)
      apps/
        seed.md                       # a16z apps seed — founder assessment framework
        series-a.md                   # a16z apps Series A — PMF, metrics, scaling
      infra/_template.md
      crypto/_template.md
    sequoia/
      overview.md                     # Sequoia philosophy (4 core questions, 10-point rubric)
      seed.md
      series-a.md
    _template/                        # Templates for adding new firms
  gps/
    _template.md                      # Template for GP-specific profiles (v2)
```

## Key design decisions

- **Firm → Fund → Stage hierarchy:** Stage criteria are nested inside each firm because a16z apps seed ≠ Sequoia seed. Firms with distinct funds (a16z) get fund subdirectories; firms without (Sequoia) put stages directly under the firm.
- **Stage detection:** Simple rule — pre-launch = seed, post-launch = Series A. Revenue from the founder's other companies doesn't count.
- **Comparative default:** The most valuable output is seeing how the same deck lands differently across firms. Single-firm deep dives are available via --firm.
- **Perspectives are markdown files:** Each perspective file contains evaluation criteria, priorities, and red/green flags. The skill loads and composes them at review time.

## Distribution

- GitHub: https://github.com/illscience/timetobuild (currently private)
- Claude Code: `npx skills add illscience/timetobuild` or `claude plugin install illscience/timetobuild`
- Claude Desktop/Cowork: Upload zip from GitHub releases
- OpenAI Codex CLI: Clone into `~/.codex/skills/timetobuild`
- Cross-platform: SKILL.md format works with 16+ AI tools

## a16z perspective sources

- [Why Software Is Eating the World](https://a16z.com/why-software-is-eating-the-world/) (2011)
- [It's Time to Build](https://a16z.com/its-time-to-build/) (2020)
- [Why Has Andreessen Horowitz Raised $2.7B in 3 Years?](https://a16z.com/why-has-andreessen-horowitz-raised-2-7b-in-3-years/) (2012)
- [Why Did We Raise $15B?](https://a16z.com/why-did-we-raise-15b/) (2025)
