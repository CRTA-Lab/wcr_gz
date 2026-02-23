# WCR Robot - ROS2 Workspace

A comprehensive ROS2 workspace for a WCR 4WIS4WID with advanced control algorithms, simulation capabilities, and odometry estimation.

## 📋 Overview

This workspace contains a complete robot system implementation including URDF description, Gazebo simulation, multiple control strategies, odometry estimation, and launch configurations for WCR 4WIS4WID robot with steering capabilities.

## 🏗️ Package Structure

### `wcr_description`
Robot description package containing URDF/Xacro models and visualization configurations.

**Features:**
- Complete robot URDF model with configurable parameters
- Multiple ros2_control hardware interface configurations:
- Gazebo world files and simulation plugins
- RViz configuration files for visualization
- Robot meshes and visual assets

**Launch Files:**
- `display.launch.py` - Visualize robot in RViz
- `gazebo.launch.py` - Launch robot in Gazebo simulation

### `wcr_controllers`
[Custom controller implementations](https://github.com/BCaran/wcr_controllers) for trajectory tracking and motion control.

**Controllers:**
- **Model-Based Controllers:**
  - `model_based_controller.cpp` - Full model-based trajectory follower
  - `model_based_controller_velocity.cpp` - Velocity-based model controller
  - `reduced_model_based_controller_velocity.cpp` - Simplified model controller
- **Torque Controllers:**
  - `torque_model_based_controller.cpp` - Torque-based control
  - `simple_torque_model_based_controller.cpp` - Simplified torque control
- **Inverse Kinematics:**
  - `inv_kin_controller.cpp` - Inverse kinematics solver
- **Utilities:**
  - `trajectory_generator.cpp` - Path and trajectory generation
  - `mimic_help_controller.cpp` - Helper for mimic joints

### `wcr_control`
ROS2 control configuration and controller management.

**Features:**
- Controller manager configuration
- ros2_control parameter files
- Integration with ros2_controllers
- Joint state broadcaster setup
- Forward command controller configuration

**Launch Files:**
- `controller.launch.py` - Start controller manager and load controllers

### `wcr_odometry`
[Odometry estimation node](https://github.com/BCaran/wcr_odometry) for robot state feedback.

**Features:**
- Wheel odometry calculation
- Robot pose estimation
- TF publishing
- Sensor fusion (if applicable)

### `wcr_launcher`
Unified launch package for starting the complete robot system.

**Features:**
- Centralized launch configuration
- YAML-based parameter management
- Conditional launching
- Namespace management
- Robot state publisher integration

**Configuration:**
- `config/robot_params.yaml` - Robot physical parameters:
  - Chassis dimensions (225mm x 225mm) and mass (3.0 kg)
  - Steering system parameters
  - Wheel specifications
  - Propeller configuration
  - EDF (Electric Ducted Fan) parameters
  - Inertia properties

**Launch Files:**
- `launcher.launch.py` - Main launch file for the complete system

## 🚀 Getting Started

### Prerequisites

- ROS2 (Humble/Iron/Rolling recommended)
- Gazebo (for simulation)
- ros2_control and ros2_controllers
- Python 3.8+
- CMake and build tools

### Installation

1. **Clone the repository:**
   ```bash
   cd ~/ros2_ws/src
   git clone <repository-url>
   ```

2. **Install dependencies:**
   ```bash
   cd ~/ros2_ws
   rosdep install --from-paths src --ignore-src -r -y
   ```

3. **Build the workspace:**
   ```bash
   cd ~/ros2_ws
   colcon build
   ```

4. **Source the workspace:**
   ```bash
   source install/setup.bash
   ```

## 🎮 Usage

### Launch the Complete System

**Gazebo:**
```bash
ros2 launch wcr_launcher launcher.launch.py
```

## 🔧 Configuration

### Robot Parameters

Edit [config/robot_params.yaml](wcr_launcher/config/robot_params.yaml) to modify:
- Robot dimensions and mass
- Wheel and steering specifications
- Motor effort and velocity limits
- Inertia parameters
- Propeller and EDF configurations

### Controller Selection

Choose the appropriate ros2_control configuration in your URDF by including the desired xacro file:
- For position/velocity: `wcr_classic.ros2_control.xacro`
- For pure velocity: `wcr_velocity.ros2_control.xacro`
- For torque control: `wcr_effort.ros2_control.xacro`
- For testing/simulation: `mock_wcr_classic.ros2_control.xacro`

## 📚 Additional Resources

- [ROS2 Documentation](https://docs.ros.org/en/humble/index.html)
- [gz_ros2_control Documentation](https://control.ros.org/humble/doc/gz_ros2_control/doc/index.html)
- [Gazebo Documentation](https://gazebosim.org/docs/fortress/getstarted/)

