---
title: 开始使用OSDK 
date: 2020-05-08
version: 4.0.0
keywords: [write apps, developemtn, SDK, integrate, DJI]
---

## 概述
OSDK 为开发者提供了所需使用的模块，具体架构如下所示：
  <div>
<div style="text-align: center"><p>图1.OSDK 架构 </p>
<div style="text-align: center"><p><span>
      <img src="../../images/OSDK.png" width="400" style="vertical-align:middle" alt/></span></p>
</div></div></div>
        
## 引入OSDK 开发包
应用程序通过DJI Onboard SDK 中的`Vehicle `类调用DJI OSDK 的功能，因此使用OSDK 开发应用程序时，请先引入OSDK 开发包，如 图1. 引入OSDK 开发包所示，详细步骤如下所示：
* **引入OSDK 头文件**       
使用如下语句在程序中引入OSDK 头文件后，即可使用OSDK 中的接口，开发应用程序。
`#include <dji_vehicle.hpp>`

* **引入OSDK 帮助文件**        
使用如下语句在程序中引入OSDK 帮助文件后，在Linux 平台上开发的应用程序即可读取用户的配置文件，激活DJI 的无人机。
`#include <dji_linux_helpers.hpp>`

<div>
<div style="text-align: center"><p>图2.引入OSDK 开发包 </p>
</div>
<div style="text-align: center"><p><span>
      <img src="../../images/workflow/integrate_sdk_includes.png" width="650" alt/></span></p>
</div></div>

>**说明：** L17～19 行为开发者自己编写的代码。

## 配置依赖项
在Linux上使用CMake 开发基于OSDK 的应用程序时，请配置相应的依赖项：
1. 指定CMake 最小版本： version 2.8
2. 指定工程名称
3. 配置编译选项（可选）     
`set(CMAKE_CXX_FLAGS"${CMAKE_CXX_FLAGS} -std=C++11 -pthread -g -O0") `
4. 包含所需头文件的路径    
5. 生成并链接可执行文件    
   
<div>
<div style="text-align: center"><p>图3.配置依赖项 </p>
</div>
<div style="text-align: center"><p><span>
      <img src="../../images/workflow/integrate_sdk_cmakelists.png" width="650" alt/></span></p>
</div></div>

## OSDK 接口调用
OSDK 为开发者提供了同步和异步调用的接口。
* 同步接口调用，开发者在*调用*接口时，该*接口*会根据应用程序实际的情况获得对应的返回值，*调用者*需要等待*调用的接口*发送返回值，因此该调用方式也成为阻塞式调用。
* 异步接口调用，开发者在*调用*接口时，该*接口*会根据应用程序实际的情况获得对应的返回值，但开发者可能无法立刻得到对应的结果，当*调用的接口*获得结果后，该接口会通过状态或通知向开发者告知该结果，开发这可通过回调函数处理该调用结果，因此该调用方式也成为非阻塞式调用。

#### 以同步的方式调用接口
同步接口调用，开发者在*调用*接口时，该*接口*会根据应用程序实际的情况获得对应的返回值，*调用者*需要等待*调用的接口*发送返回值。
如下以同步调用的方式设置相机的模式：

