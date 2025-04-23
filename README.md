# Arduino Flight Controller

This repository provides the source code and instructions for building an Arduino-based flight controller for quadcopter drones. The system utilizes the Arduino Uno to manage flight dynamics, Electronic Speed Controllers (ESCs), gyro calibration, and real-time flight control. It supports PID tuning, vibration analysis, and a WiFi-based user interface. With this setup, hobbyists and developers can create a robust quadcopter platform for experimentation and learning.

---

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Getting Started](#getting-started)
- [Hardware Requirements](#hardware-requirements)
- [Software Requirements](#software-requirements)
- [Code Structure](#code-structure)
  - [Setup Program](#1-setupino)
  - [ESC Calibration](#2-esc_calibrationino)
  - [Flight Controller](#3-flight_controllerino)
- [Usage](#usage)
  - [System Setup](#1-system-setup)
  - [ESC Calibration](#2-esc-calibration)
  - [Flight Control](#3-flight-control)
- [Safety Notes](#safety-notes)
- [Troubleshooting](#troubleshooting)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## Overview

This project is designed to turn an Arduino Uno into the central brain of a quadcopter. The source code in this repository is divided into three key components:
1. **Setup Program:** For initializing and calibrating the flight controller.
2. **ESC Calibration:** For tuning ESCs and analyzing motor vibrations.
3. **Flight Controller:** For real-time control via a WiFi interface.

This project is ideal for those looking to explore the basics of drone technology, sensor calibration, and motor control systems.

---

## Features

- **Automatic Gyro Calibration:** Supports MPU-6050, L3G4200D, and L3GD20H sensors.
- **Receiver Signal Validation:** Ensures proper communication between the transmitter and Arduino.
- **ESC Calibration and Testing:** Allows tuning of ESCs and testing of individual motors.
- **Vibration Analysis:** Uses the accelerometer to analyze and reduce motor vibrations.
- **WiFi-Based Control:** Includes a built-in web server for issuing flight commands.
- **Persistent Configuration:** Stores calibration data in EEPROM for consistent performance.
- **Real-Time Diagnostics:** Monitors receiver signals, quadcopter angles, and motor states.

---

## Getting Started

### 1. Clone the Repository
Clone this repository to your local machine:
```bash
git clone https://github.com/ZhadowNyx/Arduino-Flight-Controller.git
```

### 2. Open the Code
Open the `.ino` files in the Arduino IDE. Choose the file based on your task (e.g., `setup.ino` for initial setup).

### 3. Upload to Arduino
Connect your Arduino Uno to your computer via USB. Select the appropriate COM port and board type in the Arduino IDE, then upload the code.

---

## Hardware Requirements

- **Microcontroller:** Arduino Uno
- **Gyro Sensor:** MPU-6050, L3G4200D, or L3GD20H
- **Motor Driver:** L298N
- **Motors:** 4 Quadcopter brushless motors
- **ESCs:** 4 Electronic Speed Controllers
- **WiFi Module:** ESP8266 or similar (used in `flight_controller.ino`)
- **Propellers:** Matched to the motor specifications
- **Power Source:** LiPo battery (3S or 4S recommended)
- **Miscellaneous:** Jumper wires, breadboard (optional), and connectors.

---

## Software Requirements

- [Arduino IDE](https://www.arduino.cc/en/software)
- Required Libraries:
  - `Wire.h` (for I2C communication with sensors)
  - `EEPROM.h` (for storing calibration data)
  - `WiFi.h` (for WiFi-based control)

---

## Code Structure

### 1. `setup.ino`
The setup program initializes the flight controller by:
- Configuring the Arduino pins for input/output.
- Calibrating the gyro and storing offsets for roll, pitch, and yaw.
- Validating receiver signals and assigning channels.
- Storing all configuration data in EEPROM for future use.

This program is essential to ensure all components are functioning correctly before moving to the next steps.

---

### 2. `esc_calibration.ino`
This file is used to calibrate and test the Electronic Speed Controllers (ESCs) for the motors:
- Supports individual motor testing (`1`, `2`, `3`, `4`) and all motors simultaneously (`5`).
- Analyzes vibrations using accelerometer data to identify poorly balanced propellers.
- Outputs receiver signals and quadcopter angles for debugging.

During calibration, ensure the throttle is set to its lowest position before proceeding.

---

### 3. `flight_controller.ino`
The core file for real-time flight control:
- Sets up a WiFi access point (`nodeMCU Car`) with a web server.
- Accepts commands like `F` (forward), `B` (backward), `L` (left), `R` (right), and speed adjustments (`0`–`9`).
- Controls the motors via the L298N motor driver.
- Implements diagonal movements and speed coefficients for precise control.

---

## Usage

### 1. System Setup
- Upload `setup.ino` to the Arduino Uno.
- Open the serial monitor in the Arduino IDE at `57600` baud rate.
- Follow the prompts to calibrate the gyro, validate receiver signals, and store configuration data.

### 2. ESC Calibration
- Upload `esc_calibration.ino` to the Arduino Uno.
- Use the serial monitor to send commands:
  - `1`, `2`, `3`, `4`: Test individual motors.
  - `5`: Test all motors simultaneously.
  - `a`: Print quadcopter angles.
  - `r`: Print receiver signals.
- Observe motor behavior and ensure smooth operation.

### 3. Flight Control
- Upload `flight_controller.ino` to the Arduino Uno.
- Connect to the WiFi network (`nodeMCU Car`) using your smartphone or computer.
- Open a browser and navigate to `192.168.4.1`.
- Send commands to control the quadcopter:
  - `F`: Move forward.
  - `B`: Move backward.
  - `L`: Turn left.
  - `R`: Turn right.
  - `S`: Stop.
  - `0`–`9`: Adjust speed.

---

## Safety Notes

- **Propeller Removal:** Always remove propellers during setup, calibration, and testing to avoid accidents.
- **Clear Surroundings:** Ensure the area around the quadcopter is clear of people and objects.
- **Battery Safety:** Use appropriate LiPo chargers and avoid over-discharging.
- **Secure Connections:** Double-check all wiring and connections to prevent short circuits or loose components.

---

## Troubleshooting

### Common Issues
- **No Receiver Signals:** Ensure the transmitter is powered on and bound to the receiver.
- **Gyro Not Detected:** Check the I2C connections and ensure the correct gyro address is configured.
- **ESC Beeping Continuously:** Verify the throttle is set to the lowest position during calibration.
- **WiFi Not Connecting:** Check the SSID and ensure no other devices are using the same network name.

---

## Acknowledgments

- Inspired by the YMFC-AL project by Joop Brokking.
- For additional guidance, visit [www.brokking.net](http://www.brokking.net).

---
