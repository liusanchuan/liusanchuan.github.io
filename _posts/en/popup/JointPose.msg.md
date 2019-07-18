---
layout: popup
---

- File: `manipulation_module_msgs/JointPose.msg`

- Message Definition
 ```
 string    name
 float64   value
 float64   time
 ```

- Description
A message to move to a specific target point in the Joint Space.
If the time is set to 0, the speed is automatically configured proportional to the moving distance.

    * `name`
&emsp;&emsp; target joint name
    * `value`
&emsp;&emsp; target joint value
    * `time`
&emsp;&emsp; movement time to reach the target value
