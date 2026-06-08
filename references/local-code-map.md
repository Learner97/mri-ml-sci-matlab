# Local MATLAB Course Code Map

Use this map when the user's machine has `D:\Brain\MachineLearning_MC`. Treat the folder as a local knowledge source, not as redistributable content. Do not upload private data, NIfTI examples, PDF course materials, or bundled third-party toolboxes unless the user explicitly requests it and licensing/privacy are clear.

## High-Level Layout

- `Part1`: MATLAB practice plus SPM12/CAT-style neuroimaging toolboxes.
- `Part2`: classical ML teaching demos: LDA, KNN, logistic regression, LOOCV, and K-fold examples.
- `Part3`: SVM/SVR workflows for ROI grey-matter features, FC matrices, DTI matrices, and voxel/NIfTI-based examples; includes libsvm utilities.
- `Part4`: HYDRA disease-subtype modeling and MKL/multikernel examples.
- `Part5`: PRoNTo and NBS/NBS-Predict/CPM-style connectome prediction resources.
- `Part6`: regression and advanced model demos: Linear Regression, LASSO, Ridge, Elastic Net, Random Forest, GPR, and MKL v2.

## Useful Local Patterns

### SVM on FC Matrices

Relevant files:

- `Part3\part3_svm_FC\step1_FC_svm_selection.m`
- `Part3\part3_svm_FC\step2_FC_svm_roc.m`
- `Part3\part3_svm_FC\FC_svr.m`
- `Part3\part3_svm_FC\DTI\DTI_commom_mask.m`

Reusable ideas:

- Load subject-level FC matrices by group.
- Vectorize selected connections from upper-triangle-like indices.
- Run training-fold-only feature screening.
- Use libsvm for SVM/SVR.
- Compute AUC with `perfcurve`.
- Run permutation tests by shuffling labels/outcomes.

Modernization needed:

- Replace LOOCV-only final estimates with repeated nested CV for formal results.
- Save fold indices, selected features, predictions, and decision scores.
- Avoid any full-sample feature ranking before CV.
- Prefer MATLAB built-ins such as `fitcsvm`, `fitrsvm`, `fitclinear`, and `fitrlinear` unless libsvm is specifically required.

### Voxel-Based SVM/SVR

Relevant files:

- `Part3\part4_svm_Voxel\svm_voxel_based.m`
- `Part3\part4_svm_Voxel\svm_voxel_based_pvalue.m`
- `Part3\part4_svm_Voxel\svr_voxel_based.m`
- `Part3\part4_svm_Voxel\distance_BMatrix.m`
- `Part3\part4_svm_Voxel\fdr.m`

Reusable ideas:

- Check and apply a brain mask.
- Convert masked voxels to a subject-by-voxel matrix.
- Apply PCA/scaling inside the training fold.
- Write spatial output maps such as accuracy, p-value, or feature maps.

Modernization needed:

- Treat voxel models as high-dimensional and fragile.
- Put PCA, univariate screening, and scaling strictly inside each outer training fold.
- Save voxel mask metadata and spatial mapping between feature columns and voxels.
- Warn when sample size is inadequate for voxelwise modeling.

### Regression: LASSO, Ridge, Elastic Net, GPR

Relevant files:

- `Part6\regress\LASSO\Lasso_demo.m`
- `Part6\regress\LASSO\Lasso_fc.m`
- `Part6\regress\Ridge\Ridge_demo.m`
- `Part6\regress\Ridge\ridge_cv.m`
- `Part6\regress\ENet\Elastic_demo.m`
- `Part6\gpr\gpr_lasso.m`

Reusable ideas:

- Use correlation-based training-fold feature screening.
- Use `lasso` with internal CV for lambda selection.
- Use Ridge/SVR/GPR for continuous clinical or cognitive outcomes.
- Evaluate pooled out-of-fold predictions with Pearson r and errors.

Modernization needed:

- Treat `lasso(...,'CV',k)` as inner-loop tuning only.
- Save selected lambda/alpha by outer fold.
- Report MAE/RMSE in addition to correlation.
- Use permutation testing if claiming significance.

### Random Forest

Relevant files:

- `Part6\RF\RFclf\RF_clf1.m`
- `Part6\RF\RFclf\RF_clf2.m`
- `Part6\RF\RFreg\RFreg1.m`
- `Part6\RF\RFreg\RFreg_lasso.m`

Reusable ideas:

- Use tree ensembles for classification/regression.
- Extract predictor importance.
- Compare RF against linear models as sensitivity analysis.

Modernization needed:

- Tune number of trees and leaf size inside inner CV.
- Use balanced accuracy/macro-F1 for imbalanced classification.
- Interpret predictor importance as exploratory.

### CPM / NBS / Connectome Prediction

Relevant files:

- `Part5\CPM\codes\predict_behavior_fit.m`
- `Part5\CPM\codes\predict_behavior_regress.m`
- `Part5\CPM\codes\predict_permutation_fit.m`
- `Part5\CPM\codes\predict_permutation_regress.m`
- `Part5\NBS\Classification\README.txt`
- `Part5\NBS\Regression\README.txt`
- `Part5\toolboxes\NBS-Predict-master\start_NBSPredict.m`

Reusable ideas:

- Screen edges by training-fold association with behavior/group.
- Build positive and negative network summaries.
- Use permutation testing for network-level prediction significance.

Modernization needed:

- Perform edge screening within each training fold only.
- Save positive/negative edge masks and selection frequencies.
- Never include both upper and lower triangles for symmetric matrices.

### HYDRA and Subtyping

Relevant files:

- `Part4\HYDRA\hydra_demo.m`
- `Part4\HYDRA\hydra.m`
- `Part4\HYDRA\hydra_solver.m`
- `Part4\HYDRA\kmeans_demo1.m`
- `Part4\HYDRA\kmeans_demo2.m`

Reusable ideas:

- Use HYDRA-like semi-supervised clustering for disease heterogeneity.
- Compare subtype stability and covariate effects.

Modernization needed:

- Separate subtype discovery from predictive classification.
- Do not evaluate subtype labels on the same data used to discover them without resampling or external validation.
- Save cluster stability and subtype-size diagnostics.

### MKL / Multimodal Fusion

Relevant files:

- `Part4\mkl\demo.m`
- `Part4\mkl\mkl.m`
- `Part4\mkl\calckernel.m`
- `Part4\mkl\myCV.m`
- `Part6\mkl_v2\demo_v2.m`
- `Part6\mkl_v2\mkl_v2.m`
- `Part6\mkl_v2\calckernel_v2.m`

Reusable ideas:

- Build modality-specific kernels.
- Compare single-modality and fused models.
- Estimate modality contribution through kernel weights.

Modernization needed:

- Tune kernel and model parameters inside inner CV.
- Save fold-wise modality weights.
- Report whether modality contribution is stable across repeats/folds.

## Portable Skill Behavior

When the local folder is absent, use this map as conceptual guidance only. Generate self-contained MATLAB code with comments saying where users may plug in SPM/CAT, PRoNTo, libsvm, NBS-Predict, or local course scripts if installed.
