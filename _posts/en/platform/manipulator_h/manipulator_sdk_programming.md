---
layout: archive
lang: en
ref: manipulator_h_manipulator_sdk_programming
read_time: true
share: true
author_profile: false
permalink: /docs/en/platform/manipulator_h/manipulator_sdk_programming/
sidebar:
  title: MANIPULATOR-H
  nav: "manipulator_h"
---

<div style="counter-reset: h1 2"></div>

# [Manipulator SDK Programming](#manipulator-sdk-programming)

**ROBOTIS Manipulator SDK Download**  
[Manipulator H-32bit (zip)](http://en.robotis.com/service/download.php?no=58)  
[Manipulator L-32bit (zip)](http://en.robotis.com/service/download.php?no=59)  

## [Manipulator SDK](#manipulator-sdk)

- The ArmSDK is based on Window 7 OS and Visual Studio 2010.
- The ArmSDK trajectory is generated from the MotionPlay class’ instance and utilizes QueryPerformanceCounter. This requires the use of a thread, in which sharing said thread may reach to 100%.  
  It is highly recommended your PC is at least dual-core-based.
- The Numerical IK implements Damped Least Square Method to reach target by acquiring each joint’s angle. This allows joints to go from initial position to a point and then return to its initial pose.  
  This will allow you to perform tests to the Manipulator.     
- Preparation Before using Robotis Manipulator SDK.  
  The following are pre-requisites for the ArmSDK.  
  Eigen Package([http://eigen.tuxfamily.org], version 3.0.6 or Later)
- Installation Package
  - Download and unzip Eigen Package.
  - Start Visual Studio go to “Project Properties -> VC++ Directories -> Include Directories” set Eigen’s source directory.

    ![](/assets/images/platform/manipulator_h/manipulator_h_046.jpg)

    ![](/assets/images/platform/manipulator_h/manipulator_h_047.jpg)

    ![](/assets/images/platform/manipulator_h/manipulator_h_048.jpg)

  - Repeat procedure (i)~(ii) to include the examples and include directories.
  - Once preparations are complete press the F7 key to compile and build.

## [SDK Description](#sdk-description)

### RobotInfo
When building Manipulator at ARM SDK, you may use the Addjoint function after generating Instance of RobotInfo Class.  
AddJoint gets values from D-H Parameter and actuator’s max and min turn angle in rad and value as well as actuator ID number (min and max turn angles may not be the same as joint angle limits).

### Kinematics
Forward Kinematics(FK), Inverse Kinematics(IK) can be calculated once the instance for kinematics class is generated. Kinematics class get the instance from RobotInfo class.  
ComputeIK’s factor’s the pose from end effector and joint values, as well as, initial joint angle and error for IK. The result is joint angles when the returned error status is not 0 then the IK is not properly solved.

![](/assets/images/platform/manipulator_h/manipulator_h_070.png)

The Roll(&phi;), Pitch(&theta;) and Yaw(&psi;) are calculated as R<sub>x</sub>(&phi;), R<sub>y</sub>(&theta;), R<sub>z</sub>(&psi;) in the rotation transformation matrix. This is to be taken into consideration when entering the pose for ComputeIK.

### Trajectory Generating
The Trajectory Generator class generates an instance for the arm’s trajectory. The SDK’s  Point to Point, Linear, and Circular can generate a trajectory. For arm-only trajectory then only Set_PTP, Set_LIN, Set_Circular; for the gripper then Set_PTPwithHand, Set_LINwithHand, Set_CIRCwithHand.

### Velocity Profile
The SDK’s Velocity Profile does not take max velocity and max acceleration into consideration in the Trapezoidal Velocity Profile. The initial and final velocity are always set to 0. The following methods generate velocity profile in Joint Space and Cartesian Space, where both are independent of each other.

![](/assets/images/platform/manipulator_h/manipulator_h_071.png)

### Set_PTP
The Set_PTP function determines 2 poses for the manipulator (initial and final) by factoring in Trapezoidal Velocity Profile and receives velocity time and total time. Initial and final pose are in rad and joint angle in mm or rad (x, y, z, roll, pitch, yaw). When generating the trajectory it is recommended to factor in joint angles.

### Set_LIN
The Set_LIN function generates a 3-point coordinates for the robot’s straight trajectory. This factors in initial and final pose for Linear Euler Interpolation for orientation.

### Set_CIRC
The Set_CIRC function generates a 3-point coordinates for the robot’s circular trajectory. This factors in initial and final pose. It sets a point of origin in the area and proceeds to trajectory via MotionPlay and vector generation.

![](/assets/images/platform/manipulator_h/manipulator_h_072.png)

![](/assets/images/platform/manipulator_h/manipulator_h_073.png)

![](/assets/images/platform/manipulator_h/manipulator_h_074.png)

### Trajectory Following
When moving by the generated trajectory from TrajectorGenerator class’s instance just use NextStep function from MotionPlay. MotionPlay class accounts trajectoryGenerator class.  
The control period from MotionPlay default value is 8ms but can be changed with SetTimePeriod. If TimePeriod is 0 then 8ms default value is applied.

### Pro Arm Comm Win
Pro_Arm_Comm_Win utilizes DYNAMIXEL 2.0 Protocol from the Windows version of DYNAMIXEL SDK. Pro_Arm_Comm_Win’s functions utilizes DYNAMIXEL Pro’s control (i.e. read/write Control Table values).  
This is useful when writing separate code.

## [SDK Flowchart](#sdk-flowchart)

![](/assets/images/platform/manipulator_h/manipulator_h_075.jpg)

[http://eigen.tuxfamily.org]: http://eigen.tuxfamily.org
