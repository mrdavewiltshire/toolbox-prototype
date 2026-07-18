# Trade Partner ToolBox Prototype

## What this is
A single-file HTML prototype of the Screwfix Trade Partner ToolBox dashboard (a Power Apps app in production). It exists to demonstrate UI and typography best practice and to trial new features before they are built in Power Apps. It is not production code and must stay dependency-free.

## Hard rules
- Single file: all HTML, CSS and JS live in `index.html`. No build step, no npm, no frameworks, no external CDNs. The file must open directly from disk in a browser.
- All dummy data is fictional. Never use real Screwfix customer data, real account numbers, or real colleague names.
- Never use em dashes in any copy, comments or docs. Use commas, full stops, parentheses or semicolons.
- UK English throughout (favourite, colour). Currency is GBP formatted as £1,234.56.

## Typography: the Fluent 2 model
Every text element must map to exactly one of these five roles (see docs/typography-guide.html):

| Role            | Token          | Spec                                  |
|-----------------|----------------|---------------------------------------|
| KPI value       | Title 2        | 28px/36, semibold 600, --fg1          |
| Section header  | Subtitle 2     | 16px/22, semibold 600, --purple       |
| Tab             | Body 1 (Strong)| 14px/20, semibold active / regular off|
| Card value      | Subtitle 2     | 16px/22, semibold 600, --fg1          |
| Card label      | Caption 1      | 12px/16, regular 400, --fg3           |

Principles: labels whisper, values speak, only section headers and navigation get colour. One semibold element per component. Semibold (600), never bold (700). Sentence case for all labels and headers.

## Theming
- All colours come from CSS custom properties on `:root`, with a full dark override under `body.dark`. Never hard-code a hex in component CSS; add a token if one is missing.
- Light neutrals follow Fluent 2: --fg1 #242424 (neutralForeground1), --fg3 #616161 (neutralForeground3).
- Brand purple is #4F52B2 (lightened in dark mode for contrast).

## Architecture (keep it this way)
- One global `state` object; `render()` re-renders the active page into `#pageHost`.
- Pages: main (dashboard), review, upgrade, quotes, rewards. Each is a `render*()` function returning an HTML string.
- Dummy data lives in the constants at the top of the script (STORES, CUSTOMERS, TOP_PRODUCTS, WEEK_SALES).
- Store switching scales all figures via `scale()` so each store looks distinct.
- Keep event handling as inline `onclick` calling small named functions; this mirrors how a maker would read it.

## Testing changes
Open `index.html` in a browser and check: spender selection updates the right panel, both tab groups work, dark mode holds the type hierarchy, store switching reseeds numbers, and the layout survives a ~380px viewport.
