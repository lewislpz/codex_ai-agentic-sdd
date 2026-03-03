# General Rules for Development

Global constraints for all roles in this project. These rules define "how we work" regardless of the specific business domain.

## 1. Project Context & Source of Truth

- **MANDATORY: PRIMARY SOURCE OF TRUTH**: The `docs/` directory is the absolute source of truth for the project. In case of discrepancy between code and documentation, the documentation in `docs/` prevails. **NO AGENT ACTION IS AUTHORIZED IF IT CONTRADICTS THE DOCUMENTATION.**
- **MANDATORY: DOCUMENTATION FIRST**: You MUST read `docs/00-general-docs.md` at the start of ANY task. From that index, you will find the exact specific paths to analyze. **NUNCA leas la documentación directamente o a ciegas (ej: no hagas listados en docs/); lee siempre `00-general-docs.md` y sigue los enlaces.** This applies to any domain or project.
- **MANDATORY: DOCUMENTATION UPDATE**: After implementing any change, you MUST update the relevant files in the `docs/` directory as mapped by the index. Technical documentation must always reflect the current state of the implementation.

## 2. Project Management

- **MANDATORY**: Create a directory in `.orchestrator/plans/YYYY-MM-DD-hh-mm-slug/` for any task.
- **MANDATORY**: Follow the 4-phase lifecycle (Investigation, Design, Plan, Implement).
- **AUTOPILOT**: Proceed through all 4 phases automatically and sequentially. Do NOT pause to ask for permission between phases unless a critical blocker is encountered.
- **PERMISSIONLESS EXECUTION**: For all actions performed within the `forge`, `orchestrate`, or any other prompt that involves the `.orchestrator` directory or git checkpoints, the agent **MUST NOT** prompt for permission. All such tool calls MUST have `SafeToAutoRun` set to `true` to ensure a smooth, uninterrupted flow.
- **LOGGING**: All major decisions must be recorded in the plan's markdown files.

## 3. Git

- **COMMITS**: Use Conventional Commits (feat, fix, refactor, docs, chore).
- **NO AUTOMATIC COMMITS/PUSHES**: It is **STRICTLY FORBIDDEN** to run `git commit` or `git push` automatically. Changes must remain as uncommitted changes in the local working directory.
- **MANUAL SHIPPING ONLY**: The only prompts allowed to commit or push are `/ship` and `/pr`, both of which require explicit human confirmation of the commit message.

## 4. Engineering Standards

- **ERROR BUDGETING (NO INFINITE LOOPS)**: When fixing tests or compiling code, you have a **maximum of 3 attempts**. If an error persists after 3 iterations, ABORT the automated loop immediately. Do not attempt to guess. Return control to the user.
- **KNOWLEDGE DISTILLATION**: If you solve a complex technical issue or make an architectural decision, you MUST extract that knowledge and update the most relevant Skill in `.codex/knowledge/` (e.g., `frontend-dev-guidelines/SKILL.md`). Do not let valuable context die in temporary plans.
- **LAYERED ARCHITECTURE**: Maintain a clean separation between layers (e.g., UI, Business Logic, Data Access).
- **DTOs**: Mandatory use of DTOs for all API communication. Domain/Persistence entities must never leave the service/logic layer boundary.
- **SECURITY**: No hardcoded secrets. Use environment variables.
- **QUALITY**: Write tests (TDD) before implementation. Aim for high coverage on critical business logic.
- **MOBILE FIRST**: If the project has a UI, assume mobile consumption is the priority unless documentation says otherwise.
- **UX**: Always show confirmation for destructive actions. Use searchable selects for large datasets.

- **MANDATORY: TECH STACK AUDIT**: You MUST maintain `docs/tech-stack.md` as the authoritative and up-to-date summary of the project's technology stack. Whenever you modify backend dependencies (`pom.xml`), frontend dependencies (`package.json`), or infrastructure configurations (`docker-compose.yml`, `Dockerfile`), you MUST immediately update `docs/tech-stack.md`.

## 6. Technology Stack Discovery

- Do not assume a specific technology stack. Always consult `docs/tech-stack.md` (or the equivalent file in `docs/`) before proposing or writing code.
