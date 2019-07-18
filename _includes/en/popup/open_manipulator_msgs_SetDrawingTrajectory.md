---
layout: popup
---

- File: `open_manipulator_msgs/SetDrawingTrajectory.srv`

- Service Definition
 ```c
string end_effector_name
string drawing_trajectory_name
float64[] param
float64 path_time
---
bool is_planned
```

- Description
This service creates a drawing trajectory.

  - Request
    * `string end_effector_name`
&emsp;&emsp; End-Effector name which is relative to the base frame

    * `string drawing_trajectory_name`
&emsp;&emsp; The name of the drawing trajectory type. (line, circle, heart, rhombus)

    * `float64[] param`
&emsp;&emsp; Parameters required for the drawing trajectory generation.

    * `float64 path_time`
&emsp;&emsp; Total time of the trajectory.

  - Response
    * `bool is_planned`
&emsp;&emsp; Whether the path is created.
