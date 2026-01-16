# Changelog

All notable changes to this project will be documented in this file.

## [1.0.3] - 2026-01-16

### Added
- `-post` flag to run DDSCAT `ddpostprocess` either independently or after `-run`.
- Support for `DDPOST_EXE` and `DDPOST_PAR` environment variables.

## [1.0.2] - 2026-01-16

### Added
- Added `run() -> int` to allow running ddscatcli from Python code.
- Added `--diels file1 file2 ...` as an alternative to repeating `-DIEL`.

### Changed
- Default path resolution:
  - `ddscat.par` is searched in `$DDSCAT_PAR`, otherwise `./ddscat.par` (current working directory).
  - `ddscat` executable is searched in `$DDSCAT_EXE`, otherwise `./ddscat`, otherwise `ddscat` on `PATH`.
  - Relative paths in `$DDSCAT_PAR` and `$DDSCAT_EXE` are resolved relative to the current working directory.
- Scalar CLI options now error if provided multiple times (prevents silent overrides).
- Dielectric handling is stricter when `-NCOMP` is provided: the number of dielectric entries must match `NCOMP` exactly.
- Zenodo DOI now link to the Concept DOI

### Fixed
- `ddscat` on `PATH` is now properly detected (via `shutil.which`).

## [1.0.1] - 2025-10-31
- Initial public release.