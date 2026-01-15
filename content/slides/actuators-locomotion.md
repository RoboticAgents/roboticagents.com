+++
title = "Actuators and Locomotion"
description = "Week 2 lecture on robot movement mechanisms"
weight = 1
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

# Actuators and Locomotion

**Week 1 • CMPSC 304 Robotic Agents**

---

## Today's Agenda

- What is actuation?
- Locomotion vs. manipulation
- Static vs. dynamic stability
- Degrees of Freedom (DoF)
- Wheel types and kinematics

---

## Actuation: Making Robots Move

<div class="box">

**Actuation** = The robot's ability to move and interact with the world

</div>

Two key types:
- **Locomotion**: Moving the robot itself
- **Manipulation**: Moving objects in the environment

---

## The Duality of Movement

Both use the same principle:
- Motors exert forces on the environment
- **Locomotion**: Forces on ground/water/air → robot moves
- **Manipulation**: Forces on objects → objects move

**Example**: Insect legs do both!

---

## Locomotion Methods

Rolling • Walking • Running • Jumping  
Swimming • Flying • Crawling • Sliding

<div class="box">

**Key Question**: Which mechanism is best for your application?

</div>

Trade-offs: energy efficiency, terrain, speed, stability, cost

---

## Energy Efficiency: The Wheel Wins

<img src="/slides/power-consumption.png" alt="Power consumption vs speed" style="max-width: 70%; margin: 20px auto; display: block;">

<div class="box small">

**Rolling** provides the best energy-to-speed ratio of any locomotion method.

Railway wheels are ~10× more efficient than walking at the same speed!

</div>

---

## Static vs. Dynamic Stability

<div style="display: flex; justify-content: space-around; margin-top: 30px;">

<div style="flex: 1; text-align: center;">

### Static Stability
Won't fall when **not** moving

✓ Stable at rest  
✓ Slower movements  
✓ Simpler control

</div>

<div style="flex: 1; text-align: center;">

### Dynamic Stability
Requires **constant** motion

✓ Faster, more agile  
✗ Complex control  
✗ Always actuating

</div>

</div>

---

## Stability: The Key Principle

<img src="/slides/stability.pdf" alt="Stability examples" style="max-width: 90%; margin: 20px auto; display: block;">

<div class="box">

**Center of mass** must stay within the polygon formed by ground-contact points

</div>

- **Left**: Statically stable (stays upright at rest)
- **Middle**: Dynamically stable (must keep moving)
- **Right**: Both modes possible (configuration-dependent)

---

## Real-World Examples

**Six legs** (insects, hexapods):
- Statically stable walking
- Move 3 legs at a time

**Four legs** (dogs, quadruped robots):
- Walking = static stability
- Running/galloping = dynamic stability

---

## Degrees of Freedom (DoF)

<div class="box">

**DoF** = Independent ways a system can move

</div>

Two types to distinguish:
1. **Cartesian DoF**: Positions/orientations in space (max 6 in 3D)
2. **Mechanical DoF**: Number of actuated joints

---

## Cartesian DoF in 3D Space

<img src="/slides/pitchyawroll.pdf" alt="Pitch, yaw, and roll" style="max-width: 65%; margin: 10px auto; display: block;">

**Translation** (3 DoF): Forward/back • Left/right • Up/down

**Rotation** (3 DoF): **Pitch** • **Yaw** • **Roll**

---

## Wheel Types and Their DoF

Different wheels = different mobility

<div class="box small">

## Wheel Types and Their DoF

<img src="/slides/wheels-table.png" alt="Wheel types" style="max-width: 85%; margin: 20px auto; display: block;">

<div class="small">

Different wheel types enable different types of mobility

</div>degrees of freedom**:
1. Rotation around wheel axle
2. Rotation around ground contact point

<div class="box">

**Constraint**: Can only roll in one direction  
Cannot move sideways (would require skidding)

</div>

**Example**: Bicycle wheel, car wheel

---

## Caster Wheel (3 DoF)

**Three degrees of freedom**:
1. Rotation around wheel axle
2. Rotation around ground contact
3. Rotation around caster axis

<div class="box">

Can reorient to roll in any direction!

</div>

**Example**: Shopping cart, office chair

---

## Swedish/Mecanum Wheel (3 DoF)

**Three degrees of freedom**:
1. Rotation around main wheel axle
2. Rotation around ground contact
3. Rotation around roller axles

<div class="box">

Rollers on circumference allow sideways motion while wheel spins forward

</div>

**Result**: True omnidirectional movement!

---

## Kinematic Constraints

<div class="box">

**3-DoF wheels** = Free movement on a plane  
**2-DoF wheels** = Constrained movement

</div>

**But** constrained ≠ unreachable!
- A car can parallel park
- Requires multiple maneuvers
- Like a knight on a chessboard

---

## Mobile Robot DoF on a Plane

**Plane has 3 Cartesian DoF**:
- X position
- Y position  
- Orientation (angle θ)

<div class="box">

Robots without 3-DoF wheels have **kinematic constraints**

</div>

They may need multiple moves to reach certain poses

---

## Manipulator Arms: Mechanical DoF

<div class="box">

Each actuated joint typically adds 1 mechanical DoF

</div>

**On a plane** (2D workspace):
- Up/down position
- Left/right position
- End-effector orientation

**3 Cartesian DoF needed** → Need ≥3 joints

---

## Joint Types

**Revolute (Rotary) Joint**:
- Most common
- Rotates around an axis
- Example: Elbow, shoulder

**Prismatic (Linear) Joint**:
- Extends and contracts
- Slides along an axis
- Example: Telescope, piston

---

## Design Trade-offs

Choosing kinematics involves balancing:
- ✓ Mechanical complexity
- ✓ Maneuverability  
- ✓ Precision
- ✓ Cost
- ✓ Ease of control

<div class="box small">

**Example**: Differential drive (2 wheels) vs. car steering  
• Differential: cheap, maneuverable, hard to drive straight  
• Car steering: expensive, precise, hard to parallel park

</div>

---

## Real Robot: Differential Drive

**Configuration**:
- Two powered wheels on shared axis
- One (or two) caster wheels for support

**Advantages**:
- Very maneuverable (can spin in place)
- Simple control
- Low cost

**Challenge**: 
- Hard to drive perfectly straight
- Requires matched motors and wheels

---

## Key Takeaways

1. **Actuation** enables locomotion and manipulation
2. **Stability** can be static (at rest) or dynamic (requires motion)
3. **DoF** describes what movements are possible
4. **Wheel type** determines mobility constraints
5. **Design choices** involve complex trade-offs

---

## Before Next Class

**Hands-on activity**: Building your wheeled robot!

**Think about**:
- What DoF does your robot need?
- Static or dynamic stability?
- Which wheel configuration?
- What trade-offs will you make?

---

## Questions?

**Next**: Continue Project 1 (Wheeled Robot)
- Mechanical build
- Wiring and power
- Basic control

<div class="small">

*Readings: IAR Chapters 2 & 6*

</div>
