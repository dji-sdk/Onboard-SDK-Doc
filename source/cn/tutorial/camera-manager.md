---
title: 相机管理
date: 2020-05-08
version: 4.0.0
keywords: [相机, ISO, EV, 快门, 曝光, 变焦]
---
## 概述
为方便开发者在OSDK 的基础上快速开发出控制DJI 无人机上相机的功能，DJI OSDK 提供了相机管理功能，即`CameraManager`类。开发者使用OSDK 中的`CameraManager`类，能够同时设置并获取无人机上多个相机的感光度、光圈、快门和曝光等参数的值，控制相机实现拍照、录像及指点变焦等功能。      

## CameraManager
在使用相机管理功能时，开发者需要先**初始化**OSDK 中的相机模块，**创建实例化对象**`CameraManager`，再根据实际的使用需要**设置相机的模式**，最后根据用户的使用逻辑实现所需使用的功能，如设置相机的参数、检查功能的状态或参数对比等。

## 使用CameraManager 的功能

#### 1. 相机模块初始化
无人机初始化后，需初始化无人机上的相机模块，并将所需控制的相机注册到`vehicle->cameraManager`中，如下为初始化无人机I 号云台和II 号云台上的相机模块。

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

#### 2. CameraManager 对象实例化   
如需使用OSDK `CameraManager` 中功能，请创建`CameraManager`实例。   
##### 以同步的方式创建实例
`CameraManagerSyncSample *p = new CameraManagerSyncSample(vehicle);`  
##### 以异步的方式创建实例
`CameraManagerAsyncSample *p = new CameraManagerAsyncSample(vehicle);`   

#### 3. 设置或获取相机参数
CameraManager 对象实例化后，开发者需根据使用相机功能的逻辑，设置或获取相机的模式，如设置相机的光圈模式前需先设置相机的曝光模式，详情请参见OSDK API 文档，如下以同步和异步的方法介绍获取相机光圈值的方法。

##### 以同步的方式获取相机的光圈模式     
```c++
  retCode = pm->getApertureSync(index, apertureGet, 1);
```

##### 以异步的方式获取相机的光圈模式   
* 构造回调函数

```c++
void CameraManagerAsyncSample::getApertureCb(ErrorCode::ErrorCodeType retCode,
                                             CameraModule::Aperture apertureGet,
                                             UserData userData) {
  AsyncSampleData *uData = (AsyncSampleData *)userData;

  DSTATUS("retCode : 0x%lX", retCode);
  if (!uData) {
    DERROR("User data is a null value.");
    return;
  }
  if (retCode == ErrorCode::SysCommonErr::Success) {
    DSTATUS("Get aperture = %d", apertureGet);
    if (uData->pm) {
      if (*(CameraModule::Aperture *)uData->dataTarget == apertureGet) {
        DSTATUS("The aperture value is already %d.", apertureGet);
        if (uData->userCallBack) {
          void (*cb)(ErrorCode::ErrorCodeType, UserData);
          cb =
              (void (*)(ErrorCode::ErrorCodeType, UserData))uData->userCallBack;
          cb(ErrorCode::SysCommonErr::Success, uData->userData);
        }
      } else {
        uData->pm->setApertureAsync(
            uData->index, *(CameraModule::Aperture *)uData->dataTarget,
            (void (*)(ErrorCode::ErrorCodeType, UserData))uData->userCallBack,
            uData->userData);
      }
    }

  } else {
    DERROR("Get aperture error. Error code : 0x%lX", retCode);
    ErrorCode::printErrorCodeMsg(retCode);
    if (uData->userCallBack) {
      void (*cb)(ErrorCode::ErrorCodeType, UserData);
      cb = (void (*)(ErrorCode::ErrorCodeType, UserData))uData->userCallBack;
      cb(retCode, uData->userData);
    }
  }
}
```

* 注册回调函数
```c++
  DSTATUS("Get aperture now ...");
  pm->getApertureAsync(index, getApertureCb, &uData);
}
```

#### 4. 控制相机执行指定的动作
开发者通过CameraManager 能够控制相机执行指定的动作，如指点变焦等，详情请参见OSDK API 文档，如下以同步和异步的方法介绍控制相机执行指点变焦功能的方法。

