## Context

Higher-level subsystems composed into images via Kconfig: Bluetooth, networking, filesystems, logging, PM, DFU/mgmt, shell, and the ztest harness (`subsys/testsuite`).

## Tech

- Language: C
- Build: `subsys/CMakeLists.txt` (sorted `add_subdirectory` / `add_subdirectory_ifdef`)
- Config: `subsys/Kconfig` and per-subsystem Kconfig trees

## Architecture

Subsystems sit above drivers and below applications. Networking (`subsys/net`) and Bluetooth (`subsys/bluetooth`) are large independent stacks. Test infrastructure for in-tree suites lives under `subsys/testsuite/ztest`.

## Patterns

- DO: follow existing Kconfig gates when adding a subsystem directory (`subsys/CMakeLists.txt`)
- DO: put portable protocol/service logic here; put register-level code in `drivers/`
- DON'T: pull optional west modules without documenting the `west.yml` dependency
- DON'T: duplicate kernel primitives — use `include/zephyr/kernel.h` APIs

## Key Files

- `subsys/CMakeLists.txt` — inclusion map
- `subsys/bluetooth/CMakeLists.txt` — Bluetooth stack entry
- `subsys/net/ip/net_core.c` — IP stack core
- `subsys/testsuite/ztest/` — ztest implementation
