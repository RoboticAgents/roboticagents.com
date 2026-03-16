+++
title = "Exam 2 Review"
description = "Review for Exam 2 covering PLCs and collaborative robots"
weight = 5
+++

This content is available as an HTML slide deck at [/slides/exam2review.html](/slides/exam2review.html).

The slides cover:
- Exam format and what's covered
- Multiple Choice Practice Questions (5)
  - PLC input/output devices
  - Relay function and purpose
  - Ladder logic evaluation
  - Collaborative robot safety
  - Motion types (Joint vs. Linear)
- Short Answer Practice Questions (5)
  - Latching circuits
  - Timer logic
  - Teach mode vs. production mode
  - Gripper operation
  - Deterministic vs. reactive control
- Scenario-Based Practice Questions (5)
  - PLC troubleshooting
  - Ladder logic design
  - Robot cell safety scenario
  - Teach pendant navigation
  - Pick-and-place program design
- Key concepts review
- Exam tips and common mistakes

[View the full presentation →](/slides/exam2review.html)

---

## Study Materials

- **Project 2:** PLC documentation, condition tables, and reflection
- **Project 3:** FANUC CRX documentation and reflection
- **Slides:**
  - PLC Slides
  - Collaborative Robots Slides
- **Readings:** PLC Guidebook Parts II & III

---

# MULTIPLE CHOICE QUESTIONS

---

## Multiple Choice Practice 1

**Which of the following is an INPUT device on a PLC training system?**

A. Indicator lamp

B. Motor contactor

C. Limit switch

D. Ice cube relay coil

<div class="small">

*First hand up gets to answer!*

</div>

---

### Answer: C. Limit switch

<div class="box">

**Input devices** supply a voltage signal TO the PLC — they are sensing/triggering devices.

**Examples of inputs:**
- Limit switches
- Push buttons
- Sensors (IR, proximity)

**Output devices** receive a signal FROM the PLC — they do work.
- Indicator lamps
- Motor contactors
- Relay coils
- Solenoids

</div>

---

## Multiple Choice Practice 2

**What is the primary purpose of an ice cube relay in a PLC control system?**

A. To measure current flowing through the circuit

B. To isolate and amplify a PLC output signal to drive a higher-power load

C. To convert AC power to DC power

D. To store the PLC program when power is lost

---

### Answer: B. To isolate and amplify a PLC output signal to drive a higher-power load

<div class="box">

**Ice cube relay** acts as an electrically-operated switch:
- A low-power PLC signal energizes the relay **coil**
- The coil closes the relay **contacts**, which switch a higher-power circuit

**Why isolation matters:**
- Keeps PLC control voltage (24 VDC) separate from load voltage (e.g., 120 VAC)
- Protects the PLC from voltage spikes and shorts

**Transparent housing** allows visual inspection of contact state.

</div>

---

## Multiple Choice Practice 3

**In a PLC ladder logic rung, what condition must be true for the output coil to energize?**

A. Any one input contact on the rung must be closed (NO)

B. All series contacts on the path to the coil must be closed

C. The coil must be connected directly to the power rail

D. At least one normally-closed (NC) contact must be open

---

### Answer: B. All series contacts on the path to the coil must be closed

<div class="box">

**Ladder logic** reads like an electrical circuit:
- **Left rail** = power supply (+)
- **Right rail** = return (−)
- **Rung** = path from left to right rail

**Series contacts (AND logic):** ALL must be closed for power to reach the coil.

**Parallel contacts (OR logic):** ANY one closed path is enough.

The coil energizes when there is a **complete circuit path** from left to right rail.

</div>

---

## Multiple Choice Practice 4

**What must a FANUC CRX operator do BEFORE entering the robot's work cell during automatic operation?**

A. Reduce the override speed to 10%

B. Never enter — stop the robot before entering the work cell

C. Enable free-hand teaching mode

D. Switch from Production Mode to Teach Mode on the pendant

---

### Answer: B. Never enter — stop the robot before entering the work cell

<div class="box">

**FANUC CRX safety rules:**
- ❌ **NEVER** allow others to enter the work cell during automatic operation
- ❌ **NEVER** assume a motionless robot is safe (it may be waiting to move)
- ✓ **ALWAYS** stop the robot before entering
- ✓ **ALWAYS** have an escape plan
- ✓ **ALWAYS** know the complete task the robot is programmed to do

