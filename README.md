# SPTB-RiemannHypothesis
**Author**: Akbar Akbari Esfahani
**Affiliation**: Independent Researcher
**Contact**: akbar.esfahani@gmail.com
**Date**: March 2026

## Witness Functors

Akbar Akbari Esfahani’s November 2026 revision separates what an observation can distinguish from the error of the model fitted to it. It also revisits the spline estimates in the March paper. [Revised manuscript](paper_witness/main.pdf) [Source](paper_witness/main.tex) [Revision record](paper_witness/REVISION_NOTES.md) [Verification](paper_witness/README.md)

---

## Abstract

The Spline-Penalized Tail Bound (SPTB) measures how much of a signal remains after fitting an affine function on each time interval. The March paper proposes using this quantity to detect a zero to the right of a chosen line. The November revision proves exponential growth for a single complex exponential on an interval of fixed width. Detection for the full sum over zeros on the shrinking intervals used in the March paper remains open.

The numerical experiment assigns real part one half to 79 tabulated zeta zero ordinates and adds a synthetic zero to test its effect on the fitted slope. At the largest horizon in the table below, the measured slope for &eta; = 0.0001 differs from 2&eta; by 0.032%. [Numerical results](numerical_analysis/sptb_out/bias_summary.csv)

---

## Quick Start

### Prerequisites
```r
# Required R packages
install.packages(c(
  "data.table", "dplyr", "purrr", "tidyr",
  "ggplot2", "ggrepel", "readr", "stringr",
  "scales", "MASS"
))

# Optional: for arbitrary precision at extreme T
install.packages("Rmpfr")
```

### Running the Analysis
```bash
# 1. Clone the repository
git clone https://github.com/aakbarie/SPTB-RiemannHypothesis.git
cd SPTB-RiemannHypothesis

# Run from the repository root
Rscript numerical_analysis/sptb_analysis.R
ls numerical_analysis/sptb_out/
```

---

## Main Results

### Fitted slopes

![Empirical vs Theory](numerical_analysis/sptb_out/bias_tail_slope_vs_theory.png)

The figure compares the fitted slope with 2&eta; at three horizons for each of three positive values of &eta;.

### Synthetic zeros

![Semilog Action](numerical_analysis/sptb_out/bias_total_diff_grid.png)

Exponential signature when synthetic off-line zeros (&beta; > &sigma;) are introduced.

### Baseline variance

![Variance](numerical_analysis/sptb_out/variance_T_logT_loglogT.png)

The figure compares the baseline energy with T log T log log T at six horizons from 200 to 10,000. [Variance table](numerical_analysis/sptb_out/variance_table.csv)

### Three horizons

| T | &eta; | Empirical slope | Theory (2&eta;) | Rel. Error |
|---|-------|-----------------|-----------------|------------|
| 10<sup>4</sup> | 10<sup>-4</sup> | 2.478 &times; 10<sup>-4</sup> | 2 &times; 10<sup>-4</sup> | 23.9% |
| 2 &times; 10<sup>4</sup> | 10<sup>-4</sup> | 2.078 &times; 10<sup>-4</sup> | 2 &times; 10<sup>-4</sup> | 3.9% |
| 5 &times; 10<sup>4</sup> | 10<sup>-4</sup> | 2.001 &times; 10<sup>-4</sup> | 2 &times; 10<sup>-4</sup> | **0.03%** |

The relative errors decrease over these three runs. The injected frequency also changes with the block width, from 2.1988 at T = 10,000 to 0.45 at T = 50,000. [Fitted slopes and frequencies](numerical_analysis/sptb_out/bias_summary.csv)

---

