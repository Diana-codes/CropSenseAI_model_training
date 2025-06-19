# 🌾 CropSense AI: Crop Disease Detection in Rwanda
**Author:** Diana Ruzindana  
**Program:** BSc in Software Engineering, African Leadership University

---

## 📜 Project Summary
CropSense AI is a machine learning–driven plant disease detection system tailored for smallholder farmers in Rwanda. Every year, local farmers lose up to 30% of crop yields due to undiagnosed diseases and pest attacks. CropSense aims to solve this by empowering farmers with a mobile tool that uses computer vision to diagnose plant diseases from images — even offline, using low-end smartphones.

The project is built on a plant image classification model trained on the **PlantVillage** dataset and optimized for performance in low-resource environments. Our goal is to support Rwanda’s Vision 2050 goals for digital agriculture and food security.

---

## 🚜 Motivation & Problem
Despite agriculture employing over 70% of Rwandans, many farmers cannot access expert support in time to diagnose crop issues. Extension officer shortages, limited internet access, and non-local AI models have all contributed to poor crop protection.

CropSense addresses this by:
- Using locally relevant image data (PlantVillage)
- Running completely offline on entry-level Android phones
- Supporting multiple crops and disease classes
- Empowering youth and farmers to co-create a more resilient agricultural system

---

## 📂 Dataset Summary
- **Source:** TensorFlow Datasets → [`plant_village`](https://www.tensorflow.org/datasets/catalog/plant_village)
- **Classes:** 38+ crop disease classes (e.g., Tomato mosaic virus, Potato early blight, etc.)
- **Type:** Image classification dataset
- **Size:** 54,000+ images
- **Format:** Color images resized to 64x64 pixels
- **Usage:** Train, validation split (80% / 20%)
- **Preprocessing:** Normalized pixel values, augmented via Keras pipelines

---

## ⚙️ Model Training Overview

| Instance | Model                    | Optimizer | Regularization | Epochs | Early Stopping | Layers           | Learning Rate | Accuracy | F1 Score | Recall | Precision | Loss   |
|----------|--------------------------|-----------|----------------|--------|----------------|------------------|----------------|----------|----------|--------|-----------|--------|
| 1        | CNN                      | Adam      | None           | 10     | No             | 2 Conv + Dense   | 0.001          | 0.8300   | 0.8200   | 0.8300 | 0.8200    | 0.6417 |
| 2        | CNN                      | RMSprop   | L2             | 10     | Yes            | 3 Conv + Dense   | 0.0005         | 0.8700   | 0.8600   | 0.8700 | 0.8600    | 0.5200 |
| 3        | CNN                      | Adam      | L1             | 10     | Yes            | 4 Conv + Dense   | 0.0003         | 0.8800   | 0.8700   | 0.8800 | 0.8700    | 0.4900 |
| 4        | CNN                      | RMSprop   | L1_L2          | 10     | No             | 3 Conv + Dense   | 0.0007         | 0.8500   | 0.8400   | 0.8500 | 0.8400    | 0.5100 |
| 5        | VGG16 + Logistic Reg.    | N/A       | None           | N/A    | No             | 1 (LogReg Layer) | N/A            | **0.9610** | **0.9620** | **0.9700** | **0.9500**  | N/A    |

---

## 🏆 Best Model: Instance 5 (VGG16 + Logistic Regression)

- **Why it’s best:** Outperformed all CNN-based models in accuracy and generalization.
- **Use case:** Lightweight, high-accuracy model for deployment on devices via saved `.pkl` or `.h5`.

---

## 🧪 Evaluation Strategy
All models were evaluated on the **same validation set** using:
- **Accuracy**
- **F1 Score**
- **Precision**
- **Recall**
- **Loss Curve**
- **Confusion Matrix** (plotted using seaborn)

---

## 🔮 Prediction Pipeline
- Final predictions use the best saved model: `saved_models/best_model.pkl`
- Logistic Regression fallback model included for offline inference
- `make_predictions(model_path, images)` is included in the notebook to run new predictions

---

## 📁 Folder Structure

