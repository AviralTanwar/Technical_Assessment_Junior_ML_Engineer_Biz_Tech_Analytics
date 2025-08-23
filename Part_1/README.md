# Gloved vs. Bare Hand Detection

## 📌 Project Overview
This project is part of the Technical Assessment.  
The goal is to build a **safety compliance system** that can detect whether a worker’s hand is **gloved** or **bare (unprotected)** in images.  

The system:
- Takes images as input  
- Runs object detection (YOLOv8)  
- Outputs annotated images with bounding boxes  
- Logs detections in JSON format  

---

## 📂 Dataset
- **Source:** Provided dataset (manually labeled, stored in `train/`, `valid/`, `test/` folders)  
- **Format:** Images (`.jpg`) with annotations (`_annotations.csv`)  
- **Classes:**  
  1. `bare_hand`  
  2. `gloved_hand`  

Before training, the CSV annotations were converted into **YOLO format** (`.txt` per image).  

### Dataset Split
- **Train:** Used to teach the model patterns (~70%)  
- **Validation:** Used to tune hyperparameters (~15%)  
- **Test:** Used for final performance evaluation (~15%)  

---

## 🧠 Model
- **Model Used:** YOLOv8n (Ultralytics) – lightweight and fast CNN-based detection model  
- **Training:**  
  - 50 epochs  
  - Image size: 640×640  
  - Optimizer: SGD with momentum  
- **Output:** `runs/detect/train/weights/best.pt` (best trained model)  

---

## ⚙️ Preprocessing
- Images resized to 640×640 during training  
- Data augmentation applied (rotation, flipping, brightness/contrast changes) to make model robust against real-world camera variations  

---

## 🚀 How to Run

### 1. Install Dependencies
```bash
pip install ultralytics opencv-python
