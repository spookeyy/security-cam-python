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

## How It Works
The script continuously captures frames from the camera and compares consecutive frames to detect changes. When a significant change (motion) is detected:

The motion area is highlighted with a green rectangle.
An alert sound is played.

## Customization

Adjust the cv2.VideoCapture(1) index if you want to use a different camera.
Modify the motion sensitivity by changing the threshold value in cv2.threshold(blur, 20, 255, cv2.THRESH_BINARY).
Change the minimum contour area in if cv2.contourArea(c) < 5000: to adjust the sensitivity to small movements.

### Note
This script is designed for Windows due to the use of `winsound`. For other operating systems, you'll need to use a different audio library.

## License
MIT

## Contact
email: pangasmeshack@gmail.com
