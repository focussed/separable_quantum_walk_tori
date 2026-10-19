# Separable Quantum Walks on Tori

Research paper, programs, and dataset for the complete classification of
full-state revivals on separable discrete-time quantum walks over
two-dimensional toroidal lattices.

## Contents

| Path | Contents |
|---|---|
| `paper/` | Manuscript source: LaTeX components, bibliography, build files |
| `paper/main.tex` | Assembled LaTeX source, ready to compile |
| `notebook/EXP033.ipynb` | Analysis notebook that builds and verifies the classification |
| `data/2d_classification.csv.gz` | Reduced 2D classification: 18,174 parameter sets |
| `data/2d_classification_full.csv.gz` | Full 2D classification: 111,741 parameter-period pairs |
| `data/EXP033_1d_verification.txt` | Operator-level verification log for the 174 1D signatures |
| `data/2d_classification.hash` | SHA-256 fingerprint of the notebook inputs |
| `figures/` | The four fidelity and distribution plots from the paper |

The manuscript is archived on Zenodo: [DOI placeholder]

## The paper

**Title:** Complete Classification of Full-State Revivals on Separable Quantum Walks on Tori

**Authors:** Ian Craig (Atlantic Technological University, Sligo) and Michael McGetterick (University of Galway)

**Abstract (short).** A quantum walk revives when it returns exactly to its
starting state after some number of steps. We classify which toroidal
lattices support revivals for the separable coin family of Dukes, and for
which coin parameters. Exactly seven cycle lengths admit a 1D revival,
k in {2, 3, 4, 5, 6, 8, 10}; the 2D walk factorises as a tensor product, so
a torus revives whenever both axes revive at a common period. This gives
28 tori, 59 periods, and 18,174 reduced parameter sets. Two revivals beyond
Dukes' tabulation are found, at k = 2 and k = 4, both at delta = pi/2,
rho = 1/2, N = 6.

## Results at a glance

- **1D signatures verified:** 174, 0 failures. Worst residual 2.3 x 10^-13.
- **Reduced 2D parameter sets:** 18,174.
- **Full 2D records (parameter-period pairs):** 111,741.
- **Distinct tori:** 28.
- **Distinct periods:** 59 (smallest N = 2, largest N = 420).

## Reproducing the results

### Requirements

    Python 3.9+
    numpy
    matplotlib

### Run the notebook

    jupyter notebook notebook/EXP033.ipynb

Or open it in Google Colab. The notebook proceeds in three stages:

1. **Direct demonstration** of the two new 1D revivals (k = 2 and k = 4 at
   delta = pi/2, rho = 1/2, N = 6), with two Dukes revivals as controls.
2. **1D revival verification** of the complete Dukes signature set (174
   quadruples) at the operator level, using the eigenvalue residual.
3. **2D revival search** via the tensor-product construction, producing the
   reduced classification (one row per parameter set) and the full
   classification (one row per parameter-period pair).

The notebook writes its outputs to `data/`. A SHA-256 hash of the input
signature set is stored in `data/2d_classification.hash`; if the inputs are
unchanged and the CSVs exist, the search is skipped and the existing results
are loaded. To force a re-run:

    EXP033_FORCE_RERUN=1 jupyter notebook notebook/EXP033.ipynb

### Compile the paper

The paper uses the `revtex4-2` document class (APS Physical Review A).
Compile `paper/main.tex` with `pdflatex` and `bibtex`:

    cd paper
    pdflatex main
    bibtex main
    pdflatex main
    pdflatex main

Or upload the `paper/` directory to Overleaf as a new project.

## The data files

The classification CSVs are gzipped (`.csv.gz`); decompress with `gunzip`
or read directly with `pandas.read_csv()`.

### 2d_classification.csv.gz

One row per distinct parameter set `(k, m, rho_x, delta_x, rho_y, delta_y)`,
recorded at its smallest revival period. 18,174 entries.

Columns: `k`, `m`, `N`, `rho_x`, `delta_x`, `rho_y`, `delta_y`, `provenance`.

The `provenance` column records which 1D signatures generated the record, in
the form `k-axis source | m-axis source`.

### 2d_classification_full.csv.gz

Every revival period at which each parameter set revives. 111,741 entries.
Same columns as above.

### EXP033_1d_verification.txt

Line-by-line verification log for the 174 1D signatures. Each line gives
`k`, `rho`, `delta`, `N`, the eigenvalue residual, and the source (Dukes
table or "new").

## The classification in brief

### 1D revivals

Seven cycle lengths admit a non-trivial full-state revival:
k in {2, 3, 4, 5, 6, 8, 10}. An exhaustive search over the remaining cycle
lengths up to k = 16 finds no revival within N <= 60 steps.

The two revivals not tabulated by Dukes are at k = 2 and k = 4, both at
delta = pi/2, rho = 1/2, N = 6. They share a common eigenvalue structure:
the eigenphases pi/12 and 5pi/12 appear in the spectrum for every admissible k.

### 2D revivals

The separable walk on a k x m torus factorises as U_{kxm} = U_k tensor U_m,
so a torus revives whenever both axes revive at a common period. This gives
28 tori and 59 distinct periods.

In 1D, the phase parameter delta affects only the eigenvectors and does not
change the revival period. In 2D, the phases of the two factors must be
compatible, and delta becomes a selection mechanism. Only 25.9% of the
reduced classification uses zero phases on both axes; 48.9% has zero on
exactly one axis; 5.0% has equal non-zero phases; 20.2% has unequal non-zero
phases.

## Open problem

We conjecture that no cycle length k not in {2, 3, 4, 5, 6, 8, 10} admits a
1D full-state revival at any period or any coin parameter rho in (0,1). The
paper sketches a cyclotomic-field argument: the mode-ratio elimination of rho
produces a condition on the algebraic degree of 2cos(2pi/k), which restricts
the admissible k. The general case k >= 11 remains open.

## Citation

If you use this code or data, please cite the paper:

    @article{Craig2026,
      title = {Complete Classification of Full-State Revivals on Separable
               Quantum Walks on Tori},
      author = {Craig, Ian and McGetterick, Michael},
      year = {2026},
      note = {Manuscript submitted to Physical Review A}
    }

## License

Code: MIT. Data and figures: CC-BY 4.0. See `LICENSE` and `LICENSE-DATA`
for details.
