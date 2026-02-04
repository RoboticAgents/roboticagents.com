+++
title = "Activity 3: Environmental Sensors"
description = "Hands-on Arduino environmental sensing with temperature, light, and moisture sensors"
weight = 3
+++

## Overview

In this activity, you will wire and experiment with **three types of environmental sensors**: a temperature sensor (TMP36), a light sensor (photoresistor module), and a soil moisture sensor. You'll test how each sensor responds to different environmental conditions and document your findings. This is a team activity where you'll build a multi-sensor environmental monitoring system.

**Teams:** Work in groups of 2-3 students

**Due Date: Thursday, February 6th by 11:50 AM**

---

## Learning Objectives

By completing this activity, you will:
- Wire and operate temperature, light, and moisture sensors
- Read and interpret analog sensor values
- Calibrate sensors for different conditions
- Document experimental findings and observations

---

## Requirements

### What You Must Demonstrate

1. **Correct wiring** of all three sensors to the Arduino Uno
2. **Serial Monitor output** showing all three sensor readings
3. **At least 2 experiments per sensor** testing different conditions
4. **Documentation** of your experiments and findings in `experiments.md`
5. **Push to GitHub** and demonstrate to instructor

---

## Materials Needed

- Arduino Uno
- USB cable
- Breadboard
- Jumper wires
- TMP36 temperature sensor (3 pins)
- Photoresistor module (4 pins)
- Soil moisture sensor (3 pins)

---

## GitHub Classroom

Accept the assignment at: [https://classroom.github.com/a/hZZHXESz](https://classroom.github.com/a/hZZHXESz)

---

## Sensor Details

### TMP36 Temperature Sensor

**Principle:** Voltage output proportional to temperature

**Specifications:**
- Range: -40°C to +125°C
- Output: 10 mV per °C, 500 mV offset at 0°C
- Formula: `temp_C = (voltage - 0.5) × 100`

**Wiring (3 pins):**
- Left pin (red): 5V
- Middle pin (yellow): A0 (analog output)
- Right pin (black): GND

### Photoresistor Module

**Principle:** Resistance changes with light intensity

**Specifications:**
- 4-pin module with built-in comparator
- Use AO (analog out) pin for readings
- Values 0-1023 (higher = more light)

**Wiring:**
- VCC: 5V
- GND: GND
- AO: A1 (analog output)
- DO: Not used for this activity

### Soil Moisture Sensor

**Principle:** Measures soil conductivity (wetness)

**Specifications:**
- 3-pin sensor
- Analog output (0-1023)
- Higher value = drier soil (less conductivity)

**Wiring:**
- VCC: 5V
- AOUT: A2 (analog output)
- GND: GND

---

## Tasks

### Task 1: Wire All Three Sensors

Wire all three sensors according to the specifications above. Use the breadboard to organize your connections.

### Task 2: Read Sensor Values

Create an Arduino sketch that reads all three sensors and outputs their values to the Serial Monitor.

Example code structure:
```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  // Read temperature sensor
  int tempReading = analogRead(A0);
  float voltage = tempReading * (5.0 / 1023.0);
  float tempC = (voltage - 0.5) * 100.0;
  
  // Read light sensor
  int lightLevel = analogRead(A1);
  
  // Read moisture sensor
  int moisture = analogRead(A2);
  
  // Print values
  Serial.print("Temperature: ");
  Serial.print(tempC);
  Serial.print("°C | Light: ");
  Serial.print(lightLevel);
  Serial.print(" | Moisture: ");
  Serial.println(moisture);
  
  delay(1000);
}
```

### Task 3: Conduct Experiments

For each sensor, conduct **at least 2 experiments** testing different conditions:

**Temperature Sensor:**
- Test at room temperature
- Hold sensor between fingers (body heat)
- Place near ice or cold water
- Any other temperature variations you can safely create

**Light Sensor:**
- Measure in normal room light
- Cover sensor completely (darkness)
- Shine flashlight directly on sensor
- Test under different lighting conditions

**Moisture Sensor:**
- Test in air (completely dry)
- Test in water (completely wet)
- Test in damp soil or paper towel
- Test at different moisture levels

### Task 4: Document Your Findings

In your GitHub repository, create an `experiments.md` file documenting:
- Your experimental setup
- The conditions you tested
- The sensor readings you observed
- Any patterns or insights you discovered
- Any challenges or issues you encountered

### Task 5: Calibrate and Interpret

For each sensor, determine threshold values for different states:
- Temperature: Cold, normal, warm
- Light: Dark, dim, bright
- Moisture: Dry, moist, wet

---

## Deliverables

1. **Working circuit** with all three sensors
2. **Arduino sketch** that reads all sensors
3. **Serial Monitor output** showing readings
4. **experiments.md** file with your findings
5. **Demonstration** to instructor by due date

---

## Tips and Troubleshooting

- **Loose connections** are the most common issue - make sure wires are firmly inserted
- **Check sensor orientation** - many sensors have specific pin orders
- **Temperature readings jumping wildly?** Check for loose wires
- **Light sensor not changing?** Make sure you're reading the AO pin, not DO
- **Moisture sensor gives constant values?** Make sure the probes are clean and making contact

---

## Assessment

This activity will be assessed based on:
- ✓ Correct wiring of all sensors
- ✓ Working code that reads all sensors
- ✓ Quality of experiments conducted
- ✓ Thoroughness of documentation
- ✓ Successful demonstration

---

## Resources

- [Sensors Slides](/slides/sensors.html)
- [TMP36 Datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/TMP35_36_37.pdf)
- Arduino Analog Input Reference: `analogRead()`
