# Supplementary Examples

This directory contains representative examples from the N=500 sample, organized by reasoning quality characteristics. All examples are drawn from the evaluation dataset described in the paper.

## Overview

The examples illustrate the spectrum of reasoning quality observed across different models and prompt types. Each category highlights specific patterns in how LLMs approach reasoning tasks, from shallow to deep reasoning, and from conventional to creative responses.

## Categories

### 1. DoR Low (`dor_low/`)

**Criterion**: Depth of Reasoning (DoR) < Q1

Examples where models provided **shallow reasoning** despite potentially correct answers. These cases demonstrate minimal elaboration, limited step-by-step thinking, or superficial engagement with the problem.

**Characteristics**:

- Brief justifications
- Missing intermediate steps
- Limited exploration of alternatives
- Minimal contextual analysis

**5 examples** selected from the lower quartile of DoR scores.

---

### 2. DoR High (`dor_high/`)

**Criterion**: Depth of Reasoning (DoR) > Q3

Examples showcasing **deep, thorough reasoning**. Models demonstrate comprehensive analysis, explicit step-by-step thinking, consideration of alternatives, and detailed justifications.

**Characteristics**:

- Extensive elaboration
- Clear reasoning chains
- Exploration of edge cases
- Comprehensive problem decomposition

**5 examples** selected from the upper quartile of DoR scores.

---

### 3. ORI Low (`ori_low/`)

**Criterion**: Originality (ORI) < Q1

Examples of **conventional, predictable reasoning**. Responses follow standard patterns, use common phrasing, and lack creative or novel approaches to problem-solving.

**Characteristics**:

- Formulaic responses
- Standard templates
- Minimal creativity
- Conventional problem-solving approaches

**5 examples** selected from the lower quartile of ORI scores.

---

### 4. ORI High (`ori_high/`)

**Criterion**: Originality (ORI) > Q3

Examples demonstrating **creative, novel reasoning**. Models employ unique perspectives, unconventional approaches, or distinctive phrasing while maintaining correctness.

**Characteristics**:

- Unique problem-solving strategies
- Creative explanations
- Novel perspectives
- Distinctive reasoning patterns

**5 examples** selected from the upper quartile of ORI scores.

---

### 5. High Quality (`high_quality/`)

**Criterion**: hit=1 AND DoR > Q3 AND ORI > Q3

High-quality examples represent the **gold standard** of LLM reasoning: correct answers delivered with both deep reasoning and creative expression.

> [!NOTE]
> **About ACE (Adversarial Compensation Effect)**: ACE is **not** a category of isolated examples, but rather a **phenomenon** observed in **pairs** of responses (Naive vs. Adversarial) from the same model on the same item. ACE occurs when a model shows paradoxical accuracy gains under adversarial prompting while simultaneously exhibiting severe degradation in behavioral stability (increased variance in ORI, decreased agreement with peer models). ACE examples require paired data and are analyzed separately in the paper's main analysis, not in this supplementary examples directory.

**Characteristics**:

- Correct final answer (hit=1)
- Thorough, step-by-step reasoning (high DoR > Q3)
- Creative, engaging presentation (high ORI > Q3)
- Optimal balance of depth and originality

**5 examples** selected from cases meeting all three criteria simultaneously.

---

### 6. Compressed Reasoning (`compressed_reasoning/`)

**Criterion**: hit=1 AND at least one model with DoR < 4

**Compressed reasoning** is a critical phenomenon identified in the paper: models that arrive at **correct answers through shallow reasoning**. This pattern suggests potential shortcuts, pattern matching, or memorization rather than genuine understanding.

**Operational Definition**: A correct response (hit=1) where at least one of the five models assigned a DoR score below 4.

**Selection Strategy**: To ensure model diversity, we selected **1 example from each of the 5 models** (5 total), representing the range of compressed reasoning patterns across different architectures.

**Significance**: These cases are particularly important for understanding the limitations of accuracy-only evaluation metrics and the value of process-based assessment.

---

### 7. Crossed Cases (`crossed_cases/`)

**Purpose**: Identify cases where DoR and ORI exhibit **opposite extremes**, revealing distinct reasoning patterns.

#### 7.1 High DoR + Low ORI (`crossed_cases/high_dor_low_ori/`)

**Criterion**: DoR > Q3 AND ORI < Q1

Cases where models demonstrate **deep reasoning with conventional expression**. These responses show thorough analysis but use formulaic, predictable language.

**Interpretation**: "Thorough but templated" - comprehensive reasoning delivered through standard patterns.

**10 examples** selected from cases meeting both criteria.

#### 7.2 Low DoR + High ORI (`crossed_cases/low_dor_high_ori/`)

**Criterion**: DoR < Q1 AND ORI > Q3

Cases where models show **creative expression with shallow reasoning**. These responses use novel phrasing but lack depth of analysis.

**Interpretation**: "Creative but superficial" - original presentation masking limited reasoning depth.

**10 examples** selected from 21 cases meeting both criteria.
