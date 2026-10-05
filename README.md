# Expense Tracker

A small, responsive web app for recording, organising and understanding personal expenses. Built for the Intern Web Development Assessment.

**Live demo:** _add your deployed link here_

## Run it
No build step. Open `index.html` in a browser, or serve the folder (for example with the VS Code Live Server extension).

## Technologies
HTML, CSS and vanilla JavaScript. Data is saved in `localStorage`. Fonts: Unbounded (headings and numbers) and Manrope (text) from Google Fonts, with system-font fallbacks.

## What it does
- Add, edit and delete expenses (description, amount, category, date)
- Filter by category and period (all time, this month, custom range), search descriptions, and sort by date or amount
- Export the listed expenses to CSV
- Dashboard: total spent, number of expenses, top category, three most recent expenses
- Spending breakdown by category as proportional bars
- Monthly budget: set an amount and see this month's spending, what is left (or how far over), and a progress bar
- Light and dark mode, remembered between visits and starting from the device setting
- Sample data on first visit; data survives a refresh
- Works on mobile, tablet and desktop

## Project structure
```
index.html   the whole app in one file: page structure, styling and scripts
*.png        screenshots used in this README
```
For easy hosting, the app is a single file. Inside it the code is split into clearly labelled sections that mirror a multi-file layout: `css/style.css`, `js/storage.js` (localStorage), `js/expenses.js` (data rules, validation, CSV), `js/ui.js` (rendering only) and `js/app.js` (state and events).

## Design and technical decisions
- **Add and edit in a dialog.** The "Add expense" button sits in the header on every screen, and the form opens over the page so the user never loses their place.
- **Totals follow the filters.** The dashboard always describes what is currently listed, and the heading line says which filters are active. The "Recent expenses" panel ignores filters and shows the latest three overall.
- **Delete asks first, and can be undone.** Tapping Delete turns that row's buttons into "Yes, delete" and "Keep", naming the expense. After deleting, an Undo message appears for a few seconds. This is plain page content rather than a pop-up dialog, so it behaves the same in every browser, including phone browsers.
- **Budget follows the calendar month.** It compares all expenses dated this month with the budget, ignoring the list filters, and turns amber at 80% and red when exceeded.
- **Separated concerns.** Data rules (`expenses.js`) never touch the page; `ui.js` never changes data; `app.js` connects them. Each file is short enough to read in one sitting.
- **Plain scripts, no modules or libraries.** The app opens by double-clicking `index.html`, with nothing to install.
- **Safe handling of text.** Stored text is escaped before it is rendered, and CSV cells that start with `=`, `+`, `-` or `@` are neutralised so spreadsheets cannot run them as formulas.
- **Look and feel.** "Ultraviolet": an animated aurora of cyan, indigo and violet behind frosted-glass cards, film grain, a hero card with a rotating gradient border, a glowing gradient total that counts up, a cursor spotlight on cards, a glowing donut chart, and one lime spark colour reserved for actions. Dark by default; light mode is a lavender paper tone. Motion is switched off for people who prefer reduced motion.
- **Navigation.** Below 900px the page links collapse into a hamburger menu, which closes after a link is tapped.
- **Mobile layout.** Below 720px each table row becomes a labelled card, filters wrap, and dialogs fit the screen width.

## Assumptions
- Amounts are in Nigerian naira (₦) only; no currency switching.
- The eight sample expenses get random dates between 14 and 30 September 2026 (none in October), so the "This month" filter and the budget card start empty until you add an expense dated in the current month.
- Amounts must be greater than zero. Descriptions are required and limited to 60 characters.
- Deleting every expense leaves an empty list; sample data is only added on the very first visit.

## Optional features implemented
Description search, custom date range, sorting, CSV export, a monthly budget, and dark mode. Not included: recurring expenses, authentication, backend.

## Edge cases handled
Empty description, zero or negative amount, amounts typed with commas or the ₦ sign, invalid budget, empty list, no results after filtering, delete confirmation, corrupted saved data.
