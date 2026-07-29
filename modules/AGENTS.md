## Context

Integration glue for west-fetched external projects (HALs, crypto, filesystems, TF-M, GUI, …). Module source often lives outside this directory after `west update`.

## Tech

- Config: `modules/Kconfig` (+ per-module Kconfig fragments)
- Manifest paths: `west.yml` (`modules/hal/*`, `modules/crypto/mbedtls`, `bootloader/mcuboot`, …)
- Optional extras: `submanifests/optional.yaml`

## Architecture

West places module checkouts at paths declared in `west.yml`. CMake/Kconfig glue under `modules/` wires them into the build when selected. Binary blob handling and taint flags are expressed in `modules/Kconfig`.

## Patterns

- DO: add or revise module revisions in `west.yml` (keep sorted) and matching glue under `modules/`
- DO: document required west groups when a feature needs `babblesim` / `optional` / `testing`
- DON'T: vendor large third-party trees into `modules/` when west already manages them
- DON'T: expect filtered groups to exist after a default `west update`

## Key Files

- `west.yml`
- `modules/Kconfig`
- `submanifests/optional.yaml`
- `submanifests/README.txt`
