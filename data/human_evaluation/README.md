# Human Evaluation Data

Raw data from the human evaluation study described in Section 5 of the paper.

## Files

### `human_ratings_anonymized.csv`

Independent ratings from **3 human evaluators** on a stratified subset of model responses.

**Columns**:

- `source`: Benchmark dataset (MMLU, HellaSwag, ARC)
- `item`: Full question text with choices
- `answer`: Ground truth answer
- `model`: Evaluated model
- `prompt_type`: Prompt strategy (naive, cot, adversarial)
- `model_alternative_answer`: Model's selected answer
- `hit_alternative`: Correctness flag
- `justification`: Model's reasoning text
- `CoT`: Chain-of-thought trace
- `item_id`: Unique item identifier
- `gr_dor_human_000` / `001` / `002`: DoR scores from each evaluator
- `gr_ori_human_000` / `001` / `002`: ORI scores from each evaluator

### `human_calibrated_scores_subset.csv`

Calibrated comparison between **human median scores** and **LLM-judge median scores**, used to assess Human-LLM alignment.

**Columns**:

- `item_id`: Unique item identifier
- `source`, `model`, `prompt_type`: Item metadata
- `dor_human_median`: Median DoR from 3 human evaluators
- `dor_judge_median`: Median DoR from 5 LLM-judges
- `dor_judge_calibrated_to_human`: LLM score calibrated to human scale
- `ori_human_median`: Median ORI from 3 human evaluators
- `ori_judge_median`: Median ORI from 5 LLM-judges
- `ori_judge_calibrated_to_human`: LLM score calibrated to human scale

## Purpose

This data supports the paper's analysis of Human-LLM alignment (Section 5), demonstrating that while human and LLM evaluators show modest agreement, the LLM-judge framework is best suited for **internal comparative analysis** across models and prompt types rather than as a direct replacement for human evaluation.

## Privacy

All evaluator identities have been anonymized (evaluators labeled as `000`, `001`, `002`).
