---
layout: archive
lang: en
ref: thormang3_getting_started
read_time: true
share: true
author_profile: false
permalink: /docs/en/platform/thormang3/getting_started/
sidebar:
  title: THORMANG3
  nav: "thormang3"
---

<div style="counter-reset: h1 2"></div>

# [Getting Started](#getting-started)

## [OS Install](#os-install)

Ubuntu 16.04 LTS is installed on PCs in the THORMANG3 and the PC for Remote Control Version.

**NOTE** : [Install Ubuntu Desktop]
{: .notice}


## [Network Setting](#network-setting)

This section explains how to configure the network for MPC(Motion PC) and PPC(Perception PC) of the robot, as well as the Wi-Fi switch and the OPC(Operating PC).

![](/assets/images/platform/thormang3/THORMANG3_network_map.png)

### [Access Point Setting](#access-point-setting)

#### Access Point(AP) Information

- Model : D-Link DIR-806A
- Account
  - user : admin
  - password : admin

    `Reference` [DIR-806A Product Manual]
    {: .notice}

#### AP Server

- Router Mode(Orange light)
- IP Address : 10.17.3.1
- WiFi Name (2.4G) : THORMANG-Sxx (xx : number)
- WiFi Name (5G) : THORMANG-Sxx-5G (xx : number)
- WiFi Password : 11111111

#### AP in THORMANG3
- Repeater Mode(Green light)


### [PC Setting](#pc-setting)

#### MPC (Motion PC)
- IP Address : 10.17.3.30
- Netmask : 255.255.255.0
- Gateway : 10.17.3.1

#### PPC (Perception PC)
- IP Address : 10.17.3.35
- Netmask : 255.255.255.0
- Gateway : 10.17.3.1

#### OPC (Operating PC)
- IP Address : 10.17.3.100
- Netmask : 255.255.255.0
- Gateway : 10.17.3.1


## [ROS Install](#ros-install)

ROS(Robot Operating System) is required in order to control THORMANG3. Currently THORMANG3 is developed and tested with Kinetic Kame version of ROS.

**NOTE** : [Install ROS]
{: .notice}

## [ROS Environment Setting](#ros-environment-setting)

**NOTE** : [Environment Setting Reference]
{: .notice}

**NOTE** : [ROS Network Setup Reference]
{: .notice}

### [Network Setting Example](#network-setting-example)

Above configuration has to be repeatedly done whenever a new terminal window is created. The following method will load configuration file when creating a terminal window. ROS Network setup is also performed when the configuration file is loaded.

#### System configuration

- PPC(Perception PC) : core PC
  - IP : 10.17.3.35
- MPC(Motion PC)
  - IP : 10.17.3.30
- OPC(Operation PC)
  - IP : 10.17.3.100

#### Example setting for PPC

1. Open the bash file with an editor to apply configuration.
    ```
    $ gedit ~/.bashrc
    ```

2. Append below contents at the end of the .bashrc file.
    ```
    # Set ROS Kinetic
    source /opt/ros/kinetic/setup.bash
    source ~/catkin_ws/devel/setup.bash

    ##### Set ROS Network ####
    # PPC CORE(10.17.3.35)
    export ROS_MASTER_URI=http://10.17.3.35:11311

    # local ROS IP
    export ROS_IP=10.17.3.35
    ```

3. Use below command to apply modified configuration or open a new terminal window.
    ```
    $ source ~/.bashrc
    ```

#### Example setting for MPC

1. Open the bash file with an editor to apply configuration.
    ```
    $ gedit ~/.bashrc
    ```

2. Append below contents at the end of the .bashrc file.
    ```
    # Set ROS Kinetic
    source /opt/ros/kinetic/setup.bash
    source ~/catkin_ws/devel/setup.bash

    ##### Set ROS Network ####
    # PPC CORE(10.17.3.35)
    export ROS_MASTER_URI=http://10.17.3.35:11311

    # local ROS IP
    export ROS_IP=10.17.3.30
    ```

3. Use below command to apply modified configuration or open a new terminal window.
    ```
    $ source ~/.bashrc
    ```

#### [Example setting for OPC](#example-setting-for-opc)

1. Open the bash file with an editor to apply configuration.
    ```
    $ gedit ~/.bashrc
    ```

