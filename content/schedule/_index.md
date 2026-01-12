+++
title = "Course Schedule"
description = ""
weight = 3
+++

### Course Flow: The Big Picture

The course follows a progressive shift in **abstraction** and **uncertainty**:

**Physical Embodiment** → **Deterministic Control** → **Probabilistic Autonomy** → **System Integration**

This sequence mirrors how robotic systems are encountered in professional practice and supports cognitive development from concrete reasoning to abstract systems thinking.

#### Five Phases of Learning

{{< table style="table-bordered" >}}
| Phase | Weeks | Focus | What You'll Build | Key Concept | Assessment |
| :---: | :---: | :--- | :--- | :--- | :---: |
| **🔧 Phase 1**<br>Physical Robot | 1–3 | Hardware embodiment | Wheeled robot from components | Robots are **physical systems** with mechanical, electrical, and sensing constraints | — |
| **⚙️ Phase 2**<br>Industrial Control | 4–7 | Deterministic logic | PLC + FANUC robotic cell | Safety through **predictability** and human-centered design | **Exam 1** |
| **🧠 Phase 3**<br>Software Autonomy | 9–10 | Software architecture | ROS simulation behaviors | Autonomous systems require **abstraction** and planning | **Exam 2** |
| **🤖 Phase 4**<br>Real Autonomy | 11–12 | Uncertainty & robustness | TurtleBot navigation | Simulation ≠ reality; **robustness** requires testing | **Exam 3** |
| **🎯 Phase 5**<br>Integration | 13–15 | Synthesis & judgment | Final project of your design | Engineering is about **choices**, not just tools | Presentation |
{{< /table >}}

#### Cumulative Learning: Nothing Is Discarded

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

#### Why This Order?

- **Physical first:** You can't understand software abstractions without hardware constraints
- **Industrial before autonomous:** Most robots prioritize safety over intelligence
- **Simulation before hardware:** Learn ROS architecture without hardware debugging
- **Integration last:** Make informed design choices only after experiencing tradeoffs

---

### Detailed Weekly Schedule

#### Project Legend
- **P1** = Wheeled Robot
- **P2** = PLC + FANUC
- **P3** = ROS Simulation
- **P4** = TurtleBots
- **FP** = Final Project

{{< table style="table-bordered" >}}
| Week | Topic (Lecture Focus) | Lab / Project Focus | Readings / Resources |
| :--- | :--- | :--- | :--- |
| 1 (Jan 12–17) | Course intro; What is a robot? Systems view; Safety | Team formation; Wheeled robot overview | Intro to Autonomous Robots (IAR) Ch. 1 |
| 2 (Jan 20–24)<br>*(MLK Mon off)* | Actuators, sensors, power, control loops | P1: Mechanical build, wiring, power | IAR Ch. 6 |
| 3 (Jan 27–31) | Reactive control; failure modes; ethics of embodied systems | P1: Basic control + sensing; demo | IAR Ch. 7 |
| 4 (Feb 3–7) | Deterministic control; state machines; why PLCs exist | PLC ladder logic basics; discrete I/O | PLC Presentation: Intro, PLC basics, ladder logic fundamentals<br>IAR: Ch. 2 (sections on control architectures) |
| 5 (Feb 10–14) | Safety, interlocks, fault handling | PLC timers, counters, safety logic | PLC Presentation: Timers, counters, interlocks, fault states<br>FANUC Manual: Safety overview + operational modes |
| — | **Exam 1** (February 13th) | — | Covers P1 + basic PLC concepts |
| 6 (Feb 17–21) | Human–robot collaboration; industrial workflows | FANUC CRX task programming; PLC ↔ robot coordination | FANUC Manual: Teach pendant operation, task execution<br>IAR: Ch. 1 (human–robot interaction sections) |
| 7 (Feb 24–27) | System integration; comparison to autonomy | Full PLC–FANUC cell demo | IAR: Ch. 3 (reactive systems)<br>Short instructor note: PLC vs ROS comparison |
| 8 (Feb 28–Mar 8) | **Spring Break – No Classes** | — | — |
| 9 (Mar 10–14) | Why ROS? Robot software architectures | P3: ROS setup; simulation intro | IAR Ch. 2–3; ROS 2 Beginner Tutorials |
| — | **Exam 2** (March 13th) | — | Covers PLC/FANUC + ROS fundamentals |
| 10 (Mar 17–21) | Motion models; navigation concepts | P3: Autonomous behaviors in simulation | IAR Ch. 12 |
| 11 (Mar 24–28) | Simulation vs reality; sensing uncertainty | P4: TurtleBot bring-up & navigation | IAR Ch. 14 |
| 12 (Mar 31–Apr 4) | Robustness, recovery, evaluation | P4: TurtleBot demos & comparison | ROS navigation docs |
| — | **Exam 3** (April 3rd) | — | ROS + autonomy concepts |
| 13 (Apr 7–11)<br>*(Decl Day Apr 6; Recharge Apr 9–10)* | Project integration; system design | FP: Proposal + architecture review | No new reading |
| 14 (Apr 14–18) | Ethics, communication, deployment | FP: Build & test | Selected civic/ethics readings |
| 15 (Apr 21–27) | Reflection; future of robotics | FP demos & presentations | None |
{{< /table >}}
