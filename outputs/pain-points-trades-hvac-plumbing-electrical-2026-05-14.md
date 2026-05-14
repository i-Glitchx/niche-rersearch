# Niche pain points — 2026-05-14

**Window:** last 30 days (2026-04-14 to 2026-05-14)
**Niches in this report:** trades-hvac-plumbing-electrical
**Prior report compared:** none — first run

---

## trades-hvac-plumbing-electrical — Skilled trades operators (HVAC, plumbing, electrical contractors)

### Discovered sources this run

Bootstrap mode: `config/sources.md` had no real sources for this niche.
Source discovery was attempted via WebSearch and verification via WebFetch.
**Most canonical primary sources for this niche were not accessible via
WebFetch in this environment.** Status of each attempt:

- `https://reddit.com/r/HVAC` — inaccessible: WebFetch blocks the reddit.com host
- `https://reddit.com/r/Plumbing` — inaccessible: WebFetch blocks the reddit.com host
- `https://reddit.com/r/electricians` — inaccessible: WebFetch blocks the reddit.com host
- `https://old.reddit.com/r/HVAC/top/?t=month` — inaccessible: WebFetch blocks the old.reddit.com host
- `https://www.reddit.com/r/HVAC/top.json?t=month` — inaccessible: WebFetch blocks the www.reddit.com host
- `https://hvac-talk.com/vbb/forumdisplay.php?7-Business-Marketing-and-Sales` — inaccessible: 307 redirect to a tollbit anti-bot proxy
- `https://www.trustpilot.com/review/housecallpro.com` — inaccessible: HTTP 403 Forbidden
- `https://www.g2.com/products/housecall-pro/reviews` — inaccessible: HTTP 403 Forbidden
- `https://www.g2.com/products/jobber/reviews` — inaccessible: HTTP 403 Forbidden
- `https://www.capterra.com/p/166400/Housecall-Pro/reviews/` — inaccessible: HTTP 404 (product ID likely wrong; correct ID not discoverable without browsing)
- `https://www.softwareadvice.com/construction/housecall-profile/reviews/` — accessible, but the page returned only 5-star testimonials; no 1–3 star reviews visible from the fetched content
- `https://fieldcamp.ai/reviews/servicetitan/` — accessible: returned 6 quotes about ServiceTitan, but all are secondhand citations (labelled "Capterra Review", "G2 Review", "BBB Complaint", "YouTube Review") with no specific source URLs and dates spanning Dec 2024 – Jul 2025 — entirely outside the 30-day window

WebSearch result summaries did contain quote-like fragments (e.g. *"they want $30K to get running and $130 per user per month"*, attributed generically to "Reddit"), but without a verifiable post URL or post date these do not satisfy the skill's citation bar (verbatim quote + specific URL + date in window).

### Themes

**No themes met the citation bar this run.**

The skill requires every theme to be supported by **at least 2 independent
source quotes, each with verbatim text, a specific post/review URL, and a
post date inside the 30-day window**. In this run no primary source could
be directly accessed, and the secondhand content that was retrievable does
not carry the URLs and dates needed to clear that bar. Per the skill's
"don't fabricate" rule, producing themes from this material would be worse
than producing nothing.

This is a finding about the **environment**, not the **niche**. The trades
niche is genuinely rich with primary-source complaints — they are simply
not reachable via the current WebFetch tool. See the next section.

### Skill revision needed

This run exposed a structural assumption baked into the skill: WebFetch can
reach reddit.com, the major review aggregators (G2, Trustpilot, Capterra),
and specialized trade forums (HVAC-Talk). In this Claude Code environment,
none of those work — reddit.com is host-blocked, the review sites return
403, and the trade forums sit behind an anti-bot proxy.

Three plausible fixes, roughly in order of preference:

1. **Out-of-band gather step.** The user manually copies raw complaints
   (Reddit threads, low-star reviews, forum posts) into
   `config/raw-inputs/<niche>/YYYY-MM-DD-<source>.md` before running the
   skill. The skill becomes a cluster / score / app-concept tool over
   pre-collected text. Keeps the citation rigor; shifts the scraping
   problem to a human or browser.
2. **Authenticated fetch path.** Wire up a Reddit API key, a browser-
   automation MCP server, or a paid forum-scrape service. Heaviest setup,
   highest fidelity.
3. **Snippet-derived citation tier.** Loosen the citation rule to accept
   quotes pulled from WebSearch result summaries, but flag every such
   theme as `snippet-derived` so downstream app ideas know the
   provenance is weaker. Cheapest; lowest rigor.

---

*This report intentionally contains no themes. See "Skill revision needed"
above and `config/sources.md` (under "Proposed sources — pending review"
for niche 2) for the canonical sources to wire up next.*
