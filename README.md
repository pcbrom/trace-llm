# pcbrom/trace-llm: TraCE-LLM

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18549676.svg)](https://doi.org/10.5281/zenodo.18549676)
[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

## License

This repository, including source code, notebooks, datasets, and documentation, is licensed under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/).

You are free to use, share, and adapt this work for **non-commercial purposes**, provided you give appropriate credit and distribute derivative works under the same license.

> **Commercial use** requires a separate written agreement with the copyright holders. Contact: pcbrom@gmail.com

See [`LICENSE`](LICENSE) for full terms.

---

## Citation

Pedro Carvalho Brom, Di Oliveira, V., & Weigang, L. (2025). TraCE-LLM: Evaluation datasets and pipeline (v2.3). Zenodo. https://doi.org/10.5281/zenodo.18549677

```bibtex
@misc{brom_oliveira_weigang_2025_tracellm,
  author       = {Brom, Pedro Carvalho and Di Oliveira, V. and Weigang, L.},
  title        = {{TraCE-LLM: Evaluation datasets and pipeline (v2.3)}},
  year         = {2025},
  publisher    = {Zenodo},
  version      = {2.3},
  doi          = {10.5281/zenodo.18549677},
  url          = {https://doi.org/10.5281/zenodo.18549677}
}
```

---

# Overview

This repository contains the core assets used in the TraCE-LLM study described in the article  
*“The Adversarial Compensation Effect: Identifying Hidden Instabilities in Large Language Model Evaluation”*.

The project is centered on the **TraCE-LLM protocol**, which measures latent behavioral traits of Large Language Models (LLMs) using a multidimensional rubric with two primary dimensions:

- **Depth of Reasoning (DoR)** – logical structure and coherence of the model's reasoning.
- **Originality (ORI)** – novelty and creativity of the model's output.

For human rater instructions and rubric anchors (DoR/ORI 0–10), see `Instructions Human Evaluation Protocol.pdf`.

The full experimental pipeline (data generation, judgment, and analysis) is documented in the notebooks in this repository. An N=500 evaluation sample with derived traits is included in `data/evaluation_sample_n500.csv`. The same contents are archived on Zenodo for long-term preservation and DOI citation.

---

## Human Evaluation Protocol (DoR/ORI)

The human ratings in this study follow the protocol outlined in `Instructions Human Evaluation Protocol.pdf`, which was provided to all human evaluators. The protocol covers two main rubric dimensions:

- **DoR (Depth of Reasoning):** Assessed based on logical structure, coherence, chaining of arguments, consideration of alternatives, and quality of justification.
- **ORI (Originality):** Assessed based on novelty, creativity, non-paraphrastic content, original insights or structure while remaining on-topic.

**Scoring instructions** (as implemented and enforced in `human_baseline_results.ipynb`):

- Only rate the text under **MODEL OUTPUT**.
- Do not consult external sources; use only general knowledge for evaluating coherence.
- Scores must not reflect agreement/disagreement with the answer content, nor adherence to a specific "correct answer".
- Both DoR and ORI must be rated using **integers from 0 to 10** (no decimals).
- Identical anchors are used for both metrics (see PDF or rubric): **0, 2, 4, 6, 8, 10** are recommended anchor points, but any whole number 0–10 may be used as appropriate.
- Ratings outside 0–10 or non-integer entries are treated as missing in the baseline analyses (`human_baseline_results.ipynb`).
- During analysis, scores are often discretized into bins for agreement metrics (see code in `human_baseline_results.ipynb` for exact bins).

For further details and the rationale behind rater instructions, see both the handout PDF and the code in `human_baseline_results.ipynb`.

## Repository Structure

```
trace-llm/
├── README.md
├── LICENSE
├── Instructions Human Evaluation Protocol.pdf
├── CITATION.cff
├── .zenodo.json
│
├── first_step_and_sample.ipynb
├── second_step.ipynb
├── aed_and_model_sample.ipynb
├── classical_metrics_sample.ipynb
├── human_baseline_results.ipynb
│
├── data/
│   ├── README.md
│   ├── evaluation_sample_n500.csv
│   ├── summary_statistics_sample.csv
│   ├── ARC_test/
│   │   └── test-00000-of-00001.parquet
│   ├── MMLU_test/
│   │   └── test-00000-of-00001.parquet
│   ├── hellaswag_test/
│   │   └── hellaswag_val.jsonl
│   └── human_evaluation/
│       ├── README.md
│       ├── human_calibrated_scores_subset.csv
│       └── human_ratings_anonymized.csv
│
├── aggregated_tables/
│   ├── README.md
│   ├── cvs_by_model_prompt.csv
│   ├── kendall_tau_pairwise.csv
│   ├── means_by_model_prompt.csv
│   └── summary_statistics.csv
│
└── examples/
    ├── README.md
    ├── ace/                      (2 files)
    ├── compressed_reasoning/     (5 files)
    ├── crossed_cases/            (20 files)
    ├── dor_high/                 (5 files)
    ├── dor_low/                  (5 files)
    ├── high_quality/             (5 files)
    ├── ori_high/                 (5 files)
    └── ori_low/                  (4 files)
```

### Root Files

| File | Description |
|------|-------------|
| `first_step_and_sample.ipynb` | First-step pipeline notebook (prompt engineering and sampling). |
| `second_step.ipynb` | Second-step rubric evaluation notebook (model-internal evaluation / LLMs as judges). |
| `aed_and_model_sample.ipynb` | Analysis of ensemble vs. individual models and trait structure (DoR/ORI). |
| `classical_metrics_sample.ipynb` | Computation of classical metrics (accuracy, F1, etc.) on tidy TraCE-LLM outputs. |
| `human_baseline_results.ipynb` | Human-baseline evaluation analysis and inter-rater agreement. |
| `Instructions Human Evaluation Protocol.pdf` | One-page human rater instructions and DoR/ORI rubric anchors. |
| `CITATION.cff` | Machine-readable citation metadata (GitHub integration). |
| `.zenodo.json` | Zenodo deposit metadata for automated releases. |

### `data/`

Benchmark test sets and evaluation data used as sources for TraCE-LLM items.

| Path | Description |
|------|-------------|
| `evaluation_sample_n500.csv` | N=500 evaluation sample used in the study. |
| `summary_statistics_sample.csv` | Summary statistics for the evaluation sample. |
| `ARC_test/test-00000-of-00001.parquet` | Multiple-choice ARC-Challenge items (`id`, `question`, `choices`, `answerKey`). |
| `MMLU_test/test-00000-of-00001.parquet` | MMLU test split (`question`, `subject`, `choices`, `answer`). |
| `hellaswag_test/hellaswag_val.jsonl` | HellaSwag validation split in JSONL format. |
| `human_evaluation/human_ratings_anonymized.csv` | Anonymized human rater scores. |
| `human_evaluation/human_calibrated_scores_subset.csv` | Calibrated subset of human scores. |

### `aggregated_tables/`

Pre-computed aggregated statistics referenced in the article.

| File | Description |
|------|-------------|
| `summary_statistics.csv` | Overall summary statistics for DoR and ORI. |
| `means_by_model_prompt.csv` | Mean trait scores by model × prompt type. |
| `cvs_by_model_prompt.csv` | Coefficients of variation by model × prompt type. |
| `kendall_tau_pairwise.csv` | Pairwise Kendall-τ correlations between judge-models. |

### `examples/`

Curated illustrative cases from the evaluation, organized by trait category.

| Subdirectory | Description |
|--------------|-------------|
| `ace/` | Adversarial Compensation Effect (ACE) examples. |
| `compressed_reasoning/` | Cases of compressed or abbreviated reasoning. |
| `crossed_cases/` | Cases exhibiting crossed trait profiles. |
| `dor_high/` / `dor_low/` | High and low Depth of Reasoning examples. |
| `ori_high/` / `ori_low/` | High and low Originality examples. |
| `high_quality/` | High-quality exemplar outputs. |

> An N=500 evaluation sample with derived traits (CoT classifications, DoR/ORI scores, judge justifications) is included in `data/evaluation_sample_n500.csv`. The full-population prediction tables are not distributed.

No `figures/` directory is tracked in this repo; figures referenced in the paper are generated on demand by the analysis notebooks.

---

## Notebooks and Their Roles

This section documents what each notebook in the repository does and how it relates to the datasets.

### `first_step_and_sample.ipynb`

**Goal:** Build unified multiple-choice items from the benchmark datasets and define the first-step prompting scheme for LLMs.

- Loads benchmark test splits from `data/`:
  - ARC-Challenge items from `data/ARC_test/test-00000-of-00001.parquet`.
  - MMLU items from `data/MMLU_test/test-00000-of-00001.parquet`.
  - HellaSwag items from `data/hellaswag_test/hellaswag_val.jsonl`.
- Normalizes each dataset to a common schema, conceptually producing tables with:
  - `source` (ARC, MMLU, HellaSwag),
  - `item` (question/context plus options),
  - `answer` (A/B/C/D).
- Demonstrates how to construct balanced samples across sources for evaluation (e.g., equal number of items per dataset).
- Defines prompt templates for three prompting regimes:
  - **`cot`** – chain-of-thought prompts that request step-by-step reasoning and JSON output with fields such as `CoT`, `answer`, `justification`.
  - **`naive`** – straightforward question-answer prompts with JSON output containing `answer` and `justification`.
  - **`adversarial`** – prompts that explicitly ask the model to question its own assumptions and, if necessary, choose an extra option `E` with an alternative answer.
- Configures API clients for external LLMs via environment variables (see *Reproducibility* below) and sketches the loop that:
  - iterates over models and prompts,
  - applies the prompts to sampled items,
  - collects JSON outputs for further processing.

The notebook is written to be re-runnable with the available benchmark files and user-provided API keys; it **does not commit any generated CSV/Parquet files** to this repository.

### `second_step.ipynb`

**Goal:** Apply the zero-shot semantic interval rubric using model-internal evaluation (LLMs as judges of DoR and ORI).

- Describes the **Second Step** of TraCE-LLM: judge-models score each Chain-of-Thought on:
  - Depth of Reasoning (DoR),
  - Originality (ORI),
  according to a semantic interval rubric.
- Loads API keys from a local `.env` file and configures judge-clients for:
  - GPT-4 family,
  - Claude 3.5 Haiku,
  - xAI Grok,
  - DeepSeek Chat.
- Maintains a `models` registry and helper functions like:
  - `step_two(model_name, prompt)` – calls the appropriate client and returns the judge’s textual output.
  - `step_two_recovered(model_name, prompt)` – a self-contained variant that reconstructs the client from `model_name`.
- Expects as input a tidy table of CoT outputs from the first step, with columns conceptually including:
  - `source`, `item`, `answer`, `r`,
  - `model`, `prompt_type`,
  - `model_answer`, `hit`,
  - `model_alternative_answer`, `hit_alternative`,
  - `CoT`, `cot_steps`.
- For each row, constructs a rubric prompt, queries judge-models and parses their outputs into:
  - DoR scores (`gr_dor_*`) and explanations,
  - ORI scores (`gr_ori_*`) and explanations,
  - optional rubric criteria labels.

The resulting enriched tables (with `gr_dor_*` and `gr_ori_*` columns) are **generated at runtime**; an N=500 sample is included in `data/evaluation_sample_n500.csv`.

### `aed_and_model_sample.ipynb`

**Goal:** Analyze trait scores across models and ensembles, and study the latent structure of DoR/ORI.

- Assumes access to a trait-augmented dataset produced by the second step, containing:
  - base columns from the CoT evaluation (source, item, model, prompt type, etc.),
  - judge-model DoR and ORI scores (`gr_dor_*`, `gr_ori_*`),
  - optionally, rubric criteria (`criterion_x`, `criterion_y`).
- Computes ensemble statistics such as:
  - per-observation medians (`gr_dor_median`, `gr_ori_median`) across judge-models,
  - per-model descriptive statistics (mean, std, median, min, max, coefficient of variation) for DoR and ORI.
- Performs multivariate analyses of trait profiles, e.g.:
  - PCA projections of models in trait space,
  - hierarchical clustering of models,
  - correlation analyses (e.g., Kendall correlation between models or between traits).
- Generates figures used in the article (PCA, dendrograms, correlograms, comparisons of DoR vs ORI).  
  These figures are **not stored** in this Git repo by default but can be saved locally when running the notebook.

### `classical_metrics_sample.ipynb`

**Goal:** Compute and compare classical evaluation metrics over TraCE-LLM prediction tables.

- Expects as input a tidy table of multiple-choice predictions with, at minimum:
  - true answer labels (A/B/C/D),
  - model predictions,
  - metadata such as `model`, `prompt_type`, and `source`.
- Builds derived columns like `model_prompt_type` (e.g., `"model_gpt_4o_mini_cot"`).
- Implements helper routines to:
  - compute overall accuracy, macro and weighted precision, recall and F1,
  - produce confusion matrices (per class and aggregated),
  - aggregate metrics by:
    - prompt type (`cot`, `naive`, `adversarial`),
    - dataset source (`ARC`, `MMLU`, `HellaSwag`),
    - model or model–prompt combinations.
- Performs statistical comparisons of prompt regimes, including:
  - Friedman tests on class-level F1 scores,
  - Nemenyi post-hoc tests for pairwise comparisons.
- Optionally creates visualization-ready tables and plots (e.g., weighted F1 by condition, facet plots by hit status); these artifacts are generated at runtime and are not checked into this repository.

---

## Zenodo Archive

The Zenodo deposit mirrors the contents of this repository for long-term preservation and DOI-based citation. Both contain the same files.

When working locally, you can:

1. Use the benchmark test files in `data/` to reconstruct the item pool.  
2. Run `first_step_and_sample.ipynb` to generate model responses under different prompt regimes.  
3. Run `second_step.ipynb` to obtain DoR and ORI scores from judge-models.  
4. Use the resulting tables as input to `aed_and_model_sample.ipynb` and `classical_metrics_sample.ipynb` to reproduce analyses and figures.

---

## Reproducibility Notes

- **Environment variables:**  
  Notebooks that query external APIs (`first_step_and_sample.ipynb`, `second_step.ipynb`) expect a `.env` file (outside this repo or at a user-specified path) defining keys such as:
  - `OPENAI_API_KEY`
  - `ANTHROPIC_API_KEY`
  - `XAI_API_KEY`
  - `DEEPSEEK_API_KEY`

- **Python environment:**  
  The notebooks assume a recent Python 3 version with standard data/ML libraries (e.g., `pandas`, `numpy`, `scikit-learn`, plotting libraries) and the respective API client libraries for the LLM providers.

- **Generated artifacts:**  
  Figures produced by the notebooks are generated locally when you run them and are not committed to this repository.

---

## Suggested Uses

- **LLM behaviour auditing:**  
  Study stability and variability of model reasoning beyond simple accuracy metrics.

- **Prompt robustness testing:**  
  Compare model performance and stability across naive, chain-of-thought, and adversarial prompting strategies.

- **Trait-based benchmarking:**  
  Use Depth of Reasoning and Originality as explicit evaluation dimensions alongside classical metrics.

- **Outlier and instability analysis:**  
  Investigate cases where models give correct answers with shallow reasoning, or where adversarial prompts cause abrupt changes in behaviour.