**Key principle:** Always assume the robot is running and using lethal power.

</div>

---

## Multiple Choice Practice 5

**When jogging the FANUC CRX in Cartesian (Cart) mode, which of the following is true?**

A. Each button moves one individual robot joint

B. The robot's tool tip moves along world coordinate axes (X, Y, Z)

C. The robot moves at its maximum programmed speed

D. The MPG dial controls payload weight

---

### Answer: B. The robot's tool tip moves along world coordinate axes (X, Y, Z)

<div class="box">

**Joint mode:** Each +J1 through +J6 button moves one individual joint independently.

**Cartesian (Cart) mode:** Moves the **tool tip (TCP)** along X, Y, Z linear axes and rotates around X, Y, Z.

**Why it matters:**
- Joint mode is useful for repositioning individual joints
- Cartesian mode is useful for precise positioning of the tool in space

**Override speed** in both modes must be ≤ 250 mm/s for safe operation.

</div>

---

# SHORT ANSWER QUESTIONS

---

## Short Answer Practice 1

**Explain how a latching circuit works in PLC ladder logic and why it is useful.**

<div class="small">

*First hand up gets to answer!*

</div>

---

### Sample Answer

<div class="box small">

A **latching circuit** (also called a seal-in circuit) allows an output to remain energized even after the input that triggered it is released.

**How it works:**
- A momentary input (e.g., push button) energizes the output coil
- A **normally-open contact of that same output** is wired in parallel with the input
- Once the output energizes, it "seals itself on" through its own contact
- A separate **stop input** (normally-closed contact in series) is used to break the latch

**Why it's useful:**
- Models real-world behavior: a motor should stay ON after you press start
- Avoids the need to hold a button continuously
- Mirrors industrial conveyor, pump, and motor control logic

</div>

---

## Short Answer Practice 2

**Describe how a TON (timer on-delay) works in PLC ladder logic and give a practical use case.**

---

### Sample Answer

<div class="box small">

A **TON (timer on-delay)** timer counts time while its enabling rung is continuously TRUE.

**How it works:**
1. Enabling rung goes TRUE → timer begins counting
2. When accumulated value reaches the preset value → timer output bit (DN) energizes
3. If the enabling rung goes FALSE before preset is reached → timer resets to zero

**Key parameters:**
- **Preset (PT):** Target time (e.g., 5 seconds)
- **Accumulated (ET):** Current elapsed time
- **Done bit (DN/Q):** Becomes TRUE when ET ≥ PT

**Practical use case:**
- Turn on a warning light 10 seconds after a machine starts
- Control a conveyor delay between stages
- In Project 2, Part 3: control a timed lamp sequence

</div>

---

## Short Answer Practice 3

**Explain the difference between Teach Mode and Production Mode on the FANUC CRX, and when you would use each.**

---

### Sample Answer

<div class="box small">

**Teach Mode:**
- Used for **programming and testing** robot positions and programs
- Operator holds the Tablet TP and can jog, touch up points, and step through programs
- Speed is limited (≤ 250 mm/s) for safety
- Robot can be stopped at any point during step execution
- Required when entering the work cell

**Production Mode:**
- Used for **running completed programs automatically**
- Higher speeds are permitted
- Operator should NOT be inside the work cell
- Programs run continuously using the Play menu (Run slider FWD)

**Key distinction:** In Teach Mode, the operator is in control step-by-step; in Production Mode, the robot runs autonomously and the work cell must be clear.

</div>

---

## Short Answer Practice 4

**Describe how the SCHUNK gripper (or OnRobot RG6) is commanded in a FANUC CRX program, including the key parameters.**

---

### Sample Answer

<div class="box small">

The gripper is controlled using a **Gripper 2 Point code block** within a Basic Pick/Place motion code block in the program timeline.

**Key parameters:**

- **Width:** Sets the jaw opening distance (in mm) — determines how wide the gripper opens or closes
- **Force:** Sets the gripping force in Newtons — prevents crushing delicate objects
- **Wait (YES/NO):** Whether the program waits for the gripper to reach the target width before continuing

