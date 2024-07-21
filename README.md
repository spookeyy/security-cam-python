# Motion Detection Camera

This project implements a motion detection camera using OpenCV and Python. It captures video from a camera, detects motion, and plays an alert sound when significant movement is detected.

## Features

- Real-time motion detection
- Visual highlighting of detected motion areas
- Audio alert on motion detection

## Requirements

- Python 3.x
- OpenCV (`cv2`)
- `winsound` (Windows-specific, for audio alerts)
- For ubuntu, install `pygame`
- For macOS, install `portaudio`
- Alternative audio libraries (e.g. `pyaudio`) can be used if `winsound` is not available. install `pyaudio` with `pip install pyaudio`
## Installation

1. Ensure you have Python installed on your system.
2. Install the required libraries:

   ```bash
   pip install opencv-python
   ```
Note: winsound is included in standard Python installations on Windows.

Download or clone this repository to your local machine.

## Usage

Connect a camera to your computer (the script uses the second camera, index 1).
Place an audio file named `alert.wav` in the same directory as the script for the alert sound.
Run the script:
```bash
python main.py
```

To exit the program, press 'q' while the camera window is active.

## For Windows Users

To play the alert sound on Windows, you'll need to install the `winsound` library.

```bash
pip install winsound
```
here is the code to run on windows:

```python
import cv2
import winsound
cam = cv2.VideoCapture(1)
while cam.isOpened():
    ret, frame1 = cam.read()
    ret, frame2 = cam.read()
    diff = cv2.absdiff(frame1, frame2)
    gray = cv2.cvtColor(diff, cv2.COLOR_RGB2GRAY)
    blur = cv2.GaussianBlur(gray, (5, 5), 0)
    _, thresh = cv2.threshold(blur, 20, 255, cv2.THRESH_BINARY)
    dilated = cv2.dilate(thresh, None, iterations=3)
    contours, _ = cv2.findContours(dilated, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
    # cv2.drawContours(frame1, contours, -1, (0, 255, 0), 2)
    for c in contours:
        if cv2.contourArea(c) < 5000:
            continue
        x, y, w, h = cv2.boundingRect(c)
        cv2.rectangle(frame1, (x, y), (x+w, y+h), (0, 255, 0), 2)
        winsound.PlaySound('alert.wav', winsound.SND_ASYNC)
    if cv2.waitKey(10) == ord('q'):
        break
    cv2.imshow('Granny Cam', frame1)
cam.release()
cv2.destroyAllWindows()
```

## How It Works
The script continuously captures frames from the camera and compares consecutive frames to detect changes. When a significant change (motion) is detected:

The motion area is highlighted with a green rectangle.
An alert sound is played.

## Customization

Adjust the cv2.VideoCapture(1) index if you want to use a different camera.
Modify the motion sensitivity by changing the threshold value in cv2.threshold(blur, 20, 255, cv2.THRESH_BINARY).
Change the minimum contour area in if cv2.contourArea(c) < 5000: to adjust the sensitivity to small movements.

### Note
This script is designed for Ubuntu due to the use of pygame. For other operating systems, you'll need to use a different audio library.

## License
MIT

## Contact
email: pangasmeshack@gmail.com
