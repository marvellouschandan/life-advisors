# Life Advisors

A personal, git-versioned set of AI "advisor" skills for everyday decisions —
travel, style, money, tax, home-buying, health. Think of it as a personal
board of advisors you can consult any time.

Each skill is a `SKILL.md` instruction file. Skills read `profile/me.md` for
context so you don't repeat yourself. Sensitive data lives in gitignored
`*.private.md` and never leaves your machine.

## What's a skill (30-second version)
A skill is NOT a program. It's a markdown file that tells an AI (Claude,
ChatGPT, etc.) how to think about a topic. The AI does the reading, looking at
photos, and reasoning — the skill is its playbook.

## Requirements
- An AI runtime that supports skills / project instructions — this guide uses
  Claude Code. Cursor or a ChatGPT Project also work.
- For personal-stylist: a vision-capable model to read your photos, and image
  generation with reference-photo support (e.g. ChatGPT/DALL-E, Gemini) if you
  want the visual collage look-books. Without it you still get the text look-book
  plus a paste-ready image prompt.
- `git` (and optionally the GitHub CLI `gh`) if you want version history.

## First-time setup (do this once)

1. Get the repo on your machine
   - Clone it: `git clone <your-repo-url> && cd life-advisors`
   - (Or if you built it from the runbook, you're already inside it.)

2. Create and fill your profile — this is 50% of the quality
   - Copy the templates to your real files:
     `cp profile/me.example.md profile/me.md` and
     `cp profile/me.private.example.md profile/me.private.md`
   - Fill `profile/me.md` with your non-sensitive details: location,
     age/height/weight, marital status, languages, preferences, food
     preference, dietary needs, goals. (Budget is NOT stored here — it's a
     per-task input the skill asks for, since it changes every time.)
   - Fill `profile/me.private.md` with sensitive details: income, savings,
     investments, risk appetite, medical info.
   - Both real files are gitignored — they stay on your machine and are never
     pushed. The committed `.example` files are only templates to copy from.
   - Rule of thumb: money and medical → `me.private.md`. Everything else →
     `me.md`.

3. Add your photos (only needed for personal-stylist)
   - Put images in the `uploads/` folder, e.g.
     `uploads/face.jpg`, `uploads/full-body.jpg`, `uploads/outfit-today.jpg`.
   - The `uploads/` folder is gitignored, so photos are never committed or
     pushed. They stay local.
   - When you use a photo-based skill, tell the AI which file to look at, or
     drag-drop / attach the image in your AI tool.

4. Open the folder in your AI tool
   - In Claude Code: `cd` into the repo and run `claude`. It picks up the
     skills automatically.
   - In a ChatGPT Project: upload the relevant `SKILL.md` and your `me.md`.

## How to use a skill
Just describe what you need in plain language. The AI matches your request to
the right skill and asks for anything missing. Give it the key inputs up front
to save back-and-forth.

| Skill | What to say | Key inputs to include |
|---|---|---|
| trip-planner | "Plan a trip to Vietnam" | How many days, dates/flexibility, budget, who's going, trip type (relax/explore/adventure) |
| personal-stylist | "What should I wear?" + attach photo | The occasion (date / office / casual / beach / wedding / mountains), the vibe you want, any dress code, look at `uploads/full-body.jpg` |
| wealth-advisor | "Where should I invest 50k?" | Goal, time horizon, how much, one-time or monthly (it reads risk appetite from your private profile) |
| tax-consultant | "Help me prep my ITR" | Which financial year, salaried vs other income, old vs new regime question |
| property-advisor | "Should I buy this flat?" | City/locality, price, your budget, buy-vs-rent question |
| health-advisor | "I've had a headache for 3 days" | Symptoms, how long, severity — it triages and flags when to see a doctor |

### Example prompts
- Travel: "I have 5 days and 80k, first week of December, somewhere warm and
  veg-friendly. Give me 3 options."
- Fashion: "I have a first date at a rooftop cafe on Saturday evening,
  smart-casual. Look at uploads/full-body.jpg and suggest an outfit from what
  I own, plus one thing to buy."
- Fashion (different occasion): "Beach vacation in Goa, 3 outfits, comfortable
  and not flashy." / "Trekking in the mountains, cold weather, practical."
- Money: "I can invest 15k a month for a house down payment in 6 years — what
  mix makes sense?"

Tip: the more the occasion/goal is specified, the better the output. For
personal-stylist, always name the occasion (date, office, casual, beach, wedding,
mountains) and the dress code if there is one.

## Add a skill
1. Copy `templates/skill-template/` to `skills/<new-name>/`.
2. Fill in the frontmatter and workflow.
3. Add a row to `manifest.md`.
4. Commit.

## Improve a skill
Bad output → edit the SKILL.md instruction → commit with a message saying what
failed. Your git log is the improvement history.

## Privacy
- Private repo only. This holds your face, money, and health details.
- `me.private.md` and everything in `uploads/` are gitignored — never pushed.
- Never put bank passwords, OTPs, or full card numbers anywhere in the repo.
