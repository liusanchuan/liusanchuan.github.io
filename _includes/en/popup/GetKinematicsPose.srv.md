---
layout: popup
---

- File: `manipulation_module_msgs/GetKinematicsPose.srv`

- Service Definition
 ```
 string              group_name
 ---
geometry_msgs/Pose  group_pose
 ```

- Description
A service to read the pose of end effector from a specific kinematics group.

  - Request
    * `group_name`
&emsp;&emsp; Name of the specific kinematics group.

  - Response
    * `group_pose`
&emsp;&emsp; Pose of the specific kinematics group.
