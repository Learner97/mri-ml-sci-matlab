# MRI ML SCI MATLAB

`mri-ml-sci-matlab` is a Codex skill for building, modifying, and reviewing MATLAB workflows for MRI and neuroimaging machine learning studies.

It is designed for researchers who need leakage-resistant machine-learning pipelines for brain MRI features, functional/structural connectivity, voxel maps, radiomics, multimodal MRI fusion, and clinical or cognitive outcomes.

The skill emphasizes:

- repeated nested cross-validation
- fold-internal preprocessing and feature selection
- confound control inside cross-validation
- permutation testing for model significance
- transparent output files for review and reproduction
- conservative interpretation of feature importance
- Chinese manuscript-ready methods, results, figure legends, and reviewer-risk notes

> This skill helps generate and audit research code. It is not a validated medical device, clinical diagnostic system, or substitute for statistical, clinical, or ethics review.

## Why This Skill Exists

MRI machine-learning manuscripts are often rejected or criticized because of preventable methodological problems:

- scaling or feature selection before cross-validation
- hyperparameter tuning on test data
- reporting only accuracy in imbalanced classification
- overinterpreting model weights as biomarkers
- missing permutation tests or confidence intervals
- unclear subject matching, covariate handling, or output reproducibility
- no external validation while making clinical claims

This skill gives Codex a strict workflow for avoiding those mistakes when generating MATLAB analysis projects.

## Methodological Position

The current workflow is broadly aligned with expectations in high-impact medical imaging and clinical prediction-model papers:

- [TRIPOD+AI](https://www.bmj.com/content/385/bmj-2023-078378): transparent reporting for clinical prediction models using regression or machine learning.
- [PROBAST+AI](https://www.bmj.com/content/388/bmj-2024-082505): quality, risk-of-bias, and applicability assessment for prediction models using regression or AI.
- [CLAIM 2024](https://pubs.rsna.org/doi/10.1148/ryai.240300): reporting checklist for artificial intelligence in medical imaging.

### Strong Points

The skill is already strong for manuscript-oriented MRI machine learning because it requires:

- nested CV for final model evaluation
- inner-loop feature selection and hyperparameter tuning
- training-fold-only imputation, scaling, residualization, PCA, harmonization, and resampling
- saved fold indices and out-of-fold predictions
- classification and regression metrics beyond accuracy
- permutation testing before significance claims
- feature-selection frequency and model-importance summaries
- explicit reviewer-risk checks
- conservative wording around biomarkers and clinical usefulness

### Remaining Study-Level Requirements

No skill can make a weak study design publishable by itself. For top SCI/SSCI submissions, users should still provide or document:

- prospective or clearly defined retrospective cohort design
- sample-size justification and class-balance assessment
- independent external validation whenever clinical generalization is claimed
- scanner/site/acquisition protocol information
- missing-data rules and exclusion criteria
- fairness or subgroup performance checks when relevant
- ethics approval, consent status, and data governance
- preregistration or locked analysis plan when possible
- complete dependency/version information for MATLAB and toolboxes

Use the skill as a guardrailed workflow engine, then report the study with the appropriate journal checklist.

## Installation

### Option 1: Install As A Local Codex Skill

Clone this repository directly into your Codex skills directory:

```bash
git clone https://github.com/Learner97/mri-ml-sci-matlab.git ~/.codex/skills/mri-ml-sci-matlab
```

On Windows PowerShell:

```powershell
git clone https://github.com/Learner97/mri-ml-sci-matlab.git "$env:USERPROFILE\.codex\skills\mri-ml-sci-matlab"
```

Restart Codex after installation so the skill metadata is loaded.

### Option 2: Copy The Folder Manually

Download or clone the repository, then copy the whole folder into:

```text
~/.codex/skills/mri-ml-sci-matlab
```

Keep these files together:

```text
mri-ml-sci-matlab/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── leakage-safe-workflow.md
    ├── local-code-map.md
    ├── model-routing.md
    └── reporting-and-review.md
```

Do not copy only `SKILL.md`; the references contain the detailed routing, leakage-control, model-selection, and reporting rules.

## How To Use

After restarting Codex, ask naturally:

```text
Use mri-ml-sci-matlab to build a MATLAB nested-CV classification pipeline for patient vs control MRI ROI features.
```

```text
Use mri-ml-sci-matlab to review this MATLAB script for data leakage and SCI/SSCI reviewer risks.
```

```text
Use mri-ml-sci-matlab to create a MATLAB regression workflow for FC matrices predicting cognitive scores, with permutation testing and Chinese results text.
```

```text
Use mri-ml-sci-matlab to compare single-modality sMRI, fMRI, DTI, and multimodal MKL models.
```

## Supported Data Types

- ROI-level MRI feature tables
- voxel/NIfTI-derived feature matrices
- functional connectivity matrices
- structural connectivity matrices
- graph-theory metrics
- radiomics features
- multimodal MRI feature blocks
- clinical, cognitive, behavioral, or prognostic outcomes
- covariates such as age, sex, education, ICV, head motion, site, scanner, lesion volume, medication, and disease duration

## Supported Models And Workflows

- SVM and SVR
- logistic regression
- LASSO, Ridge, and Elastic Net
- Random Forest and ensemble models
- Gaussian Process Regression
- CPM and NBS-style connectome prediction
- HYDRA-style disease-subtype workflows
- MKL-style multimodal fusion
- model comparison across modalities and algorithms
- permutation testing
- fold-wise feature importance and stability summaries
- Chinese methods/results/reporting text

## Expected Output From Generated Projects

For formal analyses, the skill asks Codex to save outputs such as:

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
- `feature_importance_summary.xlsx`
- `important_ROI_or_edges.xlsx`
- `methods_text_for_paper_CN.txt`
- `results_text_for_paper_CN.txt`
- `review_risk_checklist_CN.txt`

## Developer Notes

The skill uses progressive disclosure:

- `SKILL.md` contains the core trigger, workflow, and non-negotiable rules.
- `references/leakage-safe-workflow.md` contains nested-CV and anti-leakage details.
- `references/model-routing.md` contains model and data-type routing guidance.
- `references/local-code-map.md` maps optional local MATLAB teaching code patterns from `D:\Brain\MachineLearning_MC`.
- `references/reporting-and-review.md` contains manuscript reporting and reviewer-risk guidance.

If you extend this skill, keep the core file concise and move detailed model-specific instructions into `references/`.

## Contributing

Useful contributions include:

- MATLAB templates for leakage-safe nested CV
- regression and classification evaluation utilities
- connectome vectorization helpers
- fold-wise confound residualization functions
- CPM/NBS/MKL examples with synthetic data
- reporting templates aligned with TRIPOD+AI, PROBAST+AI, and CLAIM
- tests that intentionally detect common leakage patterns

Avoid committing private MRI data, large third-party toolboxes, generated patient outputs, or course materials with unclear redistribution rights.

## License

MIT License

Copyright (c) 2026 Learner97

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
