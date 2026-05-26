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
| trades-hvac-plumbing-electrical-04 | electriciantalk | unknown | https://www.electriciantalk.com/threads/complex-bidding.306977/ | 2026-05-24 | I'm back for more! Looking for some advice on how to structure bids. I've been... | no | | | |
| trades-hvac-plumbing-electrical-04 | hvac-talk | unknown | https://www.hvac-talk.com/threads/anybody-else-hate-doing-quotes-in-the-driveway.2290460/post-26998480 | 2026-05-11 | I never did a quote on location, estimates yes, actual quote/proposal NEVER... | no | | | |
| trades-hvac-plumbing-electrical-04 | hvac-talk | unknown | https://www.hvac-talk.com/threads/anybody-else-hate-doing-quotes-in-the-driveway.2290460/post-26997649 | 2026-05-06 | We use a software that catalogs every piecebof our inventory. Everything is... | no | | | |
| trades-hvac-plumbing-electrical-04 | hvac-talk | unknown | https://www.hvac-talk.com/threads/anybody-else-hate-doing-quotes-in-the-driveway.2290460/post-26998241 | 2026-05-09 | I used to do quotes in the customers kitchen.  After being in business for so... | no | | | |
| trades-hvac-plumbing-electrical-04 | electriciantalk | unknown | https://www.electriciantalk.com/threads/how-do-you-handle-gc-expectations.306973/post-5828322 | 2026-05-23 | I'm a newer electrical contractor and have been working on my own since Decem... | no | | | |
| trades-hvac-plumbing-electrical-04 | reddit | unknown | https://reddit.com/r/electricians/comments/1t4ge03/how_would_you_price_this/ | 2026-05-05 | Recently completed a job and just curious how you guys would bid something... | no | | | |
| trades-hvac-plumbing-electrical-04 | reddit | unknown | https://reddit.com/r/electricians/comments/1t4ge03/how_would_you_price_this/ok28q8x/ | 2026-05-05 | T&M, unless they needed a quote, then quote as you normally would. Retail... | no | | | |
| trades-hvac-plumbing-electrical-06 | hvac-talk | unknown | https://www.hvac-talk.com/threads/anybody-else-hate-doing-quotes-in-the-driveway.2290460/post-26998241 | 2026-05-09 | I used to do quotes in the customers kitchen. […] And after 30 some-odd-years... | no | | | |
| trades-hvac-plumbing-electrical-06 | hvac-talk | unknown | https://www.hvac-talk.com/threads/anybody-else-hate-doing-quotes-in-the-driveway.2290460/post-26997649 | 2026-05-06 | I can email it to them or text it to them. Or I can walk back in go over the... | no | | | |
| trades-hvac-plumbing-electrical-06 | electriciantalk | unknown | https://www.electriciantalk.com/threads/how-do-you-handle-gc-expectations.306973/post-5828355 | 2026-05-24 | An unfortunately common 'expectation' is that since you're new in business... | no | | | |
| trades-hvac-plumbing-electrical-06 | reddit | unknown | https://reddit.com/r/HVAC/comments/1tkko5e/what_do_you_say_to_do_you_know_who_i_am_i_own_10/ | 2026-05-22 | Buddy you are a multi millionaire squabbling over $40. My company lost money... | no | | | |
| trades-hvac-plumbing-electrical-06 | reddit | unknown | https://reddit.com/r/HVAC/comments/1tkko5e/what_do_you_say_to_do_you_know_who_i_am_i_own_10/on9zg4x/ | 2026-05-22 | I'm on the wholesale side and we call them 'homeowners' and we hate them. Even... | no | | | |
| trades-hvac-plumbing-electrical-08 | reddit | unknown | https://reddit.com/r/sweatystartup/comments/1tf2mqz/quit_my_six_figure_corporate_sales_job_to_buy_a/ | 2026-05-16 | Nobody really talks about the stress side of it. Wondering if cash flow is... | no | | | |
| trades-hvac-plumbing-electrical-08 | reddit | unknown | https://reddit.com/r/sweatystartup/comments/1tf2mqz/quit_my_six_figure_corporate_sales_job_to_buy_a/om6ofo6/ | 2026-05-16 | 2 mil in revenue is still a relatively small business in some ways, likely too... | no | | | |
| trades-hvac-plumbing-electrical-08 | electriciantalk | unknown | https://www.electriciantalk.com/threads/how-do-you-handle-gc-expectations.306973/post-5828382 | 2026-05-24 | Guys I hate to say it but my wife is starting to ask me to call around for GC... | no | | | |
| trades-hvac-plumbing-electrical-08 | hvac-talk | unknown | https://www.hvac-talk.com/threads/business-owners-%E2%80%93-how-hard-was-your-first-hvac-year-really.2290602/post-27000888 | 2026-05-24 | Always worked directly for mfgs except for 4-5 yrs as bus owner.  First yr just... | no | | | |
| trades-hvac-plumbing-electrical-08 | reddit | unknown | https://reddit.com/r/sweatystartup/comments/1tf2mqz/quit_my_six_figure_corporate_sales_job_to_buy_a/om7834z/ | 2026-05-16 | I quit my software development job about 6 years to start a restoration... | no | | | |
