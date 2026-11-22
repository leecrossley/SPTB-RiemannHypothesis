# March manuscript

The March 2026 edition of *A Structural Spline-Penalized Tail Bound for L-Functions* has 34 pages. The November revision gives a counterexample to its scale-uniform affine lower bound and sets out the estimates needed to detect a mode in the full spectrum. [March manuscript](main.pdf) [November revision](../paper_witness/main.pdf) [Revision record](../paper_witness/REVISION_NOTES.md)

## Structure

```
paper_clean/
├── main.tex              # Main document (cleaned page breaks)
├── parts/
│   ├── part1.tex        # Foundations and Variance Regime
│   ├── part2.tex        # Bias Regime and Detection Theorem
│   ├── part2b_explicit_formula.tex  # Explicit formula and the surrogate field
│   ├── part3.tex        # Empirical Validation
│   └── part4.tex        # Geometric Framework (heuristic)
├── appendices/
│   ├── appA.tex         # Affine-Projection Constants
│   ├── appB.tex         # Derivative-Variance Constant
│   ├── appC.tex         # Constant-Extraction Methodology
│   └── appD.tex         # Dirichlet L-functions Extension
├── figs/                # All figures (8 PNG files)
├── bib/                 # Bibliography
│   └── references.bib
└── Makefile             # Build automation
```

## Compilation

### Using Make
```bash
make          # Compile PDF
make clean    # Remove auxiliary files
make view     # Show page count
```

### Manual Compilation
```bash
pdflatex main.tex
pdflatex main.tex
pdflatex main.tex
```

Run pdflatex three times to ensure all cross-references and TOC are correct.
