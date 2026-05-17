# Sources

Canonical pain-point sources per niche. One section per niche, keyed by the
same `<slug>` used in `niches.md`. Keep niches and sources in the same order
in both files.

## How this file is used

This file is a **checklist for collection**, not a runtime input. The skill
does not read it directly — it reads `config/raw-inputs/<slug>/`. Use this
file when you sit down to collect, to remind yourself where to look and
how each source is reached.

## Source entry format

Each source line:

    - [access-tag] URL — what to look for there
      last_collected: YYYY-MM-DD (or "never")

### Access tags

- `[reddit-pw]` — Reddit subreddit, fetched via Playwright MCP (default
  path for any Reddit source until the Reddit API upgrade lands)
- `[reddit-api]` — Reddit source eligible for the authenticated Reddit
  API path once that's set up (currently all Reddit sources will move
  here)
- `[manual]` — copy-paste from browser; the page works fine, you just
  have to do it by hand (e.g. some forums, niche Q&A)
- `[blocked]` — anti-bot wall, login required, or otherwise not
  fetchable; collect manually or skip. Note the reason after the URL.
- `[aggregator]` — secondhand source (review-aggregator blog,
  comparison site). Useful for context and source discovery, **not
  citable** — never produces a citable unit on its own.

### Tag conventions

- Tag every source. An untagged source is a bug; fix it before the next
  collection run.
- `last_collected` updates after each collection session for that
  source. If a source goes 60+ days without collection and the niche
  still has it listed, decide whether to demote (move to a "stale"
  block at the bottom of the niche) or actively recollect.
- A source that's been `[blocked]` for 30+ days without finding a
  workaround should be moved to the niche's "stale" block — it's
  cluttering the active list.

### Source categories to consider

- **Subreddits** — direct complaints, rant threads, weekly question stickies
- **Forums / Discord / Slack** — community gripes not on Reddit
- **Review sites** — 1–3 star reviews on G2, Capterra, Trustpilot, App Store
- **Q&A sites** — Stack Exchange, Quora, niche-specific Q&A
- **Social** — Twitter/X searches, TikTok hashtags, YouTube comment sections
- **Blogs / newsletters** — practitioners writing about what frustrates them

Skip categories that don't apply rather than padding.

---

## 1. privacy-compliance-smb

### Subreddits
- [reddit-pw] https://reddit.com/r/privacy — general privacy gripes; filter for SMB / business compliance angle
  last_collected: never
- [reddit-pw] https://reddit.com/r/gdpr — GDPR-specific compliance pain; some SMB content # verify activity
  last_collected: never
- [reddit-pw] https://reddit.com/r/sysadmin — SMB IT/compliance overlap; search "CCPA", "GDPR", "privacy law", "DSAR"
  last_collected: never
- [reddit-pw] https://reddit.com/r/smallbusiness — owner-side compliance complaints; search same keywords
  last_collected: never
- [reddit-pw] https://reddit.com/r/Compliance — broader compliance community; lower SMB density but worth scanning # verify activity
  last_collected: never

### Forums
- [manual] https://iapp.org/connect/communities/ — IAPP member forums; behind login but high-signal # verify access
  last_collected: never

### Review sites
- [blocked] https://www.g2.com/categories/data-privacy-management — low-star reviews of OneTrust, TrustArc, Osano (G2 anti-bot)
  last_collected: never
- [blocked] https://www.capterra.com/data-privacy-management-software/ — same category on Capterra (anti-bot)
  last_collected: never
- [manual] https://www.trustpilot.com/ — search OneTrust, Osano, Termly, Iubenda
  last_collected: never

### Blogs / newsletters
- [manual] https://iapp.org/news/ — IAPP Daily Dashboard; practitioner complaints in comments
  last_collected: never

### Out-of-scope reminder
Filter out enterprise platform complaints (OneTrust enterprise tier) and
HIPAA-specific workflows — those belong to other niches per `niches.md`.

---

## 2. trades-hvac-plumbing-electrical

### Subreddits
- [reddit-pw] https://reddit.com/r/HVAC — owner-operator and tech complaints; check "Business Tuesday" weekly thread
  last_collected: 2026-05-14
- [reddit-pw] https://reddit.com/r/Plumbing — small-shop owner gripes (pricing, scheduling, customers)
  last_collected: never
- [reddit-pw] https://reddit.com/r/electricians — residential service contractor complaints
  last_collected: never
- [reddit-pw] https://reddit.com/r/smallbusiness — cross-trade owner-operator pain; search "HVAC" / "plumbing" / "electrical"
  last_collected: never
- [reddit-pw] https://reddit.com/r/sweatystartup — small-business owner mindset; search trade-specific keywords
  last_collected: 2026-05-14

### Forums
- [blocked] https://hvac-talk.com/vbb/forumdisplay.php?7-Business-Marketing-and-Sales — Business/Marketing/Sales section (tollbit anti-bot per 2026-05-14 run)
  last_collected: never
- [manual] https://www.plumbingzone.com/ — PlumbingZone business forum # verify section URL
  last_collected: never
- [manual] https://www.electriciantalk.com/ — Electrician Talk business sections # verify section URL
  last_collected: never

### Review sites
- [blocked] https://www.g2.com/products/housecall-pro/reviews — Housecall Pro low-star (G2 403)
  last_collected: never
- [blocked] https://www.g2.com/products/jobber/reviews — Jobber low-star (G2 403)
  last_collected: never
- [blocked] https://www.capterra.com/p/166400/Housecall-Pro/reviews/ — Capterra Housecall Pro # verify product ID
  last_collected: never
