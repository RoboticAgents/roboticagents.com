+++
title = "Exam 3 Review"
description = "Review for Exam 3 covering ROS2 and autonomy concepts"
weight = 13
+++

This content is available as an HTML slide deck at [/slides/exam3review.html](/slides/exam3review.html).

The slides cover:
- Exam format and what's covered
- Multiple Choice Practice Questions (5)
  - ROS2 nodes and topics
  - Publish/subscribe pattern
  - Occupancy grid values
  - AMCL localization
  - Global vs. local costmap
- Short Answer Practice Questions (5)
  - SLAM and the chicken-and-egg problem
  - Costmap inflation and path planning
  - Topics vs. actions in ROS2
  - Writing a ROS2 velocity publisher node
  - Sim-to-real gap and odometry drift
- Scenario-Based Practice Questions (5)
  - Nav2 robot stuck troubleshooting
  - NavigateToPose waypoint code
  - SLAM mapping quality issues
  - Parameter tuning for navigation
  - TurtleBot 4 real-world deployment
- Key concepts review
- Exam tips and common mistakes

[View the full presentation →](/slides/exam3review.html)

---

## Study Materials

- **Project 4:** ROS Simulation & TurtleBots documentation and reflection
- **Slides:**
  - ROS2 Intro Slides
  - SLAM & Mapping Slides
  - Navigation & Path Planning Slides
  - Writing ROS2 Nodes Slides
  - Simulation to Reality Slides
- **Activities:** 5–9
- **Readings:** IAR Chapters 12–14

---

# MULTIPLE CHOICE QUESTIONS

---

## Multiple Choice Practice 1

**In ROS2, what is a "node"?**

A. A physical sensor attached to the robot

B. A single process that performs one job and communicates through topics

C. A configuration file that launches the robot

D. A map cell in an occupancy grid

<div class="small">

*First hand up gets to answer!*

</div>

---

### Answer: B. A single process that performs one job and communicates through topics

<div class="box">

A **node** is an independent process in the ROS2 computation graph.

**Key properties:**
- Each node does **one job** (e.g., lidar driver, path planner, motor controller)
- Nodes communicate through **topics** (pub/sub), **services**, and **actions**
- Nodes can be started, stopped, or replaced independently
- A robot system is a **graph of connected nodes**

**Example nodes:** Lidar Driver, SLAM Mapper, Path Planner, Motor Controller

**Command:** `ros2 node list` shows all running nodes.

</div>

---

## Multiple Choice Practice 2

**In the ROS2 publish/subscribe pattern, which statement is TRUE?**

A. Publishers must know the identity of all subscribers

B. Subscribers send acknowledgments back to publishers after each message

C. Publishers and subscribers are decoupled — neither knows who the other is

D. Each topic can only have one publisher and one subscriber

<div class="small">

*First hand up gets to answer!*

</div>

---

### Answer: C. Publishers and subscribers are decoupled — neither knows who the other is

<div class="box">

**Publish/subscribe** is a messaging pattern where nodes communicate through named topics without direct connections.

**Why decoupling matters:**
- **Modularity:** Swap a real lidar for a simulated one — subscribers don't change
- **Scalability:** Add a new node that listens to `/scan` without modifying existing code
- **Testing:** Record and replay topic data for debugging

**Multiple** publishers and subscribers can share the same topic.

**Contrast with Arduino:** Sensor code and motor code were tightly coupled in one file. ROS2 separates them into independent nodes connected by topics.

</div>

---

## Multiple Choice Practice 3

**In a ROS2 occupancy grid map, what does a cell value of 0 represent?**

A. An obstacle (wall)

B. Unknown/unexplored space

C. Free space — safe to traverse

D. The robot's current position

<div class="small">

*First hand up gets to answer!*

</div>

---

### Answer: C. Free space — safe to traverse

<div class="box">

An **occupancy grid** divides the world into cells, each storing a probability of being occupied.

**Cell values:**
- **0 (white):** Free space — the lidar confirmed nothing is there
- **100 / 1.0 (black):** Occupied — wall or obstacle detected
- **-1 or gray (?):** Unknown — the robot hasn't observed this area yet

**In costmaps:**
- 0 = free, 1–252 = increasing cost, 253 = inscribed, 254 = lethal, 255 = unknown

**The map is saved as a `.pgm` image file** with a companion `.yaml` file specifying resolution and origin.

</div>

---

## Multiple Choice Practice 4

**What does AMCL (Adaptive Monte Carlo Localization) do?**

A. Builds a map of the environment from lidar scans

B. Plans the shortest path from start to goal

C. Estimates the robot's position on a known map using a particle filter

D. Controls the robot's wheel motors directly

<div class="small">

*First hand up gets to answer!*

</div>

---

