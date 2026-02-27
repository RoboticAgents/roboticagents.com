# Collaborative Robot Simulator - Specification

## 1. Project Overview

**Project Name:** CobotEdu Simulator  
**Type:** Educational Web Application (Single Page)  
**Core Functionality:** Interactive 3D simulation of a 6-axis collaborative robot (cobot) for teaching payloads, Cartesian movements, axis orientation, and orientation angles (yaw, pitch, roll)  
**Target Users:** Engineering students learning robotics fundamentals

---

## 2. UI/UX Specification

### Layout Structure

```
+------------------------------------------------------------------+
|  HEADER (fixed, 60px)                                            |
|  Logo + Title                                                    |
+------------------+-----------------------------------------------+
|  SIDEBAR (280px) |  MAIN CANVAS (flex: 1)                       |
|                  |                                               |
|  - Mode Tabs     |  3D Robot Visualization                       |
|  - Controls      |  - Grid floor                                |
|  - Info Panel    |  - Axis indicators                           |
|                  |  - Robot arm                                 |
|                  |  - End effector + payload                    |
|                  |                                               |
+------------------+-----------------------------------------------+
|  FOOTER (40px) - Status bar with current values                  |
+------------------------------------------------------------------+
```

**Responsive Breakpoints:**
- Desktop: > 1024px (sidebar + canvas side by side)
- Tablet: 768px - 1024px (sidebar collapses to overlay)
- Mobile: < 768px (stacked layout, sidebar becomes bottom sheet)

### Visual Design

**Color Palette:**
- Background: `#0a0a0f` (deep space black)
- Surface: `#12121a` (card backgrounds)
- Surface Elevated: `#1a1a24` (hover states)
- Primary: `#00d4aa` (teal/cyan - robot accent)
- Secondary: `#ff6b35` (orange - warnings/payload)
- Accent X: `#ff3366` (red - X axis)
- Accent Y: `#33ff66` (green - Y axis)
- Accent Z: `#3366ff` (blue - Z axis)
- Text Primary: `#e8e8ec`
- Text Secondary: `#8888a0`
- Border: `#2a2a3a`

**Typography:**
- Font Family: `"JetBrains Mono", "Fira Code", monospace` (techy feel)
- Headings: 700 weight
- Body: 400 weight
- Font Sizes:
  - H1: 24px
  - H2: 18px
  - Body: 14px
  - Small/Labels: 12px

**Spacing System:**
- Base unit: 8px
- Margins: 8px, 16px, 24px, 32px
- Padding: 8px, 12px, 16px, 24px
- Border radius: 4px (buttons), 8px (cards), 12px (panels)

**Visual Effects:**
- Box shadows: `0 4px 20px rgba(0, 212, 170, 0.1)`
- Glow effects on active elements: `0 0 20px rgba(0, 212, 170, 0.3)`
- Subtle grid pattern on background
- Smooth transitions: 200ms ease-out

### Components

**Mode Tabs:**
- Cartesian (default)
- Payload
- Orientation (Yaw/Pitch/Roll)
- States: default, hover (glow), active (filled background)

**Sliders:**
- Custom styled range inputs
- Thumb: 16px circle with glow
- Track: 4px height, gradient fill showing value
- Label above, value display below

**Buttons:**
- Reset View
- Toggle Grid
- Toggle Labels
- States: default, hover (glow), active (pressed), disabled (50% opacity)

**Info Cards:**
- Current position display (X, Y, Z)
- Current orientation (Yaw, Pitch, Roll in degrees)
- Payload weight display
- Max payload indicator with warning

**3D Canvas Elements:**
- Grid floor (20x20 units)
- Axis helper (RGB arrows at origin)
- Robot arm (6 segments with joints)
- End effector (gripper)
- Payload cube (scales with weight)
- Orientation indicator rings

---

## 3. Functionality Specification

### Core Features

#### 3.1 Robot Visualization
- 6-axis articulated robot arm rendered in 3D
- Segments: Base, Shoulder, Elbow, Wrist 1, Wrist 2, End Effector
- Smooth interpolated joint movements
- Joint angle limits:
  - Base rotation: -180° to +180°
  - Shoulder: -90° to +90°
  - Elbow: -135° to +135°
  - Wrist 1: -90° to +90°
  - Wrist 2: -180° to +180°
  - End Effector: 0° to 90° (gripper open/close)

#### 3.2 Cartesian Movement Mode
- Three sliders for X, Y, Z position
- Range: -10 to +10 units for each axis
- Real-time IK calculation to move end effector to position
- Visual feedback showing target position (ghost cube)
- Position readout in both units and joint angles

#### 3.3 Payload System
- Slider to set payload weight: 0 to 10 kg
- Visual payload cube attached to end effector
- Payload size scales: base 0.5 units, adds 0.05 units per kg
- Color changes based on percentage of max payload:
  - Green (< 50%): Safe
  - Yellow (50-80%): Caution
  - Red (> 80%): Warning
- Animated "strain" effect when near max payload (robot shakes/vibrates)
- Info display showing: Current payload, Max payload, % capacity

#### 3.4 Axis Orientation
- Toggle-able axis visualization at end effector
- RGB arrows showing local X (red), Y (green), Z (blue)
- Coordinate display showing world vs local frame
- Ground plane grid with axis labels
- Origin marker with coordinate triplet

#### 3.5 Yaw, Pitch, Roll Control
- Three rotation sliders:
  - Yaw (Z-axis rotation): -180° to +180°
  - Pitch (X-axis rotation): -90° to +90°
  - Roll (Y-axis rotation): -180° to +180°
- Visual orientation rings around end effector
- Real-time rotation of end effector in 3D view
- Quaternion and Euler angle readout
- Interactive mode: click and drag on end effector to rotate

### User Interactions

**Mouse Controls:**
- Left click + drag: Rotate camera around robot
- Right click + drag: Pan camera
- Scroll wheel: Zoom in/out
- Click on robot joint: Highlight and show joint info

**Keyboard Shortcuts:**
- `R`: Reset view
- `G`: Toggle grid
- `L`: Toggle labels
- `1-4`: Switch mode tabs
- `Space`: Toggle animation

### Data Handling
- All state managed in JavaScript
- No backend required
- Optional: LocalStorage to save/restore last position

### Edge Cases
- Prevent robot self-collision (clamp positions)
- Smooth clamping when reaching joint limits
- Handle window resize gracefully
- Fallback for WebGL not supported

---

## 4. Acceptance Criteria

### Visual Checkpoints
- [ ] Dark theme with teal/orange accents renders correctly
- [ ] 3D robot arm visible with 6 distinct segments
- [ ] Grid floor visible with axis colors
- [ ] All three mode tabs functional and switch views
- [ ] Sliders have custom styling with glow effects

### Functional Checkpoints
- [ ] Camera orbit/pan/zoom works smoothly
- [ ] Cartesian sliders move end effector to target position
- [ ] Payload slider shows/hides and scales payload cube
- [ ] Payload color changes at correct thresholds
- [ ] Yaw/Pitch/Roll sliders rotate end effector correctly
- [ ] Axis orientation arrows update with end effector rotation
- [ ] Reset button returns to default view
- [ ] Info panel shows accurate real-time values

### Performance
- [ ] 60fps animation on modern browsers
- [ ] No console errors on load
- [ ] Responsive layout works at all breakpoints
