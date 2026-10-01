---
name: EEG-based Harmful Brain Activity Classification using Deep Learning
tools: [Python, PyTorch, Machine Learning, CNN, ResNET, XAI]
image: ../assets/images/HBAproject/gradcam.png
description: EEG signals are inherently challenging to interpret, even for trained clinicians. This study investigates whether deep learning models can accurately detect harmful brain activity from EEG data, while also addressing the interpretability of model predictions using Grad-CAM.
---


## **EEG-based Harmful Brain Activity Classification using Deep Learning**
<br>

<p class="text-center">
{% include elements/button.html link="https://github.com/hyeminss11/harmful-brain-activity-classification" text="View Project Repository" %}
</p>

### Why This Matters
EEG is central to diagnosing neurological conditions such as seizures and brain injury, but reading it is slow, costly, and subjective — expert agreement between clinicians is often low, and distinguishing visually similar abnormal patterns is error-prone. An accurate *and* interpretable automated system could give clinicians an objective second opinion they can actually trust. This project builds a model to classify five representative abnormal-EEG patterns — **Seizure, LPD, GPD, LRDA, and GRDA** — and, just as importantly, to show *why* it makes each prediction.

### Overview
This study explores how deep learning models can detect harmful brain activity from EEG data, while addressing interpretability challenges using model explainability tools.

### Dataset
- Based on the Kaggle competition [HMS - Harmful Brain Activity Classification](https://www.kaggle.com/competitions/hms-harmful-brain-activity-classification).
- We used 50-second EEG segments labeled as one of five harmful brain activity types (excluding "Others").

### Process
- Preprocessed raw EEG using **montage transformation** and **bandpass filtering (0.5–40 Hz)**
- Converted EEG into **scalogram images** using Continuous Wavelet Transform (CWT)
- Trained and compared multiple models including:
  - **ResNet18** (my implementation)
  - EfficientNet
  - Vision Transformer (ViT)
- Achieved **~81% accuracy** using a weighted ensemble, and **~75%** with ResNet18 alone

<p align="center">
  <img src="../assets/images/HBAproject/gradcam.png" alt="preview" width="500">
</p>

### My Contribution
- Implemented and trained **ResNet18** for EEG classification (baseline accuracy ~75%, a ~30%p gain over a plain 2D CNN)
- Applied **Grad-CAM** for model interpretability
- Designed and tested a baseline **2D CNN** → discontinued due to low generalization
- Collaborated on model evaluation and ablation studies

### Results & Error Analysis
- **Strong sensitivity** on LPD and GRDA classes, capturing distinct EEG patterns within the scalograms
- Some **LRDA** samples were initially misclassified as Seizure or LPD; this was mitigated through ensemble learning, lifting final system accuracy to **~81%**
- **Grad-CAM** confirmed the model attends to clinically meaningful EEG signals rather than background noise — supporting the transparency needed for AI-assisted diagnosis

### Limitations
- Grad-CAM does not support ViT well → heatmaps were not interpretable
- Future work could include SHAP, Attention Rollout, or LRP for ViT explainability
