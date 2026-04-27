


Because Google Colab operates on remote cloud servers, standard local webcam libraries like cv2.VideoCapture(0) do not work. This system solves that problem by using a JavaScript-to-Python bridge. It captures live frames from the user's local browser via the MediaDevices API, sends them to the Colab backend, processes them using the Ultralytics YOLOv8 model, and renders the annotated results back to the screen in real-time.


# Real-Time person Detection in Google Colab using YOLOv8

This repository provides a seamless implementation of real-time object detection within a Google Colab environment. It utilizes the state-of-the-art YOLOv8 model and bridges the gap between cloud computing and local hardware (webcams) using JavaScript.

## 🚀 Features
* **Live Webcam Integration:** Uses a custom JavaScript bridge to bypass Colab's local hardware limitations.
* **YOLOv8 Power:** Leverages the Ultralytics YOLOv8 nano model for high-speed inference.
* **Real-time Feedback:** Instantly displays bounding boxes and class labels (e.g., Person, Cell Phone, Laptop).
* **Easy Control:** Includes an interactive "STOP" button to safely shut down the camera hardware.

## 🛠️ Tech Stack
* **Python:** Core logic and model inference.
* **JavaScript:** Browser-side webcam handling.
* **OpenCV & PIL:** Image processing and formatting.
* **Ultralytics YOLO:** Object detection framework.
* **NumPy:** Efficient array manipulation.

## 📋 Prerequisites
No local installation of Python is required. You only need:
* A Google Account to access [Google Colab](https://colab.research.google.com/).
* A functional webcam.

## ⚙️ How It Works
1. **Model Loading:** The script downloads the pre-trained `yolov8n.pt` weights.
2. **JS Bridge:** A JavaScript function is injected into the browser to access `navigator.mediaDevices.getUserMedia`.
3. **Capture Loop:**
    - The browser captures a frame and converts it to a Base64 string.
    - Python decodes the Base64 string into a NumPy array.
    - YOLOv8 performs detection on the frame.
    - Annotated results are displayed back in the Colab output cell.
4. **Cleanup:** Clicking the "STOP" button triggers `track.stop()` to ensure your webcam isn't left active after the script ends.

## 🖥️ Usage
1. Open a new notebook in Google Colab.
2. Ensure your Runtime type is set to **Python 3**. (GPU is recommended for faster frame rates: `Runtime > Change runtime type > T4 GPU`).
3. Install the requirements:
   ```bash
   pip install ultralytics
