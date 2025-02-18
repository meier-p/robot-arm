# Compact Robot Arm Firmware Enhancements

This repository contains two firmware variants for the **Compact Robot Arm** originally created by [Build Some Stuff](https://www.printables.com/model/818975-compact-robot-arm-arduino-3d-printed). We have implemented two different approaches:

1. **Serial Console Firmware** – Used for manually determining and fine-tuning servo pulse width values.
2. **Calibration Firmware** – Automatically calibrates the potentiometers and maps the readings to servo positions, storing the data in EEPROM for persistent operation.

---

## Serial Console Firmware

### Purpose
This firmware version is designed for manual control via the serial console. It allows you to send commands to adjust individual servo positions to determine the optimal pulse width values. These values can then be used in the calibration firmware.

### Features
- **Manual Servo Control:**  
  Send commands in the format `[Servo Letter][PulseWidth]` (e.g., `W1750`) to set a specific servo (e.g., the Wrist servo) to a defined pulse width.
- **Value Determination:**  
  Adjust each servo manually and observe its movement to find the best pulse width values for your setup.
- **Extensible Design:**  
  Easily add support for additional servos by extending the command parsing logic.

### Usage
- **Connect via Serial Console:**  
  Open your preferred serial monitor at the configured baud rate.
- **Send Commands:**  
  Type commands such as `W1750` to set the Wrist servo to a 1750 µs pulse. Adjust until the desired position is reached.
- **Record Values:**  
  Note down the optimal values; these will be applied in the calibration firmware.

---

## Calibration Firmware

### Purpose
This firmware version features an automatic calibration mode that runs for a fixed 10 seconds at startup. During this time, the firmware records the minimum and maximum readings from the potentiometers and uses these values to accurately map them to servo pulse widths. The calibration data is saved in the EEPROM so that it persists between power cycles.

### Features
- **Automatic Calibration Mode:**  
  - Activated by a button (Gripper button on Pin 13) at startup.
  - After ensuring the button is released, the system calibrates for 10 seconds.
- **EEPROM Storage:**  
  The recorded potentiometer minimum and maximum values are saved in EEPROM, ensuring that calibration data is retained even after a power cycle.
- **LED Feedback:**  
  An LED blinks during the 10-second calibration period to indicate that calibration is in progress.
- **Servo Mapping:**  
  The calibrated values are used during normal operation to accurately map the potentiometer readings to the corresponding servo pulse widths.

### Usage
- **Enter Calibration Mode:**  
  To start calibration, press the Gripper button (Pin 13) during startup. The system will wait until the button is released before beginning calibration.
- **Calibrate for 10 Seconds:**  
  During the 10-second window, move the potentiometers through their full range of motion to ensure accurate capture of the minimum and maximum values.
- **Automatic Exit:**  
  After 10 seconds, the calibration mode ends, the values are saved in EEPROM, and the robot resumes normal operation using the new calibration data.

---

## Acknowledgements

- Original project by [Build Some Stuff](https://www.printables.com/model/818975-compact-robot-arm-arduino-3d-printed).
- Thanks to all contributors who helped improve the firmware with manual and automatic calibration functionalities.

Feel free to open issues or submit pull requests for further improvements or clarifications.
