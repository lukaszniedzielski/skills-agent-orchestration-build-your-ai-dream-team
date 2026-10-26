# Project Pulse agent team

The custom agents in `.github/agents/` divide Project Pulse work by role and
file ownership. The Orchestrator coordinates the work; the specialists produce
the plan, design, and implementation.

## Agents

| Agent | Profile | Configured model | Responsibilities |
| --- | --- | --- | --- |
| Orchestrator | `.github/agents/orchestrator.agent.md` | Claude Opus 5.5 (copilot) | Coordinates the specialists, turns the plan into phases, assigns explicit file scopes, manages dependencies, integrates and verifies the result, and reports the outcome. It does not implement the dashboard. |
| Planner | `.github/agents/planner.agent.md` | Claude Opus 5.5 (copilot) | Reads relevant repository context and returns an actionable plan: ordered steps, file assignments, dependencies, parallelizable work, edge cases, validation expectations, and open questions. It does not write code. |
| Designer | `.github/agents/designer.agent.md` | Gemini 3.7 Flash (copilot) | Defines and implements the dashboard's visual design and responsive, accessible presentation within its assigned scope. For Project Pulse, it should deliver polished styling, project cards, status badges, clear priority treatment, readable spacing, and deterministic CSS hooks. |
| Coder | `.github/agents/coder.agent.md` | GPT-5.5 (copilot) | Implements the static dashboard and assigned runnable-app support. It follows the design direction, keeps the data and behavior deterministic, and validates its changes. |

## Project Pulse file ownership

The finished dashboard consists of:

- `app/styles.css` — Designer: layout, typography, responsive behavior,
  project cards, status badges, priority treatment, and visual states.
- `app/index.html` — Coder: dashboard structure and presentation of active
  projects, owners, statuses, recent activity, priority or risk, and concise
  contributor-friendly summaries. It should use the Designer's CSS hooks.
- `app/project-data.json` — Coder: a top-level `projects` array; every project
  includes `name`, `owner`, `status`, `recentActivity`, and `priority`.
- `.vscode/launch.json` — Coder: strict JSON launch configuration named
  **Run Project Pulse Dashboard**, serving from `app/` and opening `index.html`
  so the dashboard appears rather than a directory listing.

Each agent should stay within the files assigned by the Orchestrator. Keep
design implementation in the stylesheet and dashboard structure and data in
the Coder's files to avoid overlapping edits.

## Work sequence

1. **Plan — Planner.** Review the brief and relevant repository context.
   Return the implementation steps, file assignments, dependencies, edge
   cases, and validation expectations. The required app and launch files are
   specified in the Project Pulse brief.
2. **Set scope — Orchestrator.** Convert the plan into phases and assign the
   file ownership above. Give the Designer the visual requirements and give
   the Coder the dashboard content, data shape, and launch behavior. Keep
   changes to the same file in separate phases.
3. **Design — Designer.** Establish the visual direction and implement
   `app/styles.css`, including the class hooks the Coder should use. Report
   design decisions and any integration needs before implementation proceeds.
4. **Implement — Coder.** Build `app/index.html` and
   `app/project-data.json` to the brief, using the agreed CSS hooks, then
   create `.vscode/launch.json` with the specified working directory and
   entry point. Keep the data fields and display aligned.
5. **Integrate and verify — Orchestrator.** Check that the HTML, data, styles,
   and launch configuration agree; confirm all requested dashboard
   information and launch behavior are covered, then report the outcome and
   any remaining risks.

This sequence is intentionally dependent: the Planner defines scope first,
the Designer establishes the visual contract, and the Coder uses that contract
in the HTML. The Orchestrator integrates after implementation. Do not parallelize
work that shares a file or depends on an unfinished design decision.
