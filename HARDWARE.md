- Hardware -

Main Controller

The robot is controlled by an ESP32-S3 development board.

The ESP32-S3 is responsible for:

- Motor control
- Sensor acquisition
- Servo control
- Wireless communication
- MQTT communication
- Robot telemetry
- Autonomous behavior logic

Motor Driver

TB6612FNG dual motor driver

The driver controls the two DC motors of the robot.

TB6612FNG| ESP32-S3
PWMA| GPIO 17
AIN1| GPIO 15
AIN2| GPIO 16
STBY| GPIO 7
BIN1| GPIO 6
BIN2| GPIO 5
PWMB| GPIO 4

Motor connections

- A01 / A02 → Right motor
- B01 / B02 → Left motor

Rotating Sensor Tower

The robot uses a servo-driven rotating sensor tower for environmental scanning.

The tower combines two different distance-sensing technologies:

US-100 Ultrasonic Sensor

The US-100 ultrasonic sensor uses ultrasonic waves to measure distance.

It is mounted facing forward on the rotating tower.

VL53L0X Time-of-Flight Sensor

A compact VL53L0X ToF sensor is mounted facing backward on the same tower.

The VL53L0X uses infrared Time-of-Flight measurements to estimate distance.

360° Environmental Scanning

The sensor tower rotates using a servo, allowing the robot to scan its surroundings.

During a sweep, the robot can collect measurements from two different sensing technologies.

The purpose of this design is to provide complementary distance information and explore how different sensing technologies behave with different surfaces and objects.

Using ultrasonic and optical ToF sensing together can provide useful information when one sensing method produces less reliable measurements for a particular surface or object.

The sensor tower is intended to support future:

- Obstacle avoidance
- Environmental mapping
- Autonomous navigation
- Sensor fusion
- Room perception

Radar Servo

Component| ESP32-S3
Sensor tower servo| GPIO 13

The servo rotates the sensor tower during environmental scans.

IR Obstacle Sensors

The robot uses multiple IR sensor pairs for short-range obstacle detection.

Left

Sensor| GPIO
IR sensor| GPIO 18
IR sensor| GPIO 8

Right

Sensor| GPIO
IR sensor| GPIO 11
IR sensor| GPIO 12

Front

Sensor| GPIO
IR sensor| GPIO 9
IR sensor| GPIO 10

Rear

Sensor| GPIO
IR sensor| GPIO 3
IR sensor| GPIO 46

The IR sensors provide short-range directional obstacle detection and complement the distance sensors on the rotating tower.

Bumper / Shock Sensors

The robot uses analog shock sensors to detect physical impacts.

Sensor| ESP32-S3
Left bumper| GPIO 1
Right bumper| GPIO 2

The sensors are read as analog inputs and compared against a threshold to detect collisions.

Remote Control Receiver

An IR receiver is connected to:

Component| ESP32-S3
IR remote receiver| GPIO 14

This input is used for local remote-control experiments and testing.

Communication

The robot uses Wi-Fi for network communication.

MQTT is used as the communication layer between the robot and the remote control system.

The current firmware uses:

- MQTT
- PubSubClient
- Wi-Fi
- Robot command topics
- Telemetry topics

The robot publishes telemetry and receives movement commands through MQTT.

Power Architecture

The robot uses a 12 V lithium battery as the main power source for the motor system.

The architecture separates:

- Motor power
- ESP32/control electronics
- Sensors and peripherals

Power distribution and battery management are still being refined as part of the prototype development.

Smartphone Integration

A smartphone is planned to act as the robot's human interface.

The phone provides:

- Camera
- Display
- Microphone
- Speaker
- Operator interface

The ESP32 remains responsible for low-level robot control, sensors and motor management.

The smartphone and ESP32 are intended to work as separate components rather than using the phone as a communication bridge for the robot's low-level hardware.

System Architecture

At a high level:

                         ┌──────────────────────┐
                         │      Smartphone      │
                         │                      │
                         │ Camera / Display     │
                         │ Microphone / Speaker │
                         │ Operator Interface   │
                         └──────────┬───────────┘
                                    │
                              Wi-Fi / Internet
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │       ESP32-S3       │
                         │                      │
                         │ Control / MQTT       │
                         │ Telemetry / Logic    │
                         └──────────┬───────────┘
                                           │
             ┌──────────────────────┼──────────────────────┐
             │                      │                      │
             ▼                      ▼                      ▼
      ┌─────────────┐       ┌──────────────┐       ┌─────────────┐
      │ TB6612FNG   │       │.         Sensor Tower │       │.               IR Sensors  │
      │ Motor Driver│       │              │       │                            │
      └──────┬──────┘       │ US-100       │               │ Left/Right  │
                  │                  │ VL53L0X      │               │ Front/Rear  │
                  ▼                  │ Servo        │                └─────────────┘
               DC Motors              └──────────────┘

Design Approach

The hardware architecture follows a multi-sensor approach.

Different sensors are used for different sensing ranges and conditions:

- US-100 → ultrasonic distance measurement
- VL53L0X → optical Time-of-Flight distance measurement
- IR sensors → short-range obstacle detection
- Shock sensors → physical collision detection
- Rotating sensor tower → directional environmental scanning

This architecture is intended to provide complementary information for future autonomous navigation and obstacle avoidance.

Future Sensor Fusion

One of the planned developments is to combine measurements from the different sensors to improve the robot's understanding of its environment.

Potential future applications include:

- Comparing ultrasonic and ToF measurements
- Detecting inconsistent measurements
- Improving obstacle detection
- Building a 360° distance profile
- Supporting autonomous navigation
- Combining sensor measurements with computer vision

Design Goals

The hardware architecture is designed to support future integration of:

- Computer vision
- Autonomous navigation
- Person detection
- QR-based room identification
- Smartphone camera integration
- Two-way audio
- Autonomous patrol behaviors
- Sensor fusion
- Environmental mapping

Status

Hardware integration is an ongoing process.

The GPIO assignments documented here correspond to the current prototype configuration. Sensor interfaces and power distribution may evolve as the project develops.
