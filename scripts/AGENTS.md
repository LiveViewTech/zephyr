## Context

Python/west tooling: twister, west extensions, Kconfig/DT helpers, compliance, and requirement pins for CI/dev.

## Tech

- Language: Python 3
- West commands: `scripts/west-commands.yml` → `scripts/west_commands/`
- Twister entry: `scripts/twister`
- Deps: `scripts/requirements*.txt` (base/build-test/run-test/compliance/actions)

## Architecture

`west` loads extensions from this tree. Twister scans `tests.yaml` metadata and builds/runs suites. CI installs hashed requirements (`scripts/requirements-actions.txt`) and invokes twister/pytest.

## Patterns

- DO: add west commands via `scripts/west-commands.yml` + module under `scripts/west_commands/`
- DO: put twister unit tests under `scripts/tests/twister` (see `.github/workflows/twister_tests.yml`)
- DON'T: change action requirement hashes without regenerating pins used by CI
- DON'T: call twister APIs without setting `PYTHONPATH` as CI does for pytest runs

## Key Files

- `scripts/twister`
- `scripts/west-commands.yml`
- `scripts/requirements-base.txt`
- `scripts/requirements.txt`
- `.github/workflows/twister_tests.yml`
