---
layout: archive
lang: en
ref: python_ping_protocol_1_0
read_time: true
share: true
author_profile: false
permalink: /docs/en/software/dynamixel/dynamixel_sdk/sample_code/python_ping_protocol_1_0/
sidebar:
  title: DynamixelSDK
  nav: "dynamixel_sdk"
---

<div style="counter-reset: h1 5"></div>
<div style="counter-reset: h2 12"></div>
<div style="counter-reset: h3 4"></div>

<!--[dummy Header 1]>
  <h1 id="sample-code"><a href="#sample-code">Sample Code</a></h1>
  <h2 id="python-protocol-10"><a href="#python-protocol-10">Python Protocol 1.0</a></h2>
<![end dummy Header 1]-->

### [Python Ping Protocol 1.0](#python-ping-protocol-10)

- Description

  This example tries to ping Dynamixel and shows the model number received from Dynamixel. The example is commonly used to check for Dynamixel connection or to get model number to refer its specification.

- Available Dynamixel

  All series using protocol 1.0

#### Sample code Parts


```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

#
# ping.py
#
#  Created on: 2016. 6. 16.
#      Author: Ryu Woon Jung (Leon)
#

#
# *********     ping Example      *********
#
#
# Available Dynamixel model on this example : All models using Protocol 1.0
# This example is designed for using a Dynamixel MX-28, and an USB2DYNAMIXEL.
# To use another Dynamixel model, such as X series, see their details in E-Manual(support.robotis.com) and edit below variables yourself.
# Be sure that Dynamixel MX properties are already set as %% ID : 1 / Baudnum : 1 (Baudrate : 1000000 [1M])
#

import os, sys

if os.name == 'nt':
    import msvcrt
    def getch():
        return msvcrt.getch().decode()
else:
    import tty, termios
    fd = sys.stdin.fileno()
    old_settings = termios.tcgetattr(fd)
    tty.setraw(sys.stdin.fileno())
    def getch():
        return sys.stdin.read(1)

os.sys.path.append('../dynamixel_functions_py')             # Path setting

import dynamixel_functions as dynamixel                     # Uses Dynamixel SDK library

# Protocol version
PROTOCOL_VERSION            = 1                             # See which protocol version is used in the Dynamixel

# Default setting
DXL_ID                      = 1                             # Dynamixel ID: 1
BAUDRATE                    = 1000000
DEVICENAME                  = "/dev/ttyUSB0".encode('utf-8')# Check which port is being used on your controller
                                                            # ex) Windows: "COM1"   Linux: "/dev/ttyUSB0"

COMM_SUCCESS                = 0                             # Communication Success result value
COMM_TX_FAIL                = -1001                         # Communication Tx Failed

# Initialize PortHandler Structs
# Set the port path
# Get methods and members of PortHandlerLinux or PortHandlerWindows
port_num = dynamixel.portHandler(DEVICENAME)

# Initialize PacketHandler Structs
dynamixel.packetHandler()

dxl_comm_result = COMM_TX_FAIL                              # Communication result

# Open port
if dynamixel.openPort(port_num):
    print("Succeeded to open the port!")
else:
    print("Failed to open the port!")
    print("Press any key to terminate...")
    getch()
    quit()

# Set port baudrate
if dynamixel.setBaudRate(port_num, BAUDRATE):
    print("Succeeded to change the baudrate!")
else:
    print("Failed to change the baudrate!")
    print("Press any key to terminate...")
    getch()
    quit()


# Try to ping the Dynamixel
# Get Dynamixel model number
dxl_model_number = dynamixel.pingGetModelNum(port_num, PROTOCOL_VERSION, DXL_ID)
if dynamixel.getLastTxRxResult(port_num, PROTOCOL_VERSION) != COMM_SUCCESS:
    dynamixel.printTxRxResult(PROTOCOL_VERSION, dynamixel.getLastTxRxResult(port_num, PROTOCOL_VERSION))
elif dynamixel.getLastRxPacketError(port_num, PROTOCOL_VERSION) != 0:
    dynamixel.printRxPacketError(PROTOCOL_VERSION, dynamixel.getLastRxPacketError(port_num, PROTOCOL_VERSION))

print("[ID:%03d] ping Succeeded. Dynamixel model number : %d" % (DXL_ID, dxl_model_number))

# Close port
dynamixel.closePort(port_num)
```



#### Details

