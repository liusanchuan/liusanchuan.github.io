---
layout: archive
lang: en
ref: csharp_windows
read_time: true
share: true
author_profile: false
permalink: /docs/en/software/dynamixel/dynamixel_sdk/library_setup/csharp_windows/
sidebar:
  title: DynamixelSDK
  nav: "dynamixel_sdk"
---

<div style="counter-reset: h1 4"></div>
<div style="counter-reset: h2 6"></div>

<!--[dummy Header 1]>
  <h1 id="library-setup"><a href="#library-setup">Library Setup</a></h1>
<![end dummy Header 1]-->

## [CSharp Windows](#csharp-windows)

For C#, only the Windows source is provided.

### [Compiler and Builder](#compiler-and-builder)

* [Download Visual Express for Windows Desktop](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx)

  ![](/assets/images/sw/sdk/dynamixel_sdk/library_setup/csharp/vs.png)

#### [Function References](#function-references)

* The function reference file is located in `[DynamixelSDK folder]/c#/dynamixel_functions_csharp/[winXX]/dynamixel.cs`

  ![](/assets/images/sw/sdk/dynamixel_sdk/library_setup/csharp/windows/library_file/1.png)

### [Building and Running the Sample Code](#building-and-running-the-sample-code)

Dynamixel SDK example code for C# uses the library files(.dll for Windows) built in C language.

Each released Dynamixel SDK have latest library files in:

`[DynamixelSDK folder]/c/build/[winXX]/output/dxl_xYY_c.dll`

which were built by its own source code.

* Open `read_write.sln` from `[DynamixelSDK folder]/C#/protocol2.0/read_write/win64/`

* Double click `ReadWrite.cs`

  ![](/assets/images/sw/sdk/dynamixel_sdk/library_setup/csharp/windows/sample_code/1.png)

* Adjust the values surrounded with red circle to proper value as shown in the comment. Then click `Start` in the Visual Studio toolbox above.

  ![](/assets/images/sw/sdk/dynamixel_sdk/library_setup/csharp/windows/sample_code/2.png)

* Console window will show the results

  ![](/assets/images/sw/sdk/dynamixel_sdk/library_setup/csharp/windows/sample_code/4.png)
