# timetobuild

A [Claude Code](https://claude.ai/code) plugin that reviews investor pitch decks from the perspective of top VC firms.

Get specific, opinionated feedback on your deck as if you were pitching to a16z, Sequoia, and more — calibrated by stage, fund, and sector.

## Quick Start

```bash
# Clone into your Claude skills directory
git clone <repo-url> ~/.claude/skills/timetobuild
```

Then in any Claude Code session:
```
/timetobuild path/to/your-deck.pdf
```

## Usage

```
/timetobuild <file> [--firm NAME] [--fund NAME] [--stage STAGE]
```

### Examples

```bash
# Comparative review across all firms (default)
/timetobuild deck.pdf

# Deep review from a specific firm
/timetobuild deck.pdf --firm a16z
/timetobuild deck.pdf --firm sequoia

# Specify fund and stage explicitly
/timetobuild deck.pdf --firm a16z --fund apps --stage series-a
```

### Parameters

| Parameter | Default | Options |
|-----------|---------|---------|
| `--firm` | All firms (comparative) | `a16z`, `sequoia` (more coming) |
| `--fund` | `apps` | Firm-specific: `apps`, `infra`, `crypto` for a16z |
| `--stage` | Auto-detected from deck | `seed`, `series-a` (more coming) |

### Two Modes

**Comparative (default):** Run with no `--firm` flag. Gets you a side-by-side verdict from every available firm — where they agree, where they diverge, and the top changes that move the needle everywhere.

**Deep dive:** Pass `--firm` to get a single firm's full review — slide-by-slide feedback, founder signal read, suggested narrative arc, and a calibrated verdict.

## Available Perspectives

### v1 (Now)

| Firm | Fund | Stages | Source |
|------|------|--------|--------|
| a16z | apps | seed, series-a | Partner evaluation framework |
| Sequoia | — | seed, series-a | [Writing a Business Plan](https://sequoiacap.com/article/writing-a-business-plan/) |

### Planned (Contributions Welcome)

- a16z infra, crypto funds
- YC
- Benchmark
- Founders Fund
- Lightspeed, Greylock, and more
- Pre-seed, Series B, and growth stages
- GP-specific profiles

## What You Get

Every review includes:
- **Overall Assessment** — would this investor take a meeting?
- **Slide-by-Slide Feedback** — specific, actionable notes on each slide
- **Strengths & Concerns** — mapped to the firm's actual evaluation criteria
- **Missing Elements** — what the firm expects but your deck doesn't include
- **Founder Signal Read** (seed only) — what your deck reveals about you as a founder
- **Suggested Narrative Arc** — how to restructure for maximum impact
- **Verdict** — Pass / Soft Pass / Take the Meeting / Strong Interest

## Contributing

We welcome contributions from investors, firms, and founders. See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

The most impactful contributions:
- **Add your firm's perspective** — help founders understand what you actually look for
- **Add a GP profile** — share your personal evaluation framework
- **Improve existing perspectives** — make feedback more specific and actionable

## License

MIT
