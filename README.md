# ddscatcli
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17493075.svg)](https://doi.org/10.5281/zenodo.17493075)
[![PyPI](https://img.shields.io/pypi/v/ddscatcli.svg)](https://pypi.org/project/ddscatcli/)

This script is a command-line utility to edit and run a `ddscat.par` file for DDSCAT in a reproducible and automated way.

It allows you to:

* Modify parameters inside a single `ddscat.par` configuration file (shape, solver, FFT method, dielectric files, wavelength, etc.).
* Run DDSCAT automatically — serial, MPI, or OpenMP.
* Create timestamped backups of the original `ddscat.par` file.
* Uses environment variables for configuration (no code editing).

---

## Configuration

Set your paths using environment variables:

```bash
export DDSCAT_PAR=/path/to/ddscat.par
export DDSCAT_EXE=/path/to/ddscat
```

---

## Installation

Install from PyPI:

```bash
pip install ddscatcli
```

This installs the `ddscatcli` command globally. If you prefer to keep it isolated in a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate   # on Linux/macOS
# .venv\Scripts\activate    # on Windows

pip install ddscatcli
```

---

## Requirements

* **Python 3.8>=**
* Standard library only 

---

## Usage

1. Get help and options:

   ```bash
   ddscatcli -h
   ```

2. List available shapes:

   ```bash
   ddscatcli -CSHAPE -h
   ```

3. Run modes:

   * `-dry-run` → preview the edits only (no file modification).
   * (no flag) → apply edits to `ddscat.par`.
   * `-run` → apply edits and automatically run DDSCAT.

4. Parallel options:

   * `-omp-threads N` → set the number of OpenMP threads.
   * `-mpi [launcher] -np N` → run DDSCAT with MPI (e.g. `mpirun`, `mpiexec`, `srun`).

---

## Examples

Preview edits without modifying:

```bash
ddscatcli -CSHAPE ANIRCTNGL -dry-run
```

Change the shape and run immediately:

```bash
ddscatcli -CSHAPE ELLIPSOID -SHPAR "16 8 4" -run
```

Set OpenMP threads:

```bash
ddscatcli -omp-threads 16 -run
```

---

## Backups

Every modification automatically creates a timestamped backup:

```
ddscat.par.bak.YYYYMMDD-HHMMSS
```

---

## Notes

* Each parameter is matched using its identifying keyword in the `ddscat.par` file.
* Supports dielectric and shape overrides via `-DIEL`, `-NCOMP`, `-SHPAR`, etc.
* DDSCAT must be compiled and installed separately — this tool just wraps it.

---

## License

This project is licensed under the **GNU General Public License v3.0 (GPLv3)**.
You are free to use, modify, and share it under the same license.

--- 

## Citation

If you use `ddscatcli`, please cite:

> Clément Argentin, **ddscatcli**, v1.0.1 (2025).  
> DOI: [10.5281/zenodo.17493075](https://doi.org/10.5281/zenodo.17493075)

You can click the **“Cite this repository”** button on the right-hand side of the GitHub page for citation formats (BibTeX, APA, etc.).
