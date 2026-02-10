+++
title = "Exam 1 Review"
description = "Review for Exam 1 covering locomotion, kinematics, actuators, and sensors"
weight = 4
draft = true
+++

This content is available as an HTML slide deck at [/slides/exam1review.html](/slides/exam1review.html).

The slides cover:
- Exam format and what's covered
- Multiple Choice Practice Questions (5)
  - Static vs. dynamic stability
  - PWM and motor control
  - Arduino current limitations
  - Degrees of freedom
  - Sensor types
- Short Answer Practice Questions (5)
  - Parameter sharing in wheels
  - H-bridge explanation
  - Proprioceptive vs. exteroceptive sensors
  - Battery configurations
  - Accuracy vs. precision
- Scenario-Based Practice Questions (5)
  - Motor troubleshooting
  - Wheel configuration selection
  - Sensor selection for different tasks
  - Environmental sensor challenges
- Key concepts review
- Exam tips and common mistakes

[View the full presentation →](/slides/exam1review.html)

---

## Study Materials

- **Project 1:** Wheeled Robot documentation and code
- **Slides:**
  - Locomotion
  - Motors and Arduino
  - Sensors
- **Activities:**
  - Activity 1: Servo Motor Control
  - Activity 2: Distance Sensors
  - Activity 3: Environmental Sensors
- **Readings:** IAR Chapters 1, 2, 6, 7

---

# MULTIPLE CHOICE QUESTIONS

---

## Multiple Choice Practice 1

**What type of stability requires constant motion to avoid falling?**

A. Static stability

B. Dynamic stability

C. Kinematic stability

D. Passive stability

<div class="small">

*First hand up gets to answer!*

</div>

---

### Answer: B. Dynamic stability

<div class="box">

**Dynamic stability** requires the robot to be constantly in motion to remain upright.

**Examples:**
- Bicycle (must keep moving to stay balanced)
- Two-wheeled segway
- Running animals

**Static stability** means stable when NOT moving (e.g., four-legged table, wheeled robot with caster wheel).

</div>

---

## Multiple Choice Practice 2

**What is the purpose of PWM (Pulse Width Modulation) in motor control?**

A. To protect the Arduino from overcurrent

B. To vary motor speed by changing the duty cycle

C. To reverse motor direction

D. To measure motor position

---

### Answer: B. To vary motor speed by changing the duty cycle

<div class="box">

**PWM** rapidly switches between HIGH (5V) and LOW (0V) signals.

**Duty cycle** = percentage of time signal is HIGH
- 25% duty cycle ≈ 1.25V average → slow motor
- 50% duty cycle ≈ 2.5V average → medium speed
- 100% duty cycle = 5V → full speed

The motor's inertia smooths out the pulses, so it "feels" like a steady voltage.

</div>

---

## Multiple Choice Practice 3

**Why can't an Arduino digital pin power a DC motor directly?**

A. The pin voltage is too high

B. The pin cannot supply enough current

C. The pin cannot control motor direction

D. Arduino pins only support digital signals

---

### Answer: B. The pin cannot supply enough current

<div class="box">

**Arduino pin specifications:**
- Max current: 40 mA
- Recommended: 20 mA

**DC motor requirements:**
- Running current: 150-300 mA
- Stall current: 1-2 A

Motor draws **10× more current** than Arduino can provide!

**Solution:** Use a motor driver (H-bridge) to amplify current

</div>

---

## Multiple Choice Practice 4

**How many Cartesian degrees of freedom (DoF) does a robot have when moving on a flat plane?**

A. 2 DoF (X, Y position)

B. 3 DoF (X, Y position, orientation θ)

C. 4 DoF (X, Y, Z position, orientation)

D. 6 DoF (full 3D position and orientation)

---

### Answer: B. 3 DoF (X, Y position, orientation θ)

<div class="box">

**On a 2D plane**, a robot can move:
1. **X position** (left/right)
2. **Y position** (forward/backward)
3. **Orientation θ** (rotation angle)

**In 3D space**, you'd have 6 DoF:
- 3 translations (X, Y, Z)
- 3 rotations (pitch, yaw, roll)

</div>

---

## Multiple Choice Practice 5

**Which sensor uses sound waves to measure distance?**

A. Infrared (IR) sensor

B. Ultrasonic sensor (HC-SR04)

C. Photoresistor

D. Temperature sensor (TMP36)

---

### Answer: B. Ultrasonic sensor (HC-SR04)

<div class="box">

**Ultrasonic sensor (HC-SR04):**
- Emits 40 kHz sound pulse
- Measures time for echo to return
- Calculates distance: `distance = (time × speed_of_sound) / 2`
- Range: 2-400 cm

**IR sensor:** Uses infrared light (not sound)

</div>

---

# SHORT ANSWER QUESTIONS

---

## Short Answer Practice 1

**Explain how parameter sharing in wheels reduces complexity compared to individually actuated legs.**

<div class="small">

*First hand up gets to answer!*

</div>

---

### Sample Answer

<div class="box small">

