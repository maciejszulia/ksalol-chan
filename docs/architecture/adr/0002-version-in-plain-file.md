# ADR 0002: Keep the version in a plain `version` file

## Status

Accepted. The `version` file appeared in commit `8d6b1b9`; `version_updater.py` was finished in commit `8279372`.

## Context

The bot prints its version at start. The project has no package metadata (`setup.py` or `pyproject.toml`).

## Decision

The first line of the file `version` holds the version number. `version_helper.get_version()` reads that line.
`version_updater.py` appends the lines of `.git/COMMIT_EDITMSG` with a timestamp to the same file, so the file is
also a short change log.

## Consequences

- The version needs no build tool.
- The updater runs only when the owner runs it; no Git hook calls it (`todo.md` lists this as open work).
- Version number and change log share 1 file, so `get_version()` depends on the first line staying the number.

## Evidence

- `version`, `version_helper.py`, `version_updater.py`, `todo.md`
- commits `8d6b1b9`, `8279372`
