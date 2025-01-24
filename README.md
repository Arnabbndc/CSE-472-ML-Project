# DEEP FAKE IMAGE DETECTOR ROBUST AGAINST ADVERSARIAL ATTACKS

This project focuses on improving the robustness of machine learning models in detecting real and fake images, even under adversarial attacks such as noise addition. The aim is to explore countermeasures to reduce performance degradation caused by such attacks.

---

## Problem Definition

Adversarial attacks, such as adding noise to images, can cause models like YOLO and ViT to misclassify real and fake images. Noise can be introduced in various ways, including:

- Pixel values
- Frequency domains
- Along gradient loss

### Countermeasures Explored

1. **Modifications to Training Data:**
   - Feature dropping
   - Data augmentations (e.g., rotating, zooming, cropping)
   - Smoothing
   - Adding random noise
   - Normalization

2. **Modifications to Model Architectures:**
   - Dropout layers
   - Adversarial noise layers
   - Regularization techniques

---

## Goals

1. **Baseline Evaluation:** Measure the performance of models without any adversarial noise.
2. **Adversarial Impact:** Evaluate performance drops after introducing noise to test data.
3. **Countermeasure Integration:** Incorporate countermeasures (data-level and model-level) and assess their impact on robustness.
4. **Performance Analysis:** Compare performance improvements post-countermeasure implementation.

---

## Models and Technologies Used

### **Models:**

- **ViT (Vision Transformer):** Used for initial classification tasks.
- **EfficientNet:** Tested for baseline performance.
- **YOLO-v11x (Custom Version):** Utilized for both baseline and adversarial robustness experiments.

### **Technologies and Tools:**

- **PyTorch:** For implementing and customizing machine learning models.
- **Python Libraries:** NumPy, Matplotlib, and SciPy for data manipulation and visualization.
- **CiFake Dataset:** A dataset with 60,000 real and 60,000 synthetic images.

---

## Experiments

### 1. Black Box Experiments

#### **Experiment 1: Baseline Model Performance**

- Dataset: [CiFake Dataset](https://www.kaggle.com/datasets/birdy654/cifake-real-and-ai-generated-synthetic-images)
- Results:

  | Model         | Accuracy |
  |---------------|----------|
  | ViT           | 98%      |
  | EfficientNet  | 88%      |
  | YOLO-v11x     | 92%      |

#### **Experiment 2: Adding Gaussian Noise**

- Noise Parameters: Mean = 0.0, Standard Deviation = 1.0
- Results:
  - Accuracy of YOLO-v11x dropped to **78%**.

#### **Experiment 3: Countermeasures**

1. **Feature Dropping:**
   - Dropped least correlated features.
   - Accuracy varied between **68-74%** based on the pixel drop percentage.
   - **Observation:** Feature dropping alone is ineffective.

2. **Resolution Reduction:**
   - Low-resolution images (32x32) further degraded performance.
   - **Observation:** Not a viable approach.

3. **Augmentations + Feature Dropping:**
   - Accuracy improved slightly to **73%** with augmentations and feature dropping.
   - **Observation:** Limited effectiveness; overfitting could be a concern.

4. **Augmentations + Adversarial Training:**
   - 50% of training data included Gaussian noise.
   - Best Accuracy: **85%**
   - **Observation:** Combining augmentations with adversarial training significantly improved robustness.

---

### 2. White Box Experiments

#### **Model Customizations**

- **Custom Dropout Layers:**
  - Dropout layers were added after convolution layers to reduce overfitting.
  - Accuracy on noisy data: **73%**

- **Adversarial Noise Layers:**
  - Adversarial noise layers were added before the initial convolution layer.
  - Accuracy on noisy data: **80%**

---

## Observations

1. **Impact of Noise:** Adding Gaussian noise significantly reduces model performance.
2. **Countermeasure Effectiveness:**
   - Adversarial training with noisy data improved robustness significantly.
   - Custom layers (e.g., adversarial noise and dropout) also provided performance boosts.
3. **Limitations:** Feature dropping and resolution reduction were ineffective due to the low resolution of the CiFake dataset.

---
