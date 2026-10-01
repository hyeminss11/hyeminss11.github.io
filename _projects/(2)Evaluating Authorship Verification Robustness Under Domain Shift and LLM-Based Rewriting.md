---
name: Evaluating Authorship Verification Robustness Under Domain Shift and LLM-Based Rewriting
tools: [Python, PyTorch, Deep Learning, NLP, LLM, AI Safety]
image: ../assets/images/dissertation/shap.png
description: An MSc dissertation examining how reliably transformer-based authorship verification (AV) models detect the same author across text domains (news vs. tweets) and under LLM-based adversarial rewriting. Using the CROSSNEWS dataset, it quantifies how vulnerable current AV systems are to style obfuscation and impersonation attacks — with implications for AI safety and misuse detection.
---

## **Evaluating Authorship Verification Robustness Under Domain Shift and LLM-Based Rewriting**
<br>

<p class="text-center">
{% include elements/button.html link="https://github.com/hyeminss11/msc-dissertation" text="View Project Repository" %}
</p>

### Why This Matters
As large language models spread, imitating someone else's writing style — or hiding your own — has become trivially easy. In August 2025, articles attributed to a specific journalist were later revealed to have been AI-generated, and AI-based impersonation fraud rose 148% year-on-year across 2024–2025. If text can be rewritten at will, how much can we still trust the models meant to tell authors apart? This dissertation puts that question to the test.

### Overview
This project investigates the robustness of transformer-based authorship verification (AV) models under two challenging real-world conditions: **domain shift** (e.g., news articles vs. tweets) and **adversarial rewriting** using large language models (style obfuscation and impersonation). The work was conducted as my MSc dissertation at the University of Sheffield.

### Key Findings
- **Model size ≠ robustness.** All BERT-based models proved vulnerable to attacks regardless of size — challenging the assumption that larger models are more reliable.
- **A catastrophic collapse.** Under combined genre-shift + LLM rewriting, ROC-AUC fell from ~0.88 to ~0.55 — essentially a coin flip.
- **Impersonation is the deadliest attack.** Targeted impersonation degraded performance more severely than untargeted obfuscation across every model.
- **Models cheat.** SHAP analysis showed models often rely on platform-specific artifacts (hashtags, URLs) and topic words rather than genuine authorial style — a structural limitation that accelerates failure under domain shift.

### Research Questions
1. **Domain Shift**: Can AV models reliably detect stylistic consistency across different genres when no adversarial rewriting is applied?
2. **Adversarial Robustness**: How robust are these models to LLM-based rewriting (obfuscation and impersonation) within the same domain?
3. **Combined Challenge**: How do AV models perform when domain shift and adversarial attacks are combined?

### Approach

**Design choices to isolate style.** Because AV models are highly sensitive to text length, all documents were standardised to 300–420 words to remove length bias. Personal identifiers (URLs, emails, usernames) were replaced with generic tokens (e.g., `USER_1234`) so the model could not rely on user IDs or names instead of writing style. A **Bi-Encoder** architecture was adopted to process large volumes of text efficiently.

**Models.** Three transformer architectures were selected to represent different design trade-offs:

| Model | Description | Parameters | Context Length |
|-------|-------------|------------|----------------|
| **DistilBERT** | Lightweight, efficient baseline | 66M | 512 tokens |
| **RoBERTa** | Enhanced BERT with robust pretraining | 125M | 512 tokens |
| **BigBird** | Sparse attention for long sequences | 128M | 4096 tokens |

**Adversarial attacks.** Two LLM-based attack strategies were built using Flan-T5-Large:
1. **Style Obfuscation** — untargeted paraphrasing to conceal authorial cues
2. **Style Impersonation** — targeted rewriting to mimic another author's style

### Results

#### In-Domain (Article–Article)

| Model | ROC-AUC | Accuracy | F1 Score |
| --- | --- | --- | --- |
| DistilBERT | 0.8882 | 0.7999 | 0.8161 |
| RoBERTa | 0.8785 | 0.7946 | 0.8084 |
| BigBird | 0.8108 | 0.7321 | 0.7438 |

#### Cross-Domain (Article–Tweet)

| Model | ROC-AUC | Accuracy | F1 Score |
| --- | --- | --- | --- |
| DistilBERT | 0.8711 | 0.7874 | 0.8006 |
| RoBERTa | 0.8703 | 0.6127 | 0.4880 |
| BigBird | 0.8149 | 0.6719 | 0.5891 |

#### Worst Case (Impersonation + Domain Shift)

| Model | ROC-AUC | Accuracy | F1 Score |
| --- | --- | --- | --- |
| DistilBERT | 0.5590 | 0.5406 | 0.5431 |
| RoBERTa | 0.5587 | 0.5391 | 0.5455 |
| BigBird | 0.5444 | 0.5316 | 0.5305 |

### Interpretability (SHAP)
**SHAP (SHapley Additive exPlanations)** analysis revealed how the models actually make decisions:
- Models often rely on **platform-specific artifacts** (hashtags, URLs) rather than genuine stylistic cues
- **Punctuation patterns** and **function words** dominate decisions under adversarial conditions
- Even correct predictions often stem from **topic-related content** rather than authorial style

This over-reliance on surface signals is a core reason performance degrades so sharply once the domain changes — evidence of a structural limitation in current AV systems.

### Dataset
This project uses the [CrossNews](https://github.com/mamarcus64/CrossNews) dataset as a Git submodule.

> **Citation**: M. Ma, "CROSSNEWS: A Cross-Genre Authorship Verification and Attribution Benchmark", AAAI, vol. 39, no. 23, pp. 24777–24785, Apr. 2025.

### Reproducibility & Ethics
All experiments use fixed random seeds (7, 1001, 1211) for reproducibility. The project was ethically reviewed and approved by the Ethics Committee of the University of Sheffield.
