---
layout: archive
lang: en
ref: matlab_groupsyncread
read_time: true
share: true
author_profile: false
permalink: /docs/en/software/dynamixel/dynamixel_sdk/api_reference/matlab/matlab_groupsyncread/
sidebar:
  title: DynamixelSDK
  nav: "dynamixel_sdk"
---

<div style="counter-reset: h1 6"></div>
<div style="counter-reset: h2 6"></div>
<div style="counter-reset: h3 3"></div>

<!--[dummy Header 1]>
  <h1 id="api-reference"><a href="#api-reference">API Reference</a></h1>
  <h2 id="matlab"><a href="#matlab">Matlab</a></h2>
<![end dummy Header 1]-->

### [Matlab GroupSyncRead](#matlab-groupsyncread)

- Description

  Base functions for simultaneous dynamixel control on reading to same length data on same control table address. The function is unavailable in protocol 1.0.

- Members

  None


- Methods

| Methods                                                   | Description                                                |
|:----------------------------------------------------------|:-----------------------------------------------------------|
| **[groupSyncRead](#groupsyncread)**                       | Initializes members of packet data pointer struct          |
| **[groupSyncReadAddParam](#groupsyncread_addparam)**      | Adds parameter storage for read                            |
| **[groupSyncReadRemoveParam](#groupsyncreadremoveparam)** | Removes parameter on the storage                           |
| **[groupSyncReadClearParam](#groupsyncreadclearparam)**   | Clears parameter storage                                   |
| **[groupSyncReadTxPacket](#groupsyncreadtxpacket)**       | Transmits packet to the number of Dynamixels               |
| **[groupSyncReadRxPacket](#groupsyncreadrxpacket)**       | receives packet from the number of Dynamixels              |
| **[groupSyncReadTxRxPacket](#groupsyncreadtxrxpacket)**   | Transmits and receives packet on the number of Dynamixels  |
| **[groupSyncReadIsAvailable](#groupsyncreadisavailable)** | Checks whether there is available data in the data storage |
| **[groupSyncReadGetData](#groupsyncreadgetdata)**         | Gets data from received packet                             |


- Enumerator

  None

#### Method References

##### groupSyncRead
- Syntax
```c
int groupSyncRead(int port_num, int protocol_version, int start_address, int data_length)
```
- Parameters

| Parameters       | Description                                 |
|:-----------------|:--------------------------------------------|
| port_num         | Port number                                 |
| protocol_version | Protocol version                            |
| start_address    | Control table address to start reading data |
| data_length      | Total data length                           |

- Detailed Description

   This function initializes the parameters for packet construction. The function resizes groupData struct and initialzes struct members.


##### groupSyncReadAddParam
- Syntax
```c
bool groupSyncReadAddParam(int group_num, int id)
```
- Parameters

| Parameters | Description  |
|:-----------|:-------------|
| group_num  | Group number |
| id         | Dynamixel ID |

- Detailed Description

   This function pushes id to the Dynamixel ID list, and initializes #`group_num` parameter storage It returns false when the class uses Protocol 1.0, or it returns true.


##### groupSyncReadRemoveParam
- Syntax
```c
void groupSyncReadRemoveParam(int group_num, int id)
```
- Parameters

| Parameters | Description  |
|:-----------|:-------------|
| group_num  | Group number |
| id         | Dynamixel ID |

- Detailed Description

   This function removes id and its data for write in the #`group_num` Dynamixel ID list. It returns false when the class uses Protocol 1.0 or target ID does not exists in the ID list, or returns true.


##### groupSyncReadClearParam
- Syntax
```c
void groupSyncReadClearParam(int group_num)
```
- Parameters

| Parameters | Description  |
|:-----------|:-------------|
| group_num  | Group number |

- Detailed Description

   This function clears #`group_num` Dynamixel ID list. It returns false when the class uses Protocol 1.0, or returns true.


##### groupSyncReadTxPacket
- Syntax
```c
int groupSyncReadTxPacket(int group_num)
```
- Parameters

| Parameters | Description  |
|:-----------|:-------------|
| group_num  | Group number |

- Detailed Description

   This function transmits the packet by using `SyncReadTx` function. The communication result and the hardware error are available when the function is terminated.


##### groupSyncReadRxPacket
- Syntax
```c
int groupSyncReadRxPacket(int group_num)
```
- Parameters

| Parameters | Description  |
|:-----------|:-------------|
| group_num  | Group number |

- Detailed Description

   This function receives the packet by using `ReadRx` function. The communication result and the hardware error are available when the function is terminated.


##### groupSyncReadTxRxPacket
- Syntax
```c
int groupSyncReadTxRxPacket(int group_num)
```
- Parameters

| Parameters | Description  |
|:-----------|:-------------|
| group_num  | Group number |

- Detailed Description

   This function transmits and receives the packet by using `TxPacket` function and `RxPacket` function. The communication result and the hardware error are available when the function is terminated.

 ##### groupSyncReadIsAvailable
 - Syntax
 ```c
 bool groupSyncReadIsAvailable(int group_num, int id, int address, int data_length)
 ```
 - Parameters

| Parameters | Description                               |
|:-----------|:------------------------------------------|
| id         | Dynamixel ID                              |
| address    | Address on the control table of Dynamixel |
| data       | Packet data                               |


 - Detailed Description

    This function checks whether there is available data in the data storage. It returns false when used Protocol is 1.0 version or there is no data from target address, or returns true.

##### groupSyncReadGetData
- Syntax
```c
int groupSyncReadGetData(int group_num, int id, int address, int data_length)
```
- Parameters

| Parameters | Description                               |
|:-----------|:------------------------------------------|
| group_num  | Group number                              |
| id         | Dynamixel ID                              |
| address    | Address on the control table of Dynamixel |
| data       | Packet data                               |


- Detailed Description

   This function gets specific data from received packet. It returns false when the class uses Protocol 1.0 or there is no data from target address, or returns true.
