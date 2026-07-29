## Context

Architecture ports (ARM, ARM64, RISC-V, x86, Xtensa, ARC, …): reset/exception entry, IRQ, context switch, and arch Kconfig.

## Tech

- Languages: C, assembly
- Build: `arch/CMakeLists.txt`, `arch/Kconfig`, `arch/archs.yml`
- Tree: one directory per architecture under `arch/`

## Architecture

Board/SoC selection pulls the matching arch sources into the image. Early boot (e.g. Cortex-M reset) lives in arch assembly before kernel C init runs.

## Patterns

- DO: keep arch-specific assembly and IRQ glue under the owning `arch/<name>/` tree
- DO: expose portable hooks the kernel already calls; avoid inventing parallel boot paths
- DON'T: put SoC clock/pinctrl details here — belong in `soc/` / `boards/` / drivers
- DON'T: break the common arch interface expected by `kernel/` and `include/zephyr/arch/`

## Key Files

- `arch/CMakeLists.txt` — arch selection
- `arch/Kconfig` — arch options
- `arch/archs.yml` — architecture metadata
- `arch/arm/core/cortex_m/reset.S` — example reset path
