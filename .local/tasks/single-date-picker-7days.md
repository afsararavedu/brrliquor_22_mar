# Single Date Picker (Last 7 Days)

## What & Why
Replace the current three-button date selector (Today / Yesterday / 2 Days Ago) on the Sales page with a single calendar date picker popover. The picker should restrict selectable dates to today and the previous 6 days (7 days total), so users can choose any of those days to load, save, or submit their sales details.

## Done looks like
- The three quick-select buttons are removed.
- A single date picker button (showing the selected date) opens a calendar popover when clicked.
- The calendar only allows selecting dates within the last 7 days (today and the 6 days before it); all other dates are disabled.
- Selecting a date in the picker updates the sales form to show/save data for that date, exactly as before.
- The submitted/locked status still reflects the chosen date.

## Out of scope
- Any changes to the backend or storage logic.
- Allowing dates beyond 7 days in the past or future dates.

## Tasks
1. **Replace date buttons with a calendar popover** — Remove the `getAvailableDates` helper and the button row UI. Add a date picker using the existing `Calendar` shadcn component inside a `Popover`, with dates outside the last 7 days disabled. Wire the selected date from the picker to the existing `selectedDate` state.

## Relevant files
- `client/src/pages/Sales.tsx:38-51,318-335`
- `client/src/components/ui/calendar.tsx`
