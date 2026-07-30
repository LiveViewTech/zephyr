## Purpose

Scalable RTOS for resource-constrained devices across many CPU architectures and boards, with a west-managed module ecosystem. See `README.rst`.

## Project Snapshot

- Type: single large RTOS tree (not an app monorepo); apps live under `samples/` / `tests/` or out-of-tree
- Version: `VERSION` (4.x development line)
- Stack: C + CMake + Kconfig + DeviceTree; Python tooling (west, twister); Sphinx docs
- Manifest: `west.yml` (upstream remotes under zephyrproject-rtos)

## Commands

Requires a west workspace with modules fetched (`west update`).

```bash
source zephyr-env.sh
west packages pip --install
west zephyr-export
west sdk install
west update
west build -p always -b <board-target> samples/basic/blinky
west flash
west twister -T samples/hello_world
./scripts/twister
PYTHONPATH=./scripts/tests pytest ./scripts/tests/twister
```

Smoke board targets used in CI include `native_sim`, `qemu_cortex_m0`, `qemu_riscv32` (see `.github/workflows/hello_world_multiplatform.yaml`).

## Conventions

- License: Apache-2.0 with SPDX headers on new files (`CONTRIBUTING.rst`, `.github/copilot-instructions.md`)
- DCO: human `Signed-off-by` on commits (`CONTRIBUTING.rst`)
- Commit titles: subsystem prefix `area: description` (`.gitlint`)
- Ownership: `MAINTAINERS.yml` + `scripts/get_maintainer.py`
- Style/compliance: `.clang-format`, `scripts/checkpatch.pl`, CI workflows under `.github/workflows/`

## Directory Map

- `kernel/` — threads, scheduling, sync, heaps; weak default `main` in `kernel/main_weak.c`
- `drivers/` — Kconfig-gated drivers (`add_subdirectory_ifdef`); consume DT bindings under `dts/bindings/`
- `subsys/` — higher-level stacks (Bluetooth, net, FS, logging, PM, shell, ztest harness)
- `arch/` — per-CPU ports (reset/IRQ/context switch); SoC/board details stay in `soc/` / `boards/`
- `boards/` — `west build -b` targets (`board.yml` + DT), organized by vendor
- `soc/` — SoC bring-up/Kconfig bridging `arch/` and `boards/`
- `dts/` — shared `.dtsi` and YAML bindings; follow `dts/binding-template.yaml`
- `include/` — public APIs under `include/zephyr/` (implementations live elsewhere)
- `scripts/` — twister, west extensions (`scripts/west-commands.yml`), requirements pins for CI
- `tests/` — twister suites via per-dir `tests.yaml` (host twister logic tested under `scripts/tests/`)
- `samples/` — example apps (`find_package(Zephyr)`); prefer `samples/hello_world` as the template
- `doc/` — Sphinx docs (`doc/Makefile`, `doc/requirements.txt`); CI in `.github/workflows/doc-build.yml`
- `cmake/` — toolchain/link/Kconfig helpers loaded by app `find_package(Zephyr)`
- `modules/` — CMake/Kconfig glue for west-fetched externals (sources live at `west.yml` paths)
- `lib/` — shared OS/libc/utility libraries compiled into the image via Kconfig

## Gotchas

- **Root CMake is not an app**: configuring with this tree as `CMAKE_SOURCE_DIR` fatals; use an app dir such as `samples/hello_world` (`CMakeLists.txt`).
- **Modules required**: many boards/drivers need `west update` checkouts from `west.yml` (mcuboot, HALs, mbedtls, TF-M, …).
- **Board target syntax**: multi-core boards need SoC/CPU qualifiers (e.g. `nrf5340dk/nrf5340/cpuapp`) — see `doc/develop/getting_started/index.rst`.
- Default `west.yml` `group-filter` excludes `babblesim`, `optional`, and `testing` groups.
