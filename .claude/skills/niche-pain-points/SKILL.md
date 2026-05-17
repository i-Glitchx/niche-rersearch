---
name: niche-pain-points
description: Produces a structured pain-point research report for the niches in this project's config/niches.md by clustering, scoring, and synthesizing real complaints from raw text the user has pre-collected under config/raw-inputs/<niche-slug>/. Writes the result to outputs/pain-points-YYYY-MM-DD.md (or outputs/pain-points-<slug>-YYYY-MM-DD.md for a single niche). Use this skill whenever the user asks for pain-point research, niche research, weekly pain-point reports, recent complaints from a specific audience, app ideas grounded in real user gripes, or anything that involves clustering complaints into themes — even when they don't say "pain points" explicitly. Also use when the user references the research routine in this project's CLAUDE.md, or types the skill name.
---

# Niche pain-point research

Cluster, score, and synthesize a pain-point report from raw text the user
has collected in `config/raw-inputs/<niche-slug>/`. **The skill never
fetches the web itself** — that gather step happens out-of-band in the
user's browser. The skill's job is to turn pre-collected raw complaints
into a structured report with strict citation rigor.

**Why this design.** Raw inputs in `config/raw-inputs/<slug>/` are the
source of truth for clustering. They can be collected two ways:

1. **Automated via the Playwright MCP** — preferred for Reddit and any
   other site Playwright can reach. The skill drives a real browser,
   pulls verbatim text with permalinks and timestamps, and writes the
   results into `raw-inputs/` in the format described below.
2. **Manual paste fallback** — the user collects in their browser and
   pastes into `raw-inputs/` directly. Use this for sources Playwright
   can't reach (login-walled forums, anti-bot-protected aggregators) or
   when the user prefers to curate by hand.

Either way, the clustering and synthesis phase reads from `raw-inputs/`
and never invents content. WebSearch snippets and aggregator summaries
are never acceptable substitutes for verbatim text — see "What not to do".

## Reddit collection via Playwright

When `config/sources.md` lists Reddit subreddits for a niche, the skill
should populate `config/raw-inputs/<slug>/` automatically via the
Playwright MCP before clustering — unless the user passed
`--skip-collection` in the prompt, in which case use whatever files
already exist.

### Query strategy

Prefer **search queries with operational keywords** over "top of month"
listings. Top listings surface what the community upvoted — often
humor, equipment rants, or shop talk — not the operational pain points
this skill clusters.

Build search queries by combining:
- **Workflow keywords** appropriate to the niche. Examples for trades:
  software, scheduling, billing, invoicing, dispatch, payroll, quote,
  estimate, payment, CRM. Adapt per niche.
- **Tool names from `config/sources.md`** for that niche (e.g.
  ServiceTitan, Jobber, Housecall Pro, FieldEdge for trades).

Apply the skill's date-window filter (default 30 days; honour user
overrides). Aim for threads where people describe specific operational
frustrations, not equipment complaints, jokes, or skill-sharing.

If a keyword search returns fewer than 3 substantive threads, broaden
the keywords before falling back to top-of-month listings. Note any
fallback in the Coverage section so the user knows which niches had
thin search results.

### What to capture per thread

For each thread the skill fetches, capture:
- Thread title, score, post date (UTC), permalink
- Post body verbatim (or note "image/link post" if no selftext)
- Top 5 top-level comments verbatim, each with permalink, author, score,
  and timestamp

### Where to write

Write one file per source per run:

`config/raw-inputs/<niche-slug>/<YYYY-MM-DD>-r-<subreddit>.md`

Example: `config/raw-inputs/trades-hvac-plumbing-electrical/2026-05-14-r-hvac.md`

Use the format described in `config/raw-inputs/README.md` — verbatim
quotes, specific URLs, post dates. Each comment with its own permalink
becomes its own citable unit.

### Failure handling

If Playwright fails on a source (anti-bot wall, timeout, page structure
change), capture what was collected, then in the report's Coverage
section note: `<slug>: r/<sub> fetch failed — [reason]`. Don't fabricate;
don't fall back to WebSearch summaries.

For sources `sources.md` flags as `(manual or other MCP)` — forums,
G2, Trustpilot, App Store reviews — skip the Playwright step and rely
on whatever the user has pre-collected.

## Read first, every run

1. `CLAUDE.md` — output format and "what not to do" rules. These bind.
2. `config/niches.md` — the only legal list of niches. Each niche's
   `Audience` and `Out of scope` fields filter what counts as a relevant
   complaint.
3. For each niche, check `config/raw-inputs/<niche-slug>/`. If Reddit
   sources are listed in `config/sources.md` for the niche and the
   prompt didn't include `--skip-collection`, run the Reddit collection
   step (see "Reddit collection via Playwright") to populate the
   directory before clustering. A niche whose directory is still empty
   after collection is **skipped**, not snippet-derived.
