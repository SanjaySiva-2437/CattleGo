# Machine Learning Module

### Livestock Breed Classification System

This module contains the **computer vision pipeline** responsible for identifying cattle breeds from images. The system uses a **MobileNetV2-based convolutional neural network** trained on images of Indian cattle breeds.

The model is designed to provide **accurate breed classification while remaining lightweight enough for mobile and edge deployment**.

---

# Overview

The machine learning system performs **image-based breed classification** using transfer learning and fine-tuning techniques.

Key goals of the model include:

* Accurate breed identification
* Efficient inference for mobile environments
* Robust generalization across different cattle images
* Integration with the mobile application and backend API

This module contains all code and assets related to:

* dataset preprocessing
* model training
* evaluation
* inference pipeline

---

# Model Architecture

The classifier is based on **MobileNetV2**, a lightweight convolutional neural network optimized for mobile environments.

**Architecture details**

* Base Model: MobileNetV2
* Framework: TensorFlow / Keras
* Input Resolution: 256 × 256 × 3
* Output: Softmax classification across cattle breed classes

MobileNetV2 was chosen due to its:

* low computational cost
* high efficiency on edge devices
* strong performance with transfer learning

---

# Training Pipeline

The training pipeline consists of several stages:

1. Data preprocessing and augmentation
2. Transfer learning using pretrained MobileNetV2 weights
3. Progressive fine-tuning
4. Model evaluation
5. Exporting the trained model for inference

---

# Dataset

The dataset consists of images representing **multiple Indian cattle breeds**.

Typical dataset characteristics:

* Breed diversity across several classes
* Images captured under varying lighting conditions
* Different camera angles and backgrounds

### Example Dataset Samples

*(Insert dataset sample images here)*

![Dataset Sample 1](ml-model/images/dataset_samples/gir.jpg)
![Dataset Sample 2](ml-model/images/dataset_samples/murrah_buffalo..jpg)

---

# Data Preprocessing

Before training, the dataset undergoes several preprocessing steps:

* image resizing to 256 × 256
* normalization
* dataset splitting (train / validation / test)
* augmentation

Augmentation techniques used:

* random rotation
* horizontal flipping
* zoom transformations
* brightness adjustments

These steps help improve **generalization and reduce overfitting**.

---

# Training Strategy

The model was trained using **transfer learning**.

### Phase 1 — Base Training

* Load pretrained MobileNetV2 weights
* Freeze base layers
* Train classification head

### Phase 2 — Fine-Tuning

* Unfreeze deeper layers
* Train with reduced learning rate
* Improve feature extraction for cattle breeds

---

# Training Progress

The training process involved multiple fine-tuning stages.

### Stage 1 — Initial Training

*(Insert training curve graph)*

![Training Stage 1](training/images/stage1.png)

Description of training behavior during the initial phase.

---

### Stage 2 — Intermediate Fine-Tuning

*(Insert training curve graph)*

![Training Stage 2](training/images/stage2.png)

Performance improvements and reduced overfitting.

---

### Stage 3 — Advanced Fine-Tuning

*(Insert training curve graph)*

![Training Stage 3](training/images/stage3.png)

Improved convergence and better generalization.

---

### Stage 4 — Final Optimization

*(Insert training curve graph)*

![Training Stage 4](training/images/stage4.png)

Final stage with stabilized accuracy and loss curves.

---

# Model Evaluation

The trained model is evaluated using multiple metrics.

Metrics include:

* accuracy
* confusion matrix
* classification distribution
* prediction confidence

---

## Confusion Matrix

*(Insert confusion matrix image here)*

![Confusion Matrix](evaluation/confusion_matrix.png)

The confusion matrix highlights:

* correct breed predictions
* misclassification patterns
* difficult breed classes

---

# Inference Pipeline

The trained model is used by the backend to perform **real-time breed detection**.

Inference pipeline:

```text
Image Input
    │
    ▼
Preprocessing
    │
    ▼
MobileNetV2 Model
    │
    ▼
Softmax Prediction
    │
    ▼
Breed Label + Confidence Score
```

Predictions are returned to the **FastAPI backend**, which then forwards results to the mobile application.

---

# Model Deployment

The trained model can be deployed in several ways:

* backend inference via FastAPI
* mobile deployment using TensorFlow Lite
* edge deployment on low-power devices

Future work includes optimizing the model for **mobile inference performance**.

---

# Repository Structure

```
ml-model
│
├── data-preparation
│   ├── dataaug.py
│   ├── traindata.py
│   ├── valdata.py
│   └── testdata.py
│
├── training
│   ├── Fine_Tune
│   └── training scripts
│
├── inference
│   └── app.py
│
├── evaluation
│   └── graphs
│
└── assets
    ├── class_indices.json
    └── path.txt
```

---

# Running the Training Pipeline

Install dependencies:

```bash
pip install -r requirements.txt
```

Prepare dataset:

```bash
python data-preparation/traindata.py
```

Train the model:

```bash
python training/train_model.py
```

Evaluate model:

```bash
python evaluation/evaluate_model.py
```

---

# Future Improvements

Potential improvements include:

* dataset expansion and balancing
* advanced augmentation strategies
* ensemble models
* hyperparameter optimization
* TensorFlow Lite deployment
* model compression techniques

---

# Integration With System

This module is part of the larger **Livestock AI Assistant architecture**.

The trained model is used by:

* FastAPI backend for inference
* mobile application for breed detection
* potential edge deployment pipelines
