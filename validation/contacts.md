# Contacts log — validation outreach

Append-only log of every cited user across all pain-point runs, linked
to the `theme_id` they support. The purpose is product-validation
outreach: when a theme looks promising, pull the rows for that
`theme_id` and reach out to the people who already articulated the
pain in public.

## Provenance rules — read before you touch this file

- **Append-only.** Like `outputs/themes-ledger.md`. Never rewrite or
  delete prior rows. If a fact in a row is wrong, add a correction
  note in `response_notes` rather than editing the original cell —
  the file is a historical record of what was cited when.
- **Reddit usernames are extracted from permalink URLs only —
  never invented or inferred.** Reddit comment permalinks
  (`reddit.com/r/SUBREDDIT/comments/THREADID/title/COMMENTID/`) do
  **not** include the author's username, so unless the username is
  visible verbatim in the raw-input file, write `unknown`. `unknown`
  is a valid value; never guess. Resolve the real username manually
  (open the permalink, copy the author) before outreach.
- **One row per `(theme_id, permalink)` pair.** If the same user
  appears under two themes, they get two rows — `theme_id` is the
  unit, not the person. Duplicates across runs (same theme keeps
  citing the same comment) are fine and expected; the file is
  append-only, so the latest run's row supersedes for outreach
  purposes but prior rows stay as history.

## Outreach rules — read before you contact anyone

- **Never cold-DM Reddit users.** The trades communities
  (r/Plumbing, r/HVAC, r/smallbusiness, r/sweatystartup and others)
  actively flag and ban this pattern — see the
  "SaaS-pitch fatigue across the trades subs" meta-finding in
  `outputs/pain-points-trades-hvac-plumbing-electrical-2026-05-17.md`.
  A cold DM is the fastest way to burn the niche.
- **Approved channels:**
  - **Public reply on the original thread.** Reply to the cited
    comment with substance (not a pitch). If it lands, the author
    may DM you back — that's the only inbound path that doesn't
    trigger the spam filter.
  - **Off-Reddit recruiting.** If you can identify the person
    elsewhere (trade-association directory, business website,
    LinkedIn for owner-operators who list it), contact them there
    with full disclosure that you found them via a public Reddit
    comment.
- When you make contact, fill in `contacted`, `contacted_via`,
  `contacted_date`, and `response_notes` in this file as a new
  append entry (not an edit to the cited row). The skill writes
  rows with `contacted = no` by default and **never** sets the
  human-only fields itself.

## Schema

| Field | Notes |
|---|---|
| `theme_id` | Matches `outputs/themes-ledger.md`. |
| `platform` | `reddit` for now. Extensible to `hvac-talk`, `plumbingzone`, etc. when off-Reddit sources are added. |
| `username` | Reddit handle extracted from the permalink path, or `unknown` if not derivable. Never invented. |
| `permalink` | The exact URL cited in the report. |
| `post_date` | The date from the citable unit (ISO). |
| `quote_preview` | First ~80 characters of the quote, verbatim from the raw-input file, with `...` appended if truncated. |
| `contacted` | `no` by default. Human-only field. |
| `contacted_via` | `public reply` / `off-reddit:<channel>` / blank. Human-only. |
| `contacted_date` | ISO date or blank. Human-only. |
| `response_notes` | Free-text: lookup hints, response summary, opt-out flags. Human-edited; the skill leaves it blank or uses it only to flag a username lookup is still needed. |

## Entries

<!-- Skill appends new rows below this line. Newest at the bottom. -->
<!-- Format: pipe-delimited table rows matching the schema above. -->

| theme_id | platform | username | permalink | post_date | quote_preview | contacted | contacted_via | contacted_date | response_notes |
| trades-hvac-plumbing-electrical-06 | reddit | unknown | https://reddit.com/r/Plumbing/comments/1te8poh/how_do_you_handle_customers_who_need_the_plumbing/ | 2026-05-15 | Any plumbers here ever run into situations where the customer genuinely needs... | no | | | OP username not in raw-input file — open thread and copy author before outreach |
| trades-hvac-plumbing-electrical-06 | reddit | unknown | https://reddit.com/r/Plumbing/comments/1te8poh/how_do_you_handle_customers_who_need_the_plumbing/om0pthp/ | 2026-05-15 | Yeah I guess I mean more for bigger jobs. Like emergency repairs, sewer lines... | no | | | Comment author not in permalink — look up manually before outreach |
| trades-hvac-plumbing-electrical-06 | reddit | unknown | https://reddit.com/r/smallbusiness/comments/1tfshrp/non_paying_customers/ | 2026-05-17 | I am an electrician and I have been running my own business for just over 3... | no | | | OP username not in raw-input file — open thread and copy author before outreach |
| trades-hvac-plumbing-electrical-06 | reddit | unknown | https://reddit.com/r/smallbusiness/comments/1tfshrp/non_paying_customers/ombnwvr/ | 2026-05-17 | I see 2 options 1) fire them and take the loss as payment for the lesson 2)... | no | | | Comment author not in permalink — look up manually before outreach |
| trades-hvac-plumbing-electrical-06 | reddit | unknown | https://reddit.com/r/sweatystartup/comments/1swfbeg/issues_with_customers_not_paying_solution/oifejc3/ | 2026-04-26 | On the blacklist app, defamation law makes public review sites a nightmare... | no | | | Comment author not in permalink — look up manually before outreach |
| trades-hvac-plumbing-electrical-06 | reddit | unknown | https://reddit.com/r/sweatystartup/comments/1swfbeg/issues_with_customers_not_paying_solution/oiihrr2/ | 2026-04-27 | The real cost of chasing a $150 invoice isn't the $150. It's the 2 hours of... | no | | | Comment author not in permalink — look up manually before outreach |
| trades-hvac-plumbing-electrical-06 | reddit | unknown | https://reddit.com/r/sweatystartup/comments/1swfbeg/issues_with_customers_not_paying_solution/oih5yua/ | 2026-04-27 | I own a stump grinding business, 3+ years in now. I've dealt with 2 no pays... | no | | | Comment author not in permalink — look up manually before outreach |
| trades-hvac-plumbing-electrical-06 | reddit | unknown | https://reddit.com/r/sweatystartup/comments/1swfbeg/issues_with_customers_not_paying_solution/oijnjhl/ | 2026-04-27 | the legal route works but it's slow and stressful. faster cure is upfront... | no | | | Comment author not in permalink — look up manually before outreach |
