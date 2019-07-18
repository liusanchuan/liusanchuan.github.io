---
layout: archive
lang: en
ref: dynamixel_sdk_download
read_time: true
share: true
author_profile: false
permalink: /docs/en/software/dynamixel/dynamixel_sdk/download/
sidebar:
  title: DynamixelSDK
  nav: "dynamixel_sdk"
---

<div style="counter-reset: h1 1"></div>

# [Download](#download)

## [Repository](#repository)

- Download Cross-compilable, all-in-one SDK for ROBOTIS Dynamixel from the [ROBOTIS Open Source Repository](https://github.com/ROBOTIS-GIT/DynamixelSDK).
- To use the latest version of Dynamixel SDK, you can download it from the terminal of Linux or macOS with the command `git clone` or directly from the repository.
- If you are an ROS user, you can install the ROS library and Python module for Dynamixel SDK directly.
- You can use one of the three methods below.

1) Git command
  
  ```
  $ git clone https://github.com/ROBOTIS-GIT/DynamixelSDK.git
  ```
  
2) Direct Download
- [DynamixelSDK-3.xx.yy.zip](https://github.com/ROBOTIS-GIT/DynamixelSDK/releases)

3) Install ROS library (C++ library and Python module)

  ```
  $ sudo apt-get install ros-[ROS Distribution]-dynamixel-sdk
  ```

## [File Structure](#file-structure)

The example codes are using either C or C++ version dll. Extract zip file, you can see the folders shown below.

![](/assets/images/sw/sdk/dynamixel_sdk/overview/dynamixel_sdk_language_map.png)

Open C++ folder, for instance, you would see 4 folders which contain cpp source files, header files, build files and example codes. 

![](/assets/images/sw/sdk/dynamixel_sdk/overview/dynamixel_sdk_library_struct.png)

Though the `PortHandler` which handles system communication environment is separated in three OS, the Linux, the macOS and the Windows, the other sources are made to be able to be cross-compiled. Basically, `Makefile` or `Microsoft Visual Studio` is used for each environment of 32bit or 64bit platform respectively. Example codes using library files(.dll, .so, .dylib) show how to use SDK functions to control one or more Dynamixels.  

![](/assets/images/sw/sdk/dynamixel_sdk/overview/dynamixel_sdk_sample_struct.png)

Each example folder also has the build files which are for Linux, macOS or Windows, 32bit or 64bit platform. Make library file before you run the example codes. The ReadWrite example code can control and read Dynamixel position.

The example sources coded with C# / Java / MATLAB / LabVIEW are not using library functions coded with the language of themselves but using the `.dll`, `.so` or `.dylib` which are built previously by C language coded source. 

![](/assets/images/sw/sdk/dynamixel_sdk/overview/dynamixel_sdk_language_struct.png)

You can find out how to run the examples in the Dynamixel SDK sources at [here](/docs/en/software/dynamixel/dynamixel_sdk/sample_code/c_read_write_protocol_1_0/#sample-code)
