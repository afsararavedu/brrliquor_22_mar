# Sales Date Picker, Save & Submit

## What & Why
Add a date picker (calendar) to the Sales page so users can work on sales for today or either of the previous two days. Enhance the existing "Save Sales" button to save with the selected date, and add a new "Submit Sales" button that freezes (locks) sales for that date so no further edits are possible.

## Done looks like
- A calendar/date picker appears near the top-middle of the Sales page, restricted to today and the previous 2 days only.
- Selecting a date loads any existing saved sales data for that date.
- "Save Sales" saves/updates the current table data for the selected date and allows re-editing later.
- "Submit Sales" button sits next to "Save Sales" and, when clicked, marks the selected day's sales as final — making all fields read-only for that date.
- If a date's sales are already submitted, the table is read-only and both buttons show an appropriate locked/submitted state.
- The unique index on `daily_sales` is updated to include `date` so records for different dates can coexist for the same brand/size.
- A new `isSubmitted` boolean column is added to `daily_sales` to track the locked state.
- A new `submit_status` table (or equivalent approach) tracks per-date submission status so the entire day can be locked in one action.

## Out of scope
- Editing or unlocking already-submitted sales (admin override).
- Historical data older than 2 days.
- Any changes to the Orders, Stock, or other pages.

## Tasks

1. **Schema & migration** — Add `is_submitted` boolean (default false) to `daily_sales`. Update the unique index from `(brand_number, size)` to `(brand_number, size, date)` to allow multi-day records. Run the migration.

2. **Backend API updates** — Update the sales list endpoint to accept a `date` query param and filter results by date. Update the bulk-save endpoint to accept and store a `date` field per record. Add a new "submit sales" endpoint (`POST /api/sales/submit`) that sets `is_submitted = true` for all records matching a given date. Update the storage layer accordingly.

3. **Sales page UI — date picker & load** — Add a date picker component near the top-middle of the Sales page, limited to today and the previous 2 days. When the date changes, reload the sales data for that date via the updated API. Show a "locked/submitted" indicator if the selected date's sales are already submitted.

4. **Sales page UI — Save & Submit buttons** — Wire the existing "Save Sales" button to include the selected date when saving. Add a "Submit Sales" button next to it. On click, call the new submit endpoint for the selected date, then refresh the table into read-only mode. Disable both buttons (or show a locked state) when the selected date is already submitted.

## Relevant files
- `shared/schema.ts`
- `server/storage.ts`
- `server/routes.ts`
- `client/src/pages/Sales.tsx`
- `client/src/hooks/use-sales.ts`
- `shared/routes.ts`
