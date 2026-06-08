---
name: mri-ml-sci-matlab
description: Generate, modify, or review MATLAB workflows for SCI/SSCI-level MRI and neuroimaging machine learning. Use for brain MRI features, ROI tables, voxel maps, fMRI metrics, structural MRI, DTI/SC matrices, FC connectomes, graph metrics, radiomics, multimodal fusion, clinical/cognitive outcomes, SVM/SVR, LASSO, Ridge, Elastic Net, Random Forest, GPR, CPM/NBS, HYDRA, MKL, nested cross-validation, permutation testing, confound control, feature selection, feature importance, leakage audit, reproducible outputs, and Chinese manuscript-ready methods/results reporting.
---

# MRI ML SCI MATLAB

Build and review MATLAB machine-learning analyses for MRI/neuroimaging studies. Prioritize leakage-resistant nested cross-validation, reproducible outputs, conservative scientific interpretation, and manuscript-ready Chinese reporting.

## First Moves

1. Identify the input type: ROI feature table, voxel/NIfTI images, FC/SC matrices, graph metrics, radiomics features, multimodal feature blocks, or clinical/cognitive variables.
2. Identify the task: binary classification, multiclass classification, regression, connectome prediction, subtype discovery, model comparison, or reviewer-risk audit.
3. Ask only for missing essentials: feature file paths, target/covariate tables, subject ID columns, target column, feature grouping, output directory, and whether formal SCI/SSCI analysis or a teaching demo is needed.
4. For formal analysis, generate a modular MATLAB project rather than one long script.
5. Inspect local course code if available at `D:\Brain\MachineLearning_MC`, but do not copy third-party toolboxes, private MRI data, or large course datasets into generated outputs unless the user explicitly asks and permissions are clear.

## Load References As Needed

- Read `references/local-code-map.md` when adapting patterns from the user's local `D:\Brain\MachineLearning_MC` MATLAB course folder.
- Read `references/leakage-safe-workflow.md` before generating nested CV, feature-selection, permutation-test, confound-control, or harmonization code.
- Read `references/model-routing.md` when choosing SVM/SVR, LASSO, Ridge, Elastic Net, Random Forest, GPR, CPM/NBS, HYDRA, MKL, or multimodal fusion.
- Read `references/reporting-and-review.md` when writing Chinese methods/results text, figure/table legends, or reviewer-risk checks.

## Non-Negotiable Rules

Use repeated nested cross-validation for final model evaluation unless the user explicitly requests a simplified teaching demo.

Keep the outer loop only for unbiased generalization estimation. Use the inner loop for imputation, scaling, confound handling decisions, ComBat/harmonization choices, PCA, SMOTE/resampling, feature selection, model selection, and hyperparameter tuning.

Never fit, select, tune, harmonize, reduce, rebalance, or interpret using the outer test fold. The outer test fold may only be transformed with parameters learned from the corresponding training fold and then evaluated once.

Never approve code that standardizes all samples before CV, selects features before CV, residualizes covariates before CV, runs PCA/ComBat before CV, tunes on the outer test set, reports only accuracy for imbalanced data, or claims biomarkers without appropriate validation.

## Default Formal Configuration

Use these defaults unless the user gives different values:

- `outer_k = 5`
- `inner_k = 5`
- `n_repeats = 20`
- `n_permutations = 1000` for final analysis
- `n_permutations = 100` for debugging only
- `random_seed = 42`
- classification primary metrics: balanced accuracy and AUC
- regression primary metrics: Pearson r, MAE, and RMSE
- main classifier: linear SVM
- main regressor: Ridge regression or SVR
- feature scaling: z-score using training-set mean and standard deviation
- imputation: training-set median or mean
- parallel computing: optional with serial fallback

## Preferred MATLAB Project Structure

For formal analyses, generate or maintain:

```text
main_run_ml.m
config_ml.m
load_mri_features.m
utils_check_data.m
utils_vectorize_connectome.m
make_outer_inner_folds.m
preprocess_inside_fold.m
residualize_covariates_train_test.m
nested_cv_classification.m
nested_cv_regression.m
train_and_tune_model.m
evaluate_classification.m
evaluate_regression.m
permutation_test_nested_cv.m
compute_feature_importance.m
plot_classification_results.m
plot_regression_results.m
write_cn_methods_results_report.m
```

Keep module boundaries clear: data loading and subject matching in `load_mri_features.m`; all leakage-safe transforms in `preprocess_inside_fold.m`; covariate residualization in `residualize_covariates_train_test.m`; tuning in `train_and_tune_model.m`; final metrics in evaluation functions; significance testing in `permutation_test_nested_cv.m`; Chinese manuscript text in `write_cn_methods_results_report.m`.

## Required Outputs

For formal analyses, save at least:

- `config_used.mat` and `config_used.txt`
- `subject_order.xlsx`
- `outer_fold_indices.xlsx`
- `inner_cv_results.xlsx`
- `best_params_by_fold.xlsx`
- `y_true_y_pred_outer_cv.xlsx`
- `performance_by_fold.xlsx`
- `performance_summary.xlsx`
- `permutation_results.xlsx`
- `selected_features_by_fold.xlsx`
- `feature_selection_frequency.xlsx`
- `feature_importance_by_fold.xlsx`
- `feature_importance_summary.xlsx`
- `model_comparison_summary.xlsx`
- `important_ROI_or_edges.xlsx`
- `methods_text_for_paper_CN.txt`
- `results_text_for_paper_CN.txt`
- `interpretation_text_for_paper_CN.txt`
- `review_risk_checklist_CN.txt`
- `MATLAB_workspace_results.mat`

For classification, also create ROC, confusion matrix, feature-importance, permutation-distribution, and model-comparison figures when applicable.

For regression, also create observed-vs-predicted, residual, feature-importance, permutation-distribution, and model-comparison figures when applicable.

## Scientific Wording

Use conservative language. Prefer "predictive model", "cross-validated predictive performance", "candidate predictive features", and "exploratory feature-importance results". Do not call features biomarkers unless external validation, study design, and statistical evidence justify that wording.

When generating Chinese reporting, write from actual output tables only. Never invent numbers. If a statistic is missing, state which output file or variable should contain it.
