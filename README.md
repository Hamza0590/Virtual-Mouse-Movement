# 🖐️ Virtual Mouse Control using Hand Gestures with MediaPipe & MLP

This project allows you to **control your computer mouse** using hand gestures captured from a **laptop camera**. It uses **MediaPipe** for hand landmark detection, **OpenCV** for video processing, and a **custom-trained MLP model** to classify gestures for **mouse movement** and **clicking** actions.

---

## 🚀 How It Works

1. **Data Collection**
   - The laptop camera captures hand gestures in real time.
   - Using MediaPipe, 21 hand landmarks (x, y coordinates) are extracted per frame.
   - The coordinates are stored in a CSV file for training with corresponding labels:
     - `1` → Click gesture (closed fist)
     - `2` → Move gesture (open hand)
     - `3` → Other/neutral gesture

2. **Model Training**
   - A Multi-Layer Perceptron (MLP) model is trained on the collected data:
     - **Input Layer:** 43 neurons (42 for 21 `(x, y)` points + 1 bias or optional extra)
     - **Hidden Layer:** 10 neurons, activation: ReLU
     - **Output Layer:** 3 neurons (click, move, other), activation: Softmax
   - The model is compiled, trained, and saved for later use.

3. **Real-Time Mouse Control**
   - The saved MLP model is loaded.
   - Live camera input is processed to extract hand landmarks.
   - The model predicts the gesture in real time:
     - If the prediction is `1`: perform a **mouse click**
     - If the prediction is `2`: **move the mouse cursor** according to index finger tip position
   - Smoothing is applied to mouse movement for better control.

---

## 🛠️ Technologies Used

- [Python](https://www.python.org/)
- [MediaPipe](https://google.github.io/mediapipe/) – for real-time hand detection
- [OpenCV](https://opencv.org/) – for camera and image processing
- [TensorFlow/Keras](https://www.tensorflow.org/) or [scikit-learn](https://scikit-learn.org/) – for MLP model
- [PyAutoGUI](https://pyautogui.readthedocs.io/) – for mouse control

---

## 📂 Project Structure
    📁 virtual-mouse-mlp/
    ├── data/
    │ └── hand_data.csv # Collected hand landmark features with labels
    ├── model/
    │ └── mlp_model.h5 # Trained MLP model
    ├── collect_data.py # Script to collect and save hand landmark data
    ├── train_model.py # Script to train and save the MLP model
    ├── run_mouse_control.py # Final script to control mouse in real-time
    ├── README.md # This file

---

## ▶️ How to Run

1. **Install Dependencies**
   ```bash
   pip install opencv-python mediapipe numpy pyautogui tensorflow
2. ** Run mouse.ipynb file**
