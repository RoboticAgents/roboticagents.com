+++
title = "Motors and Arduino for Robotics"
description = "Week 2 lecture on motors, power, and Arduino basics"
weight = 2
+++

<style>
.reveal h1 { font-size: 2.5em; }
.reveal h2 { font-size: 2em; color: #2a5599; }
.reveal h3 { font-size: 1.5em; color: #4a7fbb; }
.reveal ul { font-size: 0.9em; }
.reveal .small { font-size: 0.7em; }
.reveal .highlight { color: #d9534f; font-weight: bold; }
.reveal .box { 
    background: #f5f5f5; 
    padding: 20px; 
    border-radius: 10px; 
    margin: 20px 0;
}
</style>

---

# Motors and Arduino for Robotics

**Week 2 • CMPSC 304 Robotic Agents**

---

## Today's Agenda

- Arduino Uno basics and power flow
- Digital vs. Analog signals
- Pulse Width Modulation (PWM)
- Battery voltage calculations
- Why we need motor drivers
- DC motors for Project 1
- Motor types overview

---

## Arduino Uno Overview

### USB Connection
![Arduino USB Port](/img/arduino1.png)

- **USB-B port** connects Arduino to your computer
- Used to upload code to the Arduino microcontroller
- Powers the Arduino during programming
- Enables serial communication for debugging

---

### Digital Pins
![Arduino Digital Pins](/img/arduino2.png)

- **Digital input/output pins** (0-13)
- Pins can be **HIGH** (5V) or **LOW** (0V)
- **Outputs:** Turn on an LED every 10 seconds to make it blink
- **Inputs:** Read sensor data (e.g., is surface wet or dry?)
- **Pins with ~ symbol:** Support PWM (Pulse Width Modulation)
  - PWM pins: 3, 5, 6, 9, 10, 11
  - Allow variable "analog-like" output by rapidly switching on/off

---

### Analog Pins
![Arduino Analog Pins](/img/arduino3.png)

- **Analog input pins** (A0-A5)
- Can read a **range of values** (0-1023)
- Perfect for sensors with continuous output
- **Examples:**
  - Distance sensors
  - Light sensors
  - Temperature sensors
  - Potentiometers

---

### Power Pins
![Arduino Power Pins](/img/arduino4.png)

- **Power and ground connections**
- **5V pin:** Provides 5 volts (HIGH)
- **3.3V pin:** Provides 3.3 volts (for sensitive components)
- **GND pins:** Ground/reference voltage (LOW, 0V)
- **Vin:** Input voltage (7-12V recommended)
- **Circuits flow from GND to HIGH to complete the circuit**

---

## Digital vs. Analog Signals

### Digital Signals
<div class="box">

**Two states only**: HIGH (5V) or LOW (0V)

</div>

- Like a light switch: ON or OFF
- Arduino digital pins (0-13)
- Perfect for: LEDs, buttons, relays, on/off control
- **Example**: `digitalWrite(13, HIGH)` → Pin 13 = 5V

---

### Analog Signals
<div class="box">

**Range of values**: 0V to 5V (continuous)

</div>

- Like a dimmer switch: infinite positions
- Arduino analog inputs (A0-A5) read 0-1023 values
  - 0 = 0V, 1023 = 5V, 512 ≈ 2.5V
- Perfect for: distance sensors, light sensors, temperature
- **Example**: `analogRead(A0)` → returns value 0-1023

---

## Pulse Width Modulation (PWM)

<div class="box">

**Problem**: Arduino digital pins are only HIGH or LOW  
**Question**: How do we get "in-between" voltages?

</div>

**Answer**: PWM = rapidly switching between HIGH and LOW!

---

### How PWM Works

**Pulse Width Modulation** = varying the **duty cycle**

- Switch HIGH/LOW very fast (490-980 Hz)
- **Duty Cycle** = % of time signal is HIGH
- Motor "sees" the average voltage

**Examples**:
- 25% duty cycle ≈ 1.25V average
- 50% duty cycle ≈ 2.5V average
- 75% duty cycle ≈ 3.75V average
- 100% duty cycle = 5V (always HIGH)

---

### PWM on Arduino

**PWM pins** (marked with ~): 3, 5, 6, 9, 10, 11

```cpp
analogWrite(9, 0);    // 0% duty cycle = 0V (motor stopped)
analogWrite(9, 64);   // 25% duty cycle = 1.25V (slow)
analogWrite(9, 128);  // 50% duty cycle = 2.5V (medium)
analogWrite(9, 191);  // 75% duty cycle = 3.75V (fast)
analogWrite(9, 255);  // 100% duty cycle = 5V (full speed)
```

<div class="highlight">

PWM values: 0-255 (not 0-1023 like analogRead!)

</div>

---

### Why PWM for Motors?

✅ **Efficient**: Transistors fully ON or OFF (minimal heat)  
✅ **Simple**: No complex voltage regulation needed  
✅ **Precise**: 256 speed levels (0-255)  
✅ **Works with digital pins**: No true analog output needed

<div class="box">

**Key Insight**: Motor inertia smooths out the rapid pulses, so it "feels" like a steady lower voltage!

</div>

---

## Battery Voltage: 4 AA Batteries

<div class="box">

**Question**: Yellow DC motor kit comes with 4 AA battery holder. What voltage is this?

</div>

**Answer**: <span class="highlight">6 volts</span>

---

### How Do We Know?

**Step 1**: Check battery specifications
- Standard AA alkaline battery = **1.5V** nominal
- Rechargeable NiMH AA = **1.2V** nominal

**Step 2**: Batteries in series **add** voltages
- 4 batteries × 1.5V each = **6V total**
- (Or 4 × 1.2V = 4.8V for rechargeable)

---

### Series vs. Parallel Batteries

**Series** (end-to-end): <span class="highlight">Voltages ADD</span>
- (+) → Battery 1 → Battery 2 → Battery 3 → Battery 4 → (−)
- Total: 1.5V + 1.5V + 1.5V + 1.5V = 6V
- Capacity stays same (e.g., 2000 mAh)

**Parallel** (side-by-side): <span class="highlight">Capacity ADDS</span>
- All (+) terminals connected, all (−) connected
- Voltage stays 1.5V
- Capacity: 2000 + 2000 + 2000 + 2000 = 8000 mAh

---

### Battery Voltage Over Time

<div class="small">

| Battery State | Alkaline AA | Your 4× AA Pack |
|---------------|-------------|------------------|
| **Fresh**     | 1.5V - 1.6V | 6.0V - 6.4V     |
| **Nominal**   | 1.5V        | 6.0V            |
| **50% used**  | 1.3V        | 5.2V            |
| **Depleted**  | 1.0V        | 4.0V            |

</div>

⚠️ **Motors slow down as batteries drain!**

---

## Why We Need Motor Drivers

<div class="box">

**Critical Problem**: Arduino pins cannot directly power motors!

</div>

---

### Arduino Pin Limitations

**Arduino digital pin specifications**:
- Max current per pin: <span class="highlight">40 mA</span>
- Recommended current: <span class="highlight">20 mA</span>
- Max voltage: 5V

**Your yellow DC motor requirements**:
- Operating current: <span class="highlight">150-300 mA</span>
- Stall current: <span class="highlight">1-2 A</span> (when blocked)
- Voltage: 3-6V

<div class="highlight">

Motor draws 10× more current than Arduino can provide!

</div>

---

### What Happens Without a Driver?

❌ **Scenario 1**: Connect motor directly to Arduino pin
- Arduino pin tries to supply 150+ mA
- Pin is rated for only 20-40 mA
- **Result**: <span class="highlight">Damaged Arduino!</span> (burned pin or entire chip)

❌ **Scenario 2**: Motor stalls (gets stuck)
- Current spikes to 1-2 A
- **Result**: <span class="highlight">Permanent damage to Arduino!</span>

---

### Motor Driver to the Rescue!

<div class="box">

**Motor Driver** = Power transistor bridge controlled by low-current signals

</div>

**How it works**:
1. Arduino sends LOW-CURRENT control signals (< 20 mA)
2. Motor driver switches HIGH-CURRENT from battery (1-2 A)
3. Motor gets power from battery, NOT Arduino
4. Arduino stays safe!

---

### Motor Driver Functions

✅ **Current amplification**: Arduino controls, battery powers  
✅ **Direction control**: H-bridge reverses current flow  
✅ **Speed control**: PWM from Arduino → PWM to motor  
✅ **Protection**: Some drivers have overcurrent protection  
✅ **Isolation**: Keeps motor noise away from Arduino

<div class="box">

**Analogy**: Motor driver is like a remote-controlled power switch that can handle heavy loads

</div>

---

### Breadboard Basics
![Breadboard](/img/breadboard.png)

- **Solderless prototyping** platform
- **Horizontal rows:** Connected internally (for components)
- **Vertical rails:** Connected vertically (for power/ground distribution)
- **Red rail:** Typically connected to positive voltage (5V)
- **Blue/Black rail:** Typically connected to ground (GND)
- **Center gap:** Separates two sides, perfect for ICs

---

## DC Motors for Project 1

### Yellow Geared DC Motors
- **Type:** Brushed DC motor with gear reduction
- **Voltage:** Typically 3-6V (perfect for 4× AA = 6V!)
- **Application:** Wheeled robot car (differential drive)
- **Power:** Comes with 4× AA battery holder (6V, ~2000 mAh)
- **Characteristics:**
  - High speed reduced by internal gears
  - Increased torque for moving robot weight
  - Simple two-wire control (polarity determines direction)
  - Current draw: 150-300 mA running, 1-2A stall

---

### Motor Driver: L298N
- **Purpose:** Controls motor speed and direction
- **H-Bridge configuration:** Allows bidirectional control
- **Specifications:**
  - Drives 2 DC motors independently
  - Up to 2A per channel
  - Logic voltage: 5V (from Arduino)
  - Motor voltage: 5-35V (from battery)
- **Control:**
  - IN1/IN2 pins control Motor A direction
  - IN3/IN4 pins control Motor B direction
  - ENA/ENB pins control speed (PWM)

---

### Alternative Motor Drivers

**TB6612FNG:**
- More efficient than L298N
- Lower voltage drop
- Up to 1.2A per channel
- Better for smaller motors

**WWZMDiB Motor Driver:**
- Compact design
- Integrated motor control
- Good for space-constrained projects

*You may use any of these drivers for Project 1!*

---

## Types of Electric Motors

### Brushed DC Motors
- **Mechanism:** Commutator switches current direction via brushes
- **Advantages:**
  - Simple control (voltage → speed)
  - Inexpensive
  - Wide availability
- **Disadvantages:**
  - Brush wear over time
  - Lower efficiency due to friction
  - Maintenance required

---

### Brushless DC Motors
- **Mechanism:** Electronic commutation (no brushes)
- **Advantages:**
  - Higher efficiency
  - Longer lifespan
  - More torque per weight
  - Less maintenance
- **Disadvantages:**
  - Requires electronic speed controller (ESC)
  - More expensive
  - Complex control
- **Applications:** Drones, RC cars, industrial robots

---

### Stepper Motors
- **Mechanism:** Precise rotation in fixed steps (e.g., 1.8° per step)
- **Advantages:**
  - Precise position control without encoder
  - Hold position when powered
  - Predictable movement
- **Disadvantages:**
  - Lower top speed
  - Can lose steps under high load
  - Requires specific driver
- **Applications:** 3D printers, CNC machines, robotic arms

---

### Servo Motors
- **Components:** DC motor + gears + encoder + controller
- **Types:**
  - **Standard:** 0-180° rotation
  - **Continuous:** 360° rotation with speed control
  - **Digital:** Faster response, more torque
- **Advantages:**
  - Built-in position control
  - Easy to use (single signal wire)
  - Compact package
- **Applications:** RC vehicles, robotic arms, grippers

---

## Other Actuation Technologies

### Hydraulic Actuators
- **Mechanism:** Pressurized liquid in pistons
- **Advantages:** Very high force
- **Disadvantages:** Large, expensive, maintenance-intensive
- **Applications:** Construction equipment, large legged robots

### Pneumatic Actuators
- **Mechanism:** Compressed air
- **Advantages:** Lightweight, safe, compliant
- **Disadvantages:** Lower force than hydraulics
- **Applications:** Soft robotics, grippers, robotic fish

---

## Motor Control Considerations

### Speed Control
- **PWM (Pulse Width Modulation):** (as we discussed earlier!)
  - Rapidly switch motor on/off
  - Duty cycle determines average voltage
  - Higher duty cycle = faster speed
  - Arduino `analogWrite()` function (0-255)
  - Use PWM pins: 3, 5, 6, 9, 10, 11

### Direction Control
- **H-Bridge circuit:**
  - Four switches control current flow
  - Forward: Current flows one direction
  - Reverse: Current flows opposite direction
  - Brake: Short both motor terminals to ground

---

## Safety Considerations

### Active Safety
- **Torque limiting:** Monitor motor current
- **Collision detection:** Compare expected vs actual torque
- **Emergency stop:** Cut power immediately

### Passive Safety
- **Mechanical limits:** Physical stops on motion
- **Compliant mechanisms:** Springs, flexible materials
- **Fail-safe brakes:** Engage when power lost
- **Current limiting:** Fuses and circuit breakers

---

## Motor Selection Criteria

**For your wheeled robot, consider:**
1. **Torque:** Can it move your robot's weight?
2. **Speed:** How fast should it go?
3. **Voltage:** Match your power supply (typically 5-6V)
4. **Current:** Does your driver/battery support it?
5. **Size/Weight:** Fits your chassis design
6. **Cost:** Within project budget

---

## Next Steps for Project 1

1. **This week:** Mechanical build, wiring, power setup
2. **Install fresh batteries** (4× AA = 6V)
3. **Test motors individually** before mounting
4. **Verify motor driver connections** (common mistake: reversed polarity)
5. **Start with low PWM values** (50-100) to test safely
6. **Check battery voltage** regularly (should read ~6V when fresh)
7. **Document your wiring** (take photos!)

**Check-in:** Come to lab hours if motors aren't spinning!

---

## Key Takeaways

- **Digital** = ON/OFF; **Analog** = range of values; **PWM** = fake analog using fast switching
- **4× AA batteries in series** = 6V (1.5V each)
- Arduino pins (20-40 mA) **cannot** power motors (150-300 mA) directly
- **Motor drivers** amplify control signals and protect Arduino
- **DC motors** offer simple speed control via PWM (0-255)
- Different motor types trade off **precision**, **force**, **speed**, and **cost**

**Questions?**
