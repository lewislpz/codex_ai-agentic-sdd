# codex_ai-agentic-sdd

Language / Idioma: [English](README.en.md) | [Español](README.es.md)

Orchestration template for Codex-assisted development with a guided, verifiable workflow and living documentation.

## What does this repository do?
This repository is not a final application. It defines an **operating model** so agents and developers can collaborate with clear rules across the full delivery lifecycle:

- planning (`think`)
- implementation (`forge`)
- validation (`test`)
- review (`audit`)
- delivery (`ship` / `pr`)

Core behavior is documented through contracts in `docs/` and `.codex/`.

## Practical value
It helps standardize AI-assisted work in real repositories, reducing ambiguity and improving traceability:

- defines responsibilities by phase and role
- centralizes reusable policies and prompts
- enforces validation before publishing changes
- keeps documentation and implementation aligned

It works as a base for teams that want a repeatable agentic workflow without locking into a specific frontend/backend stack.

## Key structure
- `docs/`: repository contracts (architecture, commands, security, stack)
- `.codex/policies/`: stable invariants and rules
- `.codex/prompts/`: phase entrypoints
- `.codex/roles/`: role responsibilities
- `.codex/knowledge/`: reusable heuristics and standards

## Recommended flow
1. Run `/think` to generate a plan.
2. Implement with `/forge execute` on a feature branch.
3. Verify with `/test` (or repository validation commands).
4. Review and deliver with `/ship` or `/pr`.

## Project status
Active, stack-agnostic template designed to adapt to product repositories without imposing a framework.
