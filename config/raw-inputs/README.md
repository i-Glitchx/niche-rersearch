# Raw inputs

The `niche-pain-points` skill reads complaint text from this directory —
**not** from the live web. You collect raw text from the sources listed
in `config/sources.md` (in your browser, by copy-paste) and drop it
here. The skill clusters, scores, and writes the report from what it
finds here.

## Path convention

`config/raw-inputs/<niche-slug>/<collected-date>-<source-slug>.md`

- `<niche-slug>` — matches a slug in `config/niches.md`
- `<collected-date>` — ISO date you did the collection (`YYYY-MM-DD`)
- `<source-slug>` — short kebab-case label for where it came from
  (e.g. `r-hvac`, `g2-jobber`, `hvac-talk-business`)

Example:
`config/raw-inputs/trades-hvac-plumbing-electrical/2026-05-14-r-hvac.md`

A niche with no files in its subdirectory is **skipped** in the next
run's report — listed in the Coverage section, no themes generated.
The skill never falls back to WebSearch snippets to fill the gap.

## Recommended file structure

The skill is tolerant of layout — it extracts **citable units**, defined
as the triple **(verbatim quote, specific URL, post date)**. Units
missing any of the three are skipped and the skip is counted in the
report. Any layout that produces clean triples is fine. A practical
template:

    # Source: r/HVAC top of month
    # Collected: 2026-05-14

    ---

    ## URL: https://reddit.com/r/HVAC/comments/abc123/title/
    Date: 2026-05-08

    > Verbatim quote pasted from the post. Multi-line is fine.
    > Keep it verbatim — do not paraphrase.

    > A second verbatim quote from the same thread, possibly a reply.

    ---

    ## URL: https://www.g2.com/products/jobber/reviews/some-review-id
    Date: 2026-04-22
    Rating: 2/5

    > Verbatim review text from the cons section.

## Rules

- **Verbatim quotes only.** Don't summarise, don't paraphrase, don't
  "clean up". If a quote is too long, trim with `[…]` rather than
  rewording.
- **Every quote needs a specific URL** it can be traced to — a forum
  permalink, Reddit comment link, review detail URL. Not just the
  forum root.
- **Post dates are the original post date** (when the complaint was
  written), not the collection date. The skill's time-window filter
  uses the post date.
- One file per source per collection session is typical; mixing
  sources in one file is fine but harder to audit later.
- If a quote lacks a URL or date, **don't fabricate one** — leave it
  in the file as-is, and the skill will skip it with an honest count.
