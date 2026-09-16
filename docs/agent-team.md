# Agent team

We will build Mona's Project Pulse dashboard with a four-agent custom team orchestrated through GitHub Copilot CLI in a Codespace.

- Planner — Model: Claude Opus 4.7 (copilot). Responsibility: research the repository, identify edge cases and dependencies, and create a practical implementation plan with ordered steps, file assignments, and validation expectations. Definition file: .github/agents/planner.agent.md.
- Orchestrator — Model: Claude Opus 4.7 (copilot). Responsibility: coordinate the specialist agents, break work into phases, delegate tasks with explicit file scopes, and verify that the final integration makes sense. Definition file: .github/agents/orchestrator.agent.md.
- Coder — Model: GPT-5.5 (copilot). Responsibility: implement the code changes, fix bugs, and handle programming tasks within the scoped files assigned by the Orchestrator, including runnable app support when needed. Definition file: .github/agents/coder.agent.md.
- Designer — Model: Gemini 3.1 Pro (copilot). Responsibility: shape the UI/UX, accessibility, layout, interaction flow, and visual polish for the Project Pulse dashboard so it looks like a polished product frontend. Definition file: .github/agents/designer.agent.md.

All four definitions live under the repository's .github/agents/ folder. The workflow uses GitHub Copilot CLI in a Codespace so the Orchestrator can delegate to the Planner, Coder, and Designer, coordinate execution, and keep the dashboard build moving in structured phases.
