# Marking Book

**Twenty standalone apps that handle the admin of running a one-person tuition business in Singapore** — quoting, scheduling, marking, invoicing, chasing payment, reporting.

Each tool is its own single-file app. No build step, no CDN, no login, no server. Everything runs in the browser, works offline, and every student's data stays on the device. Drop the folder on GitHub Pages and it's live and installable.

---

## What you get (24 files)

| File | What it is |
|---|---|
| `index.html` | The hub — storefront + journey map linking to all 20 apps |
| 20 × `*.html` | The standalone apps (list below) |
| `sw.js` | Service worker — precaches everything for full offline use |
| `manifest.json` | Makes it installable ("Add to Home Screen") |
| `icon.svg` | App icon (red tick on an exercise-book page) |

### The 20 apps, by journey stage

**1 · Get found** — `rate-card.html` · `enquiry-reply.html` · `trial-confirmation.html` · `assignment-apply.html`
**2 · Onboard** — `student-cards.html` · `slot-planner.html` · `package-tracker.html` · `travel-rate.html`
**3 · Teach** — `attendance-log.html` · `syllabus-tracker.html` · `homework-tracker.html` · `marks-progress.html`
**4 · Get paid** — `invoice.html` · `payment-tracker.html` · `payment-reminder.html` · `earnings.html`
**5 · Grow** — `progress-report.html` · `review-collector.html` · `referral-tracker.html` · `reschedule.html`

**Two kinds of app:**
- **Generators** (8) — fill a short form, get copy-paste text (rate cards, replies, invoices, reminders, reports). Your reusable details (name, PayNow, rate) are remembered on the device so you don't retype them. One-tap *Copy*.
- **Trackers** (12) — add/list/filter/delete records that persist in `localStorage`, with computed columns (slot clashes, % marks, lessons left, true $/clock-hour, outstanding totals) and *Export to CSV*.

---

## Run it / host it

**Locally:** open `index.html` (or any app file) in a browser. Note: the service worker needs to be served over `http(s)`, not `file://` — for full offline/install behaviour, host it (below) or run a local server (`python3 -m http.server`).

**On GitHub Pages:**
1. Put the whole `marking-book` folder's contents in a repo (keep all files in the same directory — the links and service worker are relative).
2. Repo → **Settings → Pages** → Source = `main`, `/root`.
3. Your hub is at `https://<username>.github.io/<repo>/`. Each app is `…/invoice.html`, etc.
4. **On every deploy, bump the cache version** in `sw.js` (`markingbook-v1` → `-v2`) so returning users get the update instead of the cached old copy.

**Install as an app:** open the hub on a phone → browser menu → *Add to Home Screen*. It then opens full-screen and works with no connection.

---

## Architecture notes

- Each app is one self-contained `.html` file: vanilla HTML/CSS/JS, **zero external dependencies, no CDN**.
- Shared engine: a declarative `TOOLS` array drives two renderers (`gen` and `track`), so every app is built from the same tested core — and any app is a few lines away from a custom variant.
- Guarded `store` wrapper around `localStorage` (try/catch, JSON, namespaced `mbk_` keys). Generator defaults stored under `gendef_<id>`.
- `localDateStr()` for timezone-safe dates; money/numbers formatted `en-SG`.
- One root `sw.js` precaches all files and serves cache-first with a network fallback. Accessibility floor: keyboard focus rings, responsive to mobile.

**Honest limitation (state it to buyers up front):** data is per-browser, per-device, and does **not** sync between phone and laptop on its own. Every tracker has *Export*. If a buyer needs cloud sync, this isn't the product — say so before the sale, not at the refund.

---

## Before you build app #21: validate

This repo is **supply**. The riskiest assumption is still unproven:

> *Will a real Singapore tutor keep — or pay for — this when free spreadsheets and centre apps exist?*

The next unit of effort belongs on validation, not more apps.

**Where the tutors are (watering holes):** they cluster in assignment channels and tutor communities. Lurk, then add value — don't drop links cold.
- **Telegram:** Nanyang Tuition Jobs, Tutor Society Singapore, TutorNow Assignments, The Great Knowledge Keepers, plus general SG tutor chat groups.
- **Facebook:** SG home-tutor / tuition-teacher groups.
- **Lemon8 / TikTok:** "my life as a part-time tutor" creators — already talking about the admin grind.

**A 7-day, near-zero-cost test:**
1. Pick the sharpest single app — likely `payment-reminder.html` or `assignment-apply.html`. Host it.
2. DM 5 tutors: *"Built a free thing for the payment-chasing headache — can I send it and hear what's useless about it?"* Watch where they hesitate.
3. Post one genuinely useful free app in a community (not the store), with the line *"made this for myself, free, data stays on your phone."*
4. Offer the paid version to anyone who liked it: *S$19 to own the kit, or S$80 to set it up around your subjects.* One yes is signal.
5. Decide the model from what happened: cheap download (hard), **done-for-you customisation** (strongest — the 20 files are also 20 templates), or free-app-as-lead-magnet → the service. Don't build #21 until a stranger has used or paid for one.

---

*Built solo. No fake reviews, no stock photos. Pain points and SG market-rate references drawn from public 2025–2026 sources. Rate hints are guidance, not advice — you set your own rates.*