4. `outputs/themes-ledger.md`, for theme-ID assignment and the
   `NEW THIS WEEK` flag. If the file is missing, this is the first
   run and the ledger starts empty.

`config/sources.md` is **not** read by the skill in this design — it is
the user's checklist while they gather raw inputs in their browser.

## Scope and filename

- **Default (no niche named in the prompt):** every niche in
  `niches.md`, in the order listed. Output:
  `outputs/pain-points-YYYY-MM-DD.md`.
- **Single-niche (user names a slug or name in the prompt):** only that
  niche. Output: `outputs/pain-points-<slug>-YYYY-MM-DD.md`.

`YYYY-MM-DD` is the run date in ISO format.

## Time window

Default: **last 30 days** from the run date. The window applies to the
**post date inside each citable unit** (when the complaint was
originally written), not the file's collection date. Honour any user
override in the prompt and state the exact window in the report header.

## Citable units

A **citable unit** is the triple **(verbatim quote, specific URL, post
date)**. Units missing any of those three are skipped, counted, and
shown in the report's "Skipped units" line for that niche. Never guess
a missing URL or date; never paraphrase a quote.

The skill is tolerant about file structure inside
`config/raw-inputs/<slug>/` — it extracts triples wherever they appear.
See `config/raw-inputs/README.md` for the recommended format.

## Coverage section (top of every report)

Before any per-niche analysis, the report opens with a **Coverage**
section. This is the first thing the reader sees, by design — it
answers "which niches did I forget to collect for?" at a glance.

Build it by listing every niche in `niches.md` (not just in-scope ones
for single-niche runs — show the full picture):

- **Niches with raw inputs (used this run):** slug, file count, total
  citable units extracted, most recent collection date.
  Example: `trades-hvac-plumbing-electrical — 4 files, 31 units, most recent 2026-05-13`
- **Niches skipped (no raw inputs this run):** slug + one-line note.
  These are **skipped, not snippet-derived**. They appear in the report
  body only as a header followed by a one-line skipped notice — no
  themes, no inferred content, no "AI could imagine that...".
  Example: `private-practice-therapists — directory missing`
  Example: `independent-insurance-agents — directory exists but 0 citable units`

For a single-niche run, still show all niches in Coverage but mark the
ones outside this run's scope as `not in scope this run` rather than
skipped, so the user can distinguish "I forgot to collect" from
"I deliberately scoped to one".

## Research workflow per niche

For each in-scope niche that has raw inputs:

1. **Re-read the niche definition.** `Audience` and `Out of scope`
   filter what counts. A quote from the wrong audience or in excluded
   territory doesn't count — even if it's a great line.

2. **Extract citable units** from every file in
   `config/raw-inputs/<slug>/`. For each unit verify:
   - verbatim quote present (treat what's in the file as authoritative;
     do not "clean up" or paraphrase)
   - specific URL present (forum post, comment permalink, review
     detail page — not the forum root)
   - post date present and inside the time window
   - audience matches the niche definition
   Count skips by reason (missing URL / missing date / outside window /
   wrong audience / out of scope) for the report.

3. **Cluster into themes.** Group units into **3–7 themes** per niche.
   A theme needs **at least 2 independent source quotes** — units from
   different URLs. A one-off rant is not a theme. Prefer fewer
   well-supported themes to many thin ones; 3 strong themes beats 7
   weak ones.

4. **Score each theme:**
   - **Intensity 1–5.** From the language of the quotes. 1 = mild
     gripe; 5 = "I'm switching tools / leaving the business over this".
   - **Frequency low / med / high.** How often this complaint recurs
     across units in the window.

5. **App concept.** One concrete product idea per theme, grounded in
   the cited quotes. Concrete means: *who it's for*, *what it does in
   one sentence*, and *which quote(s) motivate it*. Vague ideas don't
   count — if the concept doesn't trace to specific quotes in the same
   theme, drop the theme or replace the concept.

If a niche has raw inputs but no cluster reaches the 2-quote bar,
produce zero themes for that niche and say so under its section. Don't
stretch single quotes into themes.

## Themes ledger (source of truth for theme identity across runs)

`outputs/themes-ledger.md` is an append-only log of every theme ever
surfaced across all runs. It is the **authoritative source for theme
identity over time** — it's how this run knows whether a pain it just
surfaced is a returning theme or a genuinely new one.

Read it before clustering, write to it after. See the file's own
header for schema and ID-assignment rules; the workflow below is what
the skill does at runtime.

### Read phase (before clustering)

1. Open `outputs/themes-ledger.md`. If the file doesn't exist, treat
   the ledger as empty — this is the first run.
2. Build an in-memory map: for each niche in scope this run, list
   every prior `(theme_id, theme_title, last seen run_date)` for that
   niche. This is your "prior themes" reference for ID assignment and
   the NEW THIS WEEK flag.