2. Append below contents at the end of the .bashrc file.
    ```
    # Set ROS Kinetic
    source /opt/ros/kinetic/setup.bash
    source ~/catkin_ws/devel/setup.bash

    ##### Set ROS Network ####
    # PPC CORE(10.17.3.35)
    export ROS_MASTER_URI=http://10.17.3.35:11311

    # local ROS IP
    export ROS_IP=10.17.3.100
    ```

3. Use below command to apply modified configuration or open a new terminal window.
    ```
    $ source ~/.bashrc
    ```

### [Time Synchronization](#time-synchronization)

In order to run the ROS on multiple PCs, each PC clock has to be synchronized. The following script file comes in handy for this synchronization procedure. PPC time becomes the reference for synchronization, and perform below procedures only for MPC and OPC.

1. Create the script file with an editor.
    ```
    $ gedit ~/timesync
    ```

2. Copy and paste below contents to the script file
    ```
    #! /bin/sh
    sudo date --set='-2 secs'
    sudo ntpdate 10.17.3.35
    sudo hwclock -w
    PPC(10.17.3.35)
    ```

3. Modify the script file permission(Add execute permission)
    ```
    $ sudo chmod +x timesync
    ```

4. Run the script file to sync time for PPC, MPC and OPC.
    ```
    $ ~/timesync
    ```

  - If NTP socket is running, Stop the ntp service and sync time.
      ```
      $ sudo service ntp stop
      $ ~/timesync
      ```

## [ROBOTIS ROS Package Install](#robotis-ros-package-install)

This section introduces how to install the ROBOTIS ROS Package for THORMANG3.

- ROBOTIS-Framework : DXL SDK based Framework for ROBOTIS platforms
- ROBOTIS-Framework-msgs : ROS Messages used in the ROBOTIS-Framework
- ROBOTIS-Math : Math library for THORMANG3
- ROBOTIS-THORMANG-MPC : ROS Packages for the Motion PC of THORMANG3(DXL PRO Ver.)
- ROBOTIS-THORMANG-P-MPC : ROS Packages for the Motion PC of THORMANG3(DXL PRO+ Ver.)
- ROBOTIS-THORMANG-MPC-SENSORs : ROS Packages of sensors that is controled the Motion PC of THORMANG3 
- ROBOTIS-THORMANG-PPC : ROS Packages for the Perception PC of THORMANG3
- ROBOTIS-THORMANG-OPC : ROS Packages for the Operating PC of THORMANG3
- ROBOTIS-THORMANG-Common : Common ROS Packages for THORMANG3
- ROBOTIS-THORMANG-msgs : ROS Messages used in the ROBOTIS THORMANG3 packages
- ROBOTIS-THORMANG-Tools
- ROBOTIS-Utility

### [MPC Installation](#mpc-installation)

Install the ROBOTIS ROS Package from the MPC. The ROS Package is installed by default.  
{% capture package_warning %}   
**CAUTION** : The packages to download differ depending on the version of ROBOTIS THORMANG3.  
{% endcapture %}
<div class="notice--warning">{{ package_warning | markdownify }}</div> 


#### [THORMANG3 WITH DYNAMIXEL PRO](#thormang3-with-dynimixel-pro)
1. Download Packages from GitHub to the source folder in the catkin workspace.  
  

    ```
    $ cd ~/catkin_ws/src
    $ git clone https://github.com/ROBOTIS-GIT/DynamixelSDK.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Math.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Framework.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Framework-msgs.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-MPC.git    
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-MPC-SENSORs.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-Common.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-msgs.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-Tools.git
    ```  
    
    
2. After installing all dependent packages, go to the workspace and build.  
    ```
    $ cd ~/catkin_ws
    $ catkin_make
    ```
    
3. Find *ft_calibration_data.yaml* and *ft_data.yaml* from provided USB and copy them to the proper folder.  
    
    `thormang3_manager/config/`  

#### [THORMANG3 WITH DYNAMIXEL PRO+](#thormang3-with-dynimixel-proplus)
  
1. Download Packages from GitHub to the source folder in the catkin workspace.    

    ```
    $ cd ~/catkin_ws/src
    $ git clone https://github.com/ROBOTIS-GIT/DynamixelSDK.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Math.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Framework.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Framework-msgs.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-P-MPC.git    
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-MPC-SENSORs.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-Common.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-msgs.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-Tools.git
    ```  

2. After installing all dependent packages, go to the workspace and build.  
    
    ```
    $ cd ~/catkin_ws
    $ catkin_make
    ```

