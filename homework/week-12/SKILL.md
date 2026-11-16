---
name: unsupervised-clustering
description: >-
  Compare unsupervised clustering approaches, select and interpret one, and
  create a concise report. Use only when explicitly invoked.
---

# Unsupervised Clustering

Use this skill only when the user explicitly invokes it. The user must provide
the dataset, observational unit, candidate features, identifiers, and any
available labels separately. Do not assume dataset-specific column names or
results.

## Workflow

1. **Check the data.** Confirm rows are observations and features are
   appropriate numeric measurements. Exclude identifiers and all outcome,
   class, or other labels from preprocessing, tuning, and method selection.
   Report missing/non-finite values, duplicates, constant features, and any
   imputation or filtering. Do not silently drop observations.
2. **Prepare features.** Consider transformations for skew or outliers, remove
   unusable features, and center/scale when feature units or variances warrant
   it. Explain choices; do not standardize automatically when that would
   amplify noise. For high-dimensional data, use PCA to explore structure and
   optionally cluster on a justified number of principal components. Report
   retained variance and note that PCA is dimension reduction, not a clustering
   algorithm. Fit all preprocessing without labels.
3. **Compare all three clustering algorithms** on a common representation
   where practical. PCA may be used for dimension reduction and visual
   exploration, but it is not a clustering algorithm:
   - **K-means:** test multiple cluster counts and random starts; retain the
     best within-cluster objective for each count and assess seed stability.
   - **Hierarchical clustering:** compare suitable linkage rules and cut levels
     using a justified distance metric.
   - **Spectral clustering:** document the similarity graph/kernel and tune its
     scale or neighborhood and cluster count.
4. **Select transparently.** Use internal measures such as average silhouette
   and, when suitable, Calinski-Harabasz or Davies-Bouldin scores. Also assess
   repeatability under seeds or reasonable perturbations, sensitivity to
   preprocessing/tuning, cluster sizes, and interpretability. Treat metrics as
   diagnostics, not proof of a uniquely correct partition. Avoid selecting a
   degenerate solution with singleton or otherwise unusably small groups
   unless substantively justified. State the trade-offs and why one method and
   cluster count were selected. Do not use labels to choose them.
5. **Present only the selected clustering's results.** Briefly name the
   alternatives and selection criteria, but do not show their assignments,
   cluster profiles, or result plots. Use one readable visualization, usually
   a PCA scatterplot colored by selected cluster; explain what its axes show.
   Summarize selected cluster sizes and a few useful feature profiles. Only
   after selection, labels may be compared with the final clusters for
   interpretation; identify this as post hoc and do not call it validation
   unless an appropriate independent design supports that claim.
6. **Explain limits.** Discuss relevant sensitivity, information lost through
   preprocessing or dimension reduction, dependence on distance/algorithm,
   small-sample or high-dimensional uncertainty, and the exploratory nature
   of clusters. Do not imply causation or that clusters are objectively true.

## Report constraint

Limit the generated analysis report to **one printed page total**, including
all text, figures, and tables. Keep the report concise and legible. Present
clustering results from **only one selected method**; other methods may be
named briefly to justify the selection, without presenting their results.
If a complete skill definition is required with the submission, place it in a
separate appendix after that one-page report; the appendix is outside the
report page limit.
