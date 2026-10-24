# مَسار — Masar v2

Single-page, client-only analytics for inspection visits (members, facilities, regions, locations, plans). Open `index.html`; no build, no backend.

## Data
Paste or upload three tables in «البيانات» (CSV / TSV / XLSX):
- Visits (required): جهة المرور، المنطقة، الخطة، المرور، التاريخ، القائم بالمرور
- Facility directory (optional): الجهة، المنطقة، الموقع، استبعاد (optional; نعم / TRUE excludes permanently)
- Location cost (optional): الموقع، بدل سفر، السعر، المسافة

Everything is stored in `localStorage` (`masar.v1`).

## What's new in v2
- **Data quality tab**: near-duplicate facility and member names (Arabic-normalized edit distance), visit names missing from the directory with the closest match, invalid date rows, same-day duplicate visits, conflicting regions. One-click merge in either direction, "not a duplicate" dismissal, undo per merge. Merges are applied at read time; source data is untouched.
- **Scope note**: Plans, Coverage, Next plan and Sites show a notice when plan, visit type, member or date filters narrow the analysis, with a one-click reset.
- **Editable priority weights**: every scoring rule exposed with its points; reason tags show their contribution on hover; reset to defaults.
- **Proposed schedule**: the top-N priorities become a dated schedule (working days learned from history, sites per day, team size, plan number), grouped by location, with balanced member rotation favoring prior familiarity. Exported as CSV / clipboard in the same column format as the visits table, so it can be pasted back in or into the plan tool. Estimated cost and distance when cost data exists.
- **Projected coverage** after executing the proposal.
- **Portable settings**: export / import exclusions, merges, weights and schedule options as JSON; directory `استبعاد` column for exclusions that travel with the data.
- Report: new sections «جودة البيانات» and «الجدول المقترح»; print CSS avoids orphaned headings and wraps long cells.

## Remaining ideas
- Render-test PDF output on real data across browsers.
- Optional per-region quotas in the schedule.
