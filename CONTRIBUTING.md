# Contributing to timetobuild

The best pitch feedback comes from hearing how different investors would react to the same deck. Every firm evaluates differently — different priorities, different red flags, different things that get them excited. This tool is most valuable when it represents many perspectives honestly.

We welcome contributions from investors, firms, founders, and anyone who can improve the quality of feedback.

## For Firms and GPs

If your firm has a way of evaluating pitch decks, we'd love to include it. When a founder runs `/timetobuild`, your perspective will appear alongside every other firm's — founders see where firms agree and where they diverge. It's a way to help founders understand what *you* actually look for, at scale.

You can contribute your firm's perspective from public sources, or if you prefer, write it yourself to capture the nuance that blog posts don't. See the templates below to get started.

## What You Can Contribute

### Add a New Firm

1. Create a directory: `perspectives/firms/your-firm/`
2. Copy `_template/overview.md` and `_template/seed.md` into your directory
3. Fill in the templates with the firm's evaluation criteria
4. Source your content from **public information only**: the firm's website, blog posts, partner talks, podcasts, published frameworks
5. Cite your sources in the files

If the firm has distinct funds (like a16z has apps/infra/crypto):
```
firms/your-firm/
├── overview.md          # Shared firm philosophy
├── fund-a/
│   ├── seed.md
│   └── series-a.md
└── fund-b/
    └── seed.md
```

If the firm doesn't have distinct funds:
```
firms/your-firm/
├── overview.md
├── seed.md
└── series-a.md
```

### Add a New Stage to an Existing Firm

1. Create the stage file in the appropriate firm (or firm/fund) directory
2. Name it after the stage: `pre-seed.md`, `seed.md`, `series-a.md`, `series-b.md`, `growth.md`
3. Use the `_template/seed.md` as a starting point and adapt for the stage

### Add a GP Profile (v2)

1. Create a file in `perspectives/gps/`
2. Copy `_template.md` and fill in the GP's evaluation framework
3. GP profiles are most valuable when contributed by the GP themselves
4. Include the `firm`, `default-fund`, and `default-stage` metadata

### Improve Existing Perspectives

- Fix inaccuracies or update outdated information
- Add more specific evaluation criteria with sources
- Improve the "In the deck, look for" guidance
- Add examples of good/bad patterns

## Guidelines

- **Public sources only**: All content must be sourced from publicly available information (blog posts, talks, interviews, published frameworks). Do not include confidential or proprietary evaluation criteria.
- **Cite your sources**: Include links to the original source material so others can verify and update.
- **Be opinionated**: The value of this project is in specific, actionable feedback. Generic advice is not helpful.
- **Be respectful**: Represent firms and GPs accurately. Don't put words in anyone's mouth.
- **Test your changes**: Install the skill locally and test with a sample deck to make sure the perspective produces good reviews.

## Testing Locally

```bash
# Option 1: Symlink into your skills directory
ln -s /path/to/timetobuild ~/.claude/skills/timetobuild

# Option 2: Use --add-dir for a single session
claude --add-dir /path/to/timetobuild

# Then test with a sample deck
/timetobuild path/to/deck.pdf --firm your-firm --stage seed
```

## Pull Request Process

1. Fork the repo
2. Create a branch: `add-firm-name` or `improve-a16z-seed`
3. Make your changes
4. Open a PR with a brief description of what you're adding/changing and your sources
