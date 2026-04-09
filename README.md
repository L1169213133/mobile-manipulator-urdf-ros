# Mobile Manipulator URDF ROS

## 项目简介
本项目是一个完整的机器人建模与仿真实验，实现了**移动操作机器人**（Mobile Manipulator）的URDF建模与ROS可视化。该机器人由移动底盘（带激光雷达）和6自由度机械臂组成，通过ROS Noetic平台进行建模、仿真和可视化。
### 核心功能
- URDF模型整合（移动底盘 + 机械臂 + 末端夹爪）
- RVIZ三维可视化
- 关节坐标轴标注（TF坐标系）
- 图形化关节控制（joint_state_publisher_gui）
- 完整的TF树构建

## 项目结构
```
composite_robot_description/
├── urdf/
│ └── mobile_manipulator.urdf # 核心URDF模型文件
├── launch/
│ └── display_composite_robot.launch # 启动文件
├── rviz/
│ └── RVIZ.rviz # RVIZ配置文件
├── frames.pdf/ # TF树文件
└── 20257007-李振-机器人建模与仿真.doc/ # 实验报告
```
## 环境要求
- **操作系统**: Ubuntu 20.04 LTS
- **ROS版本**: ROS Noetic
- **虚拟化平台**: VMware Workstation 16 Player（推荐）
- **内存**: ≥ 4GB（虚拟机分配）
- **3D加速**: 已启用
  
### 依赖包安装
```bash
# 安装基础ROS包
sudo apt-get update
sudo apt-get install ros-noetic-desktop-full
# 安装项目所需依赖
sudo apt-get install ros-noetic-robot-state-publisher \
                     ros-noetic-joint-state-publisher \
                     ros-noetic-joint-state-publisher-gui \
                     ros-noetic-rviz \
                     ros-noetic-xacro \
                     ros-noetic-check-urdf
```
## 机器人模型说明
1. 组成部分
| 部件 | 结构类型 | 关节数量 | 关节类型 | 颜色 |
|------|----------|----------|----------|------|
| 移动底盘 | 圆柱形 | 4 | 2个连续关节 + 2个固定关节 | 黄色 |
| 激光雷达 | 柱状 | 1 | 固定关节 | 黑色 |
| 机械臂 | 串联机械臂 | 6 | 旋转关节 | 蓝白相间 |
| 末端夹爪 | 二指夹爪 | 1 | 平移关节 | 蓝色 |
2. 关键参数
```xml
<!-- 机械臂安装位置 -->
<joint name="arm_base_joint" type="fixed">
    <parent link="base_link"/>
    <child link="arm_base_link"/>
    <origin xyz="0 0 0.12" rpy="0 0 0"/>
</joint>
```
3. TF树结构
```
base_link (移动底盘)
├── left_wheel_link
├── right_wheel_link
├── front_caster_link
├── back_caster_link
├── laser_link
└── arm_base_link (机械臂底座)
    └── link1 → link2 → link3 → link4 → link5 → link6
        └── gripper_finger_link1/2
```
## 项目截图
<center>
机器人模型可视化
<center>
<img width="363" height="659" alt="机器人模型图" src="https://github.com/user-attachments/assets/e7e11bd7-0573-4bb3-8ad8-d0f9c8b5a101" />
<center>
关节坐标轴标注
<center>
<img width="363" height="659" alt="机器人关节坐标轴图" src="https://github.com/user-attachments/assets/39050dba-ea94-4e08-a6ad-8383310ccd37" />
<center>
关节交互控制
<center>
![机器人关节运动测试](https://github.com/user-attachments/assets/c6e9bc6d-0059-4637-becf-1001267f8061)

作者信息<br>
姓名: 李振<br>
学号: 20257007<br>
专业: 智能科学与技术<br>
学校: 上海电力大学<br>
课程: 机器人仿真与编程技术<br>
