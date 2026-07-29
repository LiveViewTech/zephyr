## Context

Device driver implementations selected by Kconfig and described by DeviceTree. Large per-subsystem tree (GPIO, UART, flash, Bluetooth controllers, …).

## Tech

- Language: C
- Build: `drivers/CMakeLists.txt` uses `add_subdirectory_ifdef(CONFIG_*)`
- Config: `drivers/Kconfig` plus per-class Kconfig files

## Architecture

Drivers bind to DT nodes via bindings under `dts/bindings/`. Enabled drivers compile into the image; stubs/fakes exist for testing. Prefer existing class APIs in `include/zephyr/drivers/`.

## Patterns

- DO: gate new driver dirs with `add_subdirectory_ifdef` in `drivers/CMakeLists.txt`
- DO: add/extend YAML bindings under `dts/bindings/` when introducing hardware properties
- DON'T: hard-code board pins in the driver — consume DT/`CONFIG_*`
- DON'T: bypass the class API headers under `include/zephyr/drivers/` for in-tree callers

## Key Files

- `drivers/CMakeLists.txt` — subsystem enable map
- `drivers/Kconfig` — driver menuconfig root
- `dts/binding-template.yaml` — binding authoring template
- `include/zephyr/drivers/` — class APIs
