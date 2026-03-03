# Security Publishing Guide

## Goal
Publish this workspace without leaking credentials, local state, logs, or planning artifacts.

## Classification (Denylist/Allowlist)
Run:

```bash
./scripts/repo-audit.sh
```

Default denylist:
- `.codex/auth.json`
- `.codex/history.jsonl`
- `.codex/log/`
- `.codex/state_*.sqlite*`
- `.codex/sessions/`
- `.codex/tmp/`
- `.orchestrator/plans/`

## Pre-Publish Checklist
1. Ensure `.gitignore` contains required security patterns.
2. Run `./scripts/prepublish-check.sh`.
3. If using git, confirm no sensitive files are tracked.
4. Resolve scanner findings before any push.

## Local Hook Setup
```bash
pre-commit install
pre-commit install --hook-type pre-push
```

## CI Enforcement
Use `.github/workflows/secrets-scan.yml` to block merges when secret scanning fails.

## Incident Response
1. Revoke/rotate leaked credentials immediately.
2. Remove secrets from history (`git filter-repo` or equivalent).
3. Force secret scan pass before reopening PR.
4. Document root cause and prevention updates.
