# Dataset Notes — Save the Planet by 3S

## Source

All data comes from the **Community of Madrid Open Data Portal** (`datos.comunidad.madrid`) and the **Ayuntamiento de Madrid Open Data Portal** (`datos.madrid.es`), both published under **Creative Commons BY 4.0**.

Supplementary references:
- **BOE · Real Decreto 315/2025** on packaging and recycling
- **Ecoembes** public statistics on yellow-bin contamination rates

## Final dataset shape (audited)

| Entity | Count | Where it lives |
|--------|------:|----------------|
| Waste types (classes) | **164** | `waste_to_point_strategy` sheet |
| Special collection points | **3,186** | `puntos_especiales` sheet |
| Common container locations | **34,824** | 218 chunked sheets (`puntos_comunes_chunked__<chunk_id>`) |
| Chunks (spatial-index cells) | **218** | `chunk_manifest` sheet |
| Madrid territories covered | **24** | Hard-coded list in app + present in every points table |
| Total collection points | **38,010** | = 3,186 + 34,824 |

## Why we chunked the common points

Thunkable's Data Viewer List has practical limits on how many rows it can load and filter from a cloud data source. 34,824 rows in a single table produces slow refreshes and visible lag on the Points screen.

We partitioned the common-point dataset into **218 chunks** using two keys:

- **Primary key**: Madrid territory (24 values)
- **Secondary key**: waste-type group (variable per territory; 5 to 14 groups depending on coverage)

The chunking was computed analytically to keep each chunk under a size that loads smoothly on mid-range Android phones, and so that every chunk contains enough rows for the Data Viewer to render a useful list. The result is **approximately 160 rows per chunk on average**.

## `chunk_manifest` schema

| Column | Type | Description |
|--------|------|-------------|
| `chunk_id` | string | Unique identifier, e.g. `chamberi_envases_p1` |
| `distrito` | string | Territory name (one of 24) |
| `tipo_punto` | string | Waste-type group (e.g., `envases`, `vidrio`, `papel`) |
| `pagina_chunk` | integer | Page index within a (territory, type) pair, starts at 1 |
| `row_count` | integer | Rows in this chunk |

## `waste_to_point_strategy` schema (simplified)

| Column | Type | Description |
|--------|------|-------------|
| `residuo` | string | Canonical waste name in Spanish |
| `residuo_norm` | string | Pre-normalised form (lowercase, accent-folded) |
| `tokens` | string | Space-separated synonyms and regional variants |
| `contenedor` | string | Container colour / category |
| `instrucciones` | string | Short disposal instructions |
| `tipo_punto` | string | Which point type applies |
| `co2_proxy_g` | integer | Behavioural proxy in grams (placeholder until May 23) |

## `puntos_especiales` schema

| Column | Type | Description |
|--------|------|-------------|
| `id_punto` | string | Unique point ID |
| `nombre` | string | Display name |
| `distrito` | string | Territory |
| `tipo_punto` | string | Type (clean point, battery drop-off, etc.) |
| `direccion` | string | Street address |
| `lat_txt` | text | Latitude as text, decimal point |
| `lon_txt` | text | Longitude as text, decimal point |
| `mapa_link` | string | Pre-built Google Maps URL |
| `horario` | string | Opening hours |

## `puntos_comunes_chunked__<chunk_id>` schema

Same core geographic fields as `puntos_especiales`, plus the `chunk_id` column so the Filter View can key on it.

## The coordinate-locale problem (and how we fixed it)

Spanish Excel uses **comma** as the decimal separator by default. A coordinate like `40.47521,-3.67563` silently becomes `40,47521,-3,67563` when re-saved in Spanish Excel, which breaks every map integration downstream.

Our pipeline (by Sol):

1. Source CSVs from `datos.comunidad.madrid` are read with an explicit `decimal="."` setting.
2. Latitude and longitude are stored as **text columns** (`lat_txt`, `lon_txt`), not numeric, so Excel cannot reinterpret them under a different locale.
3. A **pre-built `mapa_link` column** contains the full Google Maps URL with dot-decimal coordinates, so even if the numeric columns were corrupted the user-facing route still works.
4. The data was validated with an `openpyxl` script that checks every row for a dot in each coordinate field.

## Normalisation (text search)

All text search is case-insensitive and accent-folded:

- Lowercase everything
- `á→a`, `é→e`, `í→i`, `ó→o`, `ú→u`, `ñ→n`, `ü→u`

This is applied both to the user query at runtime and to the `residuo_norm` column at data-prep time, so a match happens on two already-normalised strings.

## Reproducibility

Because the source data is open and the cleaning scripts are deterministic, a new team can rebuild an identical dataset from:

1. The source CSV files at `datos.comunidad.madrid`
2. The cleaning rules in this document
3. The chunk-manifest generation logic (partition on territory + waste type)

No proprietary tooling is needed.

## What the dataset does NOT contain

- No personal data of any kind
- No data about users of the app (the app does not collect user data)
- No data outside the Community of Madrid (the Vienna international expansion module is prototyped separately and not part of this submission)
