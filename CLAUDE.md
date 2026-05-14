# Niche Pain Point Research

## Purpose
Scheduled and on-demand research to surface recent pain points and unmet
needs in defined niches, for the purpose of brainstorming app/product ideas.

## Project structure
- `config/niches.md` — current list of target niches
- `config/sources.md` — canonical pain-point sources per niche (manual-collection checklist; the skill does not read this directly)
- `config/raw-inputs/<niche-slug>/<collected-date>-<source-slug>.md` — raw complaint text the user has pre-collected from sources; the skill reads these
- `.claude/skills/` — custom skills for this project
- `outputs/` — generated research reports, named `pain-points-YYYY-MM-DD.md`

## How to work in this project
- `config/niches.md` is the source of truth for which niches to research.
  Never invent slugs.
- `config/sources.md` is your checklist while gathering raw inputs in your
  browser — it lists canonical sources per niche. The skill does not read
  it directly.
- The skill reads complaint text from `config/raw-inputs/<niche-slug>/`,
  not the live web. Drop files there (see `config/raw-inputs/README.md`
  for the format) before running. A niche with no files in its
  subdirectory is **skipped** in the next report — never filled in with
  snippet-derived or AI-inferred content.
- Research output goes to `outputs/` as a single markdown file per run,
  dated by the run date.
- Cite sources with real URLs. Every quote in the report must trace back
  verbatim to a file under `config/raw-inputs/`.
- Prefer depth over breadth: 3–7 themes per niche, each well-supported,
  beats 20 thin themes.

## Output format
- All-niches run (default): `outputs/pain-points-YYYY-MM-DD.md`
- Single-niche run: `outputs/pain-points-<niche-slug>-YYYY-MM-DD.md`

Every report opens with a **Coverage** section listing:
- Niches with raw inputs used this run (file count, citable units, most recent collection date)
- Niches skipped (no raw inputs — no themes generated for them)
- Niches not in scope (single-niche runs only)

Then, per niche covered:
- 3–7 pain-point themes
- For each theme: pain description, 2–3 source quotes with links,
  intensity 1–5, frequency low/med/high, one concrete app concept
- "NEW THIS WEEK" flag for themes not present in the prior week's report

## What not to do
- Don't make up quotes or sources
- Don't snippet-derive: if a niche has no raw inputs, it's **skipped**,
  never filled in from WebSearch summaries, aggregator articles, or
  general knowledge. An empty Coverage row is the correct output.
- Don't pad reports with generic SaaS advice
- Don't suggest app ideas that aren't grounded in a cited complaint
- Don't research niches not listed in `config/niches.md`

## Conventions
- Markdown for all docs
- Dates in ISO format (YYYY-MM-DD)
- Commit messages: present tense, lowercase, e.g. "add fintech niche"

## Future upgrades
- **Authenticated Reddit API** for trades/SMB niches, where Reddit is
  the highest-signal source and the out-of-band paste step is most
  painful. One-time token setup; would let the skill resume live-fetch
  for those niches and skip the manual collection step. Other source
  types (G2, Trustpilot, niche forums behind anti-bot) stay out-of-band
  for now — the cost/benefit of wiring them up is worse than just
  pasting from a browser.