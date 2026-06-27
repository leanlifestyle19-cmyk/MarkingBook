# Marking Book

**Twenty tiny tools that handle the admin of running a one-person tuition business in Singapore — quoting, scheduling, marking, invoicing, chasing payment, reporting.**

Single file. No build step. No CDN. No login. No server. Everything runs in the browser and every student's data stays on the device. Drop `index.html` on GitHub Pages and it's live.

---

## Why this exists (the niche)

The polished tuition apps (Tutorbase and friends) are built for **centres** — multi-tutor, with admin staff, behind a monthly subscription. The person they don't serve is the **solo / freelance home tutor**, who personally does five jobs at once: finding students, teaching, billing, chasing money, and reporting to parents.

That tutor is a defensible niche for three researched reasons:

1. **The admin is real and unowned.** Singapore tuition operations lose roughly 8–12 hours a week to admin — scheduling clashes, payment reconciliation split across PayNow / bank transfer / cash, and parent messages scattered over WhatsApp, SMS and email. A solo tutor carries all of that with zero back office.
2. **Privacy is a feature here, not a footnote.** Tutors hold student names, levels, marks, parent numbers and home addresses — PDPA-sensitive data. Because this kit stores everything **on the device only**, the usual single-file limitation ("no cloud sync") becomes the actual selling point.
3. **The market is large and the watering holes are known.** Parents spent ~S$1.8b on private tuition in 2023 (up ~30% since 2018). Solo tutors gather in specific Telegram channels and Facebook groups waiting for assignments — so distribution is targetable, not guesswork.

---

## What's inside — 20 tools across the tutor journey

Built on a design-thinking customer journey map. Not 20 random utilities — one tool per friction point along the actual lifecycle of a tutor's relationship with a student.

| Stage | Pain it removes | Tools |
|---|---|---|
| **1 · Get found** | Quoting without overquoting; replying fast | Rate Card Maker · Enquiry First-Reply · Trial Lesson Confirmation · Assignment Quick-Apply |
| **2 · Onboard** | Where do a new student's details, slots & package live | Student Cards · Weekly Slot Planner *(clash detection)* · Package Tracker · Travel & Rate Sanity |
| **3 · Teach** | Homework done? What topic are we on? | Attendance Log · Topic/Syllabus Tracker · Homework Tracker · Marks & Progress |
| **4 · Get paid** | Chasing money; knowing what's owed | Invoice/Receipt · Payment Tracker *(running "owed" total)* · Payment Reminder *(3 tones)* · Monthly Earnings |
| **5 · Grow** | Proving it works; getting referrals | Parent Progress Report · Review Collector · Referral Tracker · Reschedule Message |

**Two kinds of tool:**
- **Generators** (8) — fill a short form, get copy-paste text (messages, invoices, rate cards). A *Copy* button is built in.
- **Trackers** (12) — add/list/delete records that persist to `localStorage`, with computed columns (clashes, % marks, lessons left, true $/clock-hr) and an *Export to CSV* button.

---

## Run it / host it

**Locally:** just open `index.html` in any browser.

**On GitHub Pages:**
1. Create a repo (e.g. `marking-book`) and add `index.html` to the root.
2. Repo → **Settings → Pages** → Source = `main` branch, `/root`.
3. Wait ~1 minute. Your link is `https://<username>.github.io/marking-book/`.
4. To update, commit a new `index.html`. (If you later add a service worker, bump the cache version on each deploy, per your usual convention.)

---

## Architecture notes

- Single `index.html`. Vanilla HTML/CSS/JS, **no external dependencies, no CDN**.
- State persists via a guarded `store` wrapper around `localStorage` (try/catch, JSON, namespaced `mbk_` keys).
- `localDateStr()` for timezone-safe dates; numbers/money rendered with `en-SG` formatting.
- Tools are **declarative**: a `TOOLS` array drives two engines (`gen` and `track`), so adding tool #21 is a few lines, and any tool can be reskinned per client — which is what turns the kit into a service (see below).
- Accessibility floor: keyboard focus rings, `Esc` to close, responsive to mobile.

**Honest limitation to state up front (avoids refund requests):** data is per-browser, per-device, and does **not** sync between phone and laptop on its own. Every tracker has *Export*; there is no cloud. If a buyer needs sync, this isn't the product.

---

## The part the last AAR kept flagging: validate before building tool #21

This repo is **supply**. There is still zero evidence of **demand**. The riskiest assumption is unchanged:

> *Will a real Singapore tutor find this useful enough to keep — or pay for — when free spreadsheets and centre apps exist?*

Until that's tested cheaply, everything else is speculation. So the next unit of effort belongs on validation, not construction.

### Where the tutors actually are (watering holes)
Solo tutors cluster in assignment channels and tutor communities. Start by **lurking, then contributing value**, not dropping links cold:
- **Telegram:** Nanyang Tuition Jobs, Tutor Society Singapore, TutorNow Assignments, The Great Knowledge Keepers — plus general SG tutor chat groups.
- **Facebook:** Singapore home-tutor / tuition-teacher groups; parent-and-tutor SME groups.
- **Lemon8 / TikTok:** creators who post "my life as a part-time tutor" content — warm, reachable, and already talking about the admin grind.

### A 7-day, near-zero-cost validation test
1. **Day 1 — pick one tool, one moment.** Likely *Payment Reminder* or *Assignment Quick-Apply* (sharpest, most universal pains). Host the page.
2. **Day 2–3 — talk to 5 tutors, don't sell.** DM in the communities above: *"I built a free thing for the payment-chasing headache — can I send it and hear what's useless about it?"* Watch where they hesitate.
3. **Day 4 — post one genuinely useful thing.** Not the store. A free tool + the line *"made this for myself, free, data stays on your phone."* See if anyone asks for more.
4. **Day 5 — offer the paid version to anyone who liked it.** "S$19 to own the full kit, or I'll set it up around your subjects for S$80." A single yes is signal.
5. **Day 6–7 — decide the model from what happened**, not what you hoped:
   - **Cheap download (S$19):** hardest — competes with free.
   - **Done-for-you customisation (from S$80):** strongest — the 20 files are also 20 templates; the service is likely the real business.
   - **Free tool as lead magnet → the service.** Probably the winning combination.

**Rule:** don't build tool #21 until at least one stranger has used or paid for one of these.

---

## Pricing (placeholders — confirm with real tutors first)
- **Try it — Free:** all 20 tools, on the page, forever.
- **Own your copy — S$19 once:** downloadable single file, runs offline, your name on the messages.
- **Done for you — from S$80:** customised to a tutor's subjects/levels/rates, their branding, hosted on their own link, 30-min setup.

These numbers are guesses. Test them before wiring real checkout.

---

*Built solo, no fake reviews, no stock photos. Pain points and SG market-rate references drawn from public 2025–2026 sources. Rate hints are guidance, not advice.*