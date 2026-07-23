# Gesture-Controlled 5-DOF Robotic Arm using Computer Vision

This project implements a gesture-controlled, 3D-printable, 5-Degrees-of-Freedom (DOF) desktop-sized robotic arm. By tracking color-coded markers worn on the user's arm (wrist, elbow, and tricep), the system detects human arm movements using computer vision (OpenCV) and translates them into joint angles. These angles are sent in real-time via Serial communication to an Arduino Uno, which actuates the servo motors to mimic the user's gestures.

---

## 📽️ Project Demo & STL Files
* **Demo Video:** Watch the robotic arm in action on [YouTube](https://www.youtube.com/watch?v=PDEdxRVkMdo).
* **3D Models & Part List:** Download the STL files for 3D printing and view the full bill of materials on [GrabCAD](https://grabcad.com/library/5-dof-robotic-arm-6).

---

## 🛠️ Hardware Requirements
* **Robotic Arm Chassis:** 3D printed parts (obtain STL files from the GrabCAD link above).
* **Actuators:**
  * 3x Standard Servo Motors (for high-torque joints like the base and lower arms)
  * 2x Micro Servo Motors (for wrist and claw gripper)
* **Controller:** Arduino Uno (or compatible microcontroller).
* **Communication:** USB Cable for serial data transfer.
* **Markers:** 3 distinct color blocks/bands (Green, Red, and Yellow) to be worn by the user:
  * **Green:** Worn on the **Wrist**
  * **Red:** Worn on the **Elbow**
  * **Yellow:** Worn on the **Tricep/Upper Arm**
  *(Can be easily made using LEGO blocks and velcro tape)*

---

## 💻 Software Dependencies
Ensure you have **Python 3.x** and the **Arduino IDE** installed.

### Python Libraries
Install the required packages using pip:
```bash
pip install numpy opencv-python imutils pyserial
```

### Arduino Libraries
* `Servo.h` (Built-in with the Arduino IDE)

---

## 📂 Project Structure
```
├── Gesture_Controlled_Robotic_Arm_Arduino_Code/
│   └── Gesture_Controlled_Robotic_Arm_Arduino_Code.ino  # Upload to Arduino Uno
├── Gesture_Controlled_Robotic_Arm_Python_Code.py       # Main OpenCV tracking script
├── HSV.py                                              # HSV calibration tool
├── README.md                                           # Project documentation
└── LICENSE                                             # License details
```

---

## 🔧 Setup & Calibration Guide

### 1. Upload Arduino Code
1. Open [Gesture_Controlled_Robotic_Arm_Arduino_Code.ino](file:///Users/prakhargupta/Gesture-Controlled-5-DOF-Robotic-Arm-using-Computer-Vision/Gesture_Controlled_Robotic_Arm_Arduino_Code/Gesture_Controlled_Robotic_Arm_Arduino_Code.ino) in the Arduino IDE.
2. Connect your Arduino Uno to your computer.
3. Select the correct Board and Port from the Tools menu.
4. Upload the sketch. Note down the COM/Serial port name (e.g., `COM3` on Windows, or `/dev/tty.usbmodem...` on macOS/Linux).

### 2. Calibrate Color HSV Thresholds
Since lighting conditions vary, you must calibrate the HSV color boundaries for your specific markers (Green, Red, Yellow):
1. Run the [HSV.py](file:///Users/prakhargupta/Gesture-Controlled-5-DOF-Robotic-Arm-using-Computer-Vision/HSV.py) script:
   ```bash
   python HSV.py
   ```
2. Six trackbars will appear (`h`, `s`, `v` for lower bounds, and `h1`, `s1`, `v1` for upper bounds).
3. Adjust the sliders until **only** one of your color blocks is visible in white against a black background.
4. Press `ESC` to close the calibration window. The calibrated HSV bounds will be printed in the terminal.
5. Repeat this process for all three colors (Green, Red, Yellow).
6. Open [Gesture_Controlled_Robotic_Arm_Python_Code.py](file:///Users/prakhargupta/Gesture-Controlled-5-DOF-Robotic-Arm-using-Computer-Vision/Gesture_Controlled_Robotic_Arm_Python_Code.py) and update the lower and upper bounds at the top of the file (lines 16-23):
   ```python
   greenLower = (H, S, V)
   greenUpper = (H1, S1, V1)
   
   redLower = (H, S, V)
   redUpper = (H1, S1, V1)
   
   yellowLower = (H, S, V)
   yellowUpper = (H1, S1, V1)
   ```

### 3. Update the Serial Port
In [Gesture_Controlled_Robotic_Arm_Python_Code.py](file:///Users/prakhargupta/Gesture-Controlled-5-DOF-Robotic-Arm-using-Computer-Vision/Gesture_Controlled_Robotic_Arm_Python_Code.py), update the serial connection initialization (line 32) to match your Arduino's port:
* **Windows:** `arduino = serial.Serial('COM3', 9600)`
* **macOS/Linux:** `arduino = serial.Serial('/dev/tty.usbmodemXXXX', 9600)`

---

## 🚀 Running the Program
1. Put on your color blocks (Green on wrist, Red on elbow, Yellow on tricep).
2. Connect the Arduino Uno to your computer via USB.
3. Start the main tracking script:
   ```bash
   python Gesture_Controlled_Robotic_Arm_Python_Code.py
   ```
4. A window showing the webcam feed will open. Ensure that all three color markers are in the camera's field of view.
5. Move your arm; the robotic arm will mimic your movements!
6. Press `q` to quit the application.

---

## 📄 License
This project is licensed under the MIT License. See the [LICENSE](file:///Users/prakhargupta/Gesture-Controlled-5-DOF-Robotic-Arm-using-Computer-Vision/LICENSE) file for details.
