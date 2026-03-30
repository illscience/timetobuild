# timetobuild

A [Claude Code](https://claude.ai/code) skill that reviews investor pitch decks from the perspective of top VC firms.

Get specific, opinionated feedback on your deck from the perspective of a16z, Sequoia, and other top firms — calibrated by stage, fund, and sector. See how the same deck lands differently depending on who's reading it.

## Install

### Claude Code (CLI, VS Code, JetBrains)

```bash
# Option 1: One-line install
npx skills add illscience/timetobuild

# Option 2: Install as a plugin
claude plugin install illscience/timetobuild

# Option 3: Clone into your skills directory
git clone https://github.com/illscience/timetobuild.git ~/.claude/skills/timetobuild
```

### Claude Desktop / Cowork

1. Download the [latest release zip](https://github.com/illscience/timetobuild/archive/refs/tags/v0.1.0.zip)
2. Open Claude Desktop and switch to the **Cowork** tab
3. Click **Customize** in the left sidebar
4. Click **Upload skill** and drag in the zip file

### OpenAI Codex CLI

```bash
# Clone into your Codex skills directory
git clone https://github.com/illscience/timetobuild.git ~/.codex/skills/timetobuild
```

### Other Tools (Cursor, Gemini CLI, Copilot, etc.)

The SKILL.md format is supported by 16+ AI tools. Clone the repo into your tool's skills directory — see your tool's docs for the path.

## Quick Start

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

### Currently Available

| Firm | Fund | Stages | Sources |
|------|------|--------|---------|
| a16z | apps | seed, series-a | Partner evaluation framework |
| Sequoia | — | seed, series-a | [Writing a Business Plan](https://sequoiacap.com/article/writing-a-business-plan/) |

### Want Your Firm Here?

Every firm evaluates decks differently — that's what makes this tool valuable. The more perspectives, the better the feedback founders get.

We'd love contributions from any firm willing to share how they think. See [CONTRIBUTING.md](CONTRIBUTING.md) to add your perspective.

On the roadmap:
- More firms (YC, Benchmark, Founders Fund, Lightspeed, Greylock, and others)
- More stages (pre-seed, Series B, growth)
- More funds/sectors (infra, crypto, bio)
- GP-specific profiles — individual partner evaluation lenses

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

Founders get the most value when they can see how their deck lands differently across firms. Every new perspective makes the tool more useful for everyone.

See [CONTRIBUTING.md](CONTRIBUTING.md) for details. The highest-impact contributions:
- **Add your firm's perspective** — founders will see your criteria alongside every other firm's, every time they run a review
- **Add a GP profile** — share how you personally evaluate decks, in your own voice
- **Improve existing perspectives** — make feedback more specific, more accurate, more actionable

## License

MIT
