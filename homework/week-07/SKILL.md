---
name: lda-qda-analysis
description: Use only when explicitly invoked to compare LDA, QDA, and probability blends for a supplied dataset and produce a concise, one-page statistical report.
---

# LDA/QDA Analysis

## Invocation and scope

Use this skill only when the user explicitly requests it. The invocation must supply a dataset, one categorical response, and the predictor columns. Do not assume a dataset or infer variables from unrelated files. If any input is missing or ambiguous, ask for it before analyzing. Do not change the substantive analysis requested by the user.

Use only linear discriminant analysis (LDA), quadratic discriminant analysis (QDA), or a classifier formed by blending their class-probability predictions. PCA may be used as a fold-fitted dimension-reduction step for these classifiers, not as a separate classifier. Do not substitute other classifier families.

## Analysis procedure

1. Inspect the supplied data and report the number of usable observations, classes, and predictors. Check response levels, class counts, missingness, nonnumeric predictors, and whether covariance estimates are feasible. Explain any exclusions or preprocessing; do not silently discard data. Fit all imputation, encoding, scaling, feature selection, and PCA steps using training data only within each resample.
2. Compare LDA, QDA, and a probability blend. Define blend probabilities as \(p_w = w p_{\mathrm{LDA}} + (1-w)p_{\mathrm{QDA}}\), with \(0 \le w \le 1\); choose the weight only from training data. Use the same class labels, folds, and prediction rule (largest class probability) for all candidates. State any class-prior choice.
3. Estimate generalization error with stratified cross-validation, using as many folds as class counts support (prefer 5 or 10) and repeating folds when practical. For honest model selection, use nested cross-validation: choose the candidate and any blend weight or PCA settings using inner folds, then assess the complete selection procedure on untouched outer folds. If nested CV is infeasible, state the alternative clearly and warn that selecting and evaluating on the same folds can be optimistic. Keep all preprocessing inside folds.
4. Use misclassification rate as the primary error measure; also report accuracy and, when class sizes are imbalanced, balanced accuracy or class-wise recall. Summarize outer-fold results across held-out predictions; give variability or an uncertainty interval when supportable. Do not present resampling results as certainty or claim causal findings.
5. Refit the selected LDA, QDA, or blend procedure on all supplied observations for final fitted probabilities or coefficients if useful. Distinguish these in-sample fit quantities from the cross-validated prediction-error estimate. Report software/package details only when relevant to reproducibility.

## Required report

Produce a clearly readable report that fits on **at most one printed page**. Include:

- A brief, descriptive title and a compact description of the response, predictors, sample size, and class counts.
- A concise account of candidate models and the cross-validation design, including folds/repeats and how model or blend selection was handled.
- A table comparing LDA, QDA, and the blend: cross-validated error (with variability or interval if available), accuracy, and an imbalance-aware metric when needed. Mark the selected model.
- A figure showing candidate cross-validated error with uncertainty/variability where available; label axes, units/metrics, and models legibly. Avoid implying tiny differences are meaningful.
- Numerical model-fitting results: selected model, its estimated prediction error, and relevant fitted quantities or held-out confusion/class-wise results. Clearly label which results are cross-validated versus in-sample.
- A brief interpretation of the main findings and material limitations, such as small class counts, unstable QDA covariance estimates, missingness, or optimistic non-nested selection.

Keep prose concise, use readable typography and restrained, accessible colors, and ensure the table and figure are legible in print. Do not omit required report elements to meet the page limit; simplify layout instead. If the page limit cannot be met without sacrificing clarity, state the issue and ask before expanding it.
