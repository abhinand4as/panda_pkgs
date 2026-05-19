# panda_pkgs

ROS2 (Jazzy) packages for the Franka Emika Panda robot — URDF description and MoveIt2 configuration.

## Packages

| Package | Description |
|---|---|
| `panda_description` | URDF model, meshes (visual + collision), and robot description resources |
| `panda_moveit_config` | MoveIt2 configuration — SRDF, kinematics, planners (OMPL, CHOMP, Pilz, STOMP), and controllers |

## Prerequisites

- ROS2 Jazzy
- MoveIt2
- `moveit_configs_utils`
- `ros2_control`

## Build

```bash
cd ~/myws/robotics/pandas_ws
colcon build --packages-select panda_description panda_moveit_config
source install/setup.bash
```

## Usage

Launch the full MoveIt2 demo with RViz (uses mock hardware by default):

```bash
ros2 launch panda_moveit_config demo.launch.py
```

### Launch arguments

| Argument | Default | Description |
|---|---|---|
| `ros2_control_hardware_type` | `mock_components` | Hardware interface type (`mock_components` or `isaac`) |
| `rviz_config` | `rviz/moveit.rviz` | Path to RViz config file |
| `db` | `False` | Start MongoDB warehouse server |

### moveit.launch.py

A standalone launch file that brings up the full MoveIt2 stack without the demo extras — move group, RViz, static TF, robot state publisher, `ros2_control`, and all three controller spawners (`joint_state_broadcaster`, `panda_arm_controller`, `panda_hand_controller`):

```bash
ros2 launch panda_moveit_config moveit.launch.py
```

| Argument | Default | Description |
|---|---|---|
| `ros2_control_hardware_type` | `mock_components` | Hardware interface type (`mock_components` or `isaac`) |
| `rviz_config` | `rviz/moveit.rviz` | Absolute path to a custom RViz config file |

To supply a custom RViz config:

```bash
ros2 launch panda_moveit_config moveit.launch.py \
  rviz_config:=/home/abhinand/custom.rviz
```

## Kinematics

Default solver is KDL. Alternative solver configs are provided:

| Config file | Solver |
| --- | --- |
| `config/kinematics.yaml` | KDL (default) |
| `config/bio_ik_kinematics.yaml` | BioIK |
| `config/trac_ik_kinematics.yaml` | TRAC-IK |

## License

BSD
