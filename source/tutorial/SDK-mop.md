---
title: SDK Interconnection
date: 2020-05-08
version: 4.0.0
keywords: [PSDK, OSDK, communication, SDK interconnection, MOP]
---
> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.     

## Overview
The application developed based on DJI OSDK can communicate with the Mobile App and the Payload, for example, user sends commands to the drone from the Mobile App to control the payload, and onboard computer; the application could control the payload and sends status to the Mobile app; the payload could send the data to Mobile App and the application such as video streams or files, as shown in Figure 1.

<div>
<div style="text-align: center"><p>Figure1. SDK Interconnection. </p>
</div>
<div style="text-align: center"><p><span>
      <img src="../../images/MOP-en.png" width="500" alt/></span></p>
</div></div>

Using SDK Interconnection, developers could:
* Create the transmission channels required dynamically
* Create the channel transmit the specified data
* Full-duplex communication

## Concept
> **NOTE**
> * Client: According to the channel ID, connect to the Others, such as Mobile App.
> * Server: Create channel and specify the channel type and ID, such as Payload.

#### Transfer Method
* Reliable Transmission
In order to translate the data reliable between the applications which developed based on different SDK, DJI SDK provide the reliable transmission method. In this mode, DJI SDK adopts retransmission、detection and other mechanisms to ensure that the data is accurate and reliable.
   * Content reliable: Use the check and encryption algorithm mechanism to encrypt the data transmitted.
   * Transmission reliable: The data transmission using the timer and ACK mechanism, which can retransmit the data after times out, the sender will send the data number, and the receiver can rearrange the received data depending the data number make the data transmission reliable.
* Unreliable Transmission
When transmitting data in an unreliable transmission mode, data can be transmitted at a faster speed between applications, but cannot guarante transmission‘s reliable .

#### Object Specified
The interconnection function of the DJI SDK can accurately specify the devices or modules that need to communicate on the drone through the device type and device slot.
* Device type: In order to facilitate developers to identify the identity and type of the peer end, and better distinguish the data transmission objects, the data transmission function provides three device types of MSDK, OSDK and PSDK according to the DJI SDK.

> **NOTE** In the SDK interconnection, only applications developed based on OSDK and payload developed based on PSDK can creat the channels, the Mobile APP based on MSDK only can receive the data that connect to the peer.

* Device Slots: DJI's drones have powerful expansion capabilities. Developers can access more than three payload, the Mobile App has two method, and onboard computer has variety expansion methods. so different slots can be used to distinguish Mobile APP, payload, and onboard computer.

* Channel ID: In order to help developers select and use communication channels with different channels on the same object, DJI SDK use the channel ID for distinguished. Developers can specify the ID for the created channel when creating the channel.

> **NOTE**
> * Only applications developed based on OSDK and payload developed based on PSDK could specify the channel ID for the created channel.
> * Developers can specify the channel ID for the created channel, the maximum is 65535.

#### Channel Manager
In order to help developer develop the powerful and reliable applications and devices without paying attention to the underlying working logic of the SDK interconnection, the DJI SDK provides powerful communication management mechanism:
* Link management: link access, close, destroy, reconnect and congestion management, etc.
* Data management: data forwarding, reading and writing, data verification, out-of-order reordering and packet loss retransmission, etc.
> **NOTE** In order to help developers to use the SDK interconnection, to distinguish it from existing interfaces, DJI MSDK uses "Pipeline" to indicate channel management function.

#### Bandwidth
* Reliable transmission
   * MSDK upstream (sending data to server) is 3KB/S; downstream (receiving data from server) is 250KB/S
   * The data transfer rate between OSDK and PSDK is 500KB/S
  
## Develop with SDK Interconnection (MSDK)
Mobile App developed based on MSDK could use the SDK Interconnection to establish the connect with the specified channel ID.

> **NOTE** The Mobile App developed based on MSDK can only used as the client to establish a connection with the specified channel by the channel ID.

#### 1. Channel Connection
When creating the channel, developer need use the following interface to specify the channel transmission mode and the channel ID to establish the connection with the specified channel, and receive the transmitted data in the blocking callback manner.

* For iOS
```c
- (void)connect:(uint16_t)Id pipelineType:(DJITransmissionControlType)transferType withCompletion:(void (^_Nullable)(DJIPipeline *_Nullable pipeline, NSError *_Nullable error))completion;
```

* For Android
```java
    void connect(int id, @NonNull TransmissionControlType transmissionType, @Nullable CommonCallbacks.CompletionCallback<PipelineError> callback);
```

#### 2. Receive Data 
After connected the channel , the Mobile App developed based on MSDK uses the following interface to receive data sent by the peer.

