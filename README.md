# ✋ Mediapipe Hand Landmarker

A beginner-friendly Python project for **detecting and drawing hand landmarks** on video frames using **MediaPipe Tasks** and **OpenCV**.

---

## 📌 Project Overview

This repository demonstrates how to:
- load the MediaPipe Hand Landmarker model (`hand_landmarker.task`)
- run hand landmark detection on each frame of a video (`video1.mp4`)
- draw hand keypoints/connections and handedness labels (Left/Right)
- display the annotated result in real time

Current entry point: `index.py`

---

## 🧰 Requirements / Prerequisites

- Python version supported by your installed `mediapipe` release (commonly Python **3.9–3.12**)
- OS with GUI/video display support (for `cv2.imshow`)
- Project files present in the same folder:
  - `index.py`
  - `hand_landmarker.task`
  - `video1.mp4`

Python libraries used:
- `mediapipe`
- `opencv-python`
- `numpy`

---

## ⚙️ Installation / Setup

From the project root:

```bash
python -m venv .venv
source .venv/bin/activate   # On Windows: .venv\Scripts\activate
pip install --upgrade pip
pip install mediapipe opencv-python numpy
```

---

## 📥 Import Libraries (used in this project)

```python
import cv2
import mediapipe as mp
from mediapipe.tasks import python
from mediapipe.tasks.python import vision
import numpy as np
import os
```

---

## 🧠 How It Works

1. **Model setup**
   - `BaseOptions(model_asset_path='hand_landmarker.task')`
   - `HandLandmarkerOptions(..., num_hands=2)`
   - Create detector via `vision.HandLandmarker.create_from_options(...)`

2. **Video input**
   - OpenCV reads frames from `video1.mp4`

3. **Detection**
   - Each BGR frame is converted to RGB
   - Frame is wrapped as `mp.Image`
   - `detector.detect(...)` returns landmark + handedness results

4. **Visualization**
   - Landmarks and connections are drawn
   - Left/Right handedness text is rendered near each detected hand

5. **Display loop**
   - Annotated frame is shown in a window
   - Press **Esc** to exit

---

## 🧮 Variables and Values Explained

In `index.py`:

- `MARGIN = 10`: pixel offset for label position
- `FONT_SIZE = 1`: OpenCV label font scale
- `FONT_THICKNESS = 1`: label stroke thickness
- `HANDEDNESS_TEXT_COLOR = (88, 205, 54)`: BGR color for label text
- `num_hands = 2` (inside `HandLandmarkerOptions`): maximum hands to detect
- `model_asset_path = 'hand_landmarker.task'`: path to landmarker model file
- `VideoCapture("video1.mp4")`: input source video file

---

## 🔧 Configuration / Adjustment Options

You can tune behavior by editing `index.py`:

- **Detect more/fewer hands**
  - Change `num_hands=2`
- **Use webcam instead of file**
  - Replace `cv2.VideoCapture("video1.mp4")` with `cv2.VideoCapture(0)` (index `0` is commonly the default camera; try `1` or `2` if needed on your system)
- **Change label appearance**
  - Update `FONT_SIZE`, `FONT_THICKNESS`, `HANDEDNESS_TEXT_COLOR`
- **Change model path**
  - Update `model_asset_path` if model file location changes

---

## ▶️ Run the Project

```bash
python index.py
```

What you should see:
- A window titled **Image** (this is the exact current title in `index.py`)
- Hand landmarks and hand-connection lines over detected hands
- Left/Right handedness labels
- Exit by pressing **Esc**

---

## ✅ Expected Output / Results

When a hand is visible in the input video:
- up to 2 hands are detected (as configured)
- each hand is annotated with landmarks + skeletal connections
- handedness classification (`Left` / `Right`) is shown near the hand

---

## 🛠️ Troubleshooting

- **`ModuleNotFoundError` for mediapipe/cv2/numpy**
  - Activate your virtual environment and reinstall dependencies.

- **Model file error (cannot find `hand_landmarker.task`)**
  - Make sure the file is in project root or update `model_asset_path`.

- **Video not opening / blank window**
  - Confirm `video1.mp4` exists and is readable.
  - Try another video path.

- **Window does not appear (headless/server environment)**
  - `cv2.imshow` requires GUI support. Run locally with desktop display.

- **No detection shown**
  - Ensure hands are visible, clear, and not heavily occluded in frames.

---

## 📝 Usage Notes

- This is a simple, educational baseline implementation.
- The script currently processes a local video file frame-by-frame.
- Current limitation: frame-read success (`ret` from `cap.read()`) is not checked before frame conversion.
- For production apps, consider adding:
  - graceful frame-read failure handling when `ret` is `False`
  - confidence thresholds and error handling
  - CLI arguments for model/video paths

---

## 📂 Repository Files (current)

- `index.py` → main script
- `hand_landmarker.task` → MediaPipe model
- `video1.mp4` → sample input video
- `hand.jpg` → sample image asset

---

## 🤝 Contributing

Feel free to open an issue or submit a PR to improve performance, robustness, or usability.
