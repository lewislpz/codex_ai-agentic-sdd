---
description: Professional and complete testing prompt (Unit, Integration, E2E, TDD).
---

// turbo-all

# Test Prompt

**Goal**: Drive a professional and complete testing process for any feature or module. This prompt ensures high coverage, follows **TDD (Test-Driven Development)**, handles **Mocks/Factories** correctly, and validates the implementation against business requirements.

---

## Phase 0: Setup Workspace & Analysis

1. **Initialize Git Branch**:
   ```bash
   git checkout main && \
   git pull origin main && \
   export BRANCH_NAME="test/$(date +'%H%M')-<SLUG>" && \
   git checkout -b "$BRANCH_NAME"
   ```

2. **Initialize Workspace Directory**:
   ```bash
   export PLAN_PATH=".orchestrator/plans/$(date +'%Y-%m-%d-%H-%M')-test-<SLUG>" && \
   mkdir -p "$PLAN_PATH" && \
   echo "Test Workspace Ready: $PLAN_PATH on branch $BRANCH_NAME"
   ```

3. **Create Status Tracker** — Create `$PLAN_PATH/status.md`:
   ```markdown
   # Status: Test <SLUG>
   | Phase                | Status  |
   |----------------------|---------|
   | 1. Test Matrix       | pending |
   | 2. Setup & Factories | pending |
   | 3. TDD Implementation| pending |
   | 4. Quality Gate      | pending |

   Branch: `<BRANCH_NAME>`
   Created: <ISO_TIMESTAMP>
   ```

---

## Phase 1: Test Matrix & Strategy

> Uses: `software-architecture`, `testing-patterns` skills

### 1A — Requirement Analysis
- Identify the target components (Service, Controller, Hook, UI).
- Define "Happy Path" and "Edge Cases" (Gherkin style: Given/When/Then).
- Determine test levels:
  - **Unit**: Business logic, pure functions.
  - **Integration**: DB interactions (JPA), API contracts (WebMvc), Hooks/Store (FE).
  - **E2E**: Full flows (optional, use if specified).

### 1B — Generate `$PLAN_PATH/test-matrix.md`
```markdown
# Test Matrix: [Name]

## Requirements
- [ ] Req 1: ...
- [ ] Req 2: ...

## Scenarios
### 🟢 Happy Path
- **Scenario**: [Name]
  - Given: [State]
  - When: [Action]
  - Then: [Result]

### 🔴 Edge Cases & Errors
- **Scenario**: [Error case]
  - Given: [Invalid State]
  - When: [Action]
  - Then: [Expected Exception/Error State]

## Coverage Plan
- [ ] Module X: Unit (Logic)
- [ ] Module Y: Integration (Persistence)
```

### 1C — Checkpoint
Update `$PLAN_PATH/status.md` → 1. Test Matrix: `done`.

---

## Phase 2: Testing Infrastructure & Data

### 2A — Dependency Audit
- **Backend (Spring)**: Check `pom.xml` for `spring-boot-starter-test`, `mockito`, `assertj`. Install `RestAssured` or `Testcontainers` if needed.
- **Frontend (React)**: Check `package.json` for `vitest`, `@testing-library/react`, `msw`. If missing, INSTALL immediately.

### 2B — Data Factories & Mocks
- **Factories**: Create/Update `TapaFactory`, `RestaurantFactory`, etc. (TS or Java). Use Lombok/Records or Object Builders.
- **Mocks**: Configure MSW handlers for FE or Mockito mocks for BE.

### 2C — Checkpoint
Update `$PLAN_PATH/status.md` → 2. Setup & Factories: `done`.

---

## Phase 3: TDD Implementation (Implementation Loop)

> Uses: `subagent-driven-development`, `clean-code`, `testing-patterns` skills

Follow the **Red-Green-Refactor** cycle for each scenario in the matrix.

### 🛑 RED: Write Failing Tests
For each scenario:
1. Create the test file (if it doesn't exist).
2. Implement the test case representing the scenario.
3. **Verify**: Run the test and ensure it **FAILS** for the right reason.

### 🟢 GREEN: Implement Minimal Code
1. Write the minimal production code to pass the test.
2. Avoid over-engineering.
3. **Verify**: Run the test and ensure it **PASSES**.

### 🔵 REFACTOR: Polish
1. Clean up duplicating code in tests or production.
2. Ensure variable names are descriptive.
3. **Verify**: All tests still pass.

### 🛑 ERROR BUDGET
- **Maximum 3 consecutive failures** per test scenario. If a test fails after 3 attempts at fixing the code, **ABORT** the automated TDD loop. Document the persistent error and ask the user for guidance. Do NOT enter an infinite loop of guessing.

### 3D — Checkpoint
Update `$PLAN_PATH/status.md` → 3. TDD Implementation: `done`.

---

## Phase 4: Quality Gate & Validation

### 4A — Full Suite Execution
Run all tests in the module/project:
- `mvn test` (Backend)
- `npm test` / `vitest run` (Frontend)

### 4B — Coverage Report
Check coverage (aiming for metrics specified in `test-matrix.md` or 80%+).
- Backend: `mvn jacoco:report` (if configured).
- Frontend: `vitest run --coverage`.

### 4C — Final Verification
Ensure all scenarios in `test-matrix.md` are tagged as `[x]`.

### 4D — Documentation Update
Update `docs/` if test patterns changed or new standards were introduced.

---

## Phase 5: Wrap-Up

Present the final state:
1. **Pass Rate**: [X/X] tests passed.
2. **Coverage**: [X]% coverage.
3. **Key Findings**: Any bugs found and fixed during TDD.
4. **Next step**: Suggest `"/ship 'test: coverage for <feature>'"` when ready.

---

## Global Rules

- **NEVER SKIP THE RED PHASE**: A test that passes without code changes is either testing nothing or implementation-coupled.
- **MOCK EXTERNAL SYSTEMS**: Never hit real external APIs (SMSGateway, Payment) in unit/integration tests. Use Mocks or Stubs.
- **ISOLATION**: Each test must be independent. Clear DB/Mocks in `@BeforeEach`.
- **BEHAVIOR OVER IMPLEMENTATION**: Test what the code DOES, not HOW it does it.
- **Skill Map**:
  - Phase 1 → `software-architecture`, `testing-patterns`
  - Phase 2 → `testing-patterns`, `backend-dev-guidelines`, `frontend-dev-guidelines`
  - Phase 3 → `subagent-driven-development`, `clean-code`, `testing-patterns`
  - Phase 4 → `testing-patterns`
- **AUTOPILOT**: Proceed through ALL phases automatically.
- **SAFE TO AUTO-RUN**: Use `SafeToAutoRun: true` for all commands.
