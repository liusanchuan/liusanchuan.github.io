---
layout: archive
lang: en
ref: labview_porthandler
read_time: true
share: true
author_profile: false
permalink: /docs/en/software/dynamixel/dynamixel_sdk/api_reference/labview/labview_porthandler/
sidebar:
  title: DynamixelSDK
  nav: "dynamixel_sdk"
---

<div style="counter-reset: h1 6"></div>
<div style="counter-reset: h2 7"></div>
<div style="counter-reset: h3 0"></div>

<!--[dummy Header 1]>
  <h1 id="api-reference"><a href="#api-reference">API Reference</a></h1>
  <h2 id="labview"><a href="#labview">LabVIEW</a></h2>
<![end dummy Header 1]-->

### [LabVIEW PortHandler](#labview-porthandler)

- Description

   PortHandler dependent functions for serial communication.

- Members

   None


- Methods

| Methods                                     | Description                                                |
|:--------------------------------------------|:-----------------------------------------------------------|
| **[portHandle](#porthandler)**              | Initializes parameters for serial port control             |
| **[openPort](#openport)**                   | Opens a serial port                                        |
| **[closePort](#closeport)**                 | Closes a serial port                                       |
| **[clearPort](#clearport)**                 | Refreshes a serial port                                    |
| **[setPortName](#setportname)**             | Sets a device name                                         |
| **[getPortName](#getportname)**             | Gets a device name                                         |
| **[setBaudrate](#setbaudrate)**             | Sets a baudrate                                            |
| **[getBaudrate](#getbaudrate)**             | Gets a baudrate                                            |
| **[getBytesAvailable](#getbytesavailable)** | Checks how many bytes can be read in port buffer           |
| **[readPort](#readport)**                   | Reads bytes from port buffer                               |
| **[writePort](#writeport)**                 | Writes bytes to port buffer                                |
| **[setPacketTimeout](#setpackettimeout)**   | Sets timeout                                               |
| **[isPacketTimeout](#ispackettimeout)**     | Checks whether communication has been succeeded in timeout |


- Enumerator

   None



#### Method References

##### portHandler
- Syntax
```c
int portHandler(string port_name)
```
- Parameters

| Parameters | Description |
|:-----------|:------------|
| port_name  | Port name   |

- Detailed Description

   The function initializes the parameters for port control. At first, this checks if the port with same device name is set already in the `portData` pointer struct. If it exists, the function returns the port number as what it has. If not, the function finds any free port, resize `portData` struct and start to initialize struct members.

##### openPort
- Syntax
```c
uint8_t openPort(int port_num)
```
- Parameters

| Parameters | Description |
|:-----------|:------------|
| port_num   | Port number |

- Detailed Description

   This function opens the port by `setBaudRate` function using default baudrate(1M). If the baudrate is needed to be changed to another baudrate value, `setBaudRate` function should be called again after calling `openPort` function. When the port succeeds to be opened, this function will return 1(true), and if not, then 0(false).


##### closePort
- Syntax
```c
void closePort(int port_num)
```
- Parameters

| Parameters | Description |
|:-----------|:------------|
| port_num   | Port number |

- Detailed Description

  This function closes the port by closing the file descriptor.


##### clearPort
- Syntax
```c
void clearPort(int port_num)
```
- Parameters

| Parameters | Description |
|:-----------|:------------|
| port_num   | Port number |

- Detailed Description

  This function clears the port by flushing the file descriptor.


##### setPortName
- Syntax
```c
void setPortName(int port_num, string port_name)
```
- Parameters

| Parameters | Description |
|:-----------|:------------|
| port_num   | Port number |
| port_name  | Port name   |

- Detailed Description

  This function sets the device name as port_name.


##### getPortName
- Syntax
```c
string getPortName(int port_num)
```
- Parameters

| Parameters | Description |
|:-----------|:------------|
| port_num   | Port number |

- Detailed Description

  This function returns the device name which the port is using.


##### setBaudrate
- Syntax

```c
uint8_t setBaudrate(int port_num, const int baudrate)
```

- Parameters

| Parameters | Description     |
|:-----------|:----------------|
| port_num   | Port number     |
| baudrate   | Target baudrate |


- Description

  This function converts `baudrate` to baudrate type value at first. Secondly, it closes the port with `closePort` function, and opens the port with `setupPort` function again. If the value of `baudrate` is not in the compatible baudrate list, the `setCustomBaudrate` function suggests the baudrate value which is closest of available baudrate value. Finally, it returns false.


##### getBaudrate
- Syntax

```c
int getBaudrate(int port_num)
```

- Parameters

| Parameters | Description |
|:-----------|:------------|
| port_num   | Port number |

- Description

  This function returns the baudrate value previously set.  


##### getBytesAvailable
- Syntax

```c
int getBytesAvailable(int port_num)
```

- Parameters

| Parameters | Description |
|:-----------|:------------|
| port_num   | Port number |

- Description

  This function checks how much the data can be read, and returns its length.


##### readPort
- Syntax

```c
int readPort(int port_num, uint8_t *packet, int length)
```

- Parameters

| Parameters | Description                              |
|:-----------|:-----------------------------------------|
| port_num   | Port number                              |
| packet     | The number of data bytes read previously |
| length     | Byte length for read                     |


- Description

  This function gets length byte data from port buffer and returns a number of read data bytes. On end-of-file, 0 is returned, on error it returns -1.


##### writePort
- Syntax

```c
int writePort(int port_num, uint8_t *packet, int length)
```

- Parameters

| Parameters | Description                       |
|:-----------|:----------------------------------|
| port_num   | Port number                       |
| packet     | The number of data bytes to write |
| length     | Byte length for write             |



- Description

  This function transmits length byte, and returns how much the data was written. On error, it returns -1.


##### setPacketTimeout
- Syntax

```c
void setPacketTimeout (int port_num, uint16_t packet_length)
```

- Parameters

| Parameters    | Description                  |
|:--------------|:-----------------------------|
| port_num      | Port number                  |
| Packet_length | Target byte length for write |


- Description

  This function sets the start time when it transmits the packet, and set the timeout of packet transmission to be ready for deciding communication result.


##### setPacketTimeoutMSec
- Syntax

```c
void setPacketTimeoutMSec (int port_num, double msec)
```

- Parameters

| Parameters | Description |
|:-----------|:------------|
| port_num   | Port number |
| msec       | Miliseconds |


- Description

  This function sets the start time with `msec` milisecond value when it transmits the packet, and set the timeout of packet transmission to be ready for deciding communication result.

##### isPacketTimeout
- Syntax

```c
uint8_t isPacketTimeout(int port_num)
```

- Parameters

| Parameters | Description |
|:-----------|:------------|
| port_num   | Port number |

- Description

  This function decides the timeover of packet communication. If the time limit is over, it returns false.
