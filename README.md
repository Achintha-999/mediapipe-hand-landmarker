# ✋🤖 MediaPipe Hand Landmarker (Python + OpenCV)

<p align="center">
  <img alt="Python" src="https://img.shields.io/badge/Python-3.x-blue?logo=python">
  <img alt="MediaPipe" src="https://img.shields.io/badge/MediaPipe-Tasks-orange">
  <img alt="OpenCV" src="https://img.shields.io/badge/OpenCV-Computer%20Vision-green?logo=opencv">
  <img alt="Status" src="https://img.shields.io/badge/Status-Beginner%20Friendly-success">
</p>

A beginner-friendly computer vision project that detects and draws **hand landmarks** from a video using **MediaPipe Tasks** and **OpenCV**.  
It also labels each detected hand as **Left** or **Right** in real time.

---

## 🌟 Highlights

✅ Detects up to **2 hands** per frame  
✅ Draws **21 keypoints** and hand connection lines  
✅ Displays **handedness labels** (*Left / Right*)  
✅ Works with a local video file (`video1.mp4`)  
✅ Easy to customize and extend

---

## 📌 Project Overview

This project demonstrates a complete hand-landmark pipeline:

1. Load MediaPipe hand landmarker model (`hand_landmarker.task`)
2. Read frames from video (`video1.mp4`)
3. Run hand landmark detection
4. Draw landmarks + connection graph
5. Render handedness label near each hand
6. Show live annotated output window

> **Entry point:** `index.py`

---

## 🧠 What Are Hand Landmarks?

MediaPipe detects a hand as a set of **21 3D landmarks** (x, y, z) representing key joints and finger tips.  
These points can be used for:
- gesture recognition ✌️
- sign language projects 🤟
- HCI / touchless interfaces 🖐️
- motion analytics 📊
- AR/VR interactions 🥽

---

## 🗂️ Repository Structure

```text
mediapipe-hand-landmarker/
├── index.py                  # Main script
├── hand_landmarker.task      # MediaPipe model file
├── video1.mp4                # Input test video
├── hand.jpg                  # Sample image asset
└── README.md
```

---

## 🧰 Requirements

- **Python** version compatible with your installed `mediapipe`
- Desktop/GUI environment (required for `cv2.imshow`)
- Required files in project root:
  - `index.py`
  - `hand_landmarker.task`
  - `video1.mp4`

### ���� Python Dependencies

- `mediapipe`
- `opencv-python`
- `numpy`

---

## ⚙️ Installation & Setup

From the project root:

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install --upgrade pip
pip install mediapipe opencv-python numpy
```

---

## 📥 Imports Used

```python
import cv2
import mediapipe as mp
from mediapipe.tasks import python
from mediapipe.tasks.python import vision
import numpy as np
import os
```

---

## 🔍 How the Pipeline Works

### 1) Model Initialization
- `BaseOptions(model_asset_path='hand_landmarker.task')`
- `HandLandmarkerOptions(num_hands=2, ...)`
- `vision.HandLandmarker.create_from_options(...)`

### 2) Video Capture
- Open video stream using OpenCV:
  - `cv2.VideoCapture("video1.mp4")`

### 3) Per-frame Detection
- Convert frame from **BGR → RGB**
- Wrap frame into `mp.Image`
- Run `detector.detect(...)`

### 4) Visualization
- Draw landmarks and hand skeleton connections
- Render handedness text near hand bounding area

### 5) Real-time Display
- Show output in a window (`Image`)
- Press **Esc** to quit

---

## 🧮 Key Variables Explained

Inside `index.py`:

- `MARGIN = 10` → Label offset in pixels
- `FONT_SIZE = 1` → Label text scale
- `FONT_THICKNESS = 1` → Label line thickness
- `HANDEDNESS_TEXT_COLOR = (88, 205, 54)` → Label color in **BGR**
- `num_hands = 2` → Max number of hands to detect
- `model_asset_path = 'hand_landmarker.task'` → Model path
- `cv2.VideoCapture("video1.mp4")` → Input source file

---

## 🎛️ Customization Options

### 👥 Detect more/fewer hands
Change:
```python
num_hands=2
```

### 📷 Use webcam instead of video file
Replace:
```python
cv2.VideoCapture("video1.mp4")
```
with:
```python
cv2.VideoCapture(0)
```
> If needed, try camera indices `1` or `2`.

### 🎨 Change label appearance
Modify:
- `FONT_SIZE`
- `FONT_THICKNESS`
- `HANDEDNESS_TEXT_COLOR`

### 🧭 Move model file
Update:
```python
model_asset_path = "path/to/hand_landmarker.task"
```

---

## ▶️ Run the Project

```bash
python index.py
```

### 👀 Expected On-screen Output

- Window title: **Image**
- Hand landmarks + connection lines
- Handedness labels (`Left` / `Right`)
- Exit with **Esc**

---

## ✅ Expected Results

When hands are visible in the video:

- Up to 2 hands detected (current config)
- Each hand gets:
  - 21 landmarks
  - skeleton/connection overlay
  - handedness label

---

## 🛠️ Troubleshooting

### ❌ `ModuleNotFoundError` (`mediapipe`, `cv2`, `numpy`)
- Activate virtual environment
- Reinstall dependencies

### ❌ Model file not found (`hand_landmarker.task`)
- Ensure file exists in project root
- Or update `model_asset_path`

### ❌ Video not opening / blank frame
- Verify `video1.mp4` exists and is readable
- Try another video path

### ❌ No display window appears
- `cv2.imshow` requires GUI support
- Run locally (not in headless server/SSH-only env)

### ❌ No landmarks detected
- Ensure hands are visible, clear, and not heavily occluded
- Improve lighting / reduce motion blur

### ❌ OpenCV `cvtColor` crash near video end
- Current script may not guard `ret == False`
- Add frame-read checks before processing

---

## 🚧 Known Limitation

Current baseline may fail if a frame read is invalid (`ret == False`) and still attempts color conversion.  
For production-quality robustness, add:
- graceful frame-read validation
- confidence filtering
- exception handling
- CLI arguments for input/model paths

---

## 🚀 Suggested Next Improvements

- [ ] Add command-line args (`--video`, `--model`, `--num-hands`)
- [ ] Save annotated output video (`cv2.VideoWriter`)
- [ ] Add FPS counter overlay
- [ ] Add gesture classification module
- [ ] Support image mode + webcam mode switch
- [ ] Add logging + error diagnostics

---

## 🤝 Contributing

Contributions are welcome!  
Feel free to open an issue or submit a PR for improvements in:
- performance ⚡
- robustness 🛡️
- readability 📚
- features ✨

---

## 📜 License

You can add an open-source license (e.g., MIT) to clarify usage rights for others.

---

<p align="center"><b>Made with ❤️ using MediaPipe + OpenCV</b></p>
