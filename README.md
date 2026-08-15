# Explainable Plant Disease Classification Using EfficientNet and Grad-CAM

> **A foundational research project developed during the second semester of my B.Tech.**

This repository contains my implementation of an explainable deep learning framework for multiclass plant disease classification using **EfficientNet** and **Grad-CAM (Gradient-weighted Class Activation Mapping)**.

This project represents one of the earliest research-oriented projects I undertook during my **second semester of B.Tech.** It was developed as an independent exploration of deep learning, computer vision, transfer learning, and explainable artificial intelligence (XAI).

---

## About the Project

The objective of this work was not only to train a deep learning model capable of classifying plant diseases from leaf images, but also to investigate **why the model makes particular predictions**.

The project combines:

- Transfer learning using EfficientNet
- Multiclass plant disease classification
- Image preprocessing and model fine-tuning
- Prediction confidence analysis
- Grad-CAM-based visual explanations
- Quantitative analysis of misclassified samples
- Investigation of high-confidence classification errors

Rather than evaluating the model solely through overall accuracy, I explored the individual failure cases and examined the visual regions that contributed to incorrect predictions.

---

## Research Motivation

Deep learning models can achieve extremely high classification accuracy while still making confident mistakes.

This led to a simple research question:

> **If a model makes a wrong prediction, what visual information caused it to make that decision?**

To investigate this, Grad-CAM was applied to the model's convolutional feature representation. In particular, misclassified samples were analyzed using the **predicted class as the Grad-CAM target**, allowing the visualization to represent the regions that contributed to the model's incorrect decision.

This resulted in an analysis combining:

**Prediction → Confidence → Misclassification → Grad-CAM → Error Interpretation**

---

## Results

The model was evaluated on an independent test set containing:

- **38 classes**
- **8,143 test images**
- **8,132 correctly classified images**
- **11 misclassified images**
- **99.8649% test accuracy**
- **0.1351% test error rate**

The analysis of the 11 incorrect predictions produced several interesting observations.

The mean confidence of the incorrect predictions was approximately **73.23%**, while several errors were made with very high confidence.

In particular:

- **7/11 errors** had confidence ≥ 75%
- **3/11 errors** had confidence ≥ 90%
- The most frequent confusion involved visually similar **corn diseases**
- Additional confusion was observed among visually similar **tomato disease categories**

These results motivated the use of Grad-CAM as an additional tool for understanding model behavior rather than relying exclusively on aggregate classification metrics.

---

## Explainability

Grad-CAM was used to generate spatial activation maps from the final convolutional representation of the EfficientNet model.

For an input image, the process can be summarized as:

```text
Input Leaf Image
       │
       ▼
   EfficientNet
       │
       ▼
Class Probabilities
       │
       ▼
Predicted Class
       │
       ├───────────────┐
       │               │
       ▼               ▼
 Correct           Incorrect
 Prediction        Prediction
       │               │
       └───────┬───────┘
               ▼
            Grad-CAM
               │
               ▼
       Spatial Activation Map
               │
               ▼
       Visual Interpretation
