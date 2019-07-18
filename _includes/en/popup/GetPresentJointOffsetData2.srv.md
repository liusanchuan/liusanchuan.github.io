---
layout: popup
---

- File: `thormang3_tuning_module_msgs/srv/GetPresentJointOffsetData.srv`

- Message Definition
 ```c
 ---
 JointOffsetPositionData[] present_data_array
 ```

- Description
The service to get offset data of each joint.

  - Request
    * `empty`

  - Response
    * `JointOffsetPositionData[] present_data_array`(thormang3_tuning_module_msgs/JointOffsetPositionData)
&emsp;&emsp; Array of the offset parameter data of each joint
