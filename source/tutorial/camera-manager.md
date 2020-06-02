---
title: Camera Management
date: 2020-05-08
version: 4.0.0
keywords: [Camera, ISO, EV, shutter, exposure, shutter]
---
> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.     

## Overview
In order to help developers develop functions to control cameras on DJI's drones based on OSDK quickly, DJI OSDK provides the class `CameraManager`. Using this class, developer could set and obtain the parameters simultaneously, such as sensitivity, aperture, shutter, exposure of multiple cameras`, control the cameras taking pictures, recording, and pointing zoom.

## CameraManager
When using the Camera Management, the developer needs to **initialize** the camera module in the OSDK, **create the instantiated object** `CameraManager`, and then **set the camera mode**, according to the user's need to design the logic to control the camera, such as setting parameters, checking status, etc.
<div>
<div style="text-align: center"> <p> Table 1. CameraManager's functions </p>
</div>
<table>
<thead>
<tr>
<th></th>
<th>X4S</th>
<th>X5S</th>
<th>X7</th>
<th>Z30</th>
<th>XTS</th>
<th>XT2</th>
<th>H20/H20T</th>
</tr>
</thead>
<tbody>
<tr>
<td>Set/Get Camera Work Mode</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
</tr>
<tr>
<td>Set/Get Camera Focus Mode</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>√</td>
</tr>
<tr>
<td>Set/Get Exposure Mode</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
</tr>
<tr>
<td>Set/Get ISO	</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>√</td>
</tr>
<tr>
<td>Set/Get Aperture</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>√</td>
</tr>
<tr>
<td>Set/Get Shutter	</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
</tr>
<tr>
<td>Set/Get EV(Exposure Compensation)	</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
</tr>
<tr>
<td>Set/Get  Zoom Parameters</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>√</td>
</tr>
<tr>
<td>Set Tap Zoom Point</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>√</td>
</tr>
<tr>
<td>Set/Get Focus Point	</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
</tr>
<tr>
<td>Set/Get Shoot-Photo Mode</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
</tr>
<tr>
<td>Shoot Single Photo</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
</tr>
<tr>
<td>Set/Get Interval Shooting Parameters</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>Shoot Interval Photo</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
</tr>
<tr>
<td>Set/Get AEB Shooting Parameters</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>Shoot AEB Photo</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>Set/Get Burst Shooting Parameters</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>Shoot Burst Photo</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<td>Record Video</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√</td>
</tr>
<tr>
<td>Download FileList (M300 Only)</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√（beta）</td>
</tr>
<tr>
<td>Download FIledata (M300 Only)</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>√</td>
<td>√</td>
<td>√</td>
<td>√（beta）</td>
</tr>
</tbody>
</table>
</div>

## Develop with CameraManager

#### 1. Initialization
After initialized the drone, developer need initialize the camera module, registered the camera module in `vehicle-> cameraManager`.

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

#### 2. CameraManager Instantiation
If you want to use the functions in OSDK `CameraManager`, please create` CameraManager` instance.
* Synchronous
`CameraManagerSyncSample * p = new CameraManagerSyncSample (vehicle);`
* Asynchronous
`CameraManagerAsyncSample * p = new CameraManagerAsyncSample (vehicle);`

#### 3. Set or Get Camera's Parameters
After instantiated the CameraManager, developer could to set or obtain the camera mode according to the logic of the camera function. For example, before setting the camera's aperture mode, developer need to set the camera's exposure mode for details please refer to API Documentation. The content below is show the method of obtaining the aperture value use synchronous and asynchronous methods.

###### Synchronous
Obtain the aperture mode of the camera in a synchronized manner.    
```c++
  retCode = pm->getApertureSync(index, apertureGet, 1);
```

###### Asynchronous
Get the aperture mode of the camera in a synchronous manner.

* Construct the callback

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

* Register the callback
```c++
  DSTATUS("Get aperture now ...");
  pm->getApertureAsync(index, getApertureCb, &uData);
}
```

#### 4. Control The Camera
Developers can use CameraManager control the camera to perform specified actions, such as pointing zoom, etc. For details, please refer to the OSDK API documentation. The method of controlling the camera to perform Pointing Zoom is introduced in the following.

###### Synchronous
```c
 ErrorCode::ErrorCodeType CameraManagerSyncSample::setTapZoomPointSyncSample(
    PayloadIndexType index, uint8_t multiplier, float x, float y) {
  if (!vehicle || !vehicle->cameraManager) {
    DERROR("vehicle or cameraManager is a null value.");
    return ErrorCode::SysCommonErr::InstInitParamInvalid;
  }
  ErrorCode::ErrorCodeType retCode;
  CameraManager *pm = vehicle->cameraManager;

  /*Enable the Pointing Zoom*/
  DSTATUS("Set tap zoom enable  = %d", true);
  retCode = pm->setTapZoomEnabledSync(index, true, 1);
  if (retCode != ErrorCode::SysCommonErr::Success) {
    DERROR("Set tap zoom enable fail. Error code : 0x%lX", retCode);
    ErrorCode::printErrorCodeMsg(retCode);
    DERROR("It is only supported Z30 camera.");
    return retCode;
  }

  /*Set the parameters of the pointing zoom*/
  DSTATUS("Set tap zoom multiplier = %d", multiplier);
  retCode = pm->setTapZoomMultiplierSync(index, multiplier, 1);
  if (retCode != ErrorCode::SysCommonErr::Success) {
    DERROR("Set tap zoom multiplier fail. Error code : 0x%lX", retCode);
    ErrorCode::printErrorCodeMsg(retCode);
    DERROR("It is only supported Z30 camera.");
    return retCode;
  }

  /*Set Pointing Zoom's object*/
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

###### Asynchronous
* Construct the callback

```c
/*Set The Pointing Zoom’s Factor*/
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
      /*Register the function to enable the Pointing Zoom*/
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

/*Enable the Pointing Zoom*/
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
      /* Set Pointing Zoom's object */
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

* Register the callback
```c++
  DSTATUS("Set tap zoom multiplier = %d", multiplier);
  pm->setTapZoomMultiplierAsync(index, multiplier, setTapZoomMultiplierCb, &uData);
}
```



