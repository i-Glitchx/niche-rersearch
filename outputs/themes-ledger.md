# Themes ledger

Append-only log of every theme surfaced across all pain-point runs.
The `niche-pain-points` skill writes to this file at the end of each
run, before producing the dated report. One row per theme per run.

## How to read this

A `theme_id` is stable across runs — if the same underlying pain shows
up in week 1 and week 3, it gets the same `theme_id` both times. The
skill matches against prior rows when assigning IDs; a genuinely new
pain gets a fresh ID.

Use this file to spot:
- **Recurring themes** — same `theme_id` appearing across 3+ runs
- **Accelerating themes** — intensity or frequency trending up
- **Fading themes** — last seen >60 days ago despite continued collection
- **Cross-niche themes** — same `theme_id` appearing under multiple niches

## Schema

| Field | Type | Notes |
|---|---|---|
| `run_date` | ISO date | Date of the run that surfaced this theme |
| `niche_slug` | string | Matches `config/niches.md` |
| `theme_id` | string | `<niche-slug>-NN` — stable across runs |
| `theme_title` | string | Short title from the report |
| `intensity` | int 1–5 | As scored in the run |
| `frequency` | enum | low / med / high |
| `quote_count` | int | Citable units supporting the theme this run |
| `is_new` | bool | True if no prior run for this niche had this theme_id |
| `report_file` | string | Path to the full report for this run |

## Theme ID assignment rules

1. On the first run for a niche, assign `<slug>-01`, `<slug>-02`, ...
   in the order themes appear in the report.
2. On subsequent runs, for each theme in the current report, check the
   ledger for prior rows in the same niche. If the underlying pain
   matches a prior `theme_id`, reuse it. Otherwise mint the next free
   number (e.g. if the niche has 01–05, the new one is 06).
3. "Matches a prior theme_id" means the same underlying pain — not the
   same wording. Be conservative: rephrasing isn't a new theme,
   genuinely different root cause is.
4. Theme IDs are never reused, never renumbered, never deleted —
   append-only. A theme that hasn't appeared in months still keeps its
   ID for when it returns.

## Entries

<!-- The skill appends new rows below this line, newest at the bottom. -->
<!-- Format: pipe-delimited table rows matching the schema above. -->

| run_date | niche_slug | theme_id | theme_title | intensity | frequency | quote_count | is_new | report_file |
|---|---|---|---|---|---|---|---|---|