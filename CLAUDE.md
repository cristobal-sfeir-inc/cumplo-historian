# cumplo-historian

## Overview
Cloud Run service that records, archives, and serves historical data on Cumplo investment
opportunities — acts as the system's long-term data store and query layer.

> **Status: stub.** No code exists yet — only `README.md`, `LICENSE`, and `.github/`. Commands
> below reflect the intended stack; update this file when the first implementation lands.

## Build & Test
_No code yet. When implemented, expected commands will be:_
- Install deps: `poetry install`
- Run tests: `poetry run pytest`
- Auto-fix lint + format: `make format`
- Verify code quality (CI gate): `make lint`
- Full local CI simulation (lint + tests): `make check`

Stack: Python 3.13, FastAPI, Pydantic v2, Poetry. Persistence: Firestore.

## CI
- Only active workflow: `.github/workflows/pr-title.yml` — enforces conventional-commit PR
  titles (`feat:`, `fix:`, `chore:`, etc.) with an uppercase subject.
- A `ci.yml` (lint + tests) and `release.yml` (Cloud Run deploy) do not exist yet; add them
  when the first code lands, following the patterns in sibling services.

## Git workflow
- Branch prefixes: `feat/`, `fix/`, `chore/`, `ci/`. Conventional-commit subjects.
- `master` is protected by the `not-cumplo-audit-gate` ruleset: every change needs a **PR +
  code-owner review** (`@cnsfeir-reviewer`). **Never push to `master` directly.**

## Architecture notes
- Intended role: receives events from the orchestrator via Pub/Sub, persists them to Firestore,
  and exposes a query API for historical investment data.
- Will depend on `cumplo-common` for shared Pydantic models, Firestore client, and Pub/Sub
  middleware — import it via the private Artifact Registry PyPI feed.
- Deployed on Cloud Run; structured Cloud Logging from day one.

## Before committing
After making changes, run the lint/format commands and ensure they pass; check no hardcoded
secrets — before committing.
