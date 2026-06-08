# Reporting And Reviewer-Risk Checks

Use this reference when writing Chinese manuscript text, figure legends, table legends, or review-risk notes.

## Chinese Methods Text Must Cover

- MATLAB version and required toolboxes.
- MRI modality and feature source.
- Sample size, group composition, and target variable.
- Subject matching and exclusion rules.
- Feature preprocessing.
- Nested CV design, including outer and inner folds.
- Inner-loop hyperparameter tuning and feature selection.
- Outer-loop generalization-performance estimation.
- Covariate handling.
- Permutation testing.
- Performance metrics.
- Model interpretation method.
- Multimodel or multimodality comparison.
- Multiple-comparison correction when applicable.
- Code and output reproducibility.

## Chinese Results Text

Generate results only from actual output tables. Never invent numbers.

For classification, report:

- balanced accuracy
- AUC
- sensitivity/specificity
- macro-F1 or class-wise metrics for imbalance/multiclass cases
- permutation-test p value
- model comparison, if performed

For regression, report:

- Pearson r and/or Spearman r
- MAE
- RMSE
- R squared
- permutation-test p value
- observed-versus-predicted plot description

For feature importance, use cautious Chinese wording equivalent to:

- candidate predictive features
- exploratory feature-importance results
- appeared relatively stably across cross-validation folds
- requiring further validation in an independent sample

Avoid Chinese wording equivalent to these claims unless the evidence supports them:

- diagnostic biomarker
- proves the mechanism
- directly usable for clinical diagnosis
- first discovery

## Figure And Table Legends

Classification figures:

- ROC curve: state pooled outer-test predictions and AUC.
- Confusion matrix: state whether values are counts or normalized percentages.
- Feature importance: state the method and that results are fold-aggregated/exploratory.
- Permutation distribution: state the observed metric and empirical p value.

Regression figures:

- Observed vs predicted: state pooled outer-test predictions.
- Residual plot: state whether residuals come from outer-test predictions.
- Feature importance: state model and aggregation method.
- Permutation distribution: state the observed metric and empirical p value.

Tables:

- Include mean, SD, and 95% CI when repeated CV is used.
- Include fold/repeat count.
- Define all metrics.
- Clearly separate primary and secondary metrics.

## Reviewer-Risk Checklist

Every generated project or review should include:

1. Is there any data leakage?
2. Is final performance based on nested CV or a proper held-out/external set?
3. Is feature selection inside training folds?
4. Is covariate control inside training folds?
5. Are outer-test predictions saved?
6. Is permutation testing performed when significance is claimed?
7. Are imbalance-aware metrics reported?
8. Are model weights overinterpreted?
9. Is external validation needed?
10. Is multiple-comparison correction needed?
11. Are exploratory and confirmatory analyses separated?
12. Are "diagnostic model", "prediction model", and "biomarker" terms justified?

## Recommended Closing Note

When the evidence is cross-validation only, write a Chinese closing note that says the model shows cross-validated predictive ability in the current sample, but independent external validation is still needed before making generalization or clinical-use claims.
