# Strict Domain Boundaries

## Purpose
To ensure 100% adherence to Separation of Concerns and prevent context pollution or disastrous cross-layer modifications by an Agent operating under a specialized context.

## The Iron Rule
**An agent acting under a specific role must NEVER touch code, configuration, or documentation belonging to another domain without explicit and documented authorization.**

## Domain Definitions & Forbidden Actions

### 1. The `@backend` Agent
- **Domain**: `src/main/java/`, `src/main/resources/`, `pom.xml`, backend tests.
- **Forbidden**: Cannot read, edit, or parse any `.ts`, `.tsx`, or `.css` files located in the frontend `/src` directory. Cannot modify `package.json`.

### 2. The `@frontend` Agent
- **Domain**: `src/`, `package.json`, `tailwind.config.mjs`, frontend testing infra.
- **Forbidden**: Cannot touch `.java`, `application.yml`, Dockerfiles, or anything related to the Spring Boot persistence and controller logic.

### 3. The `@architect` Agent
- **Domain**: `docs/`, `.codex/`, `docker-compose.yml`, cloud configuration.
- **Forbidden**: Cannot make implementation-level code changes (like building a React component or a Java method algorithm). The architect specifies the design and creates the plan; implementation is delegated to frontend/backend roles.

## Error Prevention
If an agent realizes it needs to modify a file outside its active domain, it MUST output a warning to the user and request a handover to the correct agent logic, rather than attempting to guess the syntax or architecture of a stack it hasn't loaded context for.