## Repository Structure
```
SPTB-RiemannHypothesis/
├── paper_witness/            # November revision and verification scripts
├── paper_clean/              # March paper (34 pages)
│   ├── main.tex              # Main document
│   ├── main.pdf              # Compiled PDF
│   ├── parts/
│   │   ├── part1.tex         # Foundations and Variance Regime
│   │   ├── part2.tex         # Bias Regime and Detection Theorem
│   │   ├── part2b_explicit_formula.tex  # Explicit-formula / Turán–Pintz reframe
│   │   ├── part3.tex         # Empirical Validation
│   │   └── part4.tex         # Geometric Framework (heuristic)
│   ├── appendices/
│   │   ├── appA.tex          # Affine-Projection Constants
│   │   ├── appB.tex          # Derivative-Variance Constant
│   │   ├── appC.tex          # Constant-Extraction Methodology
│   │   └── appD.tex          # Dirichlet L-functions Extension
│   ├── figs/                 # Figures (8 PNG files)
│   └── bib/                  # Bibliography
│       └── references.bib
├── numerical_analysis/
│   ├── sptb_analysis.R       # R implementation
│   └── sptb_out/             # Generated output
│       ├── variance_table.csv
│       ├── bias_summary.csv
│       ├── bias_blocks.csv
│       └── *.png             # Figures
├── data/
│   └── zeros_1.txt           # Odlyzko zero ordinates
├── archive/
│   └── paper-legacy-2025-10/ # Earlier paper version (superseded by paper_clean/)
└── README.md
```

---

## Paper

The March manuscript has 34 pages. Sections 10.2 and 10.3 of the November revision give the single-mode theorem, the scaling counterexample and the bound for a damped zeta field. [March paper](paper_clean/main.pdf) [November revision](paper_witness/main.pdf)

### Compilation
```bash
cd paper_clean
pdflatex main.tex && pdflatex main.tex && pdflatex main.tex
```
Run three times to resolve all cross-references and TOC entries.

### Citation
```bibtex
@misc{esfahani2026sptb,
  title={A Structural Spline-Penalized Tail Bound for {$L$}-Functions},
  author={Esfahani, Akbar Akbari},
  year={2026},
  url={https://github.com/aakbarie/SPTB-RiemannHypothesis/blob/def11b359321de71bb2f4e3feb9e58c790d7fd8a/paper_clean/main.pdf}
}
```

---

## Reproducibility

### Computational Environment

- **Software**: R 4.5.1
- **Core packages**: `data.table`, `dplyr`, `purrr`, `tidyr`, `readr`, `stringr`
- **Plotting**: `ggplot2`, `ggrepel`, `scales`
- **Robust regression**: `MASS` (Huber M-estimator for tail slopes)
- **Optional**: `Rmpfr` (arbitrary precision for extreme T)
- **Hardware**: Tested on Apple Silicon (M1/M2) and Intel x86_64
- The main sweep has six baseline runs and nine runs with a synthetic zero.

### Data Sources

