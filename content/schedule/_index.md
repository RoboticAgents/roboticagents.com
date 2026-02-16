+++
title = "Course Schedule"
description = ""
weight = 1
+++

### Detailed Weekly Schedule

**Note**: Some sessions will be held at **ALIC @ Bessemer** (764 Bessemer St # 105, Meadville, PA 16335) for hands-on work with industrial equipment. Please fill out the [transportation intake form](https://forms.gle/stFfgBWzxv9n988r9) to indicate your transportation preference.

#### Project Legend
- **P1** = Wheeled Robot
- **P2** = PLC
- **P3** = FANUC
- **P4** = ROS Simulation
- **P5** = TurtleBots
- **FP** = Final Project

{{< table style="table-bordered" >}}
| Week | Topic  | Class Activities | Project Assignment | Readings / Resources |
| :--- | :--- | :--- | :--- | :--- |
| 1 (Jan 12–17) | Course intro; What is a robot? Arduino, locomotion | [Modern Robots Presentations](https://docs.google.com/presentation/d/1d-GVw5LlcAGIGwjs_ngNqJljR3Ofu9X34a9EcibV2SU/edit?usp=sharing) | [Project 1: Wheeled Robot](https://classroom.github.com/a/kEovlL1p) (Due Feb 3) | [Locomotion Slides](/slides/locomotion.html)<br>IAR Ch. 1 |
| 2 (Jan 20–24)<br>*(MLK Mon off)* | Actuators; wiring, power | Project 1 work time | P1: Mechanical build, wiring, power | [Motors & Arduino Slides](/slides/motors.html)<br>IAR Ch. 2.1-2.3, 6 |
| 3 (Jan 26–30) | Actuators (cont.); sensors; kinematics; reactive control | [Activity 1: Servo and Stepper Motor Experiments](/activities/activity1) (Due Jan 28, 11:50am)<br>[Activity 2: Distance Sensors](/activities/activity2) (Due Feb 2, 11:50am) | P1: Basic control + sensing; demo | [Sensors Slides](/slides/sensors.html)<br>IAR Ch. 7 |
| 4 (Feb 2–6) | Deterministic control; state machines; why PLCs exist | [Activity 3: Environmental Sensors](https://classroom.github.com/a/hZZHXESz) (Due Feb 6, 11:50am)<br>**Feb 6: No class - read [PLC Guidebook Part II](https://drive.google.com/file/d/1gDMwGD6chMFH_-qLaJD7Ft-CEAc2gAlF/view?usp=sharing)** | P1 demos | [PLC Guidebook Part II](https://drive.google.com/file/d/1gDMwGD6chMFH_-qLaJD7Ft-CEAc2gAlF/view?usp=sharing) |
| 5 (Feb 9–13) | Safety, interlocks, fault handling | **Feb 9 (11am-11:50am @ Bessemer)**: Tour, safety instructions, PLC demo<br>**Feb 10 (2:30-4pm @ Bessemer)**: PLC work | [Project 2: PLC](https://classroom.github.com/a/Ar9L1TFS) | [PLC Slides](https://docs.google.com/presentation/d/e/2PACX-1vQVqMm1sQSfTw7AIwK6qxmptmswl_DdMyi4zwb1S8UN1s9INryruMhq0hCCyoAPCg/pub?start=false&loop=false&delayms=3000)<br>PLC Guidebook Part III<br>[Exam 1 Review](/slides/exam1review.html) |
| — | **Exam 1** (February 13th) | — | — | Covers P1 (locomotion, kinematics, sensors) |
| 6 (Feb 16–20) | Human–robot collaboration; industrial workflows | **Feb 17 (2:30-4pm @ Bessemer)**: PLC work<br>**Feb 18 (11am-11:50am @ Bessemer)**: PLC work | P2: PLC<br>[Community Project 1](https://github.com/RoboticAgents/community_project1) | [PLC Slides](https://docs.google.com/presentation/d/e/2PACX-1vQVqMm1sQSfTw7AIwK6qxmptmswl_DdMyi4zwb1S8UN1s9INryruMhq0hCCyoAPCg/pub?start=false&loop=false&delayms=3000) |
| 7 (Feb 23–27) | System integration; comparison to autonomy | **Feb 23 (11am-11:50am @ Bessemer)**: PLC work day (P2 due)<br>**Feb 24 (2:30-4pm @ Bessemer)**: FANUC work (tentative)<br>**Feb 27 (11am-11:50am @ Bessemer)**: FANUC work | P2: PLC due; P3: FANUC | — |
| 8 (Mar 1–8) | **Spring Break – No Classes** | — | — | — |
| 9 (Mar 9–13) | Why ROS? Robot software architectures | **Mar 9 (11am-11:50am @ Bessemer)**: FANUC work (tentative)<br>**Mar 10 (2:30-4pm @ Bessemer)**: FANUC work | P3: FANUC | — |
| — | **Exam 2** (March 13th) | — | — | Covers PLC/FANUC + ROS fundamentals |
| 10 (Mar 16–20) | Motion models; navigation concepts | — | P4: ROS | IAR Ch. 12 |
| 11 (Mar 23–27) | Simulation vs reality; sensing uncertainty | — | P4: ROS | IAR Ch. 14 |
| 12 (Mar 30–Apr 3) | Robustness, recovery, evaluation | — | P5: TurtleBots | ROS navigation docs |
| — | **Exam 3** (April 3rd) | — | — | ROS + autonomy concepts |
| 13 (Apr 6–10)<br>*(Decl Day Apr 6; Recharge Apr 9–10)* | Project integration; system design | — | P5: TurtleBots; FP: Proposal + architecture review | No new reading |
| 14 (Apr 13–17) | Ethics, communication, deployment | — | FP: Build & test | Selected civic/ethics readings |
| 15 (Apr 20–24) | Reflection; future of robotics | — | FP: Demos & presentations | None |
{{< /table >}}

---

### Course Flow: The Big Picture

The course follows a progressive shift in **abstraction** and **uncertainty**:

**Physical Embodiment** → **Deterministic Control** → **Probabilistic Autonomy** → **System Integration**

This sequence mirrors how robotic systems are encountered in professional practice and supports cognitive development from concrete reasoning to abstract systems thinking.

#### Five Phases of Learning

{{< table style="table-bordered" >}}
| Phase | Weeks | Focus | What You'll Build | Key Concept | Assessment |
| :---: | :---: | :--- | :--- | :--- | :---: |
| **Phase 1**<br>Physical Robot | 1–3 | Hardware embodiment | Wheeled robot from components | Robots are **physical systems** with mechanical, electrical, and sensing constraints | Project and class activities |
| **Phase 2**<br>Industrial Control | 4–7 | Deterministic logic | PLC + FANUC robotic cell | Safety through **predictability** and human-centered design | Project and class activities<br>**Exam 1** |
| **Phase 3**<br>Software Autonomy | 9–10 | Software architecture | ROS simulation behaviors | Autonomous systems require **abstraction** and planning | Project and class activities<br>**Exam 2** |
| **Phase 4**<br>Real Autonomy | 11–12 | Uncertainty & robustness | TurtleBot navigation | Simulation ≠ reality; **robustness** requires testing | Project and class activities<br>**Exam 3** |
| **Phase 5**<br>Integration | 13–15 | Synthesis & judgment | Final project of your design | Engineering is about **choices**, not just tools | Project and class activities<br>Presentation |
{{< /table >}}

#### Cumulative Learning

Each phase builds on all prior work. Concepts are revisited with increasing depth:

```
Week 1–3:   [Physical Systems]
              ↓
Week 4–7:   [Physical Systems] + [Deterministic Control] + [Safety]
              ↓
Week 9–10:  [Physical Systems] + [Control Architectures] + [Software Abstraction]
              ↓
Week 11–12: [Physical Systems] + [Control] + [Abstraction] + [Uncertainty] + [Robustness]
              ↓
Week 13–15: [Physical] + [Control] + [Abstraction] + [Uncertainty] + [Integration] + [Ethics]
```

#### Order

- **Physical first:** You can't understand software abstractions without hardware constraints
- **Industrial before autonomous:** Most robots prioritize safety over intelligence
- **Simulation before hardware:** Learn ROS architecture without hardware debugging
- **Integration last:** Make informed design choices only after experiencing tradeoffs