**Two functions:**
1. **In program:** The code block opens or closes the gripper to the specified width at that step in the timeline
2. **Manual operation:** Hold the button to manually open/close jaws to test the grip width setting

**In pick-and-place:** gripper opens at approach, closes at pick position, opens again at place position.

</div>

---

## Short Answer Practice 5

**What is the difference between deterministic and reactive control, and which best describes PLC ladder logic?**

---

### Sample Answer

<div class="box small">

**Deterministic control:** The robot/system follows a **fixed, pre-planned sequence** of actions regardless of sensor feedback.
- Behavior is predictable and repeatable
- Works well in structured, controlled environments
- Example: PLC running a fixed conveyor sequence

**Reactive control:** The system **responds dynamically** to sensor input in real time.
- Behavior depends on current environment state
- Works well in unstructured or variable environments
- Example: robot stopping when an obstacle is detected

**PLC ladder logic is primarily deterministic:**
- Programs execute rungs in a fixed scan cycle
- Outputs are determined by the current input state combinations
- The logic is pre-programmed and predictable

**However**, PLCs can incorporate sensor inputs (limit switches, proximity sensors) to make conditional decisions — blending deterministic structure with reactive elements.

</div>

---

# SCENARIO-BASED QUESTIONS

---

## Scenario Practice 1

**Your PLC program should turn on a lamp when a button is pressed and keep it on until a reset button is pressed. You test it and the lamp turns on, but immediately turns off when you release the button.**

**What is likely missing from your ladder logic, and how do you fix it?**

<div class="small">

*First hand up gets to answer!*

</div>

---

### Sample Answer

<div class="box small">

**Problem:** No latch (seal-in) circuit — the lamp output is only powered while the input button contact is TRUE.

**Fix: Add a seal-in branch**

```
[Start Button] ─────────────────────────────( Lamp Output )
      │
[Lamp Output] ─────────────────────────────
```

- Add a **normally-open contact** of the Lamp Output **in parallel** with the Start Button contact
- Now the lamp energizes when Start is pressed and stays ON through its own contact
- Add a **normally-closed Reset Button contact** in series to break the latch

**This is the standard latching circuit (Part 1 of Project 2).**

</div>

---

## Scenario Practice 2

**Design a ladder logic rung that turns on a motor (Motor_Out) ONLY when both a start button (Start_In) is pressed AND a safety door sensor (Door_Closed) confirms the door is shut. The motor must stay on until a stop button (Stop_In) is pressed.**

**Describe or sketch the rung structure.**

---

### Sample Answer

<div class="box small">

**Rung structure:**

```
[Stop_In NC] ─── [Door_Closed NO] ─── [Start_In NO] ──────( Motor_Out )
                                             │
                                      [Motor_Out NO] ──────
```

**Explanation:**
- **Stop_In (NC):** Normally-closed; opening this contact (pressing stop) cuts power to the rung
- **Door_Closed (NO):** Must be TRUE (door shut) for any output
- **Start_In (NO)** in parallel with **Motor_Out (NO):** Creates the latch — motor stays on after start is released
- **Motor_Out:** Output coil energizes when path is complete

**Safety note:** Door sensor in series ensures the motor CANNOT run with the door open — a safety interlock.

</div>

---

## Scenario Practice 3

**A student is running the FANUC CRX in Production Mode when the robot arm suddenly stops moving mid-program. The student walks up to the robot to see what happened. Identify what safety rules are being violated and what should have been done instead.**

---

### Sample Answer

<div class="box small">

**Violations:**

1. **Entering the work cell during automatic operation** — robots in Production Mode must never be approached while the program could restart
2. **Assuming robot is safe because it stopped** — a stopped robot may be paused, waiting for input, or about to resume; it is NOT safe

**Correct procedure:**
1. **Stop the program** using the Stop button on the Play menu (or E-stop if needed)
2. **Confirm the robot is fully stopped** (not just paused)
3. **Switch to Teach Mode** on the pendant before entering the work cell
4. **Investigate the fault** — check for fault messages; press RESET to clear after addressing the cause
5. **Re-verify the program** in step mode at ≤ 250 mm/s before returning to Production Mode

</div>

---

## Scenario Practice 4

**You are teaching a pick-and-place program on the FANUC CRX. After running it, the gripper closes at the correct pick position but the object is being crushed. What adjustment would you make and where?**