* For iOS
```c
- (NSData *)readData:(uint32_t)readLength error:(NSError **)error;
```

* For Android
```java
int readData(byte[] buff, int length);
```

#### 3. Send Data 
After connected the channel, the mobile APP developed based on MSDK uses the following interface send data to the peer.
> **NOTE** It is recommended that the size of the transmitted data wouldn't exceed 1KB.

* For iOS
```c
- (int32_t)writeData:(NSData *)data error:(NSError **)error;
```
* For Android
```java
int writeData(byte[] data);
```

#### 4. Close
After the communication, please use the following interface to disconnect the connected channel.
> **NOTE**
> * After closing the channel, the mobile APP developed based on MSDK will clear the local cache.
> * After close the channel, the DJI SDK will automatically destroy the created channel and release the system resources occupied.

* For iOS
```c
- (void)disconnect:(uint16_t)Id withCompletion:(DJICompletionBlock)completion;
```

* For Android
```java
    void disconnect(int id, @Nullable CommonCallbacks.CompletionCallback<PipelineError> callback);
```

## Develop with SDK Interconnection (OSDK)
Only the application which developed based on the OSDK execute on the Linux supports developer develop with SDK Interconnection and to be the client and server:
* As a client, the user can establish the connection with the specified channel by the channel ID.
* As a server, an application developed based on OSDK can create the channel and specify a channel ID. After establish the connection, the application could read or write data.

#### 1. Initialization
If the application developed based on OSDK deveoped with the SDK Interconnection, developer should initialize the SDK Interconnection module at first.

##### For Client
When the application developed based on OSDK as the client, the onboard computer can be regarded as a payload of the drone, so please use the `PSDKManager` class in the DJI Payload SDK to initialize the SDK Interconnection.

```c++
ErrorCode::ErrorCodeType ret = vehicle->psdkManager->initPSDKModule(
    PAYLOAD_INDEX_0, "Main_psdk_device");
if (ret != ErrorCode::SysCommonErr::Success) {
  DERROR("Init PSDK module Main_psdk_device failed.");
  ErrorCode::printErrorCodeMsg(ret);
}
```

##### For Server
When the application developed based on the OSDK is used as the server, developer need initialize the Vehicle class first, and block the specified channel ID by calling the accept interface in `vehicle->mopServer`.

```c
#define TEST_MO_PIPELINE_ID 20

......
  if (vehicle->mopServer->accept((PipelineID)TEST_MO_PIPELINE_ID, UNRELIABLE, MO_Pipeline) != MOP_PASSED) {
    DERROR("MOP Pipeline accept failed");
    return -1;
  } else {
    DSTATUS("Accept to mop pipeline id(%d) successfully", TEST_MO_PIPELINE_ID);
  }
......
```

#### 2. Get The Pointer Of The Client
**Only the application developed based on OSDK is used as the client**, developer need obtain the pointer of the client, and use this pointer to create the channel to read and write the data.   
```c
MopClient *mopClient = NULL;
ret = vehicle->psdkManager->getMopClient(PAYLOAD_INDEX_0, mopClient);
if (ret != ErrorCode::SysCommonErr::Success) {
  DERROR("Get MOP client object for_psdk_device failed.");
  ErrorCode::printErrorCodeMsg(ret);
  return NULL;
}
 
if (!mopClient) {
  DERROR("Get MOP client object is a null value.");
  return NULL;
}
```

#### 3. Channel Connection
**Only the application developed based on OSDK is used as the client**, developer need specify the channel ID and channel type to establish the connection with the specified channel.

```c
#define TEST_OP_PIPELINE_ID 15

MopPipeline *OP_Pipeline = NULL;
if ((mopClient->connect(TEST_OP_PIPELINE_ID, RELIABLE, OP_Pipeline)
    != MOP_PASSED) || (OP_Pipeline == NULL)) {
  DERROR("MOP Pipeline connect failed");
  return NULL;
} else {
  DSTATUS("Connect to mop pipeline id(%d) successfully", TEST_OP_PIPELINE_ID);
}
```

#### 4. Receive Data 
After created the channel, developer could receive data transmitted by the peer in the blocking callback (synchronous callback) on the channel.

##### For Client
Only the application developed based on OSDK as the client, please use the following interface to receive the data sent by the server.

```c
MopErrCode mopRet;
......
uint8_t recvBuf[1024];
MopPipeline::DataPackType readPack = {recvBuf, 1024};
mopRet = OP_Pipeline->recvData(readPack, &readPack.length);
......
```
##### For Server
Only the application developed based on OSDK as the server, please use the following interface to receive the data sent by the client.

```c
MopErrCode mopRet;
......
uint8_t recvBuf[1024];
MopPipeline::DataPackType readPack = {recvBuf, 1024};
mopRet = MO_Pipeline->recvData(readPack, &readPack.length);
......

```

