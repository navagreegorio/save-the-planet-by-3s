# Save the Planet by 3S — Judges Package

**Team**: Code & Shine (Sol · Sofía · Sara)
**Division**: Technovation Girls 2026 · Beginner · Europe
**Location**: Majadahonda, Madrid, Spain
**Submission date**: April 20, 2026

---

## What this package contains

This ZIP is the optional "source code / AI data" attachment for the Technovation 2026 submission of Save the Planet by 3S. It is designed so that judges can understand how the app was built, reproduce the demo, and verify our claims about data and AI usage, without needing access to the Thunkable project itself.

| File | Purpose |
|------|---------|
| `README.md` | This file — how to navigate the package |
| `JUDGES_DEMO_INSTRUCTIONS.md` | Step-by-step demo script for judges, with fallback plan |
| `ARCHITECTURE.md` | The 5-screen app architecture and data flow |
| `DATASET_NOTES.md` | Structure of the Google Sheets database (164 / 3,186 / 34,824 / 218 / 24) |
| `LESSONS_LEARNED.md` | The runtime lessons we documented during development |
| `AI_USAGE_DISCLOSURE.md` | What AI tools we used, for what, and how we validated outputs |
| `RESOURCES.md` | Full list of resources, open data sources, and references |
| `data/README.md` | Notes on the dataset files (the live data itself lives in Google Sheets) |

---

## What is NOT in this package, and why

- **The Thunkable project file (.aia / .anb)**: Thunkable projects are not exported as a single file; they live in the cloud under our team account. The Project Detail Page URL submitted on the Technovation platform is the canonical entry point for the app.
- **The raw Google Sheets**: The database is live and continuously audited. We provide the full schema in `DATASET_NOTES.md` and the data sources in `RESOURCES.md` (everything is open under CC BY 4.0 from `datos.comunidad.madrid`).
- **API keys**: The app uses no API keys. Google Maps walking directions are opened via the public URL scheme, which is free and requires no authentication.

---

## How to verify our key claims

| Claim | Where to verify |
|-------|-----------------|
| "164 waste types, 38,000+ collection points, 24 Madrid territories" | `DATASET_NOTES.md` section 2; source data at `datos.comunidad.madrid` |
| "60% → 85% correct sorting in 10-family pilot" | Dashboard audit log A7 (Sol's pilot log, dated, not shipped with this package for privacy) |
| "AI used only as technical assistant; girls wrote all scripts" | `AI_USAGE_DISCLOSURE.md` |
| "Data published under CC BY 4.0" | `RESOURCES.md` section 2 |
| "No personal data collected" | See Ethics Statement in the platform Project Info submission |

---

## Contact

Mentor: Paola and Edson · Majadahonda, Madrid, Spain
Team: Code & Shine — Technovation Girls 2026 · Beginner Division · Europe

*"Like Ada Lovelace wrote the first algorithm, we write code that helps our community."*
