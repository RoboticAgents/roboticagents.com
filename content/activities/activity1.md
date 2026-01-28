+++
title = "Activity 1: Servo Motor Control"
description = "Hands-on Arduino servo motor control demonstration"
weight = 1
+++

## Overview

In this activity, you will demonstrate your ability to wire and control a **servo motor** using an Arduino Uno. You'll start by using Arduino's built-in Sweep example, then modify the code to create your own custom movement pattern. This is an individual demonstration activity where you'll show your understanding of motor control, circuit wiring, and Arduino programming.

**Due Date: January 28th by 11:50 AM**

---

## Learning Objectives

By completing this activity, you will:
- Learn proper wiring techniques for servo motor control
- Use Arduino's built-in Servo library and examples
- Modify existing code to create custom servo movements
- Demonstrate safe handling of electronic components

---

## Requirements

### What You Must Demonstrate

1. **Correct wiring** of servo motor to the Arduino Uno
2. **Run the built-in Sweep example** successfully
3. **Modify the Sweep code** to create a different movement pattern
4. **Explain** what your modified code does
5. **Safe operation** (no loose wires, proper power connections)

---

## Grading Criteria

This is a **Class Activity** worth points toward your participation grade.

**Grading Rubric** (Pass/Fail with feedback):

| Criterion | Points | Description |
|:----------|:------:|:------------|
| **Sweep Example Working** | 30% | Built-in Sweep example runs successfully; servo moves smoothly |
| **Code Modification** | 30% | Created a different movement pattern; code is functional |
| **Wiring** | 20% | Servo correctly connected; proper power and ground connections; neat wiring |
| **Explanation** | 20% | Can explain what your modified code does; answers instructor questions |

**To Pass**: You must achieve at least 70% overall. Incomplete wiring or non-functional code will require you to debug and re-demonstrate.

---

## Part 1: Understanding Servo Motors

### What is a Servo Motor?

A **servo motor** is a motor with built-in position control. It can rotate to a specific angle (typically 0-180°) and hold that position. Servos are perfect for:
- Robot arms and grippers
- Camera pan/tilt mechanisms
- RC vehicles (steering)

**Key Features**:
- Built-in controller and gears
- 3-wire connection (Power, Ground, Signal)
- Precise angular positioning
- Easy to control with Arduino

---

## Part 2: Wiring Your Servo

### Components Needed:
- Arduino Uno
- Standard servo motor (e.g., SG90, TowerPro MG996R)
- 3 jumper wires
- USB cable

### Wiring Instructions:

**Servo Motor Wire Colors (standard)**:
- **BROWN/BLACK** wire  →  GND (Arduino)
- **RED** wire  →  5V (Arduino)
- **ORANGE/YELLOW/WHITE** wire  →  Pin 9 (Arduino)

**⚠️ Important**: Wire colors may vary by manufacturer, but the pattern is typically: signal-power-ground or ground-power-signal.

---

### Wiring Diagram:

```
Arduino Uno          Servo Motor
┌─────────────┐          ┌──────────┐
│             │          │  Servo   │
│         5V  ●──RED─────┤  +5V     │
│        GND  ●──BROWN───┤  GND     │
│             │          │          │
│   Pin 9 (PWM)├─ORANGE──┤  Signal  │
│             │          │          │
└─────────────┘          └──────────┘
```

**Visual Connection**:
```
        Arduino Uno
    ┌─────────────────┐
    │ [ ]          5V  ●───────┐
    │ [ ]         GND  ●───┐   │
    │ [ ]          13  [ ]  │   │
    │ [ ]          12  [ ]  │   │
    │ [ ]          11~ [ ]  │   │
    │ [ ]          10~ [ ]  │   │
    │ [ ]           9~ ●─┐  │   │
    │ [ ]           8  [ ] │  │   │
    └─────────────────┘    │  │   │
                          │  │   │
                    ORANGE  │  │   │
                       ┌────┘  │   │
                       │  BROWN │   │
                       │  ┌─────┘   │
                       │  │    RED  │
                       │  │  ┌──────┘
                    ┌──┴──┴──┴───┐
                    │  SERVO     │
                    │  MOTOR     │
                    └────────────┘
```

