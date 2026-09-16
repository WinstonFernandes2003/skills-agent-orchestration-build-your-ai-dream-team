# Project Pulse Implementation Plan

## Summary

Build Mona's Project Pulse as a small static dashboard for contributors. It should show multiple project cards with project name, owner, status, recent activity, priority or risk, and a short summary. The dashboard must run through the **Run Project Pulse Dashboard** VS Code configuration and open `index.html`, not a directory listing.

## Ordered Steps

1. **Confirm requirements and data contract**
   - Planner defines the dashboard structure, responsive behavior, accessibility expectations, project fields, dependencies, and validation checklist.
   - Establish the top-level `projects` array and required fields: `name`, `owner`, `status`, `recentActivity`, and `priority`.

2. **Create visual direction and data in parallel**
   - Designer defines the information hierarchy, responsive card layout, status and priority treatments, typography, contrast, spacing, and accessible states.
   - Coder creates representative project data using the agreed JSON contract.
   - These tasks can run in parallel because they use separate files and have no implementation dependency.

3. **Implement the dashboard**
   - After the Designer establishes selectors and the data contract is available, Coder creates the HTML structure and rendering logic in `app/index.html`.
   - Load `app/project-data.json`, render visible project cards, and expose status, recent activity, and priority values.
   - Keep the UI usable at narrow and wide viewport sizes.

4. **Add and verify local launch support**
   - Coder creates `.vscode/launch.json`.
   - Configure the Python server to run from the `app/` directory, use port `5500`, and open `index.html`.
   - Orchestrator checks that the launch configuration integrates with the completed app.

5. **Validate and hand off**
   - Validate file existence, JSON syntax, required selectors and fields, dashboard rendering, accessibility basics, and launch behavior.
   - Record agent contributions, completed validation, limitations, and final launch instructions in the handoff documentation.

## Responsibilities and File Assignments

| Owner | Files | Responsibilities |
|---|---|---|
| Planner | `docs/project-pulse-plan.md` | Define phases, dependencies, ownership, edge cases, and validation expectations. |
| Designer | `app/styles.css` | Create the polished responsive visual system, `.dashboard` layout, `.project-card` styling, status badges, priority treatment, spacing, contrast, and focus states. |
| Coder | `app/project-data.json` | Provide valid representative project records under the top-level `projects` key. |
| Coder | `app/index.html` | Build accessible dashboard markup, reference `styles.css` and `project-data.json`, render project cards, and display required fields. |
| Coder | `.vscode/launch.json` | Add strict JSON for **Run Project Pulse Dashboard**, with `cwd` set to `${workspaceFolder}/app`, `python3 -m http.server 5500`, and a browser URL ending in `/index.html`. |
| Orchestrator | Integration and review | Delegate work with explicit scopes, resolve handoff issues, run validation, and summarize the result. |

## Dependencies

- The JSON schema must be agreed before HTML rendering is finalized.
- The Designer's class contract must include `.dashboard` and `.project-card` before integration review.
- `app/index.html` depends on both `app/styles.css` and `app/project-data.json`.
- Browser loading of `project-data.json` depends on serving the `app/` directory over HTTP.
- `.vscode/launch.json` depends on the final app location and must target `index.html`.

## Parallel-Work Decisions

- **Can run in parallel:** Designer's CSS work in `app/styles.css` and Coder's initial project-data work in `app/project-data.json`.
- **Must run sequentially:** Plan creation before delegation; data/schema and CSS selector agreement before final HTML integration; app implementation before launch verification; implementation before final handoff.
- Avoid assigning overlapping edits to Designer and Coder, especially in `app/index.html` or `app/styles.css`.

## Edge Cases

- Empty or malformed project data should not produce a broken or blank interface; show a readable empty or error state where practical.
- Status and priority labels should remain legible and distinguishable without relying only on color.
- Long project names, activity text, and owner names must wrap without breaking card layout.
- The dashboard must not require a build tool or external package installation.
- Opening the server root must be avoided; the launch URL must explicitly include `index.html`.

## Validation Expectations

- Confirm `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json` exist.
- Confirm `app/index.html` contains the exact title **Project Pulse**, references both assets, and renders elements with `project-card`.
- Confirm the UI displays `status`, `recentActivity`, and `priority` for each project.
- Confirm `app/styles.css` contains `.dashboard`, `.project-card`, `border-radius`, and `box-shadow`, with responsive layout rules.
- Parse `app/project-data.json` as JSON and confirm it has a top-level `projects` array with all five required fields on each record.
- Parse `.vscode/launch.json` as strict JSON and confirm it names **Run Project Pulse Dashboard**, uses `${workspaceFolder}/app`, runs `python3 -m http.server 5500`, and opens `http://localhost:%s/index.html`.
- Run `bash scripts/validate-exercise.sh`.
- Manually launch **Run Project Pulse Dashboard** and confirm the browser shows the dashboard rather than a directory listing.
- Check keyboard focus, readable contrast, responsive wrapping, and the browser console for loading errors.

## Repository Basis

This plan follows the requirements in `.github/project-pulse-brief.md`, the agent responsibilities in `docs/agent-team.md`, and the validation gates in `.github/workflows/3-step.yml`.
