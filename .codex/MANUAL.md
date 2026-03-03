# 🧠 Generic Orchestration System Manual

This system functions as a **professional engineering team**, ensuring quality through Separation of Concerns and a prompt strictly driven by documentation as the Single Source of Truth.

---

## 👥 1. The Team (Generic Roles)

The roles have no predefined knowledge of the project; they extract it from the `docs/` directory:

* 📐 **`@architect`**: Makes high-level decisions (Models, APIs, Security) based on the requirements in `docs/`.
* 🗺️ **`@doc-planner`**: Manages the life cycle of the plan and ensures that `docs/` is always the supreme authority.
* ⚙️ **`@backend`**: Implements business logic and persistence following the technical standards defined in `docs/`.
* 🎨 **`@frontend`**: Creates premium and responsive interfaces aligned with the UX vision established in `docs/`.

---

## 🚀 2. Prompts

Use the slash commands `/` to orchestrate development:

### 🕵️ PHASE 0 - Audit: `@[/audit]`
**Goal:** Proactively scan the project for technical debt and discrepancies with the documentation in `docs/`.

### 💡 PHASE 1 - Design: `@[/think] [Idea or Feature]`
**Goal:** Plan without touching a single line of code. The AI analyzes `docs/` to generate a strategy inside `.orchestrator/plans/`.

### ⚒️ PHASE 2 - Build: `@[/forge] execute`
**Goal:** Implement code based on the approved plan, always respecting the "Source of Truth" in `docs/`.

### 🧪 PHASE 3 - Test: `@[/test]`
**Goal:** Guarantee quality through TDD (Test-Driven Development) before considering a task complete.

### 📦 PHASE 4 - Deliver: `@[/ship] "Message"`
**Goal:** Perform professional commits (Conventional Commits) after human verification.

---

## 🎒 3. Internalized Golden Rules

1. **`docs/` is the Source of Truth**: The highest authority resides in the `docs/` folder. Any change must originate or be reflected there. If the code and documentation differ, the documentation rules.
2. **Never commit directly to `main`**: Branch creation is automated for every task.
3. **Documentation First**: Roles are required to read `docs/` at the start of any task.
4. **Test-First (TDD)**: No logic is considered "finished" if it does not include its corresponding tests that validate the requirements.
5. **Mandatory DTOs**: Internal logic and persistence are never exposed directly; DTOs are used for all outer interfaces.

---

## 🧭 Project Navigation Guide

For this engine to work, the project must maintain the following in `docs/`:
- **Business Logic**: Rules, actors, and objectives.
- **Tech Stack**: Languages, frameworks, and standards.
- **Contracts**: API definitions and database schema.

---

## 🤖 4. Tutorial: Using Sub-Agent Driven Development (SDD)

The **Sub-Agent Driven Development (SDD)** model is the engine that powers the `/forge` prompt. Instead of having one AI context try to write, review, and test an entire feature at once (which leads to hallucinations and lost context), the orchestrator spawns **fresh, isolated sub-roles** for every atomic task.

Here is how you use the flow from start to finish:

### Step 1: Brainstorm & Plan (The Architect Phase)
Start by asking the system to design the feature without touching the codebase.
**Command:** Ask the AI using the `/think` prompt, e.g., `@[/think] I need to add a Google OAuth login to the backend`.
* **What happens:** The system reads the mandatory `docs/00-general-docs.md`, investigates the current codebase, and outputs a highly detailed, 4-phase plan (`investigation.md`, `design.md`, `plan.md`) into a timestamped `.orchestrator/plans/` folder.
* **Your role:** Review the generated `plan.md`. You can manually tweak the steps, change the architecture, or add new requirements directly in the markdown file.

### Step 2: The SDD Execution Loop (The Forge Phase)
Once you are happy with the plan, tell the system to build it.
**Command:** `@[/forge] execute`
* **What happens:** The Orchestrator reads `plan.md` and enters the **SDD Loop**:
  1. **Dispatch:** A fresh, blank-slate sub-agent is spawned specifically for `Task 1`. It is given the exact snippet of the task and nothing else.
  2. **Implement:** The sub-agent writes the code for that single task.
  3. **Peer Review:** The system invokes the relevant specialized personas (`@architect`, `@backend`, `@frontend`) to verify if the code meets business rules, clean code principles, and security standards.
  4. **Verify:** The task's verification command is executed to ensure it works.
  5. **Error Budget:** If a task fails 3 times, the AI aborts to prevent infinite loops and asks you for human intervention.
  6. **Document:** The `implementation.md` log is updated, the task is marked `[x]`, and the loop moves to `Task 2`.

### Step 3: Review & Ship (The Delivery Phase)
When all tasks in `plan.md` are marked `[x]`, the feature branch is ready.
**Command:** `@[/ship] "feat(auth): add google oauth login"`
* **What happens:** The system verifies there is no "Drift" (mismatch between new code and `docs/`). It consolidates its memory (updates `.codex/knowledge/` if a new technical lesson was learned), merges the branch into `main` via Squash, and pushes to remote.

### 💡 Golden Rule for SDD
If a task is too large, the sub-agent will fail or hallucinate. The core philosophy of SDD is **Atomic Tasks** (5-15 minutes of work per task). If a step in `plan.md` looks too complex, break it down into two or three smaller checkboxes before running `/forge`.
