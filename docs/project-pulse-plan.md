# Project Pulse Dashboard Plan

> **Planning only:** This document describes the work; it does not implement the dashboard.

## Deliverables and ownership

- **Designer exclusively:** `app/styles.css` — layout, hierarchy, responsive design, typography, contrast and focus states, cards, and status and priority treatments.
- **Coder exclusively:** `app/index.html` — page structure, loads data, displays all required data, and includes a contributor-friendly summary.
- **Coder exclusively:** `app/project-data.json` — top-level `projects` array; every item includes `name`, `owner`, `status`, `recentActivity`, and `priority`. An optional `summary` field may be included if chosen.
- **Coder exclusively:** `.vscode/launch.json` — strict JSON, configuration named `Run Project Pulse Dashboard`, serves from `app/`, and opens `index.html` rather than a directory listing.

## Ordered phases and dependencies

1. **Planner/Orchestrator — confirm scope, ownership, and handoffs.** Do this before implementation; communicate the deliverables and file boundaries.
2. **Designer — implement responsive, accessible visual styling.** Report the CSS hooks (class names and expected use) to the Coder. The stylesheet and hook report are prerequisites for HTML work.
3. **Coder — create `app/project-data.json` and `.vscode/launch.json`.** These can be created while the Designer works. Do not overlap edits to any file.
4. **Coder — create `app/index.html` after the Designer reports hooks.** Use those CSS hooks and the agreed JSON contract.
5. **Orchestrator — integrate and verify after all four files exist.** Report issues to the responsible owner for correction; do not take over implementation.

## Edge cases and open choices

- Handle empty or malformed project data and data-load failures clearly.
- Ensure long names, summaries, and activity text wrap or otherwise remain usable at narrow widths.
- Status must remain distinguishable without relying on color alone; provide visible keyboard focus.
- Render dynamic text safely rather than interpreting it as markup.
- Sample data and whether to include the optional `summary` field remain unresolved choices; confirm them during planning.

## Validation expectations

- Parse `project-data.json` as strict JSON; check the top-level `projects` array and all five required fields on every item.
- Parse `launch.json` as strict JSON; verify the exact configuration name, `app/` serving directory, and explicit `index.html` target.
- Check that the page references the stylesheet and data, loads the data, and displays every required field and the planned cards.
- Review responsive layouts, contrast, keyboard focus, and color-independent status cues, including long text at narrow widths.
- Run the launch configuration and confirm it opens the dashboard at `index.html`, not a directory listing; verify empty, malformed, and failed-load data states.
