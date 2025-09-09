# AGENTS.md — Spec Version 1.1

## Plan/Instructions:
You are an autonomous AI agent. Without asking clarifying questions or requesting further investigation, you must:

- Reference the `project.yaml`’s Application entry by its exact section or name.
- Create a fully autonomous plan for implementing the application or script using python if performance differences between languages are negligible.
- Respect these design principles: Security by Design, Privacy by Design, Modularity by Design, Maintainability by Design, Scalability by Design.
- Use best practices in error handling, testing, logging, secrets management, and persistence without proposing a directory structure or items for investigation.
- All user-provided variables must use UPPER_SNAKE_CASE; system-generated variables must use lower-snake-case.
- If multiple files or data storage are needed:
  - Create a workspace folder named `<app-name>-data`.
  - Inside it, create subfolders:
    - `input` for input data,
    - `output` for output data,
    - `persistence` for general persistent data.
- Log every action and test run:
  - Append human-readable notes to `reports/<app-name>/action-log.txt`.
  - Store test artifacts in `reports/<app-name>/tests/`.
- Use robust error handling for all operations.
- Provide unit tests for all functions and methods.
- Follow the "never nester" philosophy: avoid code nesting deeper than three levels (max 3 levels of indentation). Refactor deeply nested logic using early returns, extraction, or clear abstractions :contentReference[oaicite:0]{index=0}.

## Initial Prompt to the AI:
You are to autonomously execute a plan to generate code based on the Application section from `project.yaml`, following this checklist:
- Perform all steps without further input or investigation.
- Reference the application entry in `project.yaml` directly.
- Use python if performance trade-offs are low.
- Ensure Security by Design, Privacy by Design, Modularity by Design, Maintainability by Design, Scalability by Design.
- Use UPPER_SNAKE_CASE for user-provided variables; lower-snake-case for system-generated variables.
- If required, create `<app-name>-data/input`, `<app-name>-data/output`, `<app-name>-data/persistence`.
- Log actions and test artifacts in `reports/<app-name>/action-log.txt` and `reports/<app-name>/tests/`.
- Include robust error handling and comprehensive unit tests.
- Adhere to the "never nester" rule: no more than three indentation levels; refactor deeper logic accordingly :contentReference[oaicite:1]{index=1}.
