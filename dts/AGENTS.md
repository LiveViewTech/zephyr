## Context

Shared DeviceTree includes (`.dtsi`), vendor DT, and YAML bindings that drive generated device configuration at build time.

## Tech

- Formats: `.dts` / `.dtsi` / overlays, YAML bindings
- Config: `dts/Kconfig`
- Template: `dts/binding-template.yaml`
- Bindings tree: `dts/bindings/`

## Architecture

Board DT includes SoC/arch `.dtsi` from here. Bindings define properties consumed by drivers. Build-time DT scripts under `scripts/` generate C headers/linker content from the final DT.

## Patterns

- DO: add bindings under `dts/bindings/<class>/` following `dts/binding-template.yaml`
- DO: put reusable SoC includes under `dts/<arch>/` rather than copying into each board
- DON'T: invent ad-hoc property names without a binding
- DON'T: put board-only wiring in shared `.dtsi` — use board DT / overlays

## Key Files

- `dts/Kconfig`
- `dts/binding-template.yaml`
- `dts/bindings/`
- `scripts/dts/` — DT tooling (when present in tree)
