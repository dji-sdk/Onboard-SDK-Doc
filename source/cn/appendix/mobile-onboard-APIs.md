---
title: Mobile and Onboard SDK APIs
date: 2017-11-23
version: 3.4
keywords: []
---

# Onboard computer to Mobile Device (Mobile APIs)

The following code snippet shows you how to receive the data on different mobile platforms including iOS and Android.

- iOS

Please implement the following delegate method of DJIFlightControllerDelegate:

~~~objc
- (void)flightController:(DJIFlightController *_Nonnull)fc didReceiveDataFromOnboardSDKDevice:(NSData *_Nonnull)data;
~~~

For more details, please check **DJIFlightController.h** file in the iOS SDK.

- Android

Please implement the `setOnboardSDKDeviceDataCallback` callback function as shown below:

~~~java
Aircraft mAircraft = (Aircraft)DJISDKManager.getInstance().getProduct();
FlightController mFlightController = mAircraft.getFlightController();
mFlightController.setOnboardSDKDeviceDataCallback(new FlightController.OnboardSDKDeviceDataCallback() {
    @Override
    public void onReceive(byte[] bytes) {

    }
});
~~~

For more details, please check the **FlightController** class in the Android SDK.

# Mobile Device to Onboard computer (Mobile APIs)

The following SDK interface can help you understand how to communicate with Onboard SDK Device on different mobile platforms including iOS and Android.

- iOS

Please use the following method of DJIFlightController:

~~~objc
- (void)sendDataToOnboardSDKDevice:(NSData *_Nonnull)data withCompletion:(DJICompletionBlock)completion;
~~~

For more details, please check **DJIFlightController.h** file in the iOS SDK.

- Android

Please implement the `sendDataToOnboardSDKDevice` method of DJIFlightController as shown below:

~~~java
Aircraft mAircraft = (Aircraft)DJISDKManager.getInstance().getProduct();
FlightController mFlightController = mAircraft.getFlightController();
mFlightController.sendDataToOnboardSDKDevice(data, new CommonCallbacks.CompletionCallback() {
    @Override
    public void onResult(DJIError error) {

    }
});
~~~

For more details, please check the **FlightController** class in the Android SDK. 


