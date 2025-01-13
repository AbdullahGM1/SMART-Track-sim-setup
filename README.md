# 🚀 SMART-Track Simulation Setup Guide

## 📋 Prerequisites

> **Important:** Install and Use [SMART-TRACK Docker Image](https://github.com/mzahana/SMART-TRACK/tree/main/docker), and follow all the steps.

## 🛠️ Installation Steps

### 1. Initial Setup
1. Access the `smart_track` container and navigate to `/shared_volume`

2. Inside the container, excute the following commands to install SMART-TRACK packages:
```bash
# Execute the following step, if you have not created the ros2_ws already
mkdir -p ros2_ws/src
cd ros2_ws/src
git clone https://github.com/mzahana/SMART-TRACK.git smart_track
cd smart_track
./install.sh
```

> Make sure that the installation script is completed without issues. 

### 2. Additional Packages
Clone these packages into `/shared_volume/ros2_ws/src`:
* [l2d_detection](https://github.com/AbdullahGM1/l2d_detection)
* [l2i_fusion_detection](https://github.com/AbdullahGM1/l2i_fusion_detection/tree/main)
* [yolo_ros](https://github.com/AbdullahGM1/yolo_ros)
* [SMART-Track-sim-setup](https://github.com/AbdullahGM1/SMART-Track-sim-setup.git)

> ### Follow the packages instlation process


## 🔧 Building the Packages

### 1. Build YOLO Messages & Yolo Ros
```bash
cd ~/ros2_ws
colcon build --packages-select yolo_msgs
colcon build --packages-select yolo_ros  
```

### 2. Build l2i Fusion Detection package
```bash
colcon build --packages-select l2i_fusion_detection
```
### 3. Build l2d Detection package
```bash
colcon build --packages-select l2d_detection
```
### 4. Source:
```bash
source install/setup.bash
```

## ⚙️ Environment Configuration

### 1. World Setup
1. Navigate to the worlds directory:
```bash
cd /d2dtracker_cuda_shared_volume/PX4-Autopilot/Tools/simulation/gz/worlds
```
2. Add the provided world file

### 2. Model Setup
1. Navigate to the models directory:
```bash
cd /d2dtracker_cuda_shared_volume/PX4-Autopilot/Tools/simulation/gz/models
```
2. Add the provided models file

### 3. Airframe Configuration
1. Add `4022_gz_x500_lidar_camera` to:
```bash
d2dtracker_cuda_shared_volume/PX4-Autopilot/ROMFS/px4fmu_common/init.d-posix/airframes
```

2. Update CMakeLists.txt:
   * Location: `/d2dtracker_cuda_shared_volume/PX4-Autopilot/ROMFS/px4fmu_common/init.d-posix/airframes/CMakeLists.txt`
   * Add `4022_gz_x500_lidar_camera` to the list
   * ⚠️ **Important:** Maintain the existing file sequence order

### 4. Build PX4
Execute in `/shared_volume/PX4-Autopilot`:
```bash
make px4_sitl
```
