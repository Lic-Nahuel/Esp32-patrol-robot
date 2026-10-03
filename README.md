🤖 ESP32 Patrol Robot

A custom-built autonomous patrol robot based on an ESP32-S3, developed by combining embedded systems, robotics, sensors, computer vision and IoT technologies.

The project started from an old robot vacuum cleaner chassis and is being transformed into a mobile robotic platform for remote operation, obstacle detection and autonomous indoor patrol.

🚀 Project Goals

The robot is being developed to:

- Drive remotely through a mobile interface
- Detect and avoid obstacles
- Monitor its surroundings using multiple sensors
- Communicate over the Internet
- Use computer vision for environmental perception
- Identify rooms and locations using visual markers
- Perform autonomous patrol routines
- Detect people and interact with them
- Provide two-way audio and video through a connected smartphone

🔧 Hardware

Main controller

- ESP32-S3 development board
- USB-Serial-JTAG
- 8 MB PSRAM

Sensors and actuators

- HC-SR04 ultrasonic distance sensor
- Multiple IR obstacle sensors
- Analog shock / bumper sensors
- SG90 servo for rotating the radar sensor
- TB6612FNG dual motor driver
- DC motors from the original robot platform

Communication

- Wi-Fi
- MQTT
- Smartphone integration

📌 Current Pinout

Component| GPIO
HC-SR04 TRIG| GPIO 41
HC-SR04 ECHO| GPIO 42
Radar Servo| GPIO 13
IR Left| GPIO 18 / GPIO 8
IR Right| GPIO 11 / GPIO 12
IR Front| GPIO 9 / GPIO 10
IR Rear| GPIO 3 / GPIO 46
Remote IR Receiver| GPIO 14
Left Bumper| GPIO 1
Right Bumper| GPIO 2
TB6612 PWMB| GPIO 4
TB6612 BIN2| GPIO 5
TB6612 BIN1| GPIO 6
TB6612 STBY| GPIO 7
TB6612 AIN1| GPIO 15
TB6612 AIN2| GPIO 16
TB6612 PWMA| GPIO 17

💻 Software

The current firmware is based on:

- Arduino framework
- C/C++
- ESP32
- MQTT
- PubSubClient
- ESP32Servo
- WebServer

The robot publishes telemetry and receives movement commands through MQTT.

🧠 Computer Vision & AI

Computer vision is part of the planned evolution of the project.

Technologies being explored include:

- Python
- OpenCV
- MediaPipe
- Object/person detection
- Visual room identification
- QR markers
- Autonomous navigation

The long-term goal is to combine traditional sensors with computer vision to improve the robot's perception of its environment.

📡 Remote Operation

The robot is designed to support remote operation through an Internet-connected interface.

The smartphone acts as the robot's:

- Camera
- Display
- Microphone
- Speaker
- User interface

The ESP32 remains responsible for the robot's hardware control and sensor integration.

🏠 Autonomous Patrol

The autonomous mode is intended to allow the robot to patrol indoor environments while:

1. Monitoring obstacles
2. Detecting its surroundings
3. Avoiding collisions
4. Identifying locations
5. Detecting people
6. Executing predefined patrol behaviors

📈 Project Status...

Implemented

- [x] ESP32-S3 motor control
- [x] TB6612FNG motor driver integration
- [x] Ultrasonic distance sensing
- [x] IR obstacle detection
- [x] Bumper/shock sensors
- [x] Servo-controlled sensor platform
- [x] MQTT communication
- [x] Remote movement commands
- [x] Robot telemetry

In development...

- [ ] Smartphone control interface
- [ ] Two-way audio
- [ ] Video streaming
- [ ] Computer vision
- [ ] Person detection
- [ ] QR-based room identification
- [ ] Autonomous navigation
- [ ] Patrol route management
- [ ] Sleep / operator mode

🗺️ Roadmap

Future development will focus on:

1. Improving obstacle avoidance
2. Integrating computer vision
3. Adding autonomous navigation
4. Developing a mobile operator interface
5. Combining sensor data and visual perception
6. Implementing autonomous patrol behaviors
7. Improving reliability and safety

👨‍💻 Author

Nahuel Esteban Sanzol

Biomedical Engineering student with a professional background in healthcare and clinical technology.

Interested in:

- Artificial Intelligence
- Computer Vision
- Robotics
- Embedded Systems
- Medical Devices
- Healthcare Technology

🔗 "LinkedIn" (https://www.linkedin.com/in/licnahuelsanzol/)
