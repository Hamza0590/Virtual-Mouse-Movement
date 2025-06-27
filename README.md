# 🖐️ Virtual Mouse Control using Hand Gestures with MediaPipe & MLP

This project allows you to **control your computer mouse** using hand gestures captured from a **laptop camera**. It uses **MediaPipe** for hand landmark detection, **OpenCV** for video processing, and a **custom-trained MLP model** to classify gestures for **mouse movement** and **clicking** actions.

---

## 🚀 How It Works

1. **Data Collection**
   - The laptop camera captures hand gestures in real time.
   - Using MediaPipe, 21 hand landmarks (x, y coordinates) are extracted per frame.
   - The coordinates are stored in a CSV file for training with corresponding labels:
     - `0` → Click gesture (closed fist)
     - `1` → Move gesture (closed fist with thumb and index finger joined)
     - `2` → Other/neutral gesture

2. **Model Training**
   - A Multi-Layer Perceptron (MLP) model is trained on the collected data:
     - **Input Layer:** 42 neurons (42 for 21 `(x, y)` points)
     - **Hidden Layer:** 10 neurons, activation: ReLU
     - **Output Layer:** 3 neurons (click, move, other), activation: Softmax
   - The model is compiled, trained, and saved for later use.

3. **Real-Time Mouse Control**
   - The saved MLP model is loaded, or an already trained model is used.
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
    │ └── data.csv # Collected hand landmark features without labels
    │ └── new_data.csv # Collected hand landmark features with labels
    ├── model/
    │ └── mouse.h5 # Trained MLP model
    ├── mouse.ipynb # Script to collect, save hand landmark data, train model, make live prediction, and perform action on mouse.

---

## ▶️ How to Run

1. **Install Dependencies**
   ```bash
   pip install opencv-python mediapipe numpy pyautogui tensorflow scipy pandas
2. **Run mouse.ipynb file**
