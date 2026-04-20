# Lessons Learned — Save the Planet by 3S

These are the runtime lessons we accumulated while building the app in Thunkable. Each one cost us at least one debugging session to discover. We document them here because none of them appears in the official Thunkable documentation, and because we think they are the most honest evidence that a beginner team did real engineering.

---

## State & variables

**L1 · List-type app variables reset on screen navigation.**
Discovered after three sessions. Catalogue lists loaded on Home were empty on Identify. Fix: use `stored variables` for anything needed across screens, or reload the list on every `Screen Opens`.

**L2 · String-type app variables can also be unstable across multi-screen navigation in some builds.**
Less consistent than lists, but we saw it. Defensive approach: use stored variables for persistent state.

**L3 · `Screen Opens` fires before async data sources finish loading.**
If you read `list of values in <data source>` inside `Screen Opens`, you frequently get an empty list. Workaround: trigger the load from a button click with a guard flag, or use a short retry pattern.

**L4 · Function parameters are NOT accessible from event scope inside the function.**
A function that takes `distrito` as a parameter cannot read that parameter from a nested event handler. Workaround: write the parameter to an app variable inside the function and read the app variable from the event.

**L5 · Functions are screen-scoped.**
A function defined on `PuntosScreen` is not callable from `IdentifyScreen`. If you need cross-screen logic, duplicate the function or use a stored-variable contract.

## Data Viewer List / Filter Views

**L6 · Filter Views connected to a Data Viewer need an explicit `Refresh Data` after `update filter for`.**
Without the refresh, the DVL shows the old filter's rows. This is documented by Thunkable staff.

**L7 · The Data Viewer must be `visible = true` BEFORE `update filter for` is called.**
Discovered via a Thunkable staff response to an Android-only bug report. Setting the DVL hidden, filtering, then making it visible can leave the list empty. Our canonical sequence: `set visible → update filter → micro-wait → refresh data`.

**L8 · A fixed long `wait` is a bad idea for cloud operations.**
Thunkable's own documentation warns against it. Too long = wasted latency; too short = stale data. We use **micro-waits of 100–250 ms** only to sequence UI/filter/refresh, never as a substitute for handling network latency.

**L9 · `Refresh Data` does not paginate or reduce rows.**
It only re-syncs the DVL with the data source. If a chunk is too big, refreshing does not help — the chunk has to be smaller.

**L10 · Thunkable does not ship an `on DVL refreshed` event.**
So we cannot know for certain when a refresh is complete. Workaround: check `number of rows in <data source>` after a short timer; if zero, retry once.

## Blocks: subtle platform quirks

**L11 · The `in list get #` block ships with a spurious `+ list` wrapper.**
If you drag it from the drawer and plug a variable in, the count is wrong. Fix: disconnect the wrapper and plug the variable directly into the index slot.

**L12 · `does text contain` can have its slots inverted.**
The block reads naturally left-to-right but internally swaps the haystack and the needle in some versions. Always verify by testing with a known-true and a known-false pair.

**L13 · The "Disabled" toggle on a button silently blocks Click events.**
If nothing happens when you tap, check the Disabled property first — it is a quick check that has cost us twice.

**L14 · The Thunkable AI Helper generates block combinations that do not exist in the current block set.**
Treat AI-generated block suggestions as pseudocode, not as a working solution; rebuild from known-good blocks.

## Data sources & backend

**L15 · Google Sheets API has per-minute quotas.**
Reproduced when we stress-tested the app with aggressive retries. Fix: cap retries at 1, use reasonable spacing, and prefer paginated chunks over big single reads.

**L16 · Airtable has its own rate limits (5 requests per second per base) if used as a backend.**
Not our current stack, but we tested Airtable briefly and saw 429 responses. Documenting it in case v2 migrates.

**L17 · Spanish Excel silently converts `40.4752` to `40,4752`.**
Coordinates stored as numeric get corrupted. Fix (by all): store lat/lon as text columns, and pre-build the Google Maps URL in a separate column.

## Search & UX

**L18 · Strict "exact match" search fails on misspellings, synonyms, and regional waste names.**
Discovered in the pilot. Fix: two-pass search — exact first, then "contains". Accuracy jumped from 72% to 94%.

**L19 · Showing addresses is not enough; users want the walking route itself.**
Fix: the "Open route" button using a Google Maps URL with `travelmode=walking`. Free, no API key.

**L20 · Users need a sense of progress to keep using a behaviour-change app.**
Fix: the Impact screen with weekly counters and Fibonacci-style milestones. Users noticed the milestones immediately.

## Development workflow

**L21 · Web Preview is NOT a substitute for TestFlight or an installed Android build.**
Some runtime bugs only appear on a real device. Our rule: a bug is not "fixed" until it is verified in a TestFlight/installed build.

**L22 · Some fixes require updating the Thunkable Live app itself.**
A bug fixed on the web editor may not reach a user on an older Thunkable Live installation.

**L23 · For apps already downloaded or published, a new fix may require re-downloading or re-publishing.**
This trips up user testing — test families sometimes run an older build than the current web version.

**L24 · Hard-refreshing the Thunkable editor is occasionally necessary after release notes.**
If new behaviour does not appear, close and reopen the tab.

**L25 · Stored variables are significantly slower to read than app variables.**
Community benchmarks show ~100–200× slower in tight loops. Rule: snapshot stored variables into app variables at screen open, then work from the app variables.

**L26 · A well-cleaned dataset is worth more than clever code.**
Our biggest wins came from data preparation (normalising text, fixing coordinate locale, pre-building URLs), not from Thunkable tricks.
