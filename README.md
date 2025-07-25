# 🤟 Live Hand Sign Recognition System  
*Real-Time Alphabet Gesture Detection using Python and Deep Learning*

## 📌 Project Overview

This academic project focuses on developing a real-time computer vision system capable of **identifying hand signs** corresponding to the **first four letters of the alphabet (A–D)** using a webcam. The system interprets static gestures in live video, detects the corresponding letter, and displays it to the user in a GUI interface.

The project was developed by **Maria-Daniela Munteanu** and **Andreea Acsinte** (Group 1301A) as part of the *Artificial Vision Systems* curriculum. It combines techniques from **image processing**, **machine learning**, and **graphical interface development**, offering an accessible method to interact with machines using hand gestures.

---

## 🎯 Project Goals

- 📸 Collect hand gesture data for letters A, B, C, D  
- 🧠 Train a custom classifier using TensorFlow/Keras  
- 🖐️ Use OpenCV to detect live hand pose landmarks  
- 🖼️ Predict gestures in real time and display results in a user-friendly GUI  
- 🧪 Test model predictions on unknown samples in live conditions

---

## 🧰 Tools & Technologies Used

| Tool           | Purpose                                              |
|----------------|------------------------------------------------------|
| **Python**     | Programming language                                 |
| **OpenCV**     | Real-time image capture and processing               |
| **TensorFlow** | Neural network modeling and inference                |
| **Keras**      | High-level API for building and training models      |
| **Teachable Machine** | For quick model prototyping via browser      |
| **Tkinter**    | GUI framework for Python                             |
| **NumPy & PIL**| Array and image manipulation                         |

---

## 🧠 Project Workflow

### 1. 📁 Data Collection (`DataCollection.py`)
- Images were captured using webcam input and saved into folders labeled `A/`, `B/`, `C/`, `D/`
- All images were resized to **300x300 pixels**
- The hand pose was extracted and saved to ensure gesture consistency

### 2. 🧠 Model Training
- Used **Teachable Machine** for fast gesture recognition model training
- Exported the model as `.tflite` and used `labels.txt` for indexing predictions
- Loaded via TensorFlow Lite for efficient runtime performance in Python

### 3. 🖼️ Live Prediction GUI (`Testing.py`)
- GUI window built with **Tkinter**
- Real-time webcam feed displayed
- Detected gestures are passed to the model
- Predicted letters shown live on screen with visual confirmation
- One click starts, another stops prediction

---

## 🖥️ GUI Snapshot

The GUI shows:
- Webcam feed
- Predicted class (A, B, C, or D)
- Hand keypoints overlay
- Example output:  
  ![Hand gesture A prediction](https://example.com/screenshot-A.png)

---

## ⚙️ Project Structure
📦 hand-sign-recognition/
├── DataCollection.py # For image dataset creation
├── Testing.py # GUI and live prediction
├── model/
│ ├── converted_model.tflite
│ └── labels.txt
├── images/
│ ├── A/ B/ C/ D/ # Hand signs for training

---

## ✅ Results & Accuracy

| Letter | Example Accuracy | Notes                                      |
|--------|------------------|--------------------------------------------|
| A      | 99.9%            | Very stable under various lighting         |
| B      | 99.9%            | Sensitive to hand position, but reliable   |
| C      | 98.7%            | Occasionally confused with B               |
| D      | 97.7%            | Edge case when finger occlusion occurs     |

📌 Predictions were tested live with a variety of backgrounds and hand orientations.

---

## 🚧 Challenges Faced

- ❌ Misclassification due to incorrect input sizing → fixed by resizing with aspect ratio preservation
- ⚠️ GUI prediction failure when original image (not processed one) was passed to classifier
- 📐 Errors in hand detection when hand was out of frame or partially occluded
- ✋ Class confusion between B & D when hand alignment wasn't centered

✅ All were addressed via preprocessing and calibration of input capture.

---
