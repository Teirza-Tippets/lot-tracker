# Lot Tracker: an MES-style process flow demo

A small web app that moves manufacturing lots through a defined process route, enforces process rules, keeps an audit trail, and shows a live dashboard. I built it to learn how a manufacturing execution system (MES) works by modeling its core ideas.

**Live demo:** [GitHub Pages](https://teirza-tippets.github.io/lot-tracker/)]

## What it does

- **Routes lots through ordered steps.** Every lot follows the same route (Clean, Coat, Expose, Etch, Inspect) and cannot skip a step.
- **Tracks in and out.** Operators track a lot in to start work on a step, and out to finish it. The system only allows actions that make sense for the lot's current state.
- **Enforces rules.**
  - Every action requires an operator ID.
  - Leaving the Inspect step requires a measurement. A reading outside spec places the lot on hold.
  - Releasing a hold requires a written reason and a different operator than the one who placed it.
- **Keeps an audit history.** Every action is recorded with time, operator, action, and detail. Entries are only added, never edited.
- **Shows a dashboard.** Running, on-hold, and complete counts, lots at each step, and average time per step, all calculated from the audit history.

## How it maps to MES concepts

| In this project | MES concept |
| --- | --- |
| The `ROUTE` list | Process route and traveler: the defined sequence a lot must follow |
| Track in / Track out | Lot movement and state tracking |
| Operator ID requirement | Operator accountability |
| Inspection spec and automatic hold | Process control and quality gates |
| Release with reason and second person | Hold and release with an independent check |
| History table on each lot | Traceability and audit trail |
| Dashboard | Work-in-progress visibility and cycle time |

## Try it

1. Open `index.html` in a browser, or use the live demo.
2. Enter an operator ID such as `TT204`.
3. Track LOT-1003 out of Inspect and enter a reading of `120`. It goes on hold.
4. Change the operator ID to `JR310`, release the hold with a reason, and open the lot's History panel to see every step recorded.

## How it is built

- One file (`index.html`) of plain HTML, CSS, and JavaScript. No frameworks, build step, or dependencies.
- Lot data lives in a JavaScript array. A `render()` function redraws the page from that data after every action.
- Dashboard numbers are calculated from each lot's history rather than stored separately, so they always match the audit trail.

## Limitations and next steps

- Data is kept in memory and resets when the page is refreshed. Next: save to the browser's local storage, then a real database.
- Operator IDs are free text with no login or permissions. Next: user accounts and roles (operator, supervisor).
- Only one inspection spec and one route. Next: multiple products, each with its own route and specs.
- Next: add and edit lots in the interface, export history to CSV, and add automated tests for the rules.

## How I used AI

I used Claude to plan the project, draft the starter code, and talk through each step. I tested the behavior myself and extended the rules.

## Author

Teirza Tippets: [LinkedIn](https://www.linkedin.com/in/teirza-tippets) | [GitHub](https://github.com/Teirza-Tippets)