### Answer: C. Estimates the robot's position on a known map using a particle filter

<div class="box">

**AMCL** answers the question: **"Where am I on this map?"**

**How it works:**
- Spreads many **particles** (guesses) across possible robot positions
- Each particle is a possible (x, y, θ) pose
- Compares each particle's expected lidar scan to the **actual** scan
- Good matches **survive**; poor matches are removed
- Over time, the particle cloud **converges** to the true pose

**In RViz:** Green arrows start spread out, then tighten around the real position.

**Key distinction:** SLAM builds the map. AMCL uses an existing map to localize.

</div>

---

## Multiple Choice Practice 5

**What is the difference between the global costmap and the local costmap in Nav2?**

A. The global costmap is for simulation; the local costmap is for real robots

B. The global costmap covers the entire map for long-range planning; the local costmap covers a small area around the robot for real-time obstacle avoidance

C. The global costmap uses lidar; the local costmap uses the camera

D. There is no difference — they are the same costmap viewed at different zoom levels

<div class="small">

*First hand up gets to answer!*

</div>

---

### Answer: B. The global costmap covers the entire map for long-range planning; the local costmap covers a small area around the robot for real-time obstacle avoidance

<div class="box">

**Global Costmap:**
- Covers the **entire map**
- Based on the static map you saved
- Updated slowly (mostly static)
- Used for **long-range path planning**

**Local Costmap:**
- Small area **around the robot**
- Updated in **real-time** with live lidar data
- Includes **dynamic obstacles** (people, moved furniture)
- Used for **immediate driving decisions**

**Why two?** The global costmap provides the big-picture route. The local costmap handles moment-to-moment driving and unexpected obstacles.

</div>

---

# SHORT ANSWER QUESTIONS

---

## Short Answer Practice 1

**Explain what SLAM stands for, describe the "chicken-and-egg" problem it solves, and name the key inputs and outputs of a SLAM algorithm.**

<div class="small">

*First hand up gets to answer!*

</div>

---

### Sample Answer

<div class="box small">

**SLAM = Simultaneous Localization And Mapping**

**The chicken-and-egg problem:**
- To build a map, you need to know **where you are** (so you can place each scan correctly)
- To know where you are, you need **a map** (to match your sensor data against)
- SLAM solves both problems **at the same time**

**Inputs:**
- **Sensor data** (lidar scans) — what the robot sees right now
- **Odometry** (wheel encoders) — how the robot thinks it moved

**Outputs:**
- A **map** of the environment (occupancy grid)
- The robot's **estimated trajectory** (where it was at each step)

**Key techniques:** Scan matching (aligning consecutive scans), loop closure (recognizing a previously visited area to correct accumulated drift).

</div>

---

## Short Answer Practice 2

**Explain how costmap inflation works and why the path planner sometimes produces a path that curves away from walls even when a straight line would geometrically work.**

---

### Sample Answer

<div class="box small">

**Costmap inflation** expands obstacles outward by an `inflation_radius` to create a safety buffer.

**How it works:**
1. Each cell occupied by a wall is marked as **lethal** (cost 254)
2. Cells within `robot_radius` of a wall are marked **inscribed** (cost 253) — the robot center would collide
3. Cells within `inflation_radius` get **decreasing cost** — the closer to a wall, the higher the cost
4. Free space beyond the inflation radius remains at **cost 0**

**Why paths curve:**
- The global planner finds the **minimum-total-cost path**
- Even if a straight line is geometrically valid, passing near a wall accumulates high-cost cells
- A path that curves away from walls travels through **lower-cost cells**, so its total cost is lower
- The planner prefers the lower-cost route even if it's slightly longer

**Practical effect:** The robot stays safely in the middle of corridors and away from wall edges.

</div>

---

## Short Answer Practice 3

**Compare topics and actions in ROS2. When would you use each, and what does an action provide that a topic does not?**

---

### Sample Answer

<div class="box small">

**Topics (Publish/Subscribe):**
- One-way data streams: publishers send, subscribers receive
- No response expected — fire and forget
- Best for **continuous data** (sensor streams, velocity commands)
- Example: Publishing `Twist` to `/cmd_vel` to drive the robot

**Actions (Goal/Feedback/Result):**
- For **long-running tasks** with feedback
- Client sends a **goal**; server sends **feedback** during execution and a **result** when done
- Can be **cancelled** mid-execution
- Best for **complex behaviors** (navigate to a position, pick up an object)
- Example: Sending a `NavigateToPose` goal to Nav2

**What actions provide that topics don't:**
1. **Feedback** — progress updates during execution (e.g., "At position (1.5, 2.1), ETA 5s")
2. **Result** — confirmation of success or failure
3. **Goal management** — the server can accept or reject goals

