## Context

Board definitions consumed as `west build -b` targets: DeviceTree, board Kconfig, and `board.yml` metadata, organized by vendor.

## Tech

- Artifacts: `*.dts` / overlays, `board.yml`, Kconfig fragments, occasional board C
- Build: `boards/CMakeLists.txt`, `boards/Kconfig`
- Discovery: `scripts/list_boards.py`, `west boards`

## Architecture

A board target selects SoC + CPU cluster + DT. Multi-core boards use qualified names (documented in `doc/develop/getting_started/index.rst`). Shields and snippets layer additional overlays.

## Patterns

- DO: add boards under `boards/<vendor>/<board>/` with `board.yml` + DT matching existing neighbors
- DO: use full board targets including SoC/CPU when required (e.g. `nrf5340dk/nrf5340/cpuapp`)
- DON'T: embed reusable SoC support only in one board — share via `soc/` and `dts/`
- DON'T: assume unqualified board names always configure correctly on multi-core parts

## Key Files

- `boards/CMakeLists.txt`
- `boards/Kconfig`
- `scripts/list_boards.py`
- `doc/develop/getting_started/index.rst` — board target examples
