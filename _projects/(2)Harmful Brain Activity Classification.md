---
name: EEG-based Harmful Brain Activity Classification using Deep Learning
tools: [Python, PyTorch, Machine Learning, CNN, ResNET, XAI]
image: ../assets/images/HBAproject/gradcam.png
description: EEG signals are inherently challenging to interpret, even for trained clinicians. This study investigates whether deep learning models can accurately detect harmful brain activity from EEG data, while also addressing the interpretability of model predictions.
---


## **EEG-based Harmful Brain Activity Classification using Deep Learning**
<br>

<p class="text-center">
{% include elements/button.html link="https://github.com/hyeminss11/harmful-brain-activity-classification" text="View Project Repository" %}
</p>

#### 🍀 **Overview**
This study explores how deep learning models can detect neurological disorders from EEG data, while addressing interpretability challenges using model explainability tools.

---

#### 🍀 **Dataset**
  - The project is based on the Kaggle competition [HMS - Harmful Brain Activity Classification](https://www.kaggle.com/competitions/hms-harmful-brain-activity-classification).  
  - We used 50-second EEG segments labeled as one of five harmful brain activity types (excluding “Others”).<br>

---

#### 🍀 **Process**
  - Preprocessed raw EEG using **montage transformation** and **bandpass filtering**
  - Converted EEG into **scalogram images** using Continuous Wavelet Transform (CWT)
  - Trained and compared multiple models including:
    - **ResNet18** (my implementation)
    - EfficientNet
    - Vision Transformer (ViT)
  - Achieved **~81% accuracy** using ensemble, **~75%** with ResNet18

<p align="center">
  <img src="../assets/images/HBAproject/gradcam.png" alt="preview" width="500">
</p>

---

#### 🍀 **My Contribution** <br>
  - Implemented and trained **ResNet18** for EEG classification
  - Applied **Grad-CAM** for model interpretability
  - Tested baseline **2D CNN** → discontinued due to low generalization
  - Collaborated on model evaluation and ablation studies
<br>

---

#### 🍀 **Limitations**<br>
  - Grad-CAM does not support ViT well → heatmaps were not interpretable
  - Future work could include SHAP, Attention Rollout, or LRP for ViT explainability
