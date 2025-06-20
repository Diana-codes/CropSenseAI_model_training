# 🌾 CropSense AI: Crop Disease Detection in Rwanda
**Author:** Diana Ruzindana  
**Program:** BSc in Software Engineering, African Leadership University

---

## 📜 Project Summary
CropSense AI is a machine learning–driven plant disease detection system tailored for smallholder farmers in Rwanda. Every year, local farmers lose up to 30% of crop yields due to undiagnosed diseases and pest attacks. CropSense empowers farmers with a mobile tool that uses computer vision to diagnose plant diseases from images — even offline, using low-end smartphones.

The project uses the **PlantVillage** dataset and multiple classification models (CNN and VGG16 + Logistic Regression) to identify crop diseases effectively.

---

## 🚜 Motivation & Problem
Although over 70% of Rwandans work in agriculture, most lack access to timely expert advice. The shortage of extension officers, limited connectivity, and generalized AI tools are major barriers.

CropSense solves this by:
- Using a publicly available, diverse plant disease dataset
- Providing offline detection using optimized models
- Targeting low-end Android smartphones
- Supporting multiple disease categories across major crops

---

## 📂 Dataset Summary
- **Source:** TensorFlow Datasets → [`plant_village`](https://www.tensorflow.org/datasets/catalog/plant_village)
- **Classes:** 38+ crop disease classes (e.g., Tomato Early Blight, Apple Scab, Potato Late Blight)
- **Images:** ~54,000 color images
- **Preprocessing:** Normalized, resized to 64x64 pixels
- **Split:** 80% training, 20% validation

---

## ⚙️ Model Training Overview

| Instance | Model                    | Optimizer | Regularization | Epochs | Early Stopping | Layers           | Learning Rate | Accuracy | F1 Score | Recall | Precision | Loss   |
|----------|--------------------------|-----------|----------------|--------|----------------|------------------|----------------|----------|----------|--------|-----------|--------|
| 1        | CNN                      | Adam      | None           | 10     | No             | 2 Conv + Dense   | 0.001          | **0.8915** | 0.8800   | 0.8800 | 0.8700    | 0.3900 |
| 2        | CNN                      | Adam      | L1             | 15     | Yes            | 3 Conv + Dense   | 0.0001         | 0.4935   | 0.6609   | 0.9744 | 0.5000    | 5.2036 |
| 3        | CNN                      | RMSprop   | L2             | 10     | Yes            | 3 Conv + Dense   | 0.0005         | 0.5584   | 0.2917   | 0.1795 | 0.7778    | 0.7839 |
| 4        | CNN                      | RMSprop   | L1             | 15     | Yes            | 3 Conv + Dense   | 0.0001         | 0.5455   | 0.6847   | 0.9744 | 0.5278    | 5.0626 |
| 5        | VGG16 + Logistic Reg.    | N/A       | None           | N/A    | No             | 1 (LogReg Layer) | N/A            | 0.7607   | 0.7500   | 0.7700 | 0.7400    | N/A    |

---

## 🏆 Best Model: Instance 1 (CNN + Adam, No Regularization)

- **Why it's best:** Achieved the highest accuracy (89.15%) and a strong F1-score with minimal tuning.
- **Characteristics:** Lightweight, efficient, and generalizable for real-world smartphone deployment.
- **Saved as:** `saved_models/best_model.keras`

---

## 🧪 Evaluation Strategy
All models were evaluated on the same test set. Metrics used:
- **Accuracy**
- **F1 Score**
- **Precision**
- **Recall**
- **Loss**
- **Confusion Matrix** (via Seaborn)

---

## 🔮 Prediction Pipeline
- Final predictions use the best model: `best_model.keras`
- VGG16 + Logistic Regression version is also available as backup
- Custom prediction function available in notebook
