# Vehicle Detection with Supervised Domain Adaptation

This repository presents a solution to the problem of domain shift in vehicle detection systems using **Supervised Domain Adaptation (SDA)**. By leveraging both source and target labeled datasets, this method improves vehicle detection performance across diverse environmental and geographic conditions.

---

## 📌 Project Overview

Object detection models often fail when deployed in domains that differ from their training data due to issues such as lighting, weather, camera angles, and geographical variation. This project addresses this **domain shift challenge** by applying **Supervised Domain Adaptation** to align feature distributions between source and target domains.

---

## 💡 Problem Statement

- Vehicle detection models trained on one dataset perform poorly in another due to domain discrepancies.
- Manual re-labeling of new data is expensive and time-consuming.
- The goal is to enhance **cross-domain generalization** using minimal target domain data.

---

## 🧠 Approach: Supervised Domain Adaptation

SDA bridges the performance gap by:

- Utilizing labeled data from both the **source** and a small **target** dataset.
- Minimizing **feature distribution discrepancy** using **Maximum Mean Discrepancy (MMD)** or **CORAL** loss.
- Optimizing a combined **classification + domain adaptation loss**.

### 🔍 Feature Alignment Process

1. **Feature Extraction**: CNN (via YOLOv8 backbone) extracts image features.
2. **Mapping**: Features projected into a shared latent space.
3. **Domain Alignment**: Use MMD to align the distributions.
4. **Prediction**: Cross-entropy loss used for bounding box and class prediction.

---

## ⚙️ Implementation Details

- **Architecture**: YOLOv8-based object detection network
- **Framework**: PyTorch
- **Losses Used**:
  - Cross-entropy for classification
  - MMD or CORAL for domain adaptation
  - Weighted sum of losses for training
- **Hyperparameters**:
  - Batch size: Tuned for balance between speed and accuracy
  - Learning rate: Adjusted to stabilize domain alignment
  - Loss weights: Controlled impact of adaptation term

---

## 📁 Dataset

- Source domain: Kaggle vehicle datasets (urban/daylight scenarios)
- Target domain: Alternate dataset with varied lighting, weather, or camera angles

Both datasets consist of annotated images and videos for training and evaluation.

---

## 📊 Results

- Improved mAP (mean Average Precision) on target domain by aligning feature spaces
- Robust detection performance in:
  - **Urban Traffic**
  - **Surveillance Footage**
  - **Dense Traffic Scenarios**
- Enhanced detection of **small vehicles** like motorcycles and scooters

### ✨ Before vs After Domain Adaptation

| Metric            | Without Adaptation | With SDA |
|-------------------|--------------------|----------|
| Detection mAP     | 64.7%              | 81.2%    |
| False Positives   | High               | Reduced  |
| Detection on Edge | Poor               | Robust   |

---

## 📦 Repository Structure

├── datasets/
│ ├── source_dataset/
│ └── target_dataset/
├── models/
│ └── yolo_sda_model.py
├── train.py
├── evaluate.py
├── utils/
│ └── losses.py (MMD, CORAL, CE)
│ └── dataloader.py
├── results/
│ └── evaluation_metrics.csv
├── README.md
└── requirements.txt


---### yaml

## 🧪 Real-World Applications

- 🚗 **Autonomous Driving**: Vehicle detection across changing road conditions
- 📹 **Surveillance**: Detects vehicles under different lighting/weather
- 📊 **Traffic Monitoring**: More accurate vehicle counting and speed estimation
- 🛵 **Dense Traffic**: Detects small and partially occluded vehicles

---

## 🚀 How to Run

### 1. Clone the Repo
```bash
git clone https://github.com/yourusername/vehicle-detection-sda.git
cd vehicle-detection-sda

