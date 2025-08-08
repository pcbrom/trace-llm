# Datasets Used in the TraCE-LLM Study

The datasets provided correspond to the evaluation outputs and analytical views generated during the empirical study described in the article *"The Adversarial Compensation Effect: Identifying Hidden Instabilities in Large Language Model Evaluation"*.

These datasets are the structured results of the **TraCE-LLM** protocol, which was designed to assess latent behavioral traits of Large Language Models (LLMs) through a multidimensional rubric. The evaluation framework measured two primary dimensions:

* **Depth of Reasoning (DoR)** – logical structure and coherence of the model's reasoning.
* **Originality (ORI)** – novelty and creativity of the model's output.

The study involved five LLMs, three benchmark datasets (MMLU, ARC-Challenge, HellaSwag), three prompt styles (Naive, Chain-of-Thought, Adversarial), and five independent replications per condition, totaling **10,125 observations**【25†source】.

---

## Relation of Datasets to the Study

1. **`cot_classification_df.csv`**

   * Contains CoT (Chain-of-Thought) classification results for a balanced subset of items.
   * Includes raw scores assigned by model-judges for DoR and ORI, the prompt type, and the final category assigned to the CoT.
   * Directly used to validate research hypotheses such as *Asymmetric Trait Stability* (H1) and *Partial Trait Separability* (H4).

2. **`cot_classification_df_hit1.csv`**

   * Same structure as above, but restricted to instances where the model produced the correct answer (hit = 1).
   * Used to study phenomena such as *Compressed Reasoning* (H5), where correct answers had low DoR scores.

3. **`df_outliers_view.csv`**

   * Focused on identifying and categorizing outlier responses in the CoT classification dataset.
   * Supports the detection of instability patterns, particularly under adversarial prompts (*Adversarial Collapse*, H2).

4. **`df_outliers_view_hit1.csv`**

   * Outlier analysis limited to the correct-answer subset.
   * Useful to highlight cases where a correct answer was accompanied by extreme ORI or DoR values, revealing instability masked by accuracy.

---

## Structure of the Datasets

Each dataset shares a common set of key columns:

| Column            | Description                                                                 |
| ----------------- | --------------------------------------------------------------------------- |
| `source`          | Origin or source of the evaluated data                                      |
| `item`            | Unique identifier for the evaluated item                                    |
| `model`           | Name of the AI model used for the evaluation                                |
| `prompt_type`     | Prompt style used (Naive, CoT, Adversarial)                                 |
| `CoT`             | Chain-of-Thought reasoning text or ID                                       |
| `gr_dor_*`        | Depth of Reasoning score by each model-judge                                |
| `gr_ori_*`        | Originality score by each model-judge                                       |
| `outlier_columns` | Columns flagged as containing outlier values                                |
| `CoT Category`    | (Only in classification files) Category assigned based on rubric evaluation |

---

## Usage in the Article's Analyses

* **Variability and Stability Analysis:** By comparing DoR and ORI distributions, the study confirmed that reasoning depth is inherently more stable than originality.
* **Outlier Detection:** Outlier datasets enabled the quantification of volatility in latent traits, especially under adversarial stress.
* **Compressed Reasoning Identification:** The `*_hit1.csv` datasets isolated cases where a correct answer had superficial reasoning, supporting the claim that accuracy alone is insufficient.
* **Model Agreement and Baselines:** All datasets contributed to computing the *median ensemble baseline*, which showed higher stability and alignment with high-performing models than any single judge.

---

## Recommended Applications

* **LLM Behavior Auditing** – Detect behavioral instability not visible through accuracy scores.
* **Prompt Robustness Testing** – Compare performance and stability across Naive, CoT, and Adversarial prompts.
* **Outlier Analysis** – Identify unusual patterns for further investigation.
* **Multidimensional Benchmarking** – Incorporate rubric-based traits (DoR, ORI) in model evaluations instead of relying on single scalar scores.
