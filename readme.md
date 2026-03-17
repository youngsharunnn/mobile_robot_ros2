# Mobile Robot Simulation

Differential drive robot simulation in Gazebo with custom race track.

## Prerequisites

- ROS 2 Jazzy
- Gazebo Sim 8 (Harmonic)
- Ubuntu 24.04

Install dependencies:
```bash
sudo apt install ros-jazzy-ros-gz-sim ros-jazzy-ros-gz-bridge ros-jazzy-xacro ros-jazzy-robot-state-publisher
```

## Project Structure
```
mobile_robot/
├── model/
│   ├── robot.xacro          # Robot URDF definition
│   └── robot.gazebo         # Gazebo plugins
├── worlds/
│   ├── empty.sdf            # Basic world
│      
├── parameters/
│   └── bridge_parameters.yaml
└── launch/
    └── gazebo_model.launch.py
```

## Build
```bash
cd mobile_robot_ws
colcon build
source install/setup.bash
```

## Run

Launch simulation:
```bash
ros2 launch mobile_robot gazebo_model.launch.py
```

Open Gazebo GUI (in another terminal):
```bash
gz sim -g
```

Control robot with keyboard:
```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

## Robot Specs

- Body: 1m x 0.6m x 0.3m (red)
- Wheels: 0.15m radius (yellow, 2x drive wheels)
- Caster: 0.15m radius (blue, rear)
- Controller: Differential drive

## Controls

- `i` - forward
- `k` - stop
- `j` - turn left
- `l` - turn right
- `u/o/m/,` - diagonals
- `q/z` - increase/decrease speed

## Troubleshooting

**Robot not visible:** Check spawn position in launch file (spawn_z value)

**No movement:** Verify bridge is running:
```bash
ros2 topic list | grep cmd_vel
```

**Build errors:** Clean and rebuild:
```bash
rm -rf build/ install/ log/
colcon build
```