### Write phase (after clustering, before writing the report)

For each theme the skill produced this run:

1. **Assign `theme_id`.**
   - Check the prior-themes map for the same niche. If the current
     theme covers the same underlying pain as a prior theme_id, reuse
     that ID. "Same underlying pain" means same root cause, not same
     wording — be conservative; a rephrasing is a match, a different
     root cause is not.
   - If no match, mint the next free ID for the niche:
     `<niche-slug>-NN` where NN is one greater than the highest
     existing number for that niche (zero-padded to 2 digits, or more
     once the niche crosses 99).
2. **Set `is_new`.** True if `theme_id` was minted fresh in step 1,
   false if it was reused.
3. **Append one row** to `outputs/themes-ledger.md` with the schema
   columns (run_date, niche_slug, theme_id, theme_title, intensity,
   frequency, quote_count, is_new, report_file). Newest rows at the
   bottom. Never edit or delete prior rows.

## NEW THIS WEEK flag in the report

A theme is flagged `[NEW THIS WEEK]` in the report if and only if its
ledger row for this run has `is_new = true`. The flag is the
report-facing surface of the ledger's `is_new` decision — they must
agree. If no prior ledger entries exist for the niche, omit the flag
on every theme (don't write `[NEW THIS WEEK]` against everything on
the first run for a niche).

### Why this design

The ledger replaces the previous "diff against the most recent prior
report" approach. Comparing reports by reading their markdown is
fuzzy and depends on title wording; the ledger gives every theme a
stable ID, so "is this theme new?" becomes a lookup, not an
interpretation. It also enables cross-run analysis (recurring,
accelerating, fading themes) that report-by-report comparison can't
support.

## Report template

Use this structure exactly. Replace bracketed placeholders.

```
# Niche pain points — [YYYY-MM-DD]

**Window:** [last 30 days | user-specified window]
**Niches in this report:** [comma-separated slugs, or "all"]
**Prior report compared:** [filename, or "none — first run"]

## Coverage

**Used this run:**
- `[slug]` — [N] files, [M] citable units, most recent [YYYY-MM-DD]
- `[slug]` — [N] files, [M] citable units, most recent [YYYY-MM-DD]

**Skipped (no raw inputs):**
- `[slug]` — directory missing
- `[slug]` — directory exists but 0 citable units

**Not in scope this run** (single-niche runs only):
- `[slug]`
- `[slug]`

---

## [slug] — [Niche name from niches.md]

### Files used
- `config/raw-inputs/[slug]/[filename]` — [N] units, dates [YYYY-MM-DD] to [YYYY-MM-DD]

### Skipped units
- [N] missing URL
- [N] missing date
- [N] outside time window
- [N] wrong audience / out of scope

### Theme 1: [short title] [NEW THIS WEEK]
- **Pain:** [1–2 sentences in the user's own framing]
- **Quotes:**
  - "[verbatim quote]" — [URL] ([YYYY-MM-DD])
  - "[verbatim quote]" — [URL] ([YYYY-MM-DD])
- **Intensity:** [1–5]
- **Frequency:** [low | med | high]
- **App concept:** [who + what + which quote motivates it]

### Theme 2: …
[3–7 themes total]

---

## [skipped-slug] — [Niche name]

_Skipped: no raw inputs collected for this niche this run. To include
it, drop files under `config/raw-inputs/[skipped-slug]/`._

---

## [next-with-inputs-slug] — [Niche name]
[…]
```

Drop the `[NEW THIS WEEK]` bracket when it doesn't apply — don't write
`[NEW THIS WEEK: no]` or similar.

## What not to do

- **Don't fabricate quotes, URLs, dates, or attributions.** Every quote
  in the report must trace back verbatim to a file in
  `config/raw-inputs/`. If you can't trace a quote to a file, drop it.
- **Don't snippet-derive.** If a niche's `raw-inputs/` directory is
  missing or empty, the niche is **skipped** — never substitute
  WebSearch summaries, aggregator articles, or your own knowledge for
  raw-collected text. This rule is the whole point of the design.
- **Don't pad with generic SaaS / productivity / "AI could help" advice.**
  The report exists to surface specific cited complaints.
- **Don't suggest app concepts that aren't grounded in cited quotes
  from the same theme.** Every concept traces to specific text.
- **Don't research niches that aren't in `niches.md`.** Don't invent
  slugs.
- **Don't write `NEW THIS WEEK` against every theme on the first run.**
- **Don't merge raw-input files across niches** — a file under
  `raw-inputs/<slug-A>/` only contributes to niche A.

## A note on depth

The grade is whether the user can read a theme and immediately see
(a) the specific pain, (b) real people expressing it, recently, (c) a
product idea that fits the quotes. If a theme reads like something the
user could have written without any of the cited quotes, it has failed —
even if it's technically formatted correctly.
