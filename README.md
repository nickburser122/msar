# مَسار — Masar v3

Single-page, client-only analytics for inspection visits (members, facilities, regions, locations, plans). Open `index.html`; no build, no backend.

## Data
Paste or upload three tables in «البيانات» (CSV / TSV / XLSX):
- Visits (required): جهة المرور، المنطقة، الخطة، المرور، التاريخ، القائم بالمرور
- Facility directory (optional): الجهة، المنطقة، الموقع، استبعاد (optional; نعم / TRUE excludes permanently)
- Location cost (optional): الموقع، بدل سفر، السعر، المسافة

Everything is stored in `localStorage` (`masar.v1`).

## What's new in v3 — "what you see is what you copy"
- **One table model, two renderers.** Every on-screen table and chart is backed by plain data (`columns` with `type`, raw `rows`). The screen renders HTML from it; copy, CSV, XLSX and PDF serialise the same model. Column builders (`plansCols`, `prioCols`, `sitesCols`, ...) are shared by the tabs and the report, so exports match the screen. `modelOf(id)` returns the model with the current sort, search and filters applied.
- **Copy in every card.** Copy button plus a small menu in each card header: TSV with header row (default), readable text, Markdown, current page only. Writes `text/html` and `text/plain` together, so Word / Google Docs get a real RTL table and Excel / editors get TSV. Toast reports the row count. `Ctrl/Cmd+Shift+C` copies the focused card.
- **KPI rows, findings lists and detail panels** (member, site, region) copy as label/value pairs, lists and several blocks. «نسخ التبويب» in the top bar copies every card on the current tab.
- **Charts keep their numbers.** Each chart card has a «show as table» toggle and copies as a table (calendar, trend, donut, bars, coverage matrix, pairs matrix).
- **Report modal «نسخ» format**: sections separated by a title line, as TSV, readable text or Markdown. Named report presets (sections, order, options) are stored in `localStorage` and included in the settings export / import JSON.
- **Serialiser rules**: Latin digits, no thousands separators, percent as a number (header ends with %), ISO dates (or Arabic long dates in text mode), lists joined with «، », empty cells stay empty, cells starting with `= + - @` are prefixed with `'`, direction marks around numbers in text mode.
- **New text-first reports** (card + copy + report section): overdue sites by region, plan summary in words, uncovered in the current plan by region, weekly agenda from the proposed schedule, member × month and member × region matrices, plus transitions between plans as a report section.
- **Dense tables and page size** in the theme menu (25 / 50 / 100 / all); smooth scrolling honours `prefers-reduced-motion`. No new animations.
- XLSX now writes real date cells and numeric cells. `masar.v1` data and settings from v2 load unchanged.

Notes: the report's priority section now has the same columns as the on-screen table (no location column; the last plans appear as per-plan counts). The «نسخ المقترح» and schedule copy buttons now include a header row; the schedule copy keeps the visits-table column format.

## What's new in v2
- **Data quality tab**: near-duplicate facility and member names (Arabic-normalized edit distance), visit names missing from the directory with the closest match, invalid date rows, same-day duplicate visits, conflicting regions. One-click merge in either direction, "not a duplicate" dismissal, undo per merge. Merges are applied at read time; source data is untouched.
- **Scope note**: Plans, Coverage, Next plan and Sites show a notice when plan, visit type, member or date filters narrow the analysis, with a one-click reset.
- **Editable priority weights**: every scoring rule exposed with its points; reason tags show their contribution on hover; reset to defaults.
- **Proposed schedule**: the top-N priorities become a dated schedule (working days learned from history, sites per day, team size, plan number), grouped by location, with balanced member rotation favoring prior familiarity. Exported as CSV / clipboard in the same column format as the visits table, so it can be pasted back in or into the plan tool. Estimated cost and distance when cost data exists.
- **Projected coverage** after executing the proposal.
- **Portable settings**: export / import exclusions, merges, weights and schedule options as JSON; directory `استبعاد` column for exclusions that travel with the data.
- Report: new sections «جودة البيانات» and «الجدول المقترح»; print CSS avoids orphaned headings and wraps long cells.

## Remaining steps
- Check paste behaviour by hand in Excel, Google Sheets, Word and WhatsApp on real data (automated tests only cover the clipboard payloads).
- Browser-test the new header controls on narrow screens.
- Render-test PDF output on real data across browsers.
- Optional per-region quotas in the schedule.