```python
import os, sys

if os.name == 'nt':
    import msvcrt
    def getch():
        return msvcrt.getch().decode()
else:
    import tty, termios
    fd = sys.stdin.fileno()
    old_settings = termios.tcgetattr(fd)
    tty.setraw(sys.stdin.fileno())
    def getch():
        return sys.stdin.read(1)

os.sys.path.append('../dynamixel_functions_py')             # Path setting

import dynamixel_functions as dynamixel                     # Uses Dynamixel SDK library
```

`getch()` gets the input which is for example code control.

`os.sys.path.append()` sets paths of function reference.

This example uses `dynamixel_functions` library as `dynamixel` imported from `dynamixel_functions_py` package.

```python
# Protocol version
PROTOCOL_VERSION            = 1                             # See which protocol version is used in the Dynamixel
```

Dynamixel uses either or both protocols: Protocol 1.0 and Protocol 2.0. Choose one of the Protocol which is appropriate in the Dynamixel.

```python
# Default setting
DXL_ID                      = 1                             # Dynamixel ID: 1
BAUDRATE                    = 1000000
DEVICENAME                  = "/dev/ttyUSB0".encode('utf-8')        # Check which port is being used on your controller
                                                            # ex) Windows: "COM1"   Linux: "/dev/ttyUSB0"
```

Here we set some variables to let you freely change them and use them to run the example code.

As the document previously said in [previous chapter](/docs/en/software/dynamixel/dynamixel_sdk/device_setup/#dynamixel), customize Dynamixel control table items, such as `DXL_ID` number, communication `BAUDRATE`, and the `DEVICENAME`, on your own terms of needs. In particular, `BAUDRATE` and `DEVICENAME` have systematical dependencies on your controller, so make clear what kind of communication method you will use.

```python
COMM_SUCCESS                = 0                             # Communication Success result value
COMM_TX_FAIL                = -1001                         # Communication Tx Failed
```

Each of the variables above show the meaning of the communication result value.

```python
# Initialize PortHandler Structs
# Set the port path
# Get methods and members of PortHandlerLinux or PortHandlerWindows
port_num = dynamixel.portHandler(DEVICENAME)
```

`portHandler()` function sets port path as `DEVICENAME` and get `port_num`, and prepares an appropriate functions for port control in controller OS automatically. `port_num` would be used in many functions in the body of the code to specify the port for use.

```python
# Initialize PacketHandler Structs
dynamixel.packetHandler()
```

`packetHandler()` function initializes parameters used for packet construction and packet storing.

```python
dxl_comm_result = COMM_TX_FAIL                              # Communication result
```

`dxl_comm_result` indicates which error has been occurred during packet communication.

```python
# Open port
if dynamixel.openPort(port_num):
    print("Succeeded to open the port!")
else:
    print("Failed to open the port!")
    print("Press any key to terminate...")
    msvcrt.getch()
    quit()
```

First, controller opens #`port_num` port to do serial communication with the Dynamixel. If it fails to open the port, the example will be terminated.

```python
# Set port baudrate
if dynamixel.setBaudRate(port_num, BAUDRATE):
    print("Succeeded to change the baudrate!")
else:
    print("Failed to change the baudrate!")
    print("Press any key to terminate...")
    msvcrt.getch()
    quit()
```

Secondly, the controller sets the communication `BAUDRATE` at #`port_num` port opened previously.

```python
# Try to ping the Dynamixel
# Get Dynamixel model number
dxl_model_number = dynamixel.pingGetModelNum(port_num, PROTOCOL_VERSION, DXL_ID)
if dynamixel.getLastTxRxResult(port_num, PROTOCOL_VERSION) != COMM_SUCCESS:
    dynamixel.printTxRxResult(PROTOCOL_VERSION, dynamixel.getLastTxRxResult(port_num, PROTOCOL_VERSION))
elif dynamixel.getLastRxPacketError(port_num, PROTOCOL_VERSION) != 0:
    dynamixel.printRxPacketError(PROTOCOL_VERSION, dynamixel.getLastRxPacketError(port_num, PROTOCOL_VERSION))
```

`pingGetModelNum()` function orders to the #`DXL_ID` Dynamixel through #`port_num` port. Then, it receives the `dxl_model_number`. The function checks Tx/Rx result and receives Hardware error.
`getLastTxRxResult()` function and `getLastRxPacketError()` function get either, and then `printTxRxResult()` function and `printRxPacketError()` function show results on the console window if any communication error or Hardware error has been occurred.

```python
# Close port
dynamixel.closePort(port_num)
```

Finally, port becomes disposed.
