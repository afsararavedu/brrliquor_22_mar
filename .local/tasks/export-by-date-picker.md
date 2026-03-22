# Export Sales by Selected Date

## What & Why
Add a date picker near the existing "Export CSV" button on the Sales page, so users can select any past date and download the sales data for that specific day. Currently, the export only downloads whatever is loaded on screen (today's data).

## Done looks like
- A date input field appears next to (or just above) the Export CSV button on the Sales page
- The date defaults to today's date
- When the user picks a different date and clicks Export CSV, the app fetches that day's sales from the server and downloads them as a CSV file named `sales_report_[selected-date].csv`
- If the selected date matches the currently loaded data, it exports from the existing local state (no extra network call needed)
- If no sales data exists for the selected date, a toast message informs the user

## Out of scope
- Changing any other part of the Sales page UI or workflow
- Date range exports (multi-day)
- Backend changes (the `/api/sales` endpoint already supports fetching by date)

## Tasks
1. **Add export date picker UI** — Place a date input field next to the Export CSV button on the Sales page, defaulting to today's date.
2. **Wire up date-specific export logic** — On export click, if the picker date matches the currently loaded date use local state; otherwise fetch that date's sales via the existing API endpoint, then generate and trigger the CSV download. Show a toast if no data is found for the chosen date.

## Relevant files
- `client/src/pages/Sales.tsx`
- `server/routes.ts:413-425`
- `shared/schema.ts`
