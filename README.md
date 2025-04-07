# 🐛 Pest Detection Deep Learning Project

A YOLOv8-powered deep learning project for real-time pest detection in agricultural environments. This model is part of a larger system that includes:

- A **Flask API** for inference
- A **mobile app** interface built with React Native + Expo

---

## 📝 Overview

This project uses the **YOLOv8n** (nano variant) model to detect pests in images. The dataset is split into `train`, `valid`, and `test` sets. After training, the best model checkpoint (`best.pt`) is used for real-time inference via an API.

---

## 📁 Project Structure

```bash
PestDetection-Project/
├── data/
│   ├── train/
│   │   ├── images/
│   │   └── labels/
│   ├── valid/
│   │   ├── images/
│   │   └── labels/
│   └── test/
│       ├── images/
│       └── labels/
├── runs/
│   └── train/           # ✅ Folders generated while training
│       ├── weights/
|           ├── best.pt  # ✅ Trained Model
|           ├── last.pt  
│   └── predict/         # ✅ Folders generated while inference
├── data.yaml
├── requirements.txt
├── README.md
```

## Setup

### Virtual Environment

We highly recommend using a Python virtual environment to manage dependencies. To create and activate the virtual environment, run the following commands:

```bash
# Navigate to the project directory
cd /path/to/PestDetection-Project

# Create a virtual environment (using venv)
python3 -m venv venv

# Activate the virtual environment (Linux/Mac)
source venv/bin/activate

# Or, on Windows:
venv\Scripts\activate

pip install -r requirements.txt

```

### Training the Model

The model is trained using YOLOv8. For example, to train the model with the initial hyperparameters, run:

```bash
yolo task=detect mode=train model=yolov8n.pt data=data.yaml epochs=50 imgsz=640

```

### Customizing training parameters

For further tuning, you may experiment with parameters such as epochs, lr0, batch, and imgsz. For instance, to increase epochs and lower the learning rate:

```bash
yolo task=detect mode=train model=yolov8n.pt data=data.yaml epochs=70 imgsz=640 lr0=0.001 batch=16
```

### Running Inference

After training, the model checkpoint best.pt will be saved in one of the run folders (e.g., runs/train7/). This file is used for inference.

```bash
yolo task=detect mode=predict model=runs/detect/train/weights/best.pt source=path/to/test_images
```

## Integration with Other Components

### Flask API (PestDetection-API Repository):
- The trained model (best.pt) is integrated into a Flask API that exposes endpoints such as /predict and /capture for remote inference.

### Mobile Application (PestDetection Repository):
- The mobile app communicates with the Flask API to display detection results to the user
