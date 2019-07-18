---
layout: popup
---

- File: `thormang3_walking_module_msgs/AddStepDataArray.srv`

- Message Definition
 ```
 bool       auto_start
 bool       remove_existing_step_data
 StepData[] step_data_array
 ---
  int32 result
 ```


- Description
A service to add StepData to [thormang3_walking_module].

  - Request
    * `bool       auto_start`
&emsp;&emsp; A flag to initiate walking after adding StepData.
    * `bool       remove_existing_step_data`
&emsp;&emsp; A flag to delete existing StepData.
    * `StepData[] step_data_array`([thormang3_walking_module_msgs/StepData])
&emsp;&emsp; An array of StepData to be added

 &emsp;
  - Response
    * ` int32 result`
&emsp;&emsp; Result of the "AddStepDataArray" Service
&emsp;&emsp; Walking will be enabled only with NO_ERRROR result.

| Name                       | Value | Description                                    |
|----------------------------|-------|------------------------------------------------|
| NO_ERROR                   | 0x00  | There is no error.                             |
| NOT_ENABLED_WALKING_MODULE | 0x02  | The thormang3_walking_module is not enabled.   |
| PROBLEM_IN_POSITION_DATA   | 0x04  | There is some problem in "Step Time Data".     |
| PROBLEM_IN_TIME_DATA       | 0x08  | There is some problem in "Step Position Data". |
| ROBOT_IS_WALKING_NOW       | 0x400 | The Thormang3 is walking now.                  |

[thormang3_walking_module]: /docs/en/platform/thormang3/thormang3_ros_packages/#thormang3_walking_module
[thormang3_walking_module_msgs/StepData]: /docs/en/platform/msgs/StepData_msg/#stepdata-msg