- [blocked] https://www.trustpilot.com/review/housecallpro.com — Trustpilot Housecall Pro (403 per 2026-05-14 run)
  last_collected: never
- [blocked] https://www.trustpilot.com/review/getjobber.com — Trustpilot Jobber (403 per 2026-05-14 run)
  last_collected: never

### Aggregators (context only — not citable)
- [aggregator] https://fieldcamp.ai/reviews/servicetitan/ — aggregates ServiceTitan complaints
  last_collected: never
- [aggregator] https://fieldcamp.ai/blog/best-hvac-apps/ — links to other commentary on small-HVAC software
  last_collected: never

---

## 3. private-practice-therapists

### Subreddits
- [reddit-pw] https://reddit.com/r/therapists — primary practitioner subreddit; search "SimplePractice", "TherapyNotes", "Headway", "Alma", "intake", "insurance"
  last_collected: never
- [reddit-pw] https://reddit.com/r/psychotherapy — clinical practice gripes; lower volume but high signal # verify activity
  last_collected: never
- [reddit-pw] https://reddit.com/r/MentalHealthProviders — practice-management focus # verify activity
  last_collected: never
- [reddit-pw] https://reddit.com/r/socialwork — overlap niche; LCSW private practice complaints
  last_collected: never

### Forums
- [manual] https://community.simplepractice.com/ — SimplePractice user community; gripes about the platform itself # verify access
  last_collected: never

### Review sites
- [blocked] https://www.g2.com/products/simplepractice/reviews — SimplePractice low-star
  last_collected: never
- [blocked] https://www.g2.com/products/therapynotes/reviews — TherapyNotes low-star
  last_collected: never
- [blocked] https://www.capterra.com/p/151481/SimplePractice/reviews/ — # verify product ID
  last_collected: never
- [blocked] https://www.trustpilot.com/review/simplepractice.com
  last_collected: never

### Blogs / newsletters
- [manual] https://www.zynnyme.com/blog — therapist-business consultancy; comment sections sometimes useful # verify still active
  last_collected: never

### Out-of-scope reminder
Skip large clinical organizations and consumer-facing mental health apps
(Talkspace/BetterHelp complaints from users, not providers).

---

## 4. criminal-defense-discovery

### Subreddits
- [reddit-pw] https://reddit.com/r/Lawyertalk — practitioner gripes across practice areas; search "discovery", "body cam", "jail call"
  last_collected: never
- [reddit-pw] https://reddit.com/r/LawFirm — firm operations focus; lower criminal-defense density
  last_collected: never
- [reddit-pw] https://reddit.com/r/law — broader legal community; filter for criminal-defense-specific threads
  last_collected: never
- [reddit-pw] https://reddit.com/r/publicdefenders — adjacent audience; PD pain often mirrors solo-defender pain # check niche out-of-scope rule
  last_collected: never

### Forums / Listservs
- [manual] https://www.nacdl.org/ — National Assoc. of Criminal Defense Lawyers; member forums and discussion # verify access
  last_collected: never
- [manual] State criminal defense bar listservs — case-by-case, not URL-addressable; surface via member network
  last_collected: never

### Review sites
- [blocked] https://www.g2.com/products/clio/reviews — Clio low-star (general case management, filter for criminal context)
  last_collected: never
- [blocked] https://www.g2.com/products/filevine/reviews — Filevine low-star
  last_collected: never
- [manual] https://www.capterra.com/legal-software/ — broader legal-software category; filter reviews mentioning discovery/video
  last_collected: never

### Blogs / newsletters
- [manual] https://abovethelaw.com/ — search "discovery", "body cam", "criminal defense technology"
  last_collected: never
- [manual] https://www.law360.com/ — practitioner-facing legal news # verify paywall behavior
  last_collected: never

### Out-of-scope reminder
Skip civil litigation discovery (different volume profile, different tools)
and general case-management Clio/Filevine complaints unless they specifically
touch criminal-defense media workflows.

---

## 5. independent-insurance-agents

### Subreddits
- [reddit-pw] https://reddit.com/r/InsuranceAgent — primary practitioner sub; search "AMS", "CRM", "carrier portal", "commission", "AgencyBloc", "EZLynx"
  last_collected: never
- [reddit-pw] https://reddit.com/r/insurance — broader; filter for agent-side (not consumer) threads
  last_collected: never
- [reddit-pw] https://reddit.com/r/smallbusiness — search "insurance agency"
  last_collected: never

### Forums / Discord
- [manual] https://www.insurance-forums.com/ — practitioner forum # verify activity
  last_collected: never
- [manual] Independent agent Facebook groups (NABIP, PIA local chapters) — out of band; surface via member access
  last_collected: never

### Review sites
- [blocked] https://www.g2.com/products/agencybloc/reviews — AgencyBloc low-star
  last_collected: never
- [blocked] https://www.g2.com/products/ezlynx/reviews — EZLynx low-star # verify product slug
  last_collected: never
- [blocked] https://www.capterra.com/insurance-agency-software/ — broader category
  last_collected: never
- [blocked] https://www.trustpilot.com/review/agencybloc.com
  last_collected: never

### Blogs / newsletters
- [manual] https://www.insurancejournal.com/ — practitioner-facing; comment sections + columns about agency operations
  last_collected: never
- [manual] https://www.iamagazine.com/ — Independent Agent magazine
  last_collected: never

### Out-of-scope reminder
Skip captive agents (Allstate/State Farm employees), enterprise agency
management complaints (Applied Epic / Vertafore enterprise tier), and
consumer-facing insurance shopping complaints.