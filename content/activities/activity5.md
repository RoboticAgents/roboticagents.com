+++
title = "Activity 5: ROS2 Environment Setup & First Simulation"
description = "Install the ROS2 Docker environment and drive a simulated TurtleBot3 in Gazebo"
weight = 5
+++

## Overview

In this activity, you will set up a **ROS2 robotics simulation environment** using Docker and run your first robot simulation. By the end of class, you will have a working ROS2 + Gazebo + TurtleBot3 environment on your laptop and will have driven a simulated robot using keyboard teleoperation.

**Due:** Complete during class, March 17th

---

## Learning Objectives

By completing this activity, you will:

- Install and configure Docker Desktop for robotics simulation
- Understand why containerized environments are used in robotics development
- Launch a TurtleBot3 in a Gazebo simulation world
- Control a simulated robot using ROS2 teleoperation
- Use basic ROS2 CLI commands to inspect the running system

---

## Pre-Requisites (Complete BEFORE Class If Possible)

### Step 1: Install Docker Desktop

Docker Desktop must be installed before class. Download it for your operating system:

- **Windows**: [Docker Desktop for Windows](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe) (requires WSL2 — Docker will prompt you to enable it)
- **macOS (Intel)**: [Docker Desktop for Mac (Intel)](https://desktop.docker.com/mac/main/amd64/Docker.dmg)
- **macOS (Apple Silicon / M1–M4)**: [Docker Desktop for Mac (Apple Silicon)](https://desktop.docker.com/mac/main/arm64/Docker.dmg)
- **Linux**: [Docker Desktop for Linux](https://docs.docker.com/desktop/install/linux-install/)

After installation:

1. Launch Docker Desktop
2. Let it finish starting up (you should see the Docker icon in your system tray/menu bar)
3. Open a terminal and verify:

```bash
docker --version
```

### Step 2: Clone the Course ROS2 Repository

```bash
git clone https://github.com/RoboticAgents/ros2-environment.git
cd ros2-environment
```

### Step 3 (Recommended): Pre-Build the Image

To save class time, start the build now — it downloads ~4 GB and takes 15–30 minutes:

```bash
docker compose up --build
```

Once you see the desktop running, press `Ctrl+C` to stop. The built image is cached for class.

---

## Part 1: Start the ROS2 Environment

### 1.1 Build and Launch

Open a terminal in the `ros2-environment` directory and run:

```bash
docker compose up --build
```

**First time:** This downloads the base image and installs ROS2 packages. You'll see download progress in your terminal. Wait for it to complete.

**Subsequent times:** Starts almost instantly because the image is cached.

### 1.2 Connect via Browser

Open your web browser and go to:

### **[http://localhost:6080](http://localhost:6080)**

You should see a **Linux desktop** running inside your browser. This is a full Ubuntu 22.04 desktop with ROS2 Humble pre-installed.

> **Why Docker?** ROS2 runs natively on Ubuntu Linux. Docker lets us run an Ubuntu environment inside a container on any operating system. The VNC interface lets you see and interact with the graphical desktop through your browser — no matter whether you're on Windows, macOS, or Linux.

> **Troubleshooting:** If port 6080 is in use, edit `docker-compose.yml` and change `"6080:80"` to `"6081:80"`, then access `http://localhost:6081`.

---

## Part 2: Launch TurtleBot3 in Gazebo

### 2.1 Open a Terminal

In the VNC desktop (the browser window), **right-click** the desktop and select **Terminal** (or find LXTerminal in the application menu at the bottom).

### 2.2 Launch the Simulation

Run this command in the terminal:

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

Wait ~30–60 seconds for Gazebo to load. You should see:

- A **Gazebo window** with a simulated world
- A small circular robot (**TurtleBot3 Burger**) in the center
- Walls and obstacles around the robot

> **Performance note:** Gazebo uses software rendering inside Docker. It will be slower than running natively. This is normal. Keep the window small if it's laggy.

📸 **Screenshot 1:** Take a screenshot of the Gazebo window showing the TurtleBot3 in the world.

---

## Part 3: Drive the Robot

### 3.1 Open a Second Terminal

**Right-click** the VNC desktop → **Terminal** to open another terminal window.

### 3.2 Launch Keyboard Teleoperation

```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -p stamped:=true
```

You should see control instructions:

```
Control Your TurtleBot3!
---------------------------
Moving around:
        w
   a    s    d
        x

w/x : increase/decrease linear velocity
a/d : increase/decrease angular velocity
space key, s : force stop
```

### 3.2b Direct Velocity Command (Quick Movement Test)

If keyboard teleop does not move the robot, run this command in a terminal to publish forward velocity directly:

```bash
ros2 topic pub /cmd_vel geometry_msgs/msg/TwistStamped "{header: {frame_id: 'base_link'}, twist: {linear: {x: 0.2}, angular: {z: 0.0}}}" -r 10
```

You should immediately see the robot move forward. Press `Ctrl+C` to stop.

This is a useful debugging step because it bypasses keyboard input and tests whether `/cmd_vel` commands reach the simulator.

### 3.3 Drive Around

- **`w`** — move forward
- **`a`** — turn left
- **`d`** — turn right
- **`x`** — move backward
- **`s`** or **space** — stop

Drive the robot around the world. Try navigating through gaps between obstacles without colliding.

📸 **Screenshot 2:** Take a screenshot showing the robot in a different position after driving it around.

---

## Part 4: Explore ROS2

Open a **third terminal** in the VNC desktop.

### 4.1 List Active Nodes

```bash
ros2 node list
```

📝 **Write down** the list of nodes you see. Nodes are individual processes that each handle one task (e.g., simulating the robot, processing sensor data).

### 4.2 List Active Topics

```bash
ros2 topic list
```

📝 **Write down** the list of topics. Topics are named communication channels that nodes use to send and receive messages.

### 4.3 Inspect Sensor Data

View one message from the robot's simulated lidar sensor:

```bash
ros2 topic echo /scan --once
```

You'll see a `LaserScan` message with an array of distance values — these are what the robot "sees" around it.

### 4.4 Watch Velocity Commands

In this terminal, start echoing the velocity topic:

```bash
ros2 topic echo /cmd_vel
```

Now switch to the **teleop terminal** and press `w` or `a`. You should see velocity messages appear in real time in the echo terminal.

📝 **Write down** one velocity message. What do `linear.x` and `angular.z` represent?

> **Hint:** `linear.x` = forward/backward speed (m/s). `angular.z` = rotation speed (rad/s).

---

## Verification Checklist

Before you're done, verify that you can answer **YES** to all of these:

- [ ] Docker Desktop is installed and running on my laptop
- [ ] `docker compose up` successfully starts the ROS2 environment
- [ ] I can access the VNC desktop at `http://localhost:6080`
- [ ] Gazebo launches with the TurtleBot3 in `turtlebot3_world`
- [ ] I can drive the robot with keyboard teleoperation
- [ ] `ros2 node list` shows active nodes
- [ ] `ros2 topic list` shows active topics
- [ ] I can echo sensor data from `/scan`

**Submit:** Post your two screenshots and the list of nodes/topics to the class Discord channel.

---

## Key ROS2 Concepts

| Concept | What It Is |
|:---|:---|
| **ROS2** | Robot Operating System 2 — middleware that connects robot software components via a publish/subscribe messaging system |
| **Node** | A single process that performs one task (e.g., reading a sensor, controlling a motor, planning a path) |
| **Topic** | A named communication channel; nodes **publish** data to topics and **subscribe** to receive data |
| **Message** | Structured data sent over a topic (e.g., `Twist` for velocity commands, `LaserScan` for lidar data) |
| **Gazebo** | A physics simulator that models robots, sensors, and environments |
| **TurtleBot3** | A small, affordable robot platform widely used in robotics education and research |
| **Teleoperation** | Controlling a robot manually (e.g., keyboard, joystick) rather than autonomously |

---

## Shutting Down

When you're done:

1. Press `Ctrl+C` in each VNC terminal to stop running commands
2. In your **host terminal** (not VNC), press `Ctrl+C` where `docker compose up` is running
3. To fully remove the container: `docker compose down`
4. The built image stays cached — next time `docker compose up` starts instantly

---

## What's Next

This Docker environment is your **robotics simulation sandbox for the rest of the semester**. In the coming weeks, you'll use it to:

- **Map** an environment using SLAM (Simultaneous Localization and Mapping)
- **Localize** the robot's position within a known map
- **Plan paths** around obstacles using algorithms like A*
- **Navigate autonomously** using the ROS2 Nav2 navigation stack

Keep Docker Desktop installed and the `ros2-environment` repository on your machine.
