# Real-Time Hand Tracking

## Overview
This project implements a real-time hand tracking system using OpenCV and MediaPipe to detect and visualize hand landmarks from webcam video. It identifies 21 key landmarks per hand (e.g., fingertips, knuckles, wrist) and displays them as dots with skeletal connections. The system supports applications like gesture recognition, sign language interpretation, and virtual reality interactions.

## Prerequisites
- Python 3.8+ installed on your system
- A webcam (default device, index 0)
- Required Python libraries:
  - `opencv-python` (for video capture and display)
  - `mediapipe` (for hand tracking and landmark detection)
- Install dependencies manually:
  ```bash
  pip install opencv-python mediapipe
  ```

## How to Run
1. Save the project code in a file named `hand_tracking.py`.
2. Open a terminal or command prompt.
3. Navigate to the directory containing the project file.
4. Install the required libraries (see Prerequisites).
5. Run the program:
   ```bash
   python hand_tracking.py
   ```
6. View the webcam feed with hand landmarks overlaid.
7. Press the `ESC` key to exit (if implemented, see Limitations).

## Application Flow
- The program captures video from the default webcam using OpenCV.
- Each frame is flipped horizontally and converted from BGR to RGB for MediaPipe compatibility.
- MediaPipe’s Hands model processes the frame to detect up to two hands and identify 21 landmarks per hand (x, y, z coordinates).
- Landmarks and skeletal connections are drawn on the frame.
- The processed frame is displayed in a window named "handtracker".
- The loop continues until interrupted (requires manual termination or ESC key if added).

## Code Structure
- **Imports**: `cv2` (OpenCV) for video capture/display, `mediapipe` for hand tracking.
- **MediaPipe Setup**: Initializes `mp.solutions.drawing_utils`, `mp.solutions.hands` for landmark detection and visualization.
- **Video Capture**: Uses `cv2.VideoCapture(0)` to access the webcam.
- **Hands Model**: Configures `Hands()` with defaults (max 2 hands, 50% confidence for detection/tracking).
- **Processing Loop**: Reads frames, preprocesses (flip, color conversion), detects hands, draws landmarks, and displays output.

## Example Output
```
[Webcam Window: "handtracker"]
- Displays live video feed
- Overlays 21 landmarks per detected hand (dots at fingertips, knuckles, etc.)
- Draws skeletal lines connecting landmarks (e.g., wrist to thumb)
```

## Limitations
- No resource cleanup (webcam not released, windows not closed).
- Lacks error handling for failed frame captures.
- No exit condition (requires Ctrl+C or window close).
- Performance may degrade with heavy hand occlusion or extreme lighting.
- Does not label hands (left/right) or support custom visualization styles.

## Potential Improvements
- Add error handling for failed captures:
  ```python
  if not data:
      print("Failed to capture frame")
      break
  ```
- Implement an exit key (e.g., ESC):
  ```python
  if cv2.waitKey(1) & 0xFF == 27:
      break
  ```
- Add resource cleanup:
  ```python
  cap.release()
  cv2.destroyAllWindows()
  ```
- Support gesture recognition by analyzing landmark positions.
- Label hands (left/right) using `results.multi_handedness`.
- Use custom visualization styles via `mp.solutions.drawing_styles`.

## License
This project is unlicensed and free to use or modify.