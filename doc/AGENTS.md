## Context

Sphinx documentation tree: introduction, getting started, kernel/services references, and contributor guides.

## Tech

- Sphinx: `doc/conf.py`, `doc/Makefile`
- Python deps: `doc/requirements.txt`
- Content: reStructuredText under `doc/`
- Optional JS for diagrams: `doc/package.json` (d3, mermaid)

## Architecture

Docs build separately from firmware images. Getting started (`doc/develop/getting_started/index.rst`) is the authoritative host setup / `west` command sequence. CI: `.github/workflows/doc-build.yml`.

## Patterns

- DO: link APIs/samples with existing Zephyr Sphinx roles rather than duplicating code
- DO: keep command examples identical to scripts/CI when documenting workflows
- DON'T: document APIs that disagree with headers under `include/zephyr/`
- DON'T: treat `doc/package.json` as the firmware package manifest — it is docs-only

## Key Files

- `doc/conf.py`
- `doc/Makefile`
- `doc/requirements.txt`
- `doc/develop/getting_started/index.rst`
- `.github/workflows/doc-build.yml`
