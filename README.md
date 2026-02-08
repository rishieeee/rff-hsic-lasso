# Scaling Nonlinear Feature Selection with Random Fourier Feature–Based HSIC

Kernel-based dependence measures such as the Hilbert-Schmidt Independence Criterion (HSIC)
are powerful tools for nonlinear feature selection but suffer from quadratic memory and
time complexity due to explicit kernel matrix construction. This project investigates a
scalable approximation of HSIC using Random Fourier Features (RFF), enabling efficient
nonlinear dependence estimation using linear operations.

## Method Overview
We replace explicit kernel computations in HSIC with Random Fourier Feature mappings,
based on Bochner’s theorem. This approximation avoids N×N kernel matrices and reduces
memory complexity from O(N²) to O(N·D), where D is the number of random features, while
preserving nonlinear dependence estimation capability.

## Reproducibility
All experiments are contained in a single Jupyter notebook:
- Open `notebooks/rff_hsic_scaling_experiments.ipynb`
- Run all cells top to bottom

The notebook generates all results and figures used in the analysis.

## Results Summary
The experiments demonstrate:
- Approximately linear runtime scaling with respect to the number of samples
- Controlled and stable memory usage without quadratic growth
- A clear trade-off between approximation quality and computational cost via the
  number of random Fourier features

## Limitations and Future Work
This study focuses on synthetic data to isolate scalability effects. Future extensions
include:
- Nyström-based kernel approximations for alternative scalability trade-offs
- Group-aware and structured regularization (e.g., Group HSIC) for handling feature
  redundancy in high-dimensional biological datasets
