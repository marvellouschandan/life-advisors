---
name: trip-planner
description: Plans a trip and produces a structured destination guide for an
  India-based traveller — where to stay, how to get there and around, what to
  see and do, a food guide, and a day-by-day itinerary. Use when the user
  mentions travel, a trip, vacation, itinerary, a place name, or "where should
  I go". Verify live prices, timings, and visa rules at the source before booking.
---


# Trip Planner


## Read first
Load `profile/me.md` for home city, spending style, food preference,
dietary/accessibility needs, and travel preferences. The trip budget, dates,
and length are per-trip inputs — ask for them; do not assume them from the profile.


## Guardrails
- Prices, timings, visa rules, and schedules change. State them as approximate
  and tell the user to confirm at the source (operator / embassy / hotel)
  before paying.
- Never invent specific prices, distances, or visa requirements. If unsure,
  say so and point to where to check.
- Respect spending style and dietary/accessibility needs from the profile
  (e.g. list veg-friendly food first if the profile is vegetarian).
- Skip sections that don't apply (no beaches inland, no visa for domestic).


## Ask first (if missing)
Trip length (number of days), dates or month, home city / origin, who's going,
rough budget, and trip type (relax / explore / adventure). Ask before planning.


## Output structure (follow this shape — adapt sections to the place)
Produce one guide with NUMBERED sections and sub-sections as markdown headings
(`## 1. Overview`, `### 3.1 Getting there`, etc.) so the file is easy to
navigate. Follow this order; drop any section that doesn't apply, add local
ones that do.


1. Overview — one-line pitch, plus best areas/neighbourhoods to stay (with the
   vibe of each) and the layout of the place.
2. Best time to visit — seasons at a glance (peak / shoulder / off / monsoon)
   with typical weather per season, and notable festivals or events. Then judge
   the user's stated month/dates explicitly: say whether it's a good, okay, or
   poor time and why (weather, crowds, price). If dates aren't fixed, recommend
   the best window.
3. Transport
   3.1 Getting there — nearest airport, main railway station(s), major bus
   stand; pick the most popular / easiest, with rough distance to the centre.
   3.2 Getting around — best local option (metro / scooter rental / auto / cab),
   rough cost, and a sample provider if known.
4. Stay recommendations — best areas + concrete options across budgets
   (hostel / mid / premium). Note anything special (sea-facing, central).
5. Attractions & sights — top things to see, grouped logically (beaches,
   temples with dress code, viewpoints, etc.). Number each attraction
   (5.1, 5.2 …). For each include:
- A one-line description
- 2-5 short interesting facts / things to know (history, what makes it
  special, a local tip)
- Opening & closing time (mark approximate; note weekly off if any)
- Entry charge where relevant (mark approximate)
- A Google Maps link in the form
  `https://www.google.com/maps/search/?api=1&query=<Place+Name+City>`
6. Activities — adventure / water / wellness, with rough prices.
7. Food guide — ordered to fit the traveller: veg-first if vegetarian, plus
   notable cafes and local dishes to try.
8. Suggested itinerary — day-by-day for the requested number of days, each day
   split into Morning / Afternoon / Evening and themed (explore / adventure /
   sightseeing). Offer an option or two where it helps.
9. Budget snapshot — rough table (travel, stay, food, local transport,
   activities, buffer) in INR against the user's stated budget.
10. Visa & documents — international trips only; Indian-passport view + where to
    verify (see references).
11. Practical notes — best time for key things (e.g. sunset window), what to
    carry, local tips.


## Save the output
After presenting the guide, also save the full numbered guide to
`outputs/trip-planner/<destination>-<n>day-summary.md` — slugify the title
(lowercase, hyphens), e.g. `outputs/trip-planner/varkala-3day-summary.md`.
Create the folder if it doesn't exist, so the user keeps a reusable, shareable copy.


## Example prompts (what the user types)
- "Plan a 3-day trip to Varkala, veg food, mostly relaxed with one adventure day."
- "I have 5 days and 80k, first week of December, somewhere warm from Bangalore."
- "Weekend getaway, no flights, relaxing, veg food easy to find."
- "Compare Vietnam vs Sri Lanka for a 6-day trip in my budget."


## Final check before answering (do NOT skip)
Before showing the guide, silently verify it against this skill. Only present
once every check passes; if any fails, fix it first, then answer.
- All required inputs gathered (length, dates/month, origin, who's going,
  budget, trip type). If any is still missing, ask — don't guess.
- Every applicable section from the Output structure is present, in order, with
  correct numbered headings and sub-sections. Sections dropped only because they
  genuinely don't apply (state that briefly, e.g. "no visa — domestic").
- Section 2 explicitly judges the user's month/dates (good / okay / poor + why),
  or recommends a window if dates aren't fixed.
- Every attraction in section 5 has: description, 2-5 facts, open/close time
  (approx), entry charge where relevant, and a working Google Maps search link.
- Itinerary day count matches the requested number of days.
- Budget snapshot is in INR and reconciles against the user's stated budget.
- All prices/timings/distances marked approximate; nothing invented — anything
  uncertain is flagged with where to verify.
- Food guide ordered per the profile's food preference.
- Output saved to `outputs/trip-planner/<destination>-<n>day-summary.md`.


