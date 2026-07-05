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
Produce one guide with these sections, in this order. Drop any that don't
apply; add local ones that do.

1. Overview — one-line pitch, plus best areas/neighbourhoods to stay (with the
   vibe of each) and the layout of the place.
2. Transport
   - Getting there: nearest airport, main railway station(s), major bus stand
     — pick the most popular / easiest, with rough distance to the centre.
   - Getting around: best local option (metro / scooter rental / auto / cab),
     rough cost, and a sample provider if known.
3. Stay recommendations — best areas + concrete options across budgets
   (hostel / mid / premium). Note anything special (sea-facing, central).
4. Attractions & sights — top things to see, grouped logically (beaches,
   temples with dress code, viewpoints, etc.). For each attraction include:
   - A one-line description
   - 2-5 short interesting facts / things to know (history, what makes it
     special, a local tip)
   - Opening & closing time (mark approximate; note weekly off if any)
   - Entry charge where relevant (mark approximate)
   - A Google Maps link in the form
     `https://www.google.com/maps/search/?api=1&query=<Place+Name+City>`
5. Activities — adventure / water / wellness, with rough prices.
6. Food guide — ordered to fit the traveller: veg-first if vegetarian, plus
   notable cafes and local dishes to try.
7. Suggested itinerary — day-by-day for the requested number of days, each day
   split into Morning / Afternoon / Evening and themed (explore / adventure /
   sightseeing). Offer an option or two where it helps.
8. Budget snapshot — rough table (travel, stay, food, local transport,
   activities, buffer) in INR against the user's stated budget.
9. Visa & documents — international trips only; Indian-passport view + where to
   verify (see references).
10. Practical notes — best time for key things (e.g. sunset window), what to
    carry, local tips.

## Example prompts (what the user types)
- "Plan a 3-day trip to Varkala, veg food, mostly relaxed with one adventure day."
- "I have 5 days and 80k, first week of December, somewhere warm from Bangalore."
- "Weekend getaway, no flights, relaxing, veg food easy to find."
- "Compare Vietnam vs Sri Lanka for a 6-day trip in my budget."

## References
- `references/india-passport-visa.md`  # only for international trips