3. Find *ft_calibration_data.yaml* and *ft_data.yaml* from provided USB and copy them to the proper folder.  

    `thormang3_p_manager/config/`  

### [PPC Installation](#ppc-installation)

Install the ROBOTIS ROS Package from the PPC. The ROS Package is installed by default.

1. Download Packages from GitHub to the source folder in the catkin workspace.
    ```
    $ cd ~/catkin_ws/src
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Framework-msgs.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-msgs.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-PPC.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Utility.git
    ```

2. After installing all dependent packages, go to the workspace and build.  
    ```
    $ cd ~/catkin_ws
    $ catkin_make  
    ```

### [OPC Installation](#opc-installation)

Install the ROBOTIS ROS Package from the OPC.

1. Download Packages from GitHub to the source folder in the catkin workspace.
    ```
    $ cd ~/catkin_ws/src
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Framework-msgs.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Math.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-OPC.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-msgs.git
    $ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-Common.git
    ```

2. After installing all dependent packages, go to the workspace and build.   

    ```
    $ sudo apt install ros-kinetic-sbpl
    $ sudo apt install ros-kinetic-map-server
    $ sudo apt install ros-kinetic-humanoid-nav-msgs
    $ sudo apt install ros-kinetic-octomap ros-kinetic-octomap-msgs ros-kinetic-octomap-ros ros-kinetic-octomap-server
    $ sudo apt install ros-kinetic-qt-ros
    $ cd ~/catkin_ws/src
    $ git clone https://github.com/ROBOTIS-GIT/humanoid_navigation.git
    $ cd ~/catkin_ws
    $ catkin_make  
    ```

- Dependencies Package contains ..  
  - qt-ros  
  - map_server   
  - nav_msgs  
  - humanoid_nav_msgs  
  - sbpl  
  - octomap-ros  
    
**INFO** : If  `libGL` in 64bit Ubuntu has a problem, refer to [Trouble Shooting](http://techtidings.blogspot.kr/2012/01/problem-with-libglso-on-64-bit-ubuntu.html).
{: .notice--info}



### [Update](#update)

When the source is modified, update & build is necessary.

1. Go to the folder where source is copied and run the pull command.(ex : ROBOTIS-THORMANG-OPC)
    ```
    $ cd ~/catkin_ws/src/ROBOTIS-THORMANG-OPC
    $ git pull
    ```

2. Build
    ```
    $ cd ~/catkin_ws
    $ catkin_make
    ```

## [Additional ROS Package Install](#additional-ros-package-install)

The followings are required ROS Packages for THORMANG3 when installing desktop-full.

### [ROS Packages for MPC](#ros-packages-for-mpc)

Install below ROS Packages from the MPC. The Package is installed by default.

#### urg_node : ROS Package for Lidar
```
$ sudo apt install ros-kinetic-urg-node
```

`Reference` : [http://wiki.ros.org/urg_node]
{: .notice}

### [ROS Packages for PPC](#ros-packages-for-ppc)
Install the below ROS Package from the PPC. The Package is installed by default.

#### uvc_camera : ROS Package for USB camera
```
$ sudo apt install libv4l-dev
$ sudo apt install ros-kinetic-uvc-camera
```

`Reference` : [http://wiki.ros.org/uvc_camera]
{: .notice}

#### realsense
`Reference` : [http://wiki.ros.org/RealSense]
{: .notice}

#### ros_madplay_player, ros_mpg321_player  
```
$ sudo apt install madplay mpg321
```


[Install Ubuntu Desktop]: http://www.ubuntu.com/download/desktop/install-ubuntu-desktop
[DIR-806A Product Manual]: ftp://ftp.dlink.ru/pub/Router/DIR-806A/Data_sh/
[Install ROS]: http://wiki.ros.org/kinetic/Installation/Ubuntu
[Environment Setting Reference]: http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment
[ROS Network Setup Reference]: http://wiki.ros.org/ROS/NetworkSetup
[sbpl install instruction]: https://github.com/sbpl/sbpl

[http://wiki.ros.org/urg_node]:http://wiki.ros.org/urg_node
[http://wiki.ros.org/RealSense]:http://wiki.ros.org/RealSense
[http://wiki.ros.org/uvc_camera]:http://wiki.ros.org/uvc_camera
[http://wiki.ros.org/RealSense]:http://wiki.ros.org/RealSense
