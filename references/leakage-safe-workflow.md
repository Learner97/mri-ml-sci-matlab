# Leakage-Safe MATLAB Workflow

Use this reference before writing formal MRI machine-learning code.

## Data Intake

Require or infer:

- feature table or matrix paths
- target table path
- covariate table path, if any
- subject ID column in every table
- target column
- feature columns or feature matrix layout
- modality labels for multimodal analyses
- output directory

Always check:

- subject IDs match across feature, target, and covariate sources
- no duplicated subject IDs
- no label-feature misalignment
- NaN, Inf, constant, and near-zero variance features
- class counts and imbalance
- feature dimensionality relative to sample size

## Outer and Inner CV

For formal analysis:

1. Set random seed.
2. Create repeated outer folds.
3. For each outer fold, split subjects before any data-driven operation.
4. Within the outer-training set, create inner folds.
5. Use inner folds to tune preprocessing decisions, feature selection, models, and hyperparameters.
6. Fit the chosen pipeline on the complete outer-training set.
7. Transform the outer-test set only with parameters learned from the outer-training set.
8. Predict the outer-test set exactly once.
9. Save predictions, scores, selected features, parameters, and fold indices.
10. Pool outer-test predictions across folds/repeats for final metrics.

## Fold-Internal Preprocessing

Fit on training data only:

- imputation parameters
- scaling parameters
- covariate residualization coefficients
- ComBat/harmonization parameters
- PCA or dimensionality reduction bases
- feature-selection thresholds
- SMOTE/resampling operations

Apply learned parameters to validation/test data. Never recompute parameters on validation/test data.

## Confound Control

Common covariates include age, sex, education, intracranial volume, site, scanner, head motion, framewise displacement, lesion volume, disease duration, and medication.

Inside each outer fold:

1. Center continuous covariates using training-set means.
2. Dummy-code categorical variables using training-set levels.
3. Fit residualization models on training subjects only.
4. Apply fitted covariate models to test subjects.
5. Save covariate names, coding rules, and residualization targets.

Do not residualize classification labels unless the design explicitly justifies it.

## Feature Selection

Acceptable methods, training-fold only:

- variance thresholding
- two-sample t tests for binary classification
- ANOVA or appropriate univariate tests for multiclass classification
- correlation screening for regression
- LASSO or Elastic Net selection
- CPM-style edge selection
- ReliefF when justified

Save selected features for every fold and compute selection frequency. Treat frequency as stability evidence, not as a confirmed mechanism.

## Permutation Testing

When claiming significance:

1. Shuffle labels/outcomes at the subject level.
2. Re-run the entire nested CV pipeline for each permutation, including feature selection and tuning.
3. Compute the same primary metric for each permutation.
4. Report empirical p value as `(sum(null_metric >= observed_metric) + 1) / (n_permutations + 1)` for higher-is-better metrics, with the appropriate direction for error metrics.
5. Save the null distribution and plotting data.

## Classification Metrics

Save:

- accuracy
- balanced accuracy
- sensitivity
- specificity
- precision
- recall
- F1
- AUC, if scores are valid
- confusion matrix
- per-subject true label, predicted label, probability, and decision score
- fold-wise and repeat-wise metrics
- mean, standard deviation, and 95% confidence interval

For multiclass tasks, add macro-F1 and class-wise metrics. Define whether AUC is one-vs-rest, macro, or micro averaged.

## Regression Metrics

Save:

- Pearson r
- Spearman r
- MAE
- RMSE
- R squared
- slope and intercept
- per-subject observed and predicted values
- fold-wise and repeat-wise metrics
- mean, standard deviation, and 95% confidence interval

Use pooled outer-test predictions for final scatter plots.
