- Software -

Overview

The robot firmware runs on an ESP32-S3 and is responsible for controlling the robot's hardware, reading sensors, communicating over Wi-Fi and exchanging commands and telemetry through MQTT.

The software architecture is being developed incrementally, with individual hardware components tested before being integrated into the complete system, one by one.

Firmware

The current firmware is developed using the Arduino framework for ESP32.

Main technologies and libraries include:

- C/C++
- Arduino framework
- ESP32
- Wi-Fi
- MQTT
- PubSubClient
- ESP32Servo
- WebServer

Robot Control

The ESP32 controls the two DC motors through a TB6612FNG dual motor driver.

The firmware provides independent control of:

- Forward movement
- Reverse movement
- Left/right turning
- Motor speed
- Stop

PWM is used to control motor speed.

Sensor Processing

The firmware continuously reads information from several sensors.

Distance sensing

The rotating sensor tower combines:

- US-100 ultrasonic distance sensor
- VL53L0X Time-of-Flight sensor

The tower is rotated by a servo to perform directional distance scans.

Short-range obstacle detection

IR sensors are positioned around the robot to detect nearby obstacles.

Collision detection

Analog shock sensors are used to detect physical impacts with obstacles.

Sensor Tower

The sensor tower is controlled by a servo connected to the ESP32-S3.

During a scan, the robot can rotate the tower and collect distance measurements from different directions.

The long-term goal is to use these measurements to create a directional representation of the robot's surroundings.

MQTT Communication

MQTT is used as the communication protocol between the robot and the remote control system.

The robot subscribes to command topics and publishes telemetry.

Conceptually:

Remote Control
      │
      │ MQTT command
      ▼
   ESP32-S3
      │
      ├── Motor control
      ├── Sensor processing
      └── Robot behavior
      │
      │ MQTT telemetry
      ▼
Remote Monitoring

The current firmware uses the robot identifier:

ROBOT-01

Example topic structure:

robot/ROBOT-01/cmd
robot/ROBOT-01/telemetry

Telemetry

The robot periodically publishes information about its current state.

Telemetry is intended to provide information such as:

- Sensor readings
- Robot state
- Movement state
- Obstacle detection
- Connection status

Telemetry allows the remote system to monitor the robot while it is operating.

Watchdog

A watchdog mechanism is used to improve system reliability.

If the firmware stops responding within the expected interval, the watchdog can trigger a recovery/reset mechanism.

This is particularly important for a mobile robot operating without continuous physical supervision.

Development Approach

The project follows an incremental development approach.

Hardware components are tested individually before integration:

1. Motor driver
2. IR sensors
3. Collision sensors
4. Distance sensors
5. Servo-controlled sensor tower
6. MQTT communication
7. Complete robot behavior

This approach helps isolate hardware and software problems during development.

Planned Software Features

Future development includes:

- Smartphone operator interface
- Video streaming
- Two-way audio
- Computer vision
- Person detection
- QR-based room identification
- Autonomous patrol routines
- Autonomous navigation
- Sensor fusion
- Environmental mapping
- Sleep/operator mode

Computer Vision

Computer vision is planned as a higher-level perception layer.

Potential technologies include:

- Python
- OpenCV
- MediaPipe
- Object detection
- Person detection
- QR recognition

The long-term architecture is intended to combine visual information with the physical sensors already integrated into the robot.

Architecture Direction

The project is evolving toward a layered architecture:

┌──────────────────────────────────┐
│          User Interface          │
│       Smartphone / Operator      │
└────────────────┬─────────────────┘
                             │
┌────────────────▼─────────────────┐
│       Network Communication      │
│             MQTT / Wi-Fi         │
└────────────────┬─────────────────┘
                             │
┌────────────────▼─────────────────┐
│          Robot Control           │
│             ESP32-S3             │
└────────────────┬─────────────────┘
                        │
       ┌─────────┼─────────┐
       ▼               ▼               ▼
    Motors           Sensors          Servo
                        │ 
       ┌─────────┼─────────┐
       ▼               ▼               ▼
     IR              US-100          VL53L0X

The architecture is designed to allow higher-level AI and computer-vision functionality to evolve independently from the low-level embedded control system.

Current Status

The software is under active development.

The current prototype has working hardware-control, sensor-integration and MQTT communication components. Higher-level autonomous and computer-vision capabilities are being developed incrementally.