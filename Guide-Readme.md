# Object Following Robot using Arduino UNO

A smart **Human Following Robot** built using **Arduino UNO**, **L298N Motor Driver**, **HC-SR04 Ultrasonic Sensor**, **Dual IR Sensors**, **SG90 Servo Motor**, and a **0.96" OLED Display**. The robot follows a nearby person or object, scans its surroundings using a servo-mounted ultrasonic sensor, and displays the measured distance on the OLED.

---

## 📌 Features

- 🤖 Object Following
- 📏 Real-time Distance Measurement
- 🔄 Servo-based Ultrasonic Scanning
- 📺 OLED Distance Display
- 🚗 Differential Drive using 4 BO Motors
- ⚡ PWM Speed Control
- 🛑 Automatic Stop at Minimum Distance
- ↩️ Automatic Left/Right Turning using IR Sensors

---

## 📷 Project Overview

The robot continuously measures the distance to the object in front using the HC-SR04 ultrasonic sensor. Two IR sensors detect whether the target is slightly left or right. Based on this information, the robot adjusts its movement to follow the target while maintaining a safe distance.

The ultrasonic sensor is mounted on an SG90 servo motor, enabling left-center-right scanning whenever the target is lost or an obstacle is encountered. The measured distance is displayed in real-time on the OLED display.

---

# Hardware Components

| Component                    |    Quantity |
| ---------------------------- | ----------: |
| Arduino UNO                  |           1 |
| L298N Motor Driver           |           1 |
| HC-SR04 Ultrasonic Sensor    |           1 |
| SG90 Servo Motor              |           1 |
| SSD1306 OLED Display (0.96") |           1 |
| IR Obstacle Sensors          |           2 |
| BO Motors                    |           4 |
| Robot Chassis                |           1 |
| Wheels                       |           4 |
| 18650 Batteries              |         2–3 |
| Buck Converter (Servo Power) |           1 |
| Jumper Wires                 | As Required |

---

# Circuit Connections (Arduino UNO)

## Arduino UNO Pin Map

| Arduino Pin | Connected To     |
| ----------- | ---------------- |
| D2          | Servo Signal      |
| D3          | ENB (L298N, PWM) |
| D4          | IN4 (L298N)       |
| D5          | ENA (L298N, PWM) |
| D6          | IN1 (L298N)       |
| D7          | IN2 (L298N)       |
| D8          | IN3 (L298N)       |
| D9          | Ultrasonic TRIG   |
| D10         | Ultrasonic ECHO   |
| D11         | Left IR Sensor OUT|
| D12         | Right IR Sensor OUT|
| A4          | OLED SDA          |
| A5          | OLED SCL          |
| 5V          | OLED & Sensors    |
| GND         | Common Ground     |

> **Note:** Pins D3–D12 are dedicated to the ultrasonic sensor, IR sensors, and motor driver, freeing D2 for the servo and A4/A5 for the OLED (I2C).

---

## HC-SR04 Ultrasonic Sensor

| HC-SR04 | Arduino UNO |
| ------- | ----------- |
| VCC     | 5V          |
| GND     | GND         |
| TRIG    | D9          |
| ECHO    | D10         |

---

## Left IR Sensor

| IR Sensor | Arduino UNO |
| --------- | ----------- |
| VCC       | 5V          |
| GND       | GND         |
| OUT       | D11         |

## Right IR Sensor

| IR Sensor | Arduino UNO |
| --------- | ----------- |
| VCC       | 5V          |
| GND       | GND         |
| OUT       | D12         |

---

## L298N Motor Driver

| L298N | Arduino UNO |
| ----- | ----------- |
| ENA   | D5 (PWM)    |
| IN1   | D6          |
| IN2   | D7          |
| IN3   | D8          |
| IN4   | D4          |
| ENB   | D3 (PWM)    |

### Motor Outputs

- **OUT1 & OUT2** → Left-side motors (front and rear connected in parallel)
- **OUT3 & OUT4** → Right-side motors (front and rear connected in parallel)

> **Note:** If your robot moves in the wrong direction, swap the two wires on that side's OUT terminals rather than rewriting the code.

---

## Servo Connections

| Servo Wire | Connection               |
| ---------- | ------------------------ |
| Signal     | Arduino D2                |
| VCC        | Buck Converter 5V Output |
| GND        | Buck Converter GND       |

---

## OLED Display

| OLED | Arduino UNO |
| ---- | ----------- |
| VCC  | 5V          |
| GND  | GND         |
| SDA  | A4          |
| SCL  | A5          |

---

## Power Supply

### Battery Pack

- 2 × 18650 Batteries (Recommended)
- 3 × 18650 Batteries (Higher Speed)

### Power Connections

- **Battery +** → L298N **12V / VIN**
- **Battery −** → L298N **GND**
- **Arduino GND** ↔ **L298N GND** (common ground — required)
- Arduino can be powered through the L298N **5V output** (only if the L298N's onboard 5V regulator is enabled and battery voltage is suitable, e.g. 7–12V), **or** power the Arduino separately via USB/barrel jack.

### Buck Converter Output (Servo Power)

```
OUT+ → Servo VCC
OUT- → Servo GND
```

All grounds (Arduino, L298N, buck converter, battery) must be connected together.

---

# Software Requirements

- Arduino IDE
- Arduino UNO Board Package

---

## Required Libraries

Install the following libraries using the Arduino Library Manager:

- Servo
- Adafruit GFX
- Adafruit SSD1306

---

# Working Principle

1. The HC-SR04 measures the distance to the object.
2. The OLED displays the measured distance.
3. If the object is between the minimum and maximum distance:
   - The robot moves forward.
4. If the left IR sensor detects the object:
   - The robot turns left.
5. If the right IR sensor detects the object:
   - The robot turns right.
6. If the object is too close:
   - The robot stops.
7. If no object is detected:
   - The servo scans left and right.
   - The robot turns toward the direction with greater free space.

---

# Pin Configuration

```cpp
#define SERVO_PIN 2

#define ENB 3
#define IN4 4
#define ENA 5
#define IN1 6
#define IN2 7
#define IN3 8

#define TRIG 9
#define ECHO 10

#define LEFT_IR 11
#define RIGHT_IR 12
```

---

# Motor Speed

```cpp
#define MOTOR_SPEED 255
#define TURN_SPEED 200
```

PWM Range

```
0 - 255
```

---

# Future Improvements

- ESP32-CAM Human Detection
- Bluetooth Manual Control
- Voice Commands
- Gesture Recognition
- Obstacle Avoidance
- Line Following Mode
- Mobile App Control
- Battery Voltage Monitoring
- Automatic Charging Dock

---

# Applications

- Personal Assistant Robot
- Smart Shopping Cart
- Warehouse Automation
- Object Following Robot
- Educational Robotics
- Human Assistance Robot
- Indoor Navigation