**Course connection:** Activity 8 uses topics (direct velocity). P4 Part 3 uses actions (waypoint navigation).

</div>

---

## Short Answer Practice 4

**Describe how to write a ROS2 Python node that publishes velocity commands to make a robot drive forward. Include the key components: node class, publisher, timer, and the message type.**

---

### Sample Answer

<div class="box small">

**Key components:**

1. **Import** `rclpy`, `Node`, and `Twist` (from `geometry_msgs.msg`)
2. **Create a class** that extends `Node`
3. In `__init__`:
   - Call `super().__init__('node_name')` to register the node
   - Create a **publisher** on `/cmd_vel` with message type `Twist`
   - Create a **timer** (e.g., every 0.1 seconds) that calls a callback
4. In the **timer callback**:
   - Create a `Twist()` message
   - Set `msg.linear.x = 0.2` (forward speed in m/s)
   - Publish the message
5. In `main()`:
   - `rclpy.init()` → create node → `rclpy.spin(node)` → `rclpy.shutdown()`

**`spin()` is the event loop** — like Arduino's `loop()`, it keeps the node running and processes timer callbacks.

**The Twist message** has `linear` (x, y, z) and `angular` (x, y, z) components. For a ground robot, `linear.x` = forward speed, `angular.z` = turn rate.

</div>

---

## Short Answer Practice 5

**What is the sim-to-real gap? Give three specific examples of differences between a simulated robot and a physical TurtleBot 4.**

---

### Sample Answer

<div class="box small">

**The sim-to-real gap** (also called the reality gap) is the difference in behavior between a robot operating in simulation vs. the real world.

**Three specific examples:**

1. **Sensor noise:** In simulation, lidar returns clean, consistent distance readings. On the real RPLIDAR A1, there is noise (±a few cm), reflective surfaces (glass, mirrors) may not reflect the laser, and dark objects may absorb it.

2. **Odometry drift:** In simulation, wheel encoders give nearly perfect position estimates. On a real robot, wheels slip on smooth floors, different surfaces (carpet vs. tile) change dynamics, and small errors compound — after 10m the position may be off by 20+ cm. This is why AMCL is essential.

3. **Network latency:** In Docker, everything runs in one container with instant communication. With a physical TurtleBot 4, the robot and laptop communicate over Wi-Fi, adding 5–50 ms of delay. RViz may lag slightly behind the real robot.

**Other valid examples:** battery drainage, dynamic obstacles (people), auto-docking behavior, lidar stopping when docked.

</div>

---

# SCENARIO-BASED QUESTIONS

---

## Scenario Practice 1

**Your Nav2 robot is trying to navigate to a goal but keeps triggering recovery behaviors (spinning in place, backing up) instead of reaching the destination. In RViz, you can see the robot is near a narrow doorway. What could be wrong, and how would you fix it?**

<div class="small">

*First hand up gets to answer!*

</div>

---

### Sample Answer

<div class="box small">

**Likely problem:** The `inflation_radius` is too large, causing the inflated costmap to completely fill the doorway. The planner cannot find a path through a corridor where all cells are inscribed or lethal.

**Diagnosis steps:**
1. **Visualize the costmap** in RViz — check if the doorway appears completely blocked by inflation
2. Check if `robot_radius` is set correctly for your robot
3. Look at the global planner output — if no path is drawn, the doorway is blocked in the costmap

**Fixes:**
1. **Reduce `inflation_radius`** so the buffer doesn't fill narrow passages
2. **Check `robot_radius`** — if set too large, the inscribed zone blocks the doorway
3. **Reduce `cost_scaling_factor`** to make inflation decay faster away from obstacles
4. As a last resort, increase `goal tolerance` or place the goal on the other side of the doorway

**Key principle:** `robot_radius` + `inflation_radius` together determine the minimum passable corridor width. Their combined effect must be less than half the doorway width.

</div>

---

## Scenario Practice 2

**You need to write a ROS2 node that navigates a TurtleBot to three waypoints in sequence: (1.0, 0.0), (2.0, 1.0), and (0.0, 0.0). Describe the structure of this node, including how you handle the transition from one waypoint to the next.**

---

### Sample Answer

<div class="box small">

**Node structure:**

1. **Create an `ActionClient`** for the `NavigateToPose` action
2. **Store waypoints** as a list: `[(1.0, 0.0), (2.0, 1.0), (0.0, 0.0)]`
3. **Track current index** (`self.current = 0`)

**Execution flow:**
1. Call `wait_for_server()` to ensure Nav2 is ready
2. Create a `PoseStamped` message with `frame_id = 'map'` and the first waypoint coordinates
3. Send the goal with `send_goal_async(goal)`
4. In **`goal_response_callback`**: check if goal was accepted, then request the result with `get_result_async()`
5. In **`result_callback`**: increment `self.current`, check if more waypoints remain, and call `send_next_goal()` if so
6. When all waypoints are done, log "Route complete!"

