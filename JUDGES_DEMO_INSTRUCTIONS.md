# Judges Demo Instructions — Save the Planet by 3S

A 3-minute guided walk-through of the app, with a fallback plan in case of network or GPS issues. The demo assumes you are running the app on a phone or through the Thunkable Project Detail Page URL submitted on the Technovation platform.

---

## Before you start

1. Open the app (via the Thunkable Project Detail Page link) on a phone or the Thunkable Live web preview.
2. Grant location permission **only when prompted** — the app never reads GPS in the background.
3. Have an internet connection available (the app reads from a Google Sheets backend).

**Estimated demo time**: 2 minutes, 55 seconds.

---

## Demo script (step by step)

### Step 1 — Home screen (15 seconds)
- The app opens on the Home screen with an Animal-Crossing-inspired welcome.
- **Tap "Start"** → you will see a list of 24 territories in the Community of Madrid.
- **Select "Majadahonda"** (or any other territory you prefer).

*What to notice*: All 24 Madrid territories are covered equally, including lower-income districts. No personal data is requested at any point.

### Step 2 — Identify screen (45 seconds)
- Type a waste item, for example: `pilas` (batteries) or `glass bottle` or `brik de zumo`.
- The app normalises your text (lowercase, removes accents) and runs a two-pass search: first exact token match, then "contains" match across 164 waste classes.
- You should see:
  - ✅ Container colour (e.g., red point for batteries)
  - ✅ Disposal instructions
  - ✅ A button to jump to nearby collection points

*What to notice*: The search works with misspellings and partial words because of the two-pass logic. This was one of our three pilot-driven improvements (accuracy went from 72% to 94% after this change).

### Step 3 — Points screen (45 seconds)
- Tap "View nearby points".
- The app queries our chunk-manifest architecture: it looks up the correct chunk (one of 218) for your territory + waste type, applies a Filter View to Google Sheets, then refreshes the Data Viewer List.
- You should see a list of collection points with addresses and distances.
- **Tap any point** → the details screen opens.
- **Tap "Open route"** → Google Maps opens in walking-directions mode, from your current GPS position to the bin. No API key is used.

*What to notice*: GPS is only read at the exact moment "Open route" is pressed — never in the background.

### Step 4 — Impact screen (Development use only not production)
- Return to Home and tap "Impact".
- You will see a weekly summary: items sorted, points visited, and a behavioural CO₂ proxy.
- The milestone bar uses Avatar/Fibonacci thresholds (3, 5, 8, 13, 21) to keep early progress visible.

*What to notice*: The CO₂ number is explicitly labelled as a **behavioural proxy** in-app. We do not present it as a verified life-cycle assessment. The full per-category model is under active development for the May 23 finals version.

### Step 5 — Report screen (Development use only not production)
- Tap "Report a point" from Home.
- You can flag a missing or outdated collection point.
- Reports are reviewed weekly against `datos.comunidad.madrid`.

*What to notice*: This is how user feedback enters the product loop. Our pilot with ten families already produced three shipped changes via this mechanism.

---

## Fallback plan (if something fails on demo day)

| What fails | What to do |
|------------|------------|
| App loads slowly | The presenter narrates over a pre-recorded screen capture: "While it loads, let me tell you..." |
| GPS denied / not available | Show the "Show on map" feature, which uses a pre-built map link from the dataset (no live GPS needed) |
| Network down | Open the PDF screenshots in this package (`data/demo_screenshots/`) |
| A specific territory returns no points | Switch to Majadahonda or Madrid Centro, which are fully covered |

---

## Frequently asked questions

**Q: Why not just use Google Maps?**
A: Google Maps shows you bins but does not tell you **which** bin is correct for your waste. We solve the identification problem first, then hand off routing to Google Maps. Google Maps is the wheel; we are the steering.

**Q: Is Haversine implemented?**
A: Haversine is documented in our Learning Journey as a mathematical-modelling lesson (great-circle distance on a sphere). In the current build we delegate routing to Google Maps, which uses Haversine-equivalent maths internally; a direct Haversine implementation is planned for v2.

**Q: How do you know the 60% → 85% result is not random?**
A: The 25-point delta comes from ten families over two weeks. We report it with the sample size and duration every time; we do not hide n. The approximate confidence interval is wide (it is a small pilot), and we say so in our Dashboard audit.

**Q: How does the app scale beyond Madrid?**
A: The chunk-manifest architecture is region-agnostic. A new city only needs its own cleaned waste classification table and its own geocoded collection-point dataset; the app logic does not change.

---

## Contact for judges

If anything in the demo does not work as described, please note the step number above and we will diagnose it in real time. Our mentors Paola and Edson are available throughout the judging day.

*Code & Shine · Save the Planet by 3S · Technovation Girls 2026*
