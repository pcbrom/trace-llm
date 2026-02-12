# Intermediate Data

Raw model outputs from the Chain-of-Thought (CoT) classification pipeline, including individual scores from all 5 LLM-judges.

## Note on Data Scope

This file contains the **full pipeline output** prior to sampling. Items corresponding to the N=500 sample can be identified by cross-referencing with `sample_data/evaluation_sample_n500.csv` using the shared keys (`source`, `item`, `model`, `prompt_type`).

## Purpose

This file provides direct access to the individual model-judge scores, enabling:

1. **Inspection of inter-judge agreement** without re-executing API calls
2. **Verification of score aggregation** (medians, means) reported in the paper
3. **Analysis of judge-specific patterns** (e.g., which judges tend to score higher/lower)
4. **Outlier detection** across the panel of 5 evaluators