```c++
    ErrorCode::ErrorCodeType retCode;
    CameraManager *pm = vehicle->cameraManager;
    /*set camera work mode as SHOOT_PHOTO*/
    DSTATUS("set camera work mode as SHOOT_PHOTO");
    retCode == pm->setModeSync(index, camreamodule::WorkMode::SHOOT_PHOTO, 3);
    if (retCode != ErrorCode::SysCommonErr::Success){
        DERROR("Set camera as SHOOT_PHOTO fail. Error code : 0x%lX", retCode);
        ErrorCode::printErrorCodeMsg(retCode);
        return retCode;
    }
```
#### 以异步的方式调用接口
异步接口调用，开发者在*调用*接口时，该*接口*会根据应用程序实际的情况获得对应的返回值，但开发者可能无法立刻得到对应的结果，当*调用的接口*获得结果后，该接口会通过状态或通知向开发者告知该结果，开发这可通过回调函数处理该调用结果。
如异步调用的方式设置相机的模式：
* 构造回调函数
```c++
    /*set camera work mode as RECORD_VIDEO*/
    DSTATUS("set camera mode to RECORD_VIDEO");
    pm->setModeAsync(index, camreamodule::WorkMode::RECORD_VIDEO, 
                     setCameraModeForRecordVideoCb, &udata);

  void CameraManagerAsyncSample::setCameraModeForRecordVideoCb(
       ErrorCode ::ErrCodeType retCode, UserData userData){
       AsyncSampleData *uData = (AsyncSampleData *)userData;
       
       DSTATUS("retCode : 0x%lX", retCode);
    if (!uData) {
       DERROR("User data is a null value.");
    return;
  }
  if (retCode == ErrorCode::SysCommonErr::Success) {
    DSTATUS("set camera work mode successfully");
    if (uData->pm) {
        DSTATUS("start to RECORD_VIDEO");
        uData->pm->startRecordVideoAsync) {
        uData->index,
        (void(*)ErrprCode::ErrorCodeType, UserData))uData->userCallBack,
        uData-> userData);
        }
      } else {
        DERROR("start to record video error. Error code : 0x%lX", retCode);
        ErrorCode::printErrorCodeMsg(retCode);
      if (uData->userCallBack) {
      void (*cb)(ErrorCode::ErrorCodeType, UserData);
      cb = (void (*)(ErrorCode::ErrorCodeType, UserData))uData->userCallBack;
      cb(retCode, uData->userData);
    }
  }
}
```

* 注册回调函数函数     
开发者调用OSDK 中的异步接口后，将会接收到相应的数据，开发者需要注册回调函数处理所接收的数据。
如下以注册回调函数的方式订阅无人机中的数据：

```c++
void NMEA Callback(Vehicle* vehiclePtr, RecvContainer recvFrame, UserData userdata)
{
  int length =recvFrame.recvinfo.len-OpenProtocol::PackageMin-4;
  uint8_t rawBuf[length];
  memcpy(rawBuf, recvFrame.recvData.raw_ack_array, length);
  DSTATUS("&s/n",std string((char*)rawBuf, length).c_str())
}
```

## 使用 Vehicle
#### 1. “无人机”对象实例化
使用OSDK 开发应用程序时，应用程序需要先读取环境配置参数、初始化无人机并创建实例对象`vehicle`。
1. 读取环境配置参数（Userconfig.txt）     
编译OSDK 提供的示例代码时，基于OSDK 开发的应用程序需要读取如第三方库、波特率以及驱动权限等环境配置参数。
```C++
  LinuxSetup linuxEnvironment(argc, argv);            
```

2. 创建实例对象`vehicle`   
创建实例对象`vehicle` 并完成初始化。
```c++
  Vehicle *vehicle = linuxEnvironment.getVehicle(); 
  if (vehicle == NULL) {
    std::cout << "Vehicle not initialized, exiting. \n";
    return -1;
  }
  std::string sampleCase = linuxEnvironment.getEnvironment()->getSampleCase(); 
```

#### 2.功能模块实例化
无人机对象实例化后，开发者可根据实际的使用需求，实例化所需使用的功能模块。
如下代码以实例化相机模块，并初始化`PAYLOAD_INDEX_0`和`PAYLOAD_INDEX_1`为例。

```c++
ErrorCode::ErrorCodeType 
ret = vehicle->cameraManager->initCameraModule(PAYLOAD_INDEX_0,"Sample_camera_1");
  if (ret != ErrorCode::SysCommonErr::Success) {
    DERROR("Init Camera module Sample_camera_1 failed.");
    ErrorCode::printErrorCodeMsg(ret);
  }
ret = vehicle->cameraManager->initCameraModule(PAYLOAD_INDEX_1,"Sample_camera_2");
  if (ret != ErrorCode::SysCommonErr::Success) {
    DERROR("Init Camera module Sample_camera_2 failed.");
    ErrorCode::printErrorCodeMsg(ret);
  }
```