In wheeled locomotion, **two motors** can control an entire robot (e.g., differential drive), whereas legged robots require **multiple motors per leg** (typically 2-3 DoF per leg × 4-6 legs = 8-18 motors).

**Advantages of wheels:**
- Fewer motors = lower cost, weight, power consumption
- Simpler control algorithms
- No need to coordinate gait timing
- Mechanically simpler (continuous rolling contact)

**Trade-off:** Wheels are limited to flat terrain, while legs can navigate rough terrain.

</div>

---

## Short Answer Practice 2

**What is an H-bridge and why is it necessary for motor direction control?**

---

### Sample Answer

<div class="box small">

An **H-bridge** is a circuit configuration of four switches (transistors) that allows **bidirectional current flow** through a DC motor.

**How it works:**
- **Forward direction:** Current flows left-to-right through motor
- **Reverse direction:** Current flows right-to-left through motor
- **Brake:** Both motor terminals connected to ground

**Why necessary:**
DC motors change direction based on current polarity. Without an H-bridge, you'd need to physically swap wires to reverse direction.

**Where you've used it:** L298N motor driver, TB6612FNG motor driver

</div>

---

## Short Answer Practice 3

**Describe the difference between proprioceptive and exteroceptive sensors, and give one example of each.**

---

### Sample Answer

<div class="box small">

**Proprioceptive sensors:** Measure the robot's **internal state**
- Sense the robot itself
- Examples: wheel encoders (measure rotation), accelerometer (measure tilt/acceleration), gyroscope (measure rotation rate), motor current sensors

**Exteroceptive sensors:** Measure the **external environment**
- Sense things outside the robot
- Examples: ultrasonic distance sensor (HC-SR04), IR obstacle sensor, camera, temperature sensor, light sensor

**Why the distinction matters:** Robots need both to function autonomously!
- Proprioceptive → "Where am I? How fast am I moving?"
- Exteroceptive → "What's around me? Where are obstacles?"

</div>

---

## Short Answer Practice 4

**Explain the relationship between battery configuration (series vs. parallel) and voltage/capacity.**

---

### Sample Answer

<div class="box small">

**Series connection** (end-to-end):
- **Voltages ADD**: 4× 1.5V AA batteries = 6V total
- **Capacity stays same**: Still 2000 mAh
- Used when you need higher voltage

**Parallel connection** (side-by-side):
- **Voltage stays same**: Still 1.5V
- **Capacities ADD**: 4× 2000 mAh = 8000 mAh total
- Used when you need longer runtime at same voltage

**Project 1 example:** 4× AA battery holder is wired in **series** → 6V to power motors

</div>

---

## Short Answer Practice 5

**What are the key differences between accuracy and precision in sensor measurements?**

---

### Sample Answer

<div class="box small">

**Accuracy:** How **close** measurements are to the **true value**
- If your ultrasonic sensor reads 10 cm when an object is actually at 10 cm → accurate
- If it reads 15 cm when object is at 10 cm → inaccurate

**Precision:** How **consistent** measurements are when repeated
- If sensor reads 10.1, 10.0, 10.2, 10.1 cm → high precision (consistent)
- If sensor reads 8, 15, 11, 13 cm → low precision (inconsistent)

**Best case:** High accuracy AND high precision

**Reality:** IR sensors are often precise but not accurate; ultrasonic sensors can be accurate but less precise

</div>

---

# SCENARIO-BASED QUESTIONS

---

## Scenario Practice 1

**Your wheeled robot moves forward when both motors are powered, but when you try to turn left, the robot barely moves and the left motor gets hot.**

**Identify two potential causes and explain how you would diagnose them.**

<div class="small">

*First hand up gets to answer!*

</div>

---

### Sample Answer

<div class="box small">

**Potential Cause 1: Wiring issue (reversed polarity)**
- **Diagnosis:** Check that left motor wires are connected correctly to motor driver (IN1/IN2)
- **Test:** Swap IN1/IN2 connections and see if behavior changes
- **Fix:** Rewire motor to correct terminals

**Potential Cause 2: Software bug (incorrect PWM values)**
- **Diagnosis:** Print motor speed values to Serial Monitor during turn
- **Test:** Check if left motor PWM is too low or negative
- **Fix:** Adjust turn logic in code: `leftSpeed = baseSpeed - turnAmount;`

**Why motor gets hot:** If motor is receiving power but can't turn (due to incorrect signal or mechanical binding), current increases → heat

</div>

---

## Scenario Practice 2

**You're designing a robot to navigate a warehouse with narrow aisles and must make tight turns. Should you use:**

**A. Differential drive (two powered wheels)**

**B. Car-like steering (Ackermann)**

**C. Mecanum wheels**

**Explain your choice.**

---

### Sample Answer

<div class="box small">

**Best choice: A. Differential drive** (or C. Mecanum wheels)

**Differential drive advantages:**
- Can **rotate in place** (zero turning radius)
- Simple control (two motors)
- Low cost
- Perfect for tight spaces

**Car-like steering (Ackermann):**
- ❌ Cannot turn in place (needs wide turning radius)
- ❌ More complex mechanically
- ❌ Harder to control
- Only good for outdoor robots at high speeds

