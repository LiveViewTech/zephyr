## Context

Core RTOS services: threads, scheduling, synchronization, heaps, IRQ helpers, and boot/init. Supplies a weak `main` when the application omits one (`kernel/main_weak.c`).

## Tech

- Language: C
- Build: `kernel/CMakeLists.txt`, `kernel/Kconfig*`
- Public API: `include/zephyr/kernel.h`

## Architecture

App `main` runs after kernel init (`kernel/init.c`). Scheduler and primitives live alongside device/IRQ helpers. Linked as the kernel library into the Zephyr image, not as a standalone binary.

## Patterns

- DO: extend kernel behavior via existing `kernel_sources` / `kernel_sources_ifdef` hooks in `kernel/CMakeLists.txt`
- DO: keep public APIs in `include/zephyr/`; keep internals in `kernel/include/` / `kernel_internal.h`
- DON'T: put board- or SoC-specific code here — use `boards/`, `soc/`, or `arch/`
- DON'T: assume a strong `main` always exists — see `kernel/main_weak.c`

## Key Files

- `kernel/init.c` — boot/init path
- `kernel/main_weak.c` — weak default `main`
- `kernel/CMakeLists.txt` — source selection
- `include/zephyr/kernel.h` — public kernel API
