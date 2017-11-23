# Onboard computer to Mobile Device (Mobile APIs)

The following code snippet shows you how to receive the data on different mobile platforms including iOS and Android.

- iOS

Please implement the following delegate method of DJIFlightControllerDelegate:

~~~objc
- (void)flightController:(DJIFlightController *)fc didReceiveDataFromExternalDevice:(NSData *)data;
~~~

For more details, please check **DJIFlightController.h** file in the iOS SDK.

- Android

Please implement the `FlightControllerReceivedDataFromExternalDeviceCallback` callback function as shown below:

~~~java
DJIAircraft mAircraft = (DJIAircraft)DJISDKManager.getInstance().getDJIProduct();
DJIFlightController mFlightController = mAircraft.getFlightController();

mFlightController.setReceiveExternalDeviceDataCallback(new FlightControllerReceivedDataFromExternalDeviceCallback() {         
          @Override
          public void onResult(byte[] data) {
          }
        });
~~~

For more details, please check the **FlightController** class in the Android SDK.

# Mobile Device to Onboard computer (Mobile APIs)

The following SDK interface can help you understand how to communicate with Onboard SDK Device on different mobile platforms including iOS and Android.

- iOS

Please use the following method of DJIFlightController:

~~~objc
- (void)sendDataToOnboardSDKDevice:(NSData *)data withCompletion:(DJICompletionBlock)completion;
~~~

For more details, please check **DJIFlightController.h** file in the iOS SDK.

- Android

Please implement the `sendDataToOnboardSDKDevice` method of DJIFlightController as shown below:

~~~java
DJIAircraft mAircraft = (DJIAircraft)DJISDKManager.getInstance().getDJIProduct();
DJIFlightController mFlightController = mAircraft.getFlightController();

mFlightController.sendDataToOnboardSDKDevice(data,
                new DJICompletionCallback() {
                    @Override
                    public void onResult(DJIError pError) {
                    }
                });
~~~

For more details, please check the **FlightController** class in the Android SDK. 


