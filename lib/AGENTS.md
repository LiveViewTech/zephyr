## Context

Support libraries used across the tree: OS utilities (e.g. printk), heaps, libc helpers, SMF, net_buf, and related helpers.

## Tech

- Language: C
- Build: `lib/CMakeLists.txt`, `lib/Kconfig`
- Areas: `lib/os/`, `lib/libc/`, `lib/utils/`, …

## Architecture

Libraries compile into the Zephyr image based on Kconfig. They provide shared helpers above the raw kernel and below subsystem/driver logic.

## Patterns

- DO: place reusable non-driver helpers here when multiple subsystems need them
- DO: gate optional pieces with Kconfig consistent with `lib/Kconfig`
- DON'T: put hardware-specific register code here — use `drivers/` / `soc/`
- DON'T: introduce new public APIs without headers under `include/zephyr/`

## Key Files

- `lib/CMakeLists.txt`
- `lib/Kconfig`
- `lib/os/` — OS utility sources
- `include/zephyr/` — corresponding public headers