---

### Sample Answer

<div class="box small">

**Problem:** Gripper force is too high for the object being picked.

**Adjustment:** Modify the **Force parameter** in the Gripper 2 Point code block.

**Steps:**
1. Open the pick position code block in the program timeline
2. Navigate to the **Details tab** of the Gripper code block
3. Reduce the **Force value** (in Newtons) until the grip is firm but not damaging
4. Use the **Play button** in the Details tab to test the grip manually before running the full program
5. Also verify the **Width** is appropriate — too narrow a closing width can also cause crushing

**General principle:** Start with a low force value and increase until the object is held reliably without slipping or being crushed.

</div>

---

## Scenario Practice 5

**Your FANUC CRX pick-and-place program picks the object correctly, but during the move to the place position the robot takes a long, sweeping arc that nearly hits the table edge. How would you address this?**

---

### Sample Answer

<div class="box small">

**Problem:** The robot is using **Joint motion** for the transit move, which optimizes each joint independently and can produce unexpected TCP paths.

**Solutions:**

1. **Switch transit motion to Linear (L):**
   - In the Basic Pick/Place code block Details, change **Motion Type** from Joint to Linear
   - Linear motion moves the TCP in a straight line, giving predictable paths
   - Use Cartesian jogging to verify the path doesn't pass through obstacles

2. **Add an intermediate waypoint:**
   - Teach a safe intermediate position between pick and place
   - Add it as a separate motion step before the place code block

3. **Reduce the approach height:**
   - Lower the **Height Between Pick/Place Point and Approach Point** so the robot lifts less before traveling

4. **Reduce override speed** while testing to catch unexpected paths before they cause damage

</div>

---

## Key Concepts Review

<div class="box small">

**PLCs:**
- Input vs. output devices
- Ladder logic: rungs, contacts (NO/NC), coils
- Latching circuits (seal-in)
- Timers (TON: preset, accumulated, done bit)
- Ice cube relays: isolation, amplification
- Deterministic scan-cycle execution

**FANUC CRX:**
- Cell components: robot, controller, Tablet TP, gripper, control panel
- Safety rules: work cell entry, E-stop, escape plan
- Teach Mode vs. Production Mode
- Jogging: Joint mode vs. Cartesian (Cart) mode vs. MPG
- Free-hand teaching; teaching weight
- Programming: code blocks, timeline, touch-up, Basic Pick/Place
- Gripper code block: width, force, wait
- Motion types: Joint vs. Linear; override speed
- Step mode verification before full-speed runs

</div>

---

## General Exam Tips

✓ **Understand WHY**, not just memorize facts

✓ **Draw diagrams** if helpful (ladder rungs, work cell layouts)

✓ **Show your reasoning** in short-answer and scenario questions

✓ **Refer to Project 2 and Project 3** experiences in scenario questions

✓ **Budget time:** Don't spend too long on one question

✓ **Check terminology:** inputs vs. outputs, NO vs. NC contacts, Joint vs. Cartesian

---

## Practice Resources

**Review:**
- Your Project 2 condition tables and reflection
- Your Project 3 build log and reflection
- PLC lecture slides and PLC Guidebook Parts II & III
- Collaborative Robots slides

**Test yourself:**
- Can you trace a ladder logic rung and predict the output?
- Can you describe what happens step-by-step in a latch circuit?
- Can you explain each safety rule and WHY it exists?
- Can you describe how to teach and verify a pick-and-place program?

---

## Common Mistakes to Avoid

❌ Confusing input devices (supply signal to PLC) with output devices (receive signal from PLC)

❌ Forgetting the seal-in contact in a latching circuit

❌ Thinking a stopped robot in Production Mode is safe to approach

❌ Confusing Joint mode jogging (moves individual joint) with Cartesian mode (moves TCP along axes)

❌ Confusing Teach Mode (programming/testing) with Production Mode (autonomous run)

❌ Forgetting that timer accumulated value resets when the enabling rung goes FALSE before preset is reached

---

## Questions?

**Review sessions:** Check Discord for study group times

**Office hours:** See [instructor schedule](https://janyljumadinova.com/schedule)

**Day before exam:** Final Q&A in class

<div class="box">

**Good luck on Exam 2!**

</div>
