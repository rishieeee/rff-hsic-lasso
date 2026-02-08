# Scaling Nonlinear Feature Selection via Random Fourier Feature–Based HSIC

## Overview

The Hilbert–Schmidt Independence Criterion (HSIC) is a kernel-based dependence measure
widely used in nonlinear feature selection, most notably in HSIC Lasso. By embedding
variables into a reproducing kernel Hilbert space (RKHS), HSIC enables the detection of
nonlinear statistical dependencies that are not captured by linear correlation measures.

Despite its theoretical appeal, practical adoption of HSIC-based methods is severely
limited by computational constraints. Standard HSIC formulations require the explicit
construction of N × N kernel matrices, resulting in O(N²) memory and time complexity.
This quadratic scaling makes HSIC infeasible for modern high-dimensional or large-sample
datasets, particularly in scientific domains such as genomics and proteomics.

This repository investigates a scalable approximation of HSIC using **Random Fourier
Features (RFF)**. By replacing explicit kernel evaluations with randomized feature
mappings based on Bochner’s theorem, HSIC computation can be reformulated in terms of
linear algebra operations, enabling efficient dependence estimation without constructing
kernel matrices.

---

## Research Objective

The goal of this project is to **empirically study the scalability bottleneck of HSIC**
and demonstrate how Random Fourier Feature approximations alleviate this limitation.

Specifically, we aim to:
- Quantify the runtime and memory cost of standard kernel-based HSIC
- Implement an RFF-based approximation that avoids N × N kernel matrices
- Empirically evaluate how runtime and memory scale with:
  - the number of samples (N)
  - the number of random Fourier features (D)
- Validate approximation fidelity against full HSIC on small-scale problems

This work focuses on **computational scalability**, not on improving predictive accuracy
or proposing new statistical estimators.

---

## Methodological Summary

### Full HSIC Baseline
We first implement the standard HSIC formulation using RBF kernels. This baseline serves
two purposes:
1. To establish correctness and reference values for HSIC
2. To empirically demonstrate the quadratic memory and runtime bottleneck

Due to its O(N²) complexity, this baseline is evaluated only for small sample sizes.

### Random Fourier Feature Approximation
To address scalability, we employ Random Fourier Features to approximate shift-invariant
kernels. The input data is mapped into a finite-dimensional randomized feature space,
where kernel evaluations are approximated by inner products.

HSIC computation is then performed using centered random features and linear algebra,
reducing memory complexity from O(N²) to O(N·D), where D is the number of random features.

This formulation preserves nonlinear dependence estimation while enabling scalability.

---

## Experimental Design

All experiments are conducted in a controlled synthetic setting to isolate computational
effects from dataset-specific artifacts.

The experimental pipeline includes:
- Validation of RFF–HSIC against full HSIC on small datasets
- Runtime scaling analysis as a function of sample size
- Memory usage analysis as a function of sample size
- Evaluation of the computational trade-off introduced by the number of random features

Both runtime and peak memory usage are explicitly measured.

---

## Results Summary

The experiments demonstrate that:
- Full HSIC exhibits rapid growth in runtime and memory usage due to kernel matrix
  construction
- RFF-based HSIC avoids quadratic memory growth and scales smoothly with the number of
  samples
- Increasing the number of random Fourier features increases computational cost in a
  controlled and predictable manner
- Approximation fidelity improves with higher feature dimensionality, revealing a clear
  accuracy–efficiency trade-off

These results empirically confirm that Random Fourier Features provide a practical
mechanism for scaling HSIC-based dependence estimation.

---

## Reproducibility

All experiments are fully reproducible.

To reproduce the results:
1. Open `notebooks/rff_hsic_scaling_experiments.ipynb`
2. Run all cells from top to bottom

The notebook generates:
- All experimental results (CSV files)
- All figures used for analysis

No external datasets are required.

---

## Limitations

This study focuses exclusively on synthetic data in order to isolate scalability effects.
As such:
- No claims are made regarding downstream predictive performance
- No real-world biological datasets are evaluated
- Statistical optimality is not analyzed

The current implementation studies HSIC computation in isolation and does not include
feature selection pipelines or regularization strategies.

---

## Future Work

This project is intended as a foundational scalability study. Natural extensions include:

- **Nyström-based kernel approximations**  
  Investigating alternative low-rank kernel approximations and comparing their empirical
  trade-offs with Random Fourier Features.

- **Structured and Group-Aware HSIC**  
  Incorporating block-sparse or group-structured regularization (e.g., Group HSIC) to
  address feature redundancy, particularly in biological and genomic data.

- **Application to High-Dimensional Scientific Datasets**  
  Applying scalable HSIC approximations to real-world gene expression or proteomics
  datasets, where the number of features far exceeds the number of samples.

- **Integration with HSIC Lasso**  
  Extending the current framework to full HSIC Lasso pipelines with scalable kernel
  approximations.

---

## Intended Audience

This repository is intended for:
- Researchers working on kernel methods and statistical dependence measures
- Graduate students studying scalable machine learning algorithms
- Scientific machine learning practitioners dealing with high-dimensional data

It is not designed as a tutorial or introductory resource.

---

## License

This project is released for academic and research use.

