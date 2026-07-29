## Context

In-tree verification suites for twister/ztest/BabbleSim covering kernel, drivers, subsystems, and integration scenarios.

## Tech

- Harness: twister (`scripts/twister` / `west twister`)
- On-target/unit API: ztest (`subsys/testsuite/ztest`)
- Bluetooth/radio sim: `tests/bsim` + BabbleSim west projects
- Config: `tests/test_config.yaml`, `tests/test_config_ci.yaml`

## Architecture

Each suite directory carries `tests.yaml` (or sample metadata) discovered by twister. Platforms may be QEMU, `native_sim`, hardware, or bsim. Host-side twister logic is tested with pytest under `scripts/tests/`.

## Patterns

- DO: add scenarios via `tests.yaml` next to the test app CMake project
- DO: use ztest APIs from `subsys/testsuite/ztest/include/zephyr/ztest.h`
- DON'T: assume BabbleSim groups are fetched — default `west.yml` `group-filter` excludes `babblesim`
- DON'T: land tests without a platform/filter strategy twister can schedule

## Key Files

- `tests/test_config.yaml`
- `tests/ztest/`
- `tests/bsim/`
- `.github/workflows/twister.yaml`
- `.github/workflows/bsim-tests.yaml`
