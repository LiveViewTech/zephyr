## Context

CMake modules and helpers for toolchains, linking, Kconfig integration, SCA, flashing, and Zephyr package export.

## Tech

- Language: CMake (`.cmake` modules)
- Root consumer: repo `CMakeLists.txt` (kernel/image orchestration)
- Extensions: `cmake/modules/extensions.cmake`
- Toolchain: `cmake/toolchain/`, `cmake/compiler/`

## Architecture

Application `find_package(Zephyr)` loads this infrastructure. Multi-pass linking and generated artifacts (ISR tables, device deps, syscall tables) are coordinated from the root `CMakeLists.txt` using helpers here.

## Patterns

- DO: reuse helpers in `cmake/modules/` instead of copying toolchain logic into apps
- DO: verify toolchain with existing `cmake/verify-toolchain.cmake` flows
- DON'T: treat repo-root `CMakeLists.txt` as an application `project()` entry
- DON'T: bypass `west build` / Zephyr package export when integrating out-of-tree apps (`west zephyr-export`)

## Key Files

- `cmake/modules/extensions.cmake`
- `cmake/verify-toolchain.cmake`
- `CMakeLists.txt` — image link stages / orchestration
- `samples/hello_world/CMakeLists.txt` — app-side `find_package(Zephyr)`