##### 以同步的方式控制相机指点变焦
```c
 ErrorCode::ErrorCodeType CameraManagerSyncSample::setTapZoomPointSyncSample(
    PayloadIndexType index, uint8_t multiplier, float x, float y) {
  if (!vehicle || !vehicle->cameraManager) {
    DERROR("vehicle or cameraManager is a null value.");
    return ErrorCode::SysCommonErr::InstInitParamInvalid;
  }
  ErrorCode::ErrorCodeType retCode;
  CameraManager *pm = vehicle->cameraManager;

  /*开启指点变焦功能*/
  DSTATUS("Set tap zoom enable  = %d", true);
  retCode = pm->setTapZoomEnabledSync(index, true, 1);
  if (retCode != ErrorCode::SysCommonErr::Success) {
    DERROR("Set tap zoom enable fail. Error code : 0x%lX", retCode);
    ErrorCode::printErrorCodeMsg(retCode);
    DERROR("It is only supported Z30 camera.");
    return retCode;
  }

  /*设置指点变焦参数*/
  DSTATUS("Set tap zoom multiplier = %d", multiplier);
  retCode = pm->setTapZoomMultiplierSync(index, multiplier, 1);
  if (retCode != ErrorCode::SysCommonErr::Success) {
    DERROR("Set tap zoom multiplier fail. Error code : 0x%lX", retCode);
    ErrorCode::printErrorCodeMsg(retCode);
    DERROR("It is only supported Z30 camera.");
    return retCode;
  }

  /*设置指点变焦对象*/
  DSTATUS("Set tap zoom target point : (%f,%f)", x, y);
  retCode = pm->tapZoomAtTargetSync(index, {x, y}, 1);
  if (retCode != ErrorCode::SysCommonErr::Success) {
    DERROR("Set tap zoom target fail. Error code : 0x%lX", retCode);
    ErrorCode::printErrorCodeMsg(retCode);
    DERROR("It is only supported Z30 camera.");
    return retCode;
  } else {
    DSTATUS(
        "tap zoom at target (%0.2f, %0.2f) successfully, need several seconds "
        "to zoom.",
        x, y);
  }

  return retCode;
}
```

##### 以异步的方式控制相机指点变焦
* 构造回调函数
```c
/*设置指点变焦系数*/
void CameraManagerAsyncSample::setTapZoomMultiplierCb(
    ErrorCode::ErrorCodeType retCode, UserData userData) {
  AsyncSampleData *uData = (AsyncSampleData *)userData;

  DSTATUS("retCode : 0x%lX", retCode);
  if (!uData) {
    DERROR("User data is a null value.");
    return;
  }
  if (retCode == ErrorCode::SysCommonErr::Success) {
    DSTATUS("Set tap zoom multiplier successfully ");
    if (uData->pm) {
      /*注册开启指点变焦功能的函数*/
      uData->pm->setTapZoomEnabledAsync(uData->index, true, setTapZoomEnableCb,
                                        uData);
    }
  } else {
    DERROR("Set tap zoom multiplier error. Error code : 0x%lX", retCode);
    ErrorCode::printErrorCodeMsg(retCode);
    if (uData->userCallBack) {
      void (*cb)(ErrorCode::ErrorCodeType, UserData);
      cb = (void (*)(ErrorCode::ErrorCodeType, UserData))uData->userCallBack;
      cb(retCode, uData->userData);
    }
  }
}

/*开启指点变焦功能*/
void CameraManagerAsyncSample::setTapZoomEnableCb(
    ErrorCode::ErrorCodeType retCode, UserData userData) {
  AsyncSampleData *uData = (AsyncSampleData *)userData;

  DSTATUS("retCode : 0x%lX", retCode);
  if (!uData) {
    DERROR("User data is a null value.");
    return;
  }
  if (retCode == ErrorCode::SysCommonErr::Success) {
    DSTATUS("Set tap zoom enable successfully ");
    if (uData->pm) {
      /* 设置指点变焦的对象 */
      uData->pm->tapZoomAtTargetAsync(
          uData->index, *(CameraModule::TapZoomPosData *)uData->dataTarget,
          (void (*)(ErrorCode::ErrorCodeType, UserData))uData->userCallBack,
          uData->userData);
    }
  } else {
    DERROR("Tap zoom at enable error. Error code : 0x%lX", retCode);
    ErrorCode::printErrorCodeMsg(retCode);
    if (uData->userCallBack) {
      void (*cb)(ErrorCode::ErrorCodeType, UserData);
      cb = (void (*)(ErrorCode::ErrorCodeType, UserData))uData->userCallBack;
      cb(retCode, uData->userData);
    }
  }
}
```

* 注册回调函数
```c++
  DSTATUS("Set tap zoom multiplier = %d", multiplier);
  pm->setTapZoomMultiplierAsync(index, multiplier, setTapZoomMultiplierCb, &uData);
}
```

## 产品适配
<table>
<thead>
<tr>
<th></th>
<th>X4S</th>
<th>X5S</th>
<th>X7</th>
<th>Z30</th>
<th>XT</th>
<th>XT2</th>
</tr>
</thead>
<tbody>
<tr>
<td>设置/获取相机工作模式</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
</tr>
<tr>
<td>设置/获取相机对焦模式</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>设置/获取曝光模式</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>设置/获取ISO</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>设置/获取光圈</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>设置/获取快门</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>设置/获取EV（曝光补偿）</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>设置/获取分接缩放参数</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>设置/获取分接缩放点</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>设置/获取焦点</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>设置/获取拍摄照片模式</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>拍摄单张照片</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
</tr>
<tr>
<td>设置/获取间隔拍摄参数</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>拍摄间隔照片</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
</tr>
<tr>
<td>设置/获取自动包围曝光拍摄参数</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>拍摄自动包围曝光照片</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>设置/获取连拍参数</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>拍摄连拍照片</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>录视频</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
</tr>
</tbody>
</table>