- **Odlyzko zeros**: [www-odlyzko.dtc.umn.edu/zeta_tables](https://www-odlyzko.dtc.umn.edu/zeta_tables/)
The analysis uses the 79 positive ordinates at or below 200. The input file supplies their imaginary parts. The R loader assigns real part one half and weight two to account for each conjugate pair. [Input table](data/zeros_1.txt) [R implementation](numerical_analysis/sptb_analysis.R)

### Reproduction

Run `Rscript numerical_analysis/sptb_analysis.R` from the repository root. The script writes its CSV files and figures to `numerical_analysis/sptb_out/`.

---

## Mathematical Framework

### The SPTB Functional
```
F_λ(H_σ; T, Δ) = Σ_j [ ∫_{I_j} |H_σ - S_j|² dt + λ ∫_{I_j} |∂_t(H_σ - S_j)|² dt ]
```

In this expression, `S_j` is the least-squares affine fit on block `I_j`. The numerical signal is the centred sum of the terms `w_ρ |ρ|^{-α} e^{(β−σ)t} cos(γt)`. The block width is `Δ = c_Δ / log T`, with `c_Δ = 2π` for baseline runs and an adaptive value between 2π and 60π for synthetic-zero runs. The derivative penalty is `λ = 1 / (log T)²`.

### Detection estimates

For a complex mode of the form `c exp((η + iω)t)` with nonzero amplitude, &eta; > 0 and fixed positive width and derivative penalty, the squared distance to the best affine fit in the weighted norm grows as a positive constant times exp(2&eta;T). The real-mode estimate proposed in the March paper fails uniformly in the width. Setting &eta; = 1/&Delta; and &omega; = 2/&Delta; gives a squared projection error proportional to &Delta;, while the proposed lower bound is proportional to 1/&Delta;. [Single-mode theorem and counterexample](paper_witness/main.tex)

For a sum, the other modes can cancel part of the chosen mode after projection. A sufficient bound is that their projected norm is at most a fixed fraction less than one of the chosen mode’s projected norm. The March application needs estimates for the actual spectrum and its shrinking mesh. For the separately damped zeta field, assuming all nontrivial zeta zeros have real part one half, the revision proves an upper bound of order T(1 + &lambda;) for the optimised energy when &alpha; > 2 and 1/2 &le; &sigma; &le; 1. The March application uses &alpha; = 1. [Remainder estimate and damped-field theorem](paper_witness/main.tex)

### Horocycle conjecture

The March manuscript asks whether boundedness of F<sub>&lambda;</sub> divided by T log T log log T for all sufficiently large T forces every zeta zero to satisfy &beta; &le; &sigma;, for 1/2 &le; &sigma; < 1. This remains open for the proposed functional and general zero configurations. [Statement in Part 2](paper_clean/parts/part2.tex)

---

## Numerical Parameters

| Parameter | Variance runs | Bias runs |
|-----------|--------------|-----------|
| T range | 200 &ndash; 10<sup>4</sup> | 10<sup>4</sup> &ndash; 5&times;10<sup>4</sup> |
| &eta; values | &mdash; | 10<sup>-4</sup>, 5&times;10<sup>-4</sup>, 10<sup>-3</sup> |
| &sigma; | 0.50 | 0.50 |
| c<sub>&Delta;</sub> (&kappa;) | 2&pi; | Adaptive, [2&pi;, 60&pi;] |
| &lambda; | 1 / (log T)<sup>2</sup> | 1 / (log T)<sup>2</sup> |
| n<sub>t</sub> (grid points) | 4,000 to 234,544 | 120,000 |
| Zero source | Odlyzko (79, &gamma; &le; 200, weight 2) | Odlyzko + synthetic (&beta; > &sigma;, weight 1) |
| Standardization | Mean-centered | Mean-centered |
| Quadrature | Trapezoidal | Trapezoidal |
| Tail slope | &mdash; | Huber-robust regression on last 1/3 of blocks |

---

## Code Documentation

### Main Functions (`numerical_analysis/sptb_analysis.R`)
```r
# Core computation
build_H_sigma()              # Construct harmonic field H_σ(t), chunked, MPFR-capable
blockwise_functionals()      # Compute F_λ with affine projection + central differences
run_variance_regime()        # Polynomial growth sweep (β ≤ σ)
run_bias_sweep()             # Exponential growth sweep across (η, T) grid
run_bias_once()              # Single bias run with adaptive κ

# Utilities
thin_zeros()                 # Zero selection (head / uniform / gamma threshold)
inject_offline_zero()        # Add synthetic off-line zero (weight = 1)
choose_kappa_bias()          # Adaptive block width for bias runs
kahan_cumsum()               # Compensated summation (reduces floating-point drift)
fit_affine_block()           # Ridge-regularized least squares on each block
trapz()                      # Trapezoidal quadrature
central_diff()               # Central finite differences for derivative term
```

---

## Related Work

The March paper discusses spectral approaches by Connes, Berry and Keating, and Balazs and Voros, alongside Li’s positivity criterion. Its geometric comparison is heuristic. Its numerical results concern the finite zero lists described above. [Geometric discussion and references](paper_clean/parts/part4.tex)

---

## Contributing

Contributions are welcome. Areas for extension:

1. Bound cancellation in the full projected spectrum on a shrinking mesh.
2. **Numerical**: Extend to T > 10<sup>6</sup> using MPFR
3. **Applications**: Test on Dirichlet L-functions, modular forms
4. **Optimization**: Parallelize across (T, &eta;) grid

Please open an issue or pull request.

---

## License

- **Code**: MIT License
- **Paper & Data**: CC-BY-SA 4.0

See [LICENSE](LICENSE) for details.

---

## Acknowledgments

- **A.M. Odlyzko**: Zero tables (publicly available)
- **H.L. Montgomery & R.C. Vaughan**: Short-interval mean-value inequality (1974)
- **Conceptual influences**: A. Connes, M. Berry, J. Keating, N. Balazs, A. Voros

---

## Contact

**Akbar Akbari Esfahani**
akbar.esfahani@thealliance.health

For questions about the paper, code, or data, please open an issue on GitHub.
