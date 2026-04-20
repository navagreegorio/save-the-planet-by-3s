# Resources Used — Save the Planet by 3S

Complete list of resources, tools, data sources, and references used to build the app. Required for Technovation Girls 2026 (new for 2026).

---

## 1. Platforms and tools

- **Thunkable** — App development platform (block-based cross-platform builder). `https://thunkable.com` · Documentation: `https://docs.thunkable.com`
- **Thunkable Community Forum** — Debugging advice, examples, staff responses. `https://community.thunkable.com`
- **Google Sheets** — Cloud database backend for the app.
- **Google Maps URL scheme** — Walking directions without an API key. `https://www.google.com/maps/dir/?api=1`
- **GitHub** — Dataset hosting under CC BY 4.0.
- **Claude (Anthropic)** — AI assistant used by the mentor for Thunkable debugging and English language review. See `AI_USAGE_DISCLOSURE.md`.

## 2. Data sources (all open data)

- **Community of Madrid Open Data Portal** · `https://datos.comunidad.madrid` · CC BY 4.0 — Primary source for collection points across 24 territories.
- **Ayuntamiento de Madrid Open Data** · `https://datos.madrid.es` · CC BY 4.0 — Supplementary municipal data.
- **Ecoembes** — Public statistics on yellow-bin contamination in Spain. `https://www.ecoembes.com`
- **Boletín Oficial del Estado (BOE)** · Real Decreto 315/2025 on packaging and recycling · `https://www.boe.es`

## 3. Competition & ecosystem

- **Technovation Girls** · `https://technovationgirls.com` — 2026 rubric, guidelines, submission platform.
- **Technovation App Gallery** · `https://technovationchallenge.org/app-gallery/` — For benchmarking with prior projects.
- **Power To Code** · `https://powertocode.org` — Spain regional workshops and mentorship.
- **Universidad Carlos III de Madrid (UC3M)** · `https://www.uc3m.es` — Spain regional finals and benchmark scale.

## 4. References & inspiration

- **Ada Lovelace** — First algorithm (Notes on Babbage's Analytical Engine, 1843). UNESCO biographical profile · `https://www.unesco.org`
- **Ángela Ruiz Robles** — Spanish inventor, OEPM profile · `https://www.oepm.es`
- **Bletchley Park** — Women in wartime computing · `https://bletchleypark.org.uk` — used as a narrative reference for "women who coded when no one called it coding".
- **Haversine formula** — Great-circle distance on a sphere, used as a mathematical-modelling learning reference (planned for v2).
- **Fibonacci sequence** — Inspiration for milestone thresholds (3, 5, 8, 13, 21) on the Impact screen.

## 5. Technical articles consulted during development

### Thunkable documentation
- Data Viewer List · `https://docs.thunkable.com/app-design/ui-components/data-components/data-viewers/data-viewer-list`
- Data Sources · `https://docs.thunkable.com/snap-to-place/data-sources`
- Live Test · `https://docs.thunkable.com/getting-started/live-test`
- Device blocks (`seconds since 1970`, etc.) · `https://docs.thunkable.com/blocks/blocks/device`
- Timer blocks · `https://docs.thunkable.com/blocks/app-features/timer`
- Release Notes 2024 · `https://docs.thunkable.com/additional-resources/release-notes/release-notes-2024`

### Thunkable community threads (debugging references)
- *"Data Viewer Table Filter with Variable not working on Android"* — staff workaround: set DVL visible before update filter · `https://community.thunkable.com/t/data-viewer-table-filter-with-variable-not-working-on-android/3873437`
- *"New way to add Search and Filtering feature in to your app"* — staff post on Filter Views + wait pattern · `https://community.thunkable.com/t/new-way-to-add-search-and-filtering-feature-in-to-your-app/3939241`
- *"Data Viewer List causes app to slow down"* — performance at scale · `https://community.thunkable.com/t/data-viewer-list-causes-app-to-slow-down/1846748`
- *"Data Viewer List refresh"* — semantics of Refresh Data · `https://community.thunkable.com/t/data-viewer-list-refresh/2182506`
- *"My Data Viewer List Grid is extremely slow"* — volume thresholds · `https://community.thunkable.com/t/my-data-viewer-list-grid-is-extremely-slow/2098533`
- *"Accelerate your Thunkable application"* — stored vs app variable benchmarks · `https://community.thunkable.com/t/accelerate-your-thunkable-application/2716433`
- *"How to detect Data Viewer List refresh event"* — absence of on-refresh event · `https://community.thunkable.com/t/how-to-detect-data-viewer-list-refresh-event/1207488`
- *"Response time in app vs Live Test"* — preview vs installed build differences · `https://community.thunkable.com/t/response-time-in-app-vs-live-test/2482842`
- *"Using TestFlight to check my design"* — TestFlight as source of truth · `https://community.thunkable.com/t/using-test-flight-to-check-my-design/2325062`

### External technical references
- **Google Sheets API usage limits** · `https://developers.google.com/workspace/sheets/api/limits`
- **Airtable Web API rate limits** · `https://airtable.com/developers/web/api/rate-limits` (consulted for v2 planning; not used in current build)
- **Expo (React Native framework underlying Thunkable)** · Development mode docs · `https://docs.expo.dev/workflow/development-mode/` · Source on GitHub · `https://github.com/expo/expo`

### Video tutorials
- Thunkable official — CRUD and Data Sources · `https://www.youtube.com/watch?v=kXex673U2Aw`
- Spanish-language tutorial on filtering Google Sheets in Thunkable · `https://www.youtube.com/watch?v=Aum1N8JzdNA`

## 6. What we did NOT use

For transparency:

- **No paid APIs**. The app has zero operating cost.
- **No generated / synthetic data**. Every record is traceable to an open data source.
- **No proprietary ML models or image-generation tools**.
- **No third-party analytics or tracking SDKs**. The app collects no user data.

---

*Code & Shine · Save the Planet by 3S · Technovation Girls 2026*