#### 5. Send Data 
After creating the channel, developers could send data to the peer.

##### For Client
Only the application developed based on OSDK as the client, please use the following interface send data to the peer.

```c
MopErrCode mopRet;
uint8_t sendBuf[1024];
......
MopPipeline::DataPackType reqPack = {sendBuf, 1024};
mopRet = OP_Pipeline->sendData(reqPack, &reqPack.length);
......
```

##### For Server
Only the application developed based on OSDK as the server, please use the following interface send data to the peer.


```c
MopErrCode mopRet;
uint8_t sendBuf[1024];
......
MopPipeline::DataPackType reqPack = {sendBuf, 1024};
mopRet = MO_Pipeline->sendData(reqPack, &reqPack.length);
......
```
#### 6. Close
After the communication, please use the following interface to disconnect the connected channel and release the system resources occupied by the channel.

##### For Client
Only the application developed based on OSDK as the client, please use the following interface to close the created channel.

```c
if (mopClient->disconnect(TEST_OP_PIPELINE_ID) != MOP_PASSED) {
  DERROR("MOP Pipeline disconnect pipeline(%d) failed", TEST_OP_PIPELINE_ID);
} else {
  DSTATUS("Disconnect mop pipeline id(%d) successfully", TEST_OP_PIPELINE_ID);
}
```

##### For Server
Only the application developed based on OSDK as the server, please use the following interface to close the created channel.

```c
if (vehicle->mopServer->close(TEST_MO_PIPELINE_ID) != MOP_PASSED) {
  DERROR("MOP Pipeline disconnect pipeline(%d) failed", TEST_MO_PIPELINE_ID);
} else {
  DSTATUS("Disconnect mop pipeline id(%d) successfully", TEST_MO_PIPELINE_ID);
}
```

## Develop with SDK Interconnection (PSDK)
Only the payload which developed based on the OSDK execute on the Linux supports developer develop with SDK Interconnection and to be the server.

> **NOTE** The sample of the PSDK developed on the Manifold 2-C/G, with the network port, make ensure that the network port of the development board is avilible.

#### 1. Initialization
If the application developed based on PSDK deveoped with the SDK Interconnection, developer should initialize the SDK Interconnection module at first.

```c
T_PsdkReturnCode PsdkMopChannel_Init(void);
```

#### 2. Creat The Channel
The payload developed based on PSDK creates channel will specified the channel's type: reliable or unreliable.
      
```c
T_PsdkReturnCode PsdkMopChannel_Create(T_PsdkMopChannelHandle *channelHandle, E_PsdkMopChannelTransType trans);
```

#### 3. Channel Connection    
The payload developed based on PSDK as the server establish the connection with the peer, need specified the channel ID for the client to bind. To establishment the connection with multiple clients at the same time, PSDK provides the handle outChannelHandle.
 
1. Channel Binding
The payload developed based on PSDK use the channel ID to communicate with the client.

```c
T_PsdkReturnCode PsdkMopChannel_Bind(T_PsdkMopChannelHandle channelHandle, uint16_t channelId);
```
2. Accept The Connection
The payload device developed based on PSDK accepts the connection request sent by the peer in the following interface.

```c
T_PsdkReturnCode PsdkMopChannel_Accept(T_PsdkMopChannelHandle channelHandle, T_PsdkMopChannelHandle *outChannelHandle);
```
> **NOTE** This interface is the blocking interface. When the payload as the server to establishment the connection with multiple clients at the same time, please call this interface in a separate thread.

#### 4. Receive Data
After created the channel, developer could receive the data sent by the peer。

```c
T_PsdkReturnCode PsdkMopChannel_RecvData(T_PsdkMopChannelHandle channelHandle, uint8_t *data,  uint32_t len,  uint32_t *realLen);
```

#### 5. Send Data
After created the channel, developer could send the data to the peer.

```c
T_PsdkReturnCode PsdkMopChannel_SendData(T_PsdkMopChannelHandle channelHandle, uint8_t *data, uint32_t len, uint32_t *realLen);
```

#### 6. Close
After the communication, please use the following interface to disconnect the connected channel and release the system resources occupied by the channel.

* Close Channel
Call the following interface to close the created channel. After that, the channel couldn’t send or receive data, but it can be re-established with other channels.

```c
T_PsdkReturnCode PsdkMopChannel_Close(T_PsdkMopChannelHandle channelHandle);
```

* Destroy The Channel
Call the following interface to destroy the specified channel.
```c
T_PsdkReturnCode PsdkMopChannel_Destroy(T_PsdkMopChannelHandle channelHandle);
```