**Critical details:**
- Set `goal.pose.header.frame_id = 'map'` (not `base_link`)
- Set initial pose in RViz before running the node
- Handle goal rejection (Nav2 may reject unreachable goals)
- Orientation uses quaternions: for yaw, set `orientation.z = sin(yaw/2)` and `orientation.w = cos(yaw/2)`

</div>

---

## Scenario Practice 3

**A student builds a map using SLAM in the Gazebo simulation. The resulting map has clean, sharp walls. They then map a real classroom with the TurtleBot 4 and the walls appear thick, noisy, and some areas show gaps. What is causing these differences, and what can the student do to improve the real-world map quality?**

---

### Sample Answer

<div class="box small">

**Causes of differences:**

1. **Sensor noise:** The RPLIDAR A1 has ±a few cm of variation per scan, making walls appear thicker
2. **Reflective/absorbing surfaces:** Glass doors, whiteboards, or dark furniture may not reflect the laser, creating gaps
3. **Irregular objects:** Chair legs, cables, and curved surfaces produce scattered points unlike clean sim walls
4. **Odometry drift:** Real wheel slip causes scan alignment errors, adding blur to the map
5. **Dynamic obstacles:** If people walked through during mapping, their ghosts may appear in the map

**How to improve:**
1. **Drive slowly** (0.1–0.15 m/s) to give SLAM more time to align scans
2. **Revisit the starting area** to enable loop closure, which corrects accumulated drift
3. **Map when the space is empty** to avoid dynamic obstacles
4. **Remove the dock from the mapping area** — the IR sensors can cause auto-docking mid-session
5. **Use consistent, steady movements** — avoid fast turns that cause odometry errors

</div>

---

## Scenario Practice 4

**Your robot navigates well in an open room but oscillates wildly (wobbles back and forth) when entering a long, featureless corridor. What are two likely causes—one related to localization and one related to the local planner—and how would you address each?**

---

### Sample Answer

<div class="box small">

**Localization issue (AMCL):**
- **Cause:** In a long featureless corridor, every position looks the same to the lidar. AMCL's particles spread out because multiple locations match equally well — the robot becomes **uncertain of its position**.
- **Fix:** Increase `max_particles` so AMCL can track more hypotheses. Also, reduce `odom_alpha` parameters if odometry is noisy, or improve the map to include more distinctive features at corridor ends.

**Local planner issue (DWB controller):**
- **Cause:** The `lookahead_dist` may be too large, causing the controller to overshoot corrections. Or `max_angular_vel` is too high, allowing aggressive turns that oscillate.
- **Fix:** Reduce `lookahead_dist` so the controller makes smaller, more frequent corrections. Lower `max_angular_vel` to limit turn rate. Consider reducing `desired_linear_vel` in narrow spaces.

**General principle:** Featureless environments are the hardest for both localization (no landmarks to match) and control (no nearby obstacles to constrain the path). Tuning parameters for the worst-case environment ensures stability everywhere.

</div>

---

## Scenario Practice 5

**Your team has a working waypoint navigation node in the Gazebo simulation. You now need to deploy it on a physical TurtleBot 4 in the lab. List the key steps for this deployment, and identify at least three things that could go wrong that wouldn't happen in simulation.**

---

### Sample Answer

<div class="box small">

**Deployment steps:**
1. **Build a real-world map:** Undock the robot, run SLAM, drive slowly through the lab, save the map files
2. **Update coordinates:** Real-world waypoints will be different from simulation — find new coordinates using RViz hover or `ros2 topic echo /goal_pose`
3. **Transfer and build:** Copy the node to the robot's workspace, `colcon build`, source the workspace
4. **Set the initial pose** precisely in RViz before running the node
5. **Test one waypoint first** before running the full route

**Three things that could go wrong:**
1. **Auto-docking:** The robot wanders near the dock and the IR sensors trigger autonomous docking mid-mission — lidar stops, `/cmd_vel` is ignored. **Fix:** Keep the dock away from the navigation area.
2. **Odometry drift near goal:** The robot oscillates near a waypoint because odometry error prevents it from reaching the tight default tolerance. **Fix:** Increase goal tolerance (e.g., 0.3–0.5 m).
3. **Network latency:** Wi-Fi delay causes the node to send its next goal before getting the result callback for the current one. **Fix:** Always wait for the result callback before sending the next waypoint. Use `ROS_DOMAIN_ID` to avoid cross-talk with other teams.

**Other valid answers:** cliff sensor false positives on dark floors, battery dying mid-run, people walking through the path, chair legs not detected by lidar.

</div>
