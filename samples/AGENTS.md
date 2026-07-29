## Context

Example applications demonstrating APIs and serving as CI/build smoke targets. Canonical minimal app: `samples/hello_world`.

## Tech

- Build: each sample has `CMakeLists.txt` with `find_package(Zephyr)` and `target_sources(app …)`
- Config: `prj.conf` (+ optional overlays)
- Twister metadata: `tests.yaml` / sample YAML where present

## Architecture

Samples are real applications. `west build -b <board> samples/...` configures Zephyr against the sample as `CMAKE_SOURCE_DIR`. CI builds hello_world variants via `west twister -T samples/hello_world` (`.github/workflows/hello_world_multiplatform.yaml`).

## Patterns

- DO: copy structure from `samples/hello_world/` (`CMakeLists.txt`, `prj.conf`, `src/main.c`)
- DO: keep samples focused; put deep verification under `tests/`
- DON'T: invoke CMake on the Zephyr repo root as the app (`CMakeLists.txt` at repo root fatals)
- DON'T: hard-code a single board in CMake — take `-b` / twister platform

## Key Files

- `samples/hello_world/CMakeLists.txt`
- `samples/hello_world/src/main.c`
- `samples/hello_world/prj.conf`
- `samples/basic/blinky/` — getting-started build target
- `samples/index.rst`