**Connection Checklist**:
- [ ] Brown/Black wire connected to GND
- [ ] Red wire connected to 5V
- [ ] Orange/Yellow/White wire connected to Pin 9
- [ ] All connections are secure
- [ ] No wires are touching each other

---

## Part 3: Running the Sweep Example

### Step 1: Open the Built-in Example

1. Connect your Arduino to your computer via USB
2. Open Arduino IDE
3. Go to: **File → Examples → Servo → Sweep**
4. A new window will open with the Sweep example code

### Step 2: Upload and Test

1. Select your Arduino board: **Tools → Board → Arduino Uno**
2. Select your port: **Tools → Port → [your Arduino port]**
3. Click the **Upload** button (→)
4. Watch your servo sweep back and forth!

**What the Sweep Example Does**:
- Moves the servo from 0° to 180° gradually
- Pauses briefly at 180°
- Moves back from 180° to 0°
- Repeats continuously

### Step 3: Verify It Works

✅ Your servo should smoothly sweep back and forth  
✅ The movement should be continuous  
✅ No error messages in the Arduino IDE

If it doesn't work, see the **Troubleshooting** section at the end of this document.

---

## Part 4: Modify the Code

Now that you have the Sweep example working, **modify it** to create a different movement pattern. Here are some ideas:

### Modification Ideas:

1. **Different Angles**: Make it sweep between different angles (e.g., 45° to 135° instead of 0° to 180°)
2. **Different Speed**: Change the delay to make it move faster or slower
3. **Multiple Positions**: Make it move to 3-4 specific positions instead of sweeping continuously
4. **Back-and-forth**: Make it go to 90°, back to 0°, to 180°, back to 0°, repeat
5. **Your Own Pattern**: Create any unique movement pattern you want!

### Requirements for Your Modification:

- Must be **different** from the original Sweep example
- Must be **functional** (code compiles and runs without errors)
- Must create **visible movement** in the servo
- Should demonstrate your understanding of servo control

### Example Modification Ideas in Words:

**Example 1**: "Move to 0°, wait 1 second, move to 90°, wait 1 second, move to 180°, wait 1 second, repeat"

**Example 2**: "Sweep from 30° to 150° faster than the original, then pause for 2 seconds"

**Example 3**: "Move to center (90°), sweep left to 0°, back to center, sweep right to 180°, back to center, repeat"

---

## Part 5: Demonstration

### When & Where
- In class, on Monday, January 26th or during lab, on Tuesday, January 27th, demonstrate your servo functionality to the instructor.

---

## Troubleshooting

### Servo Issues

| Problem | Possible Cause | Solution |
|:--------|:--------------|:---------|
| Servo doesn't move at all | Wrong pin or loose wire | Verify Pin 9 is used; check all connections |
| Servo jitters/vibrates | Insufficient power | Try external 5V supply for high-torque servos |
| Servo moves erratically | Loose connections | Secure all jumper wires firmly |
| Code won't compile | Library issue | Servo library is built-in; restart Arduino IDE |
| Servo moves but not correctly | Code issue | Check your angle values (must be 0-180) |

### Common Code Issues

- **`myservo.write(angle)`**: Make sure `angle` is between 0 and 180
- **`delay(ms)`**: Time is in milliseconds (1000 ms = 1 second)
- **Forgetting to call `myservo.attach(9)`**: Must be in `setup()` function

---

## Additional Resources

### Arduino Documentation
- [Servo Library Reference](https://www.arduino.cc/reference/en/libraries/servo/)
- [Basic Servo Control Tutorial](https://docs.arduino.cc/tutorials/generic/basic-servo-control/)

### Safety Reminders
- Never connect motors directly to Arduino pins without understanding power requirements
- Always double-check power and ground connections before plugging in USB
- If a servo gets hot, disconnect immediately and check your wiring
- Don't force servos by hand when powered - you can damage internal gears

---

## Learning Outcomes Alignment

This activity supports the following course learning outcomes:
- **LO2**: Demonstrate proficiency in programming robotic systems
- **LO3**: Apply fundamental concepts of sensors and actuators
- **LO4**: Design, build, and test robotic systems
