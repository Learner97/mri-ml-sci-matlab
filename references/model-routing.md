# Model Routing

Choose models by input type, sample size, interpretability needs, and manuscript risk.

## Default Choices

- Binary classification: linear SVM with `fitcsvm` or `fitclinear`.
- High-dimensional regression: Ridge, SVR, or LASSO/Elastic Net when feature selection is desired.
- Small neuroimaging samples: prefer simple linear models with nested CV and permutation testing.
- Imbalanced classification: optimize balanced accuracy, macro-F1, or AUC; use class weights when appropriate.
- Multimodal MRI: compare each modality alone against early fusion and MKL-style kernel fusion.

## MATLAB Built-Ins To Prefer

Classification:

- `fitcsvm`
- `fitclinear`
- `fitcecoc`
- `lassoglm`
- `fitcensemble`
- `TreeBagger`
- `perfcurve`
- `confusionmat`

Regression:

- `fitrsvm`
- `fitrlinear`
- `lasso`
- `ridge`
- `fitrensemble`
- `TreeBagger`
- `fitrgp`
- `corr`

Cross-validation and output:

- `cvpartition`
- `writetable`
- `writecell`
- `save`
- `exportgraphics`

Use libsvm only when matching legacy course code or a published analysis. When using libsvm, document version, path setup, and score polarity for AUC.

## Connectome Data

For FC/SC matrices:

1. Check matrix dimensions for all subjects.
2. Check NaN and Inf.
3. Set diagonal to zero unless diagonal contains meaningful subject features.
4. Test symmetry.
5. For undirected symmetric matrices, extract only the upper triangle.
6. For directed matrices, preserve direction.
7. Save edge labels such as `ROI_i_to_ROI_j`.
8. Reconstruct important-edge matrices only after fold-level selection/importance is computed.

## CPM / NBS

Use CPM/NBS-style methods when the user explicitly has connectome matrices and wants behavior prediction or edge-network interpretation.

Guardrails:

- Screen edges only inside training folds.
- Save positive and negative edge masks by fold.
- Evaluate prediction on held-out outer-test subjects.
- Use permutation testing for significance.
- Report edge networks as candidate predictive networks.

## Voxel Models

Use voxel-level models only when the user has masks/images and accepts high-dimensional risks.

Guardrails:

- Read NIfTI via SPM/NIfTI-compatible functions.
- Apply masks consistently.
- Preserve voxel-to-column mapping.
- Put PCA/screening/scaling inside folds.
- Warn about sample-size limitations.
- Save spatial maps only from leakage-safe fold summaries or clearly labeled exploratory full-training models.

## HYDRA and Subtypes

Use HYDRA-like workflows for disease heterogeneity, not for simple patient-control classification.

Guardrails:

- Separate subtype discovery from predictive evaluation.
- Assess subtype stability across resampling.
- Report subtype sizes and covariate differences.
- Do not overstate clinical subtype validity without external replication.

## MKL / Multimodal Fusion

Use MKL when modalities have distinct feature spaces, such as sMRI, fMRI, DTI, and clinical features.

Guardrails:

- Build modality-specific kernels inside training folds.
- Tune kernel/model parameters inside inner CV.
- Save fold-wise kernel weights.
- Compare against single-modality baselines.
- Treat modality weights as exploratory unless stable across folds and externally validated.

## SHAP

MATLAB does not have the same mature SHAP ecosystem as Python.

Offer these alternatives first:

- permutation importance
- linear SVM weights
- logistic coefficients
- LASSO/Elastic Net coefficients
- Random Forest predictor importance
- feature selection frequency

If SHAP is mandatory, export fold-level feature matrices, fold indices, predictions, and trained-model metadata for a Python SHAP workflow.
