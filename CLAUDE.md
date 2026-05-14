# Niche Pain Point Research

## Purpose
Scheduled and on-demand research to surface recent pain points and unmet
needs in defined niches, for the purpose of brainstorming app/product ideas.

## Project structure
- `config/niches.md` — current list of target niches
- `config/sources.md` — pain-point sources per niche (subreddits, forums, review sites)
- `.claude/skills/` — custom skills for this project
- `outputs/` — generated research reports, named `pain-points-YYYY-MM-DD.md`

## How to work in this project
- The niche and source lists in `config/` are the source of truth. Always
  read them before doing research. Never invent niches or sources.
- Research output goes to `outputs/` as a single markdown file per run,
  dated by the run date.
- Cite sources with real URLs. If a source can't be accessed, say so
  explicitly rather than fabricating quotes.
- Prefer depth over breadth: 3–7 themes per niche, each well-supported,
  beats 20 thin themes.

## Output format
Each report contains, per niche:
- 3–7 pain-point themes
- For each theme: pain description, 2–3 source quotes with links,
  intensity 1–5, frequency low/med/high, one concrete app concept
- "NEW THIS WEEK" flag for themes not present in the prior week's report

## What not to do
- Don't make up quotes or sources
- Don't pad reports with generic SaaS advice
- Don't suggest app ideas that aren't grounded in a cited complaint
- Don't research niches not listed in `config/niches.md`

## Conventions
- Markdown for all docs
- Dates in ISO format (YYYY-MM-DD)
- Commit messages: present tense, lowercase, e.g. "add fintech niche"