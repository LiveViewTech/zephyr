## Context

SoC-level support bridging architecture ports and boards: clocks, memory maps, SoC Kconfig, and vendor SoC CMake packages.

## Tech

- Language: C (+ linker/Kconfig)
- Build: `soc/CMakeLists.txt`, `soc/Kconfig`, `soc/Kconfig.v2`
- Layout: vendor directories under `soc/`

## Architecture

Board selection resolves a SoC. SoC code provides early hardware bring-up and config symbols boards and drivers depend on. DT SoC `.dtsi` includes often live under `dts/` with SoC C glue here.

## Patterns

- DO: mirror existing vendor directory layout when adding a SoC
- DO: keep board-only peripherals/overlays in `boards/`, not here
- DON'T: fork arch exception/reset code into SoC trees without following existing arch hooks
- DON'T: introduce undocumented binary blobs — see `modules/Kconfig` blob/taint options

## Key Files

- `soc/CMakeLists.txt`
- `soc/Kconfig`
- `soc/Kconfig.v2`
- `modules/Kconfig` — blob/taint related options
