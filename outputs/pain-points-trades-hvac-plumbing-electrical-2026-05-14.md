# Niche pain points — 2026-05-14

**Window:** last 90 days (2026-02-13 to 2026-05-14). Deviates from the skill default of 30 days; aligned to the scope the user collected at in this conversation. Re-run with default to narrow.
**Niches in this report:** trades-hvac-plumbing-electrical
**Prior report compared:** none — the file already at this path was a bootstrap-mode attempt from earlier today (this run's filename) and is ignored per spec; this is effectively the first real run with raw inputs.

## Coverage

**Used this run:**
- `trades-hvac-plumbing-electrical` — 2 files, 45 citable units, most recent 2026-05-14 (collection date); newest in-window post date 2026-05-12

**Skipped (no raw inputs):**
- _(none — see "Not in scope this run" below)_

**Not in scope this run** (single-niche invocation):
- `privacy-compliance-smb`
- `private-practice-therapists`
- `criminal-defense-discovery`
- `independent-insurance-agents`

---

## trades-hvac-plumbing-electrical — Skilled trades operators (HVAC, plumbing, electrical contractors)

### Files used
- `config/raw-inputs/trades-hvac-plumbing-electrical/2026-05-14-reddit-hvac.md` — 30 units, post dates 2026-02-25 to 2026-05-12
- `config/raw-inputs/trades-hvac-plumbing-electrical/2026-05-14-reddit-sweatystartup.md` — 15 units, post dates 2026-02-27 to 2026-04-03

### Skipped units
- 0 missing URL
- 0 missing date
- 0 outside time window (90-day window applied)
- 0 wrong audience / out of scope

### Theme 1: Private-equity rollups push replacement quotas and "find problems" culture
- **Pain:** Techs at PE-acquired shops report that meetings became sales-numbers and replacement-quota driven, and the shop owner pushes them to "find" problems rather than fix them. Independent owners and prospective hires explicitly position against this.
- **Quotes:**
  - "Every meeting felt more focused on sales numbers and replacement quotas than actually helping people. I got tired of feeling like I was supposed to 'find' problems instead of fixing them, so I decided to bet on myself and start my own company." — https://reddit.com/r/HVAC/comments/1taenx3/starting_a_company/ (2026-05-11)
  - "No private equity BS. No ServiceTitan. No flat rate book. No upsell quotas. Just good work and good pay." — https://reddit.com/r/HVAC/comments/1skvtuc/where_do_you_actually_find_good_techs_in_this/ (2026-04-14)
  - "Most good techs dont want to work for someone that just bought their shop up and has zero experience in the field." — https://reddit.com/r/HVAC/comments/1skvtuc/comment/og4221m/ (2026-04-14)
  - "Good luck if your resi only, your only way to make money is gonna be to scam idiots and rich people for a PE company or get licensed and work for yourself." — https://reddit.com/r/HVAC/comments/1t9q0ma/comment/ol49r36/ (2026-05-11)
- **Intensity:** 5 — quitting jobs, starting own companies, refusing to work for PE-owned shops
- **Frequency:** high — recurs across 3 separate threads in the window
- **App concept:** A trade-side hiring/employer-discovery board for techs who want to leave PE-owned shops. Independent owners post openings tagged with explicit "no upsell quotas / no flat-rate book / no AI sales coaching" attestations; techs filter by those tags. Motivated by the explicit hiring criteria in 1skvtuc ("No private equity BS. No ServiceTitan. No flat rate book. No upsell quotas") and the supply of disgruntled techs implied by 1taenx3 + og4221m.

### Theme 2: ServiceTitan "Field Pro" surveillance and AI sales coaching of techs
- **Pain:** Shops are rolling out call-recording and AI-coaching features on top of their FSM, aimed at the tech-customer conversation. Techs uniformly react with "run" / "quit" language, reading it as a signal the shop has gone sales-first. At least one operator built his own lightweight alternative.
- **Quotes:**
  - "My shop wants to implement the pro features like recording tech conversations with customers and AI coaching. Kind of sketches me out ayone have experience with these features?" — https://reddit.com/r/HVAC/comments/1s53gd8/service_titan_field_pro/ (2026-03-27)
  - "Lol 'coaching'. Sounds like your shop owner is pushing the sales route. Only a matter of time before that place turns to shit. I would be looking to leave immediately" — https://reddit.com/r/HVAC/comments/1s53gd8/comment/ocrmsim/ (2026-03-27)
  - "Custom field service app I built myself (basically my own lightweight ServiceTitan)" — https://reddit.com/r/HVAC/comments/1taenx3/starting_a_company/ (2026-05-11)
- **Intensity:** 5 — multiple techs in 1s53gd8 said "run" / "Nope. Run." / "I'd be out of there quick"
- **Frequency:** med — one strong thread plus corroborating self-build evidence from a separate thread
- **App concept:** A sub-$150/mo dispatch + quote + invoice app for 1–15 person trade shops that explicitly ships *without* call recording, conversation analysis, or AI sales coaching — and markets that surveillance-free posture as a hiring advantage to small-shop owners trying to retain techs. The "lightweight ServiceTitan" comment in 1taenx3 validates the build-vs-buy demand directly.

### Theme 3: Office overrides field schedule; tech absorbs the customer anger
- **Pain:** Office staff reshuffle commercial maintenance to chase new no-heat contracts. The technician who shows up months late at the displaced customer has no authority over scheduling but takes the blame face-to-face. The standard response across the thread is some variant of "I don't make the schedule."
- **Quotes:**
  - "we've been behind on heating pms for a lot of our commercial accounts because the office has no problem rescheduling a solid customer for someone we have no history with one unit down [...] I am getting cornered by people in charge at these places asking why we are checking their heat now and not month or two ago when they were first scheduled. Feels like they are trying to railroad me into getting them a discount or something when Im not a manager and have zero control of where I go between 8am-5pm." — https://reddit.com/r/HVAC/comments/1re19y1/forced_to_choose_sides_customer_or_office/ (2026-02-25)
  - "I don't make the schedule man" — https://reddit.com/r/HVAC/comments/1re19y1/comment/o79cjmk/ (2026-02-25)
  - "I apologize for the inconvenience, however I don't do scheduling, if there's an issue I'll have to direct you to the office." — https://reddit.com/r/HVAC/comments/1re19y1/comment/o79cq2k/ (2026-02-25)
  - "I'm sorry, I don't write the schedule." — https://reddit.com/r/HVAC/comments/1re19y1/comment/o79crsd/ (2026-02-25)
- **Intensity:** 3 — chronic friction, not a quit-trigger, but real and recurring
- **Frequency:** high — 4+ independent commenters confirm the same defensive script
- **App concept:** A customer-comms layer for small-shop FSMs that auto-notifies commercial PM customers when their visit is rescheduled, with a reason code (e.g., "displaced by no-heat emergency at another site, next available [date]"), so the conversation happens between office and customer *before* the tech arrives. Motivated directly by the 1re19y1 post ("getting cornered by people in charge at these places asking why we are checking their heat now") and the unanimous "not my problem" comment script.

### Theme 4: Hidden job-cost leakage between quote and final invoice
- **Pain:** Operators with steady revenue keep finding actual job margin far below quoted margin once warranty callbacks, drive time, refrigerant overages, and ad-hoc rentals are accounted for. The diagnosed pattern is consistent: 1–2 cost categories account for most of the leakage, and they're forgotten line items at quote time, not efficiency problems on the job site.
- **Quotes:**
  - "We're busy as hell, booking out two weeks most of the year, but when I sit down and actually look at job profitability after everything's done I keep getting surprised by how thin the margins are or how jobs I thought would be winners barely made any money. [...] somehow we barely cleared 8% after accounting for the warranty callback we had to do, the extra refrigerant we didn't price in, drive time that ate more hours than I budgeted, and the rental equipment we needed for a day that I just forgot to include in the estimate." — https://reddit.com/r/sweatystartup/comments/1rg0rml/profitable_jobs_on_paper_keep_turning_into/ (2026-02-27)
  - "Warranty callbacks aren't surprises, they're a cost of doing business. [...] Same idea for drive time. If your techs are logging 8 hours on site but you're only billing the 8, you're eating the windshield time." — https://reddit.com/r/sweatystartup/comments/1rg0rml/comment/o7o80v5/ (2026-02-27)
  - "Most shops find 1-2 categories that account for 80% of the leakage - once you see it in the data, you fix it at the template level instead of the judgment level." — https://reddit.com/r/sweatystartup/comments/1rg0rml/comment/o7pcygt/ (2026-02-27)
  - "it'qs easier to forget that a technician who drives 45 minutes each way is essentially gone for half a day, even if the job only takes two hours. [...] I was underpricing by a significant amount because I wasn't accounting for half of this shit." — https://reddit.com/r/sweatystartup/comments/1rg0rml/comment/o7opb8z/ (2026-02-27)
- **Intensity:** 4 — operators describe being surprised, underpriced, and working on a business advisor to diagnose it
- **Frequency:** med — anchored to one thread, but with 4+ independent commenters confirming the same pattern from their own shops
- **App concept:** A standalone post-job profitability dashboard for 1–15 person trade shops that ingests quote line-items plus actuals (labor hours, drive time, materials, warranty callbacks, equipment rentals — pulled from existing tools like QuickBooks/Jobber/Housecall Pro or CSV upload), computes quoted-vs-actual variance per cost category across the last 30–40 jobs, and surfaces the 1–2 categories driving 80% of margin leakage as concrete template-fix recommendations. Motivated directly by o7pcygt's framing of the fix ("fix it at the template level instead of the judgment level") and o7opb8z's windshield-time underpricing example.

### Theme 5: B2B commercial sales gatekeeping — front desk wall, wrong decision-maker
- **Pain:** Small trade-shop operators trying to expand from residential into commercial (office buildings, clinics) hit a brick wall at reception. The standard scripts ("we're not interested", "I'll leave it with the doctor") don't differentiate them; meanwhile the actual decision-maker for HVAC/landscaping at many buildings isn't at the building at all but at a separate property-management company.
- **Quotes:**
  - "I do B2B sales and I am hitting an absolute brick wall. The front desk receptionists and office managers are bulletproof. [...] every time, it's been 'we are not interested', 'I'll leave it with the doctor' and similar sentences." — https://reddit.com/r/sweatystartup/comments/1sbmess/for_the_guys_doing_commercial_cleaning_hvac_or/ (2026-04-03)
  - "Depending on the business, it might be a completely separate property manger that handles things like HVAC, landscaping, etc either in house or subcontract. [...] So it could be a toss up if directly calling the place is worth it." — https://reddit.com/r/sweatystartup/comments/1sbmess/comment/oe4nveq/ (2026-04-03)
  - "I own a plumbing company that specializes in service. We do 85-90% residential work and I would love to branch our team into more commercial work but have been hitting similar brick walls" — https://reddit.com/r/sweatystartup/comments/1sbmess/comment/oe4gwlw/ (2026-04-03)
  - "You're probably getting stuck because the front desk hears the same generic pitch all day. The easier route is a tighter target list plus a reason that specific clinic or building should take the meeting, otherwise every call sounds interchangeable." — https://reddit.com/r/sweatystartup/comments/1sbmess/comment/oe4wpcz/ (2026-04-03)
- **Intensity:** 3 — operational frustration, not a quit-trigger
- **Frequency:** med — anchored to one thread, but the residential-to-commercial transition appears across multiple operators (HVAC, plumbing, cleaning)
- **App concept:** A commercial-prospecting tool for small trade shops that maps, per service area, which buildings have outsourced facilities/property managers (vs. in-house) and lists the contact path through the property-management company — paired with a per-building "specific opening" prompt (visible building deficiency, recent permit, equipment age signals) so the walk-in or call leads with something specific instead of a generic pitch. Motivated directly by oe4nveq's property-manager structural insight and oe4wpcz's "tighter target list plus a reason that specific clinic or building should take the meeting."

---

## Notes for next run

- Themes 4 and 5 are anchored to single threads each (1rg0rml and 1sbmess). They cleared the ≥2-independent-URL-quotes bar because each thread's comments have unique permalinks, but corroborating threads on the same pain would harden the signal. Worth a targeted r/sweatystartup search for "job costing" / "margin" and "commercial sales" / "cold call" in the next collection pass.
- Theme 1 (PE rollups) is the highest-intensity finding in the window and has supply-side (techs leaving) *and* demand-side (independent owners hiring) evidence — the strongest theme to validate first.
- The r/sweatystartup Google-listing thread (1rjw2pc) contributed 3 valid units but they clustered to "pure marketing/SEO" pain, which the niche definition flags as out of scope for product concepts. Quotes remain in raw-inputs but didn't drive a theme.
