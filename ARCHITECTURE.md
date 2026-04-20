# Architecture — Save the Planet by 3S

## Stack

- **Front end**: Thunkable (block-based cross-platform app builder, based on React Native + Expo)
- **Backend / data layer**: Google Sheets (queried directly from Thunkable via Data Sources)
- **Directions**: Google Maps URL scheme (free; no API key required)
- **Geo data**: `datos.comunidad.madrid` (CC BY 4.0), cleaned and structured by the team

## Screens

The app has **five screens**:

| # | Screen | Role |
|---|--------|------|
| 1 | **Home (Inicio)** | Territory selection (24 options). Entry point. |
| 2 | **Identify (Identificar)** | Text search over 164 waste classes; returns container, instructions, impact. |
| 3 | **Points (Puntos)** | Filtered list + map of nearby collection points; "Open route" launches Google Maps walking directions. |
| 4 | **Impact (Impacto)** | Weekly summary of user actions; behavioural CO₂ proxy; Fibonacci milestones. |
| 5 | **Report (Reporte)** | User-submitted flag for a missing or outdated point. |

## Data loading strategy

Thunkable's Data Viewer List has practical limits on how many rows it can load at once from a cloud data source. With 34,824 common container locations to handle, we designed a **chunk-manifest architecture**:

1. The common-points dataset is split into **218 chunks** (or *trocitos* in Spanish), partitioned by district + waste type.
2. A **chunk manifest** table maps `(territory, waste_type, page) → chunk_id`.
3. On the Points screen, the app:
   - Reads the user's territory and the waste type from the Identify screen (via stored variables, see below)
   - Looks up the correct `chunk_id` in the manifest
   - Sets the Data Viewer visible first (critical — see `LESSONS_LEARNED.md`)
   - Calls `update filter for` on the Filter View, passing the `chunk_id`
   - Waits ~150ms (micro-wait for sequencing, not for latency)
   - Calls `Refresh Data` on the Data Viewer List

This yields O(1) lookup on a spatial index instead of scanning 38,000+ records each time.

## State management

Thunkable has two variable scopes that matter for multi-screen apps:

- **App variables**: In-memory; **reset on screen navigation if the variable is a list**. Used for transient state within a single screen.
- **Stored variables**: Persisted on device; survive screen navigation. Used for anything the next screen needs to read.

We use **7 critical stored variables** to pass state between screens (territory, waste type, selected chunk id, last-searched term, impact counters, user-flag draft, onboarding completion). A full inventory is in our internal Runtime document.

## Search logic (Identify screen)

Two passes over the 164-row waste table:

1. **Pass 1 — Exact token match**: Normalise user input (lowercase, accent-fold `á→a`, `é→e`, `ñ→n`), split into tokens, check for an exact match against the pre-normalised token list.
2. **Pass 2 — "Contains" match**: If pass 1 returns nothing, iterate through the token list and check `does text contain` for each token.

This two-pass approach was the result of user feedback: early testers said "it didn't find my item" when they misspelled the word or used a regional name. Accuracy jumped from 72% to 94% after switching to contains-match as pass 2.

## Routing (Points screen)

Walking directions are opened via a plain URL that Google Maps recognises:

```
https://www.google.com/maps/dir/?api=1
  &origin=<user_lat>,<user_lng>
  &destination=<point_lat>,<point_lng>
  &travelmode=walking
```

The user's GPS coordinates are read **only at the moment** the "Open route" button is pressed, via Thunkable's `get current location` block. The app does not poll or track location.

## Impact model (Impact screen — under active development)

The Impact screen currently shows:

- Count of items sorted correctly this week
- Count of unique collection points visited this week
- A **behavioural CO₂ proxy** — an estimated value in grams avoided per bin type (yellow, blue, green, brown, grey, red clean point). The numbers are placeholders based on public Ecoembes life-cycle reports, calibrated at the category level.

We explicitly call this a **proxy**, not a verified life-cycle assessment. The complete per-category model is under development for the May 23 regional finals version.

## Coordinate locale — a subtle but critical detail

Spanish Excel (and many Spanish-locale systems) use a comma as the decimal separator. This breaks map APIs that expect a dot. During data cleaning, Sol enforced decimal-point notation end-to-end using an `openpyxl`-based Python pipeline, and stored latitude and longitude as text to prevent accidental locale re-interpretation.

## What is not in the current build

- Offline mode (planned for v2)
- Notification reminders (planned for v2)
- Haversine distance in-app (currently delegated to Google Maps)
- Multi-language UI beyond Spanish + basic English labels
- Vienna international expansion module (prototyped, not shipped)
