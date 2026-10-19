# Data files

This directory contains the classification data produced by
`notebook/EXP033.ipynb`.

## Files

Both classification files are gzipped to keep the repository lightweight.
`gunzip` them to read as plain CSV, or read directly from Python:

    import pandas as pd
    df = pd.read_csv("2d_classification_full.csv.gz")| `data/2d_classification_full.csv.gz` | Full 2D classification: 111,741 parameter-period pairs |

### 2d_classification.csv.gz

Reduced 2D classification. One row per distinct parameter set
`(k, m, rho_x, delta_x, rho_y, delta_y)`, recorded at its smallest revival
period. 18,174 entries.

| Column | Type | Description |
|---|---|---|
| `k` | int | Cycle length of the x-axis |
| `m` | int | Cycle length of the y-axis |
| `N` | int | Smallest revival period |
| `rho_x` | float | Reflection parameter on the x-axis |
| `delta_x` | float | Phase on the x-axis (radians) |
| `rho_y` | float | Reflection parameter on the y-axis |
| `delta_y` | float | Phase on the y-axis (radians) |
| `provenance` | string | 1D signatures that generated the record |

### 2d_classification_full.csv.gz

Full 2D classification. Every revival period at which each parameter set
revives. 111,741 entries. Same columns as above.

### EXP033_1d_verification.txt

Line-by-line verification log for the 174 1D signatures. Each line gives
k, rho, delta, N, the eigenvalue residual, and the source. An entry passes
if the residual is below 1e-6. The source is either a Dukes table reference
or "new" for the two revivals not tabulated by Dukes.

### 2d_classification.hash

SHA-256 fingerprint of the notebook inputs. Used to detect whether the 2D
search needs to re-run. Delete this file to force a fresh search on the next
notebook run.

## Reproducing the data

Run `notebook/EXP033.ipynb` from the repository root. The notebook writes all
four files to this directory. To force a re-run even when the hash matches:

    EXP033_FORCE_RERUN=1 jupyter notebook notebook/EXP033.ipynb

## License

These data files are licensed under CC-BY 4.0. See `../LICENSE-DATA`.
