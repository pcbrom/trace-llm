# Aggregated Tables - Data Transparency

This directory contains aggregated statistical tables generated from the **full dataset (N=10,125)** for reproducibility and transparency.

## Files

### 1. `means_by_model_prompt.csv`
**Mean scores by model and prompt type**

Columns:
- `model`: Model name
- `prompt_type`: Prompt style (naive, cot, adversarial)
- `n_cases`: Number of cases
- `hit_rate`: Accuracy (proportion of correct answers)
- `dor_mean`: Mean Depth of Reasoning score
- `dor_std`: Standard deviation of DoR
- `ori_mean`: Mean Originality score
- `ori_std`: Standard deviation of ORI

### 2. `cvs_by_model_prompt.csv`
**Coefficients of Variation (CVs) by model and prompt type**

Columns:
- `model`: Model name
- `prompt_type`: Prompt style
- `n_cases`: Number of cases
- `dor_cv_mean`: Mean CV for DoR (std/mean)
- `dor_cv_median`: Median CV for DoR
- `dor_cv_std`: Standard deviation of DoR CVs
- `ori_cv_mean`: Mean CV for ORI
- `ori_cv_median`: Median CV for ORI
- `ori_cv_std`: Standard deviation of ORI CVs

### 3. `kendall_tau_pairwise.csv`
**Pairwise Kendall's tau correlations between model-judges**

Columns:
- `prompt_type`: Prompt style
- `metric`: DoR or ORI
- `model_1`, `model_2`: Pair of model-judges being compared
- `kendall_tau`: Kendall's tau correlation coefficient
- `p_value`: Statistical significance
- `n_pairs`: Number of paired observations

### 4. `summary_statistics.csv`
**Overall summary statistics**

General statistics across the entire dataset (N=10,125).

## Methodology

All tables are generated from the full dataset using the script `generate_aggregated_tables.py`.

- **DoR/ORI scores**: Median across 5 model-judges per case
- **CVs**: Calculated as std/mean for each case, then aggregated
- **Kendall's tau**: Pairwise correlations between all model-judge pairs

## Usage

These tables enable:
1. Verification of reported statistics in the paper
2. Independent analysis without re-running model evaluations
3. Comparison with other evaluation frameworks
4. Meta-analysis of inter-rater reliability
