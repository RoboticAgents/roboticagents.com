+++
title = "Activity 2: Distance Sensors"
description = "Hands-on Arduino distance sensing with ultrasonic and IR sensors"
weight = 2
+++

## Overview

In this activity, you will wire and experiment with **two types of distance sensors**: an ultrasonic sensor (HC-SR04) and an infrared (IR) obstacle detection sensor. You'll test how each sensor responds to different objects, surfaces, and distances. This is a team demonstration activity where you'll show your understanding of sensor operation and explore their strengths and limitations.

**Teams:** Work in groups of 2-3 students

**Due Date: Monday, February 3rd by 11:50 AM**

---

## Learning Objectives

By completing this activity, you will:
- Wire and operate ultrasonic and IR distance sensors
- Understand how different sensors detect obstacles
- Explore sensor performance across various conditions
- Learn when to use each sensor type in robotics applications

---

## Requirements

### What You Must Demonstrate

1. **Wire both sensors** correctly to Arduino Uno
2. **Show both sensors working** with Serial Monitor output
3. **Conduct at least 2 experiments per sensor** from the suggested list below
4. **Explain your findings** to the instructor

---

## Grading Criteria

This is a **Class Activity** worth points toward your participation grade.

**Grading Rubric** (Pass/Fail with feedback):

| Criterion | Points | Description |
|:----------|:------:|:------------|
| **Ultrasonic Wiring & Demo** | 25% | HC-SR04 correctly wired; distance readings displayed |
| **IR Wiring & Demo** | 25% | IR sensor correctly wired; obstacle detection working |
| **Experiments** | 30% | Completed at least 2 experiments per sensor; systematic testing |
| **Explanation** | 20% | Can explain sensor behavior; answers instructor questions |

**To Pass**: You must achieve at least 70% overall. Both sensors must be functional.

---

## Part 1: Ultrasonic Sensor (HC-SR04)

### Understanding Ultrasonic Sensors

The **HC-SR04** uses **sound waves** (40 kHz ultrasonic) to measure distance:
- Sends out a sound pulse
- Measures time for echo to return
- Calculates distance: `distance = (time × speed_of_sound) / 2`

**Specifications:**
- Range: 2 cm to 400 cm
- Accuracy: ±3 mm
- Beam angle: ~15°

---

### Wiring the HC-SR04

**Components:**
- Arduino Uno
- HC-SR04 ultrasonic sensor
- 4 jumper wires
- Breadboard (optional)

| HC-SR04 Pin | Arduino Pin | Purpose |
|:------------|:------------|:--------|
| VCC | 5V | Power |
| TRIG | Any digital pin (e.g., Pin 9) | Trigger pulse |
| ECHO | Any digital pin (e.g., Pin 10) | Echo response |
| GND | GND | Ground |

---

### Arduino Code for HC-SR04

```cpp
// HC-SR04 Ultrasonic Sensor
#define TRIG_PIN 9
#define ECHO_PIN 10

void setup() {
  Serial.begin(9600);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  Serial.println("HC-SR04 Test - Distance in cm:");
}

void loop() {
  // Send trigger pulse
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);
  
  // Measure echo duration
  long duration = pulseIn(ECHO_PIN, HIGH);
  
  // Calculate distance in cm
  float distance = duration * 0.034 / 2;
  
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  
  delay(500);
}
```

---

## Part 2: Infrared (IR) Obstacle Sensor

### Understanding IR Sensors

**Digital IR sensors** emit infrared light and detect reflections:
- Output: **HIGH (1)** when no obstacle detected, **LOW (0)** when obstacle is present
- The sensor compares reflected IR light intensity to an internal threshold
- If reflection is strong enough (object is close/reflective), output goes LOW
- If reflection is weak (object far/absent), output stays HIGH

**Key Component - Potentiometer:**
- Small adjustable screw or dial on the sensor
- Controls the **sensitivity threshold** - how much reflected light triggers detection
- **Turn clockwise** → sensor becomes more sensitive (detects from farther away)
- **Turn counter-clockwise** → sensor becomes less sensitive (only detects very close objects)
- This lets you tune the sensor for your specific use case

**Typical range:** 2-30 cm (adjustable via potentiometer)

---

### Wiring the IR Sensor

**Components:**
- Arduino Uno
- IR obstacle detection sensor
- 3 jumper wires

| IR Sensor Pin | Arduino Pin | Purpose |
|:--------------|:------------|:--------|
| VCC | 5V | Power |
| OUT | Any digital pin (e.g., Pin 2) | Detection signal |
| GND | GND | Ground |

---

### Arduino Code for IR Sensor

```cpp
// Digital IR Obstacle Sensor
#define IR_PIN 2

void setup() {
  Serial.begin(9600);
  pinMode(IR_PIN, INPUT);
  Serial.println("IR Sensor Test:");
}

void loop() {
  int sensorState = digitalRead(IR_PIN);
  
  Serial.print("Sensor value: ");
  Serial.print(sensorState);
  Serial.print(" - ");
  
  if (sensorState == LOW) {
    Serial.println("OBSTACLE DETECTED!");
  } else {
    Serial.println("Clear");
  }
  
  delay(300);
}
```

**Tip:** The IR sensor outputs binary (0 or 1) values. Adjust the potentiometer to set when it switches from 0→1:
- **Clockwise rotation** = more sensitive = detects farther away
- **Counter-clockwise** = less sensitive = only detects very close objects
- Find the "sweet spot" for your detection distance by testing with an object and slowly turning the potentiometer

---

## Part 3: Suggested Experiments

### For Ultrasonic Sensor:

1. **Distance Test**: Measure objects at 10cm, 30cm, 50cm, 100cm - how accurate is it?
2. **Surface Test**: Try flat wall, angled surface (45°), soft material (cloth/foam)
3. **Object Size**: Test with large box, thin object (pencil), your hand
4. **Material Test**: Compare wood, metal, cardboard, plastic

### For IR Sensor:

1. **Distance Range**: Find minimum and maximum detection distances
2. **Color Test**: Try white paper, black paper, colored objects
3. **Surface Test**: Compare matte vs. glossy/reflective surfaces
4. **Angle Test**: Move object side-to-side to find detection angle

**Choose at least 2 experiments per sensor to demonstrate.**

---

## Part 4: Demonstration Checklist

When demonstrating to the instructor, be ready to:

- ✓ Show both sensors wired correctly
- ✓ Display Serial Monitor output for both sensors
- ✓ Demonstrate at least 2 experiments per sensor
- ✓ Explain what you observed and why
- ✓ Answer questions about sensor behavior

---

## Troubleshooting

### Ultrasonic Sensor Issues

| Problem | Solution |
|:--------|:---------|
| Always reads 0 or 400+ cm | Check wiring; verify TRIG and ECHO pins |
| Inconsistent readings | Test in quiet environment; ensure stable power |

### IR Sensor Issues

| Problem | Solution |
|:--------|:---------|
| Always/never detects | Adjust potentiometer; check wiring |
| Inconsistent detection | Calibrate for specific distance |

---

## Resources

- [HC-SR04 Datasheet](https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf)
- [Arduino pulseIn() Documentation](https://www.arduino.cc/reference/en/language/functions/advanced-io/pulsein/)

---

**Good luck exploring robot perception! 🤖📏**
