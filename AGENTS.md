## Purpose

Scalable RTOS for resource-constrained devices across many CPU architectures and boards, with a west-managed module ecosystem. See `README.rst`.

## Project Snapshot

- Type: single large RTOS tree (not an app monorepo); apps live under `samples/` / `tests/` or out-of-tree
- Version: `VERSION` (4.x development line)
- Stack: C + CMake + Kconfig + DeviceTree; Python tooling (west, twister); Sphinx docs
- Manifest: `west.yml` (upstream remotes under zephyrproject-rtos)
- Area guides: see Directory Map below

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

- `kernel/` → `kernel/AGENTS.md`
- `drivers/` → `drivers/AGENTS.md`
- `subsys/` → `subsys/AGENTS.md`
- `arch/` → `arch/AGENTS.md`
- `boards/` → `boards/AGENTS.md`
- `soc/` → `soc/AGENTS.md`
- `dts/` → `dts/AGENTS.md`
- `include/` → `include/AGENTS.md`
- `scripts/` → `scripts/AGENTS.md`
- `tests/` → `tests/AGENTS.md`
- `samples/` → `samples/AGENTS.md`
- `doc/` → `doc/AGENTS.md`
- `cmake/` → `cmake/AGENTS.md`
- `modules/` → `modules/AGENTS.md`
- `lib/` → `lib/AGENTS.md`

## Gotchas

- **Root CMake is not an app**: configuring with this tree as `CMAKE_SOURCE_DIR` fatals; use an app dir such as `samples/hello_world` (`CMakeLists.txt`).
- **Modules required**: many boards/drivers need `west update` checkouts from `west.yml` (mcuboot, HALs, mbedtls, TF-M, …).
- **Board target syntax**: multi-core boards need SoC/CPU qualifiers (e.g. `nrf5340dk/nrf5340/cpuapp`) — see `doc/develop/getting_started/index.rst`.
- Default `west.yml` `group-filter` excludes `babblesim`, `optional`, and `testing` groups.