**Mecanum wheels:**
- ✓ Can move sideways AND rotate in place
- ❌ More expensive (4 motors + special wheels)
- ✓ Best maneuverability if budget allows

</div>

---

## Scenario Practice 3

**Your robot needs to detect transparent glass walls in a building. You have ultrasonic (HC-SR04) and IR sensors available. Which should you use and why?**

---

### Sample Answer

<div class="box small">

**Best choice: Ultrasonic sensor (HC-SR04)**

**Why ultrasonic is better:**
- ✓ Sound waves **reflect off glass** surfaces
- ✓ Works with transparent/translucent materials
- ✓ Not affected by surface color or texture
- ✓ Reliable for flat surfaces like walls

**Why IR fails:**
- ❌ Infrared light **passes through** glass (transparent to IR)
- ❌ May not detect glass walls at all
- ❌ Dark surfaces absorb IR → poor detection

**Limitation to consider:** Angled glass may reflect sound away → might not detect at steep angles

</div>

---

## Scenario Practice 4

**You're building a line-following robot that must detect black tape on a white floor. Which sensor type is most appropriate?**

**A. Ultrasonic distance sensor**

**B. Temperature sensor (TMP36)**

**C. IR reflectance sensor**

**D. Photoresistor**

**Explain your reasoning.**

---

### Sample Answer

<div class="box small">

**Best choice: C. IR reflectance sensor** (or D. Photoresistor with proper setup)

**Why IR reflectance sensor:**
- ✓ Detects **surface color** by measuring reflected light
- ✓ White surface → high reflectance → high sensor reading
- ✓ Black tape → low reflectance → low sensor reading
- ✓ Fast response time for real-time control
- ✓ Works at close range (1-3 cm)

**Why other sensors fail:**
- Ultrasonic: Measures distance, not color
- Temperature sensor: Floor and tape are same temperature
- Photoresistor alone: Could work but needs controlled lighting; less precise than IR sensor

</div>

---

## Scenario Practice 5

**Your robot's ultrasonic sensor works perfectly indoors but gives erratic readings outdoors on a sunny day. What's likely happening and how would you address it?**

---

### Sample Answer

<div class="box small">

**Likely cause: Temperature/environmental interference**

**Explanation:**
- Speed of sound changes with temperature (faster when hot)
- HC-SR04 assumes constant speed → errors in hot weather
- Wind can deflect sound waves
- Soft surfaces (grass, dirt) absorb sound → weaker echo
- Temperature formula: `speed = 331.4 + (0.6 × temperature_C)` m/s

**Solutions:**
1. **Calibrate for temperature:** Add temperature sensor (TMP36) and adjust calculation
2. **Use multiple measurements:** Average 5-10 readings to reduce noise
3. **Switch sensor type:** Use IR sensor or camera for outdoor use
4. **Shield sensor:** Add physical barrier to reduce wind interference

</div>

---

## Key Concepts Review

<div class="box small">

**Locomotion:**
- Static vs. dynamic stability
- Degrees of Freedom (DoF)
- Wheel types and constraints

**Actuators:**
- Motor types (DC, servo, stepper, brushless)
- H-bridge for direction control
- PWM for speed control

**Arduino:**
- Digital vs. analog signals
- PWM pins (3, 5, 6, 9, 10, 11)
- Current limitations (20-40 mA per pin)

**Sensors:**
- Proprioceptive vs. exteroceptive
- Ultrasonic (sound-based, 2-400 cm)
- IR (light-based, affected by color/material)
- Accuracy vs. precision
- Range, resolution, response time

</div>

---

## General Exam Tips

✓ **Understand WHY**, not just memorize facts

✓ **Draw diagrams** if helpful (circuit diagrams, DoF illustrations)

✓ **Show your reasoning** in short-answer and scenario questions

✓ **Refer to Project 1** experiences in scenario questions

✓ **Budget time:** Don't spend too long on one question

✓ **Check units** in calculations (volts, amps, centimeters, degrees)

---

## Practice Resources

**Review:**
- Your Project 1 code and documentation
- All class slides (locomotion, motors, sensors)
- Activity code (servo, ultrasonic, IR, environmental sensors)
- IAR textbook chapters

**Test yourself:**
- Can you explain each concept to a classmate?
- Can you wire a circuit from memory?
- Can you debug a motor control circuit?
- Can you choose appropriate sensors for different tasks?

---

## Common Mistakes to Avoid

❌ Confusing static and dynamic stability

❌ Thinking Arduino pins can power motors directly

❌ Mixing up PWM range (0-255) with analogRead range (0-1023)

❌ Not considering sensor limitations (glass + IR, soft surfaces + ultrasonic)

❌ Forgetting about battery series/parallel voltage rules

❌ Confusing mechanical DoF with Cartesian DoF

---

## Questions?

**Review sessions:** Check Discord for study group times

**Office hours:** See [instructor schedule](https://janyljumadinova.com/schedule)

**Day before exam:** Final Q&A in class

<div class="box">

**Good luck on Exam 1!**

Remember: This exam tests your understanding of fundamental robotics concepts that you've **built and programmed** in Project 1.

</div>
