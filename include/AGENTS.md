## Context

Public C API headers under `include/zephyr/` for kernel, drivers, subsystems, and arch interfaces.

## Tech

- Language: C headers
- Primary umbrella: `include/zephyr/kernel.h`
- Driver APIs: `include/zephyr/drivers/`

## Architecture

Applications and in-tree code include these headers. Syscall/userspace generation consults annotated APIs. Implementation lives in `kernel/`, `drivers/`, `subsys/`, `lib/`, not under `include/`.

## Patterns

- DO: add public APIs here with subsystem prefixes (`k_`, `sys_`, `net_`, `bt_`, …) per `.github/copilot-instructions.md`
- DO: keep Doxygen comments on public APIs
- DON'T: put `.c` implementation files in this tree
- DON'T: expose unstable internals — prefer `kernel/include/` or local headers

## Key Files

- `include/zephyr/kernel.h`
- `include/zephyr/drivers/`
- `include/zephyr/linker/sections.h`
- `.github/copilot-instructions.md` — naming/API rules
