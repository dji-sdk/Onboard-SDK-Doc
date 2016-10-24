---
title: FAQ 
date: 2016-10-14
keywords: [OES, N1/A3, FAQ, stackOverFlow, Github Issues, activation fail, M100, video, lightbridge, flight control, data transparent transmission, open protocol, frequency, commands]
---

## Table of Contents

**Getting Started**

* [How can I become a DJI Onboard SDK Developer?](#how-can-i-become-a-dji-onboard-sdk-developer)
* [Where are the DJI Onboard SDK Resources?](#where-are-the-dji-onboard-sdk-resources)
* [How do I set up hardware for running the Onboard SDK?](#how-do-i-set-up-hardware-for-running-the-onboard-sdk)
* [Where can I get the DJI Open Protocol Documentation?](#where-can-i-get-the-dji-onboard-sdk-protocol-documentation)
* [If I have questions, where can I get help?](#if-i-have-questions-where-can-i-get-help)
* [Why does activation fail?](#why-does-activation-fail)

**Product Related**

* [Which DJI products are supported by the Onboard SDK?](#which-dji-products-are-supported-by-the-onboard-sdk)
* [What does Onboard Embedded System (OES) mean?](#what-does-onboard-embedded-system-oes-mean)
* [Which OES and Operating Systems are supported by Onboard SDK?](#which-oes-and-operating-systems-are-supported-by-onboard-sdk)
* [Is an OES with an OS running needed in the development of Onboard SDK?](#is-an-oes-with-an-os-running-needed-in-the-development-of-onboard-sdk)
* [What are the communication ports between an OES and an N1 or A3 flight controller?](#what-are-the-communication-ports-between-an-oes-and-an-n1-or-a3-flight-controller)
* [Does M100 support third party video capturing devices? Can I use the M100's built-in ‘Lightbridge’ functionality?](#does-m100-support-third-party-video-capturing-devices-can-i-use-the-m100-s-built-in-lightbridge-functionality)

**Platform Related**
* [Manifold - Why does restoring system image cause issues?](#manifold-why-does-restoring-system-image-cause-issues)
* [Manifold - How do I purchase a Manifold?](#manifold-how-do-i-purchase-a-manifold)
* [A3 - Do I need a LightBridge 2 RC to use Onboard SDK?](#a3-do-i-need-a-lightbridge-2-rc-to-use-onboard-sdk)
* [STM32 - Do all parts of the SDK work with low-power embedded systems?](#stm32-do-all-parts-of-the-sdk-work-with-low-power-embedded-systems)

**General SDK**

* [What flight data of M100/M600/A3 can I get via the Onboard SDK?](#what-flight-data-of-m100-m600-a3-can-i-get-via-the-onboard-sdk)
* [With the Open Protocol on UART port, what is the data output frequency of N1/A3?](#with-the-open-protocol-on-uart-port-what-is-the-data-output-frequency-of-n1-a3)
* [Can I encrypt data on the UART line?](#can-i-encrypt-data-on-the-uart-line)
* [How do I get the camera's video feed on the OES?](how-do-i-get-the-camera-s-video-feed-on-the-oes)
* [Suppose some data onboard the drone needs to be transmitted to a mobile device. Can this functionality be supported by Onboard SDK?](#suppose-some-data-onboard-the-drone-needs-to-be-transmitted-to-a-mobile-device-can-this-functionality-be-supported-by-onboard-sdk)
* [For the development of Onboard SDK, can I use some bandwidth from the remote controller to get my own data back to a ground station?](#for-the-development-of-onboard-sdk-can-i-use-some-bandwidth-from-the-remote-controller-to-get-my-own-data-back-to-a-ground-station)
* [Are there any simulators provided for the development of Onboard SDK with M100/M600/A3?](#are-there-any-simulators-provided-for-the-development-of-onboard-sdk-with-m100-m600-a3)
* [Can I set the initial height of the ‘take off’ function manually?](#can-i-set-the-initial-height-of-the-take-off-function-manually)
* [What is the recommended transmission rate for N1/A3 flight controller to receive external commands?](#what-is-the-recommended-transmission-rate-for-n1-a3-flight-controller-to-receive-external-commands)
* [If I choose 'Raw data' in DJI Assistant 2, Flight Data is incorrectly reported when using simulator. Is this a bug?](#if-i-choose-raw-data-in-dji-assistant-2-flight-data-is-incorrectly-reported-when-using-simulator-is-this-a-bug)
* [How do I send commands to the drone when it is flying? Wireless keyboards or Wireless Serial Ports are impractical and unsafe.](#how-do-i-send-commands-to-the-drone-when-it-is-flying-wireless-keyboards-or-wireless-serial-ports-are-impractical-and-unsafe)


## Getting Started

### How can I become a DJI Onboard SDK Developer?

Becoming a DJI Onboard SDK developer is easy. Please see [this](../quick-start/index.html#onboard-application-registration) section in the Quick Start guide for details.

### Where are the DJI Onboard SDK Resources?

All [documentation](http://developer.dji.com/onboard-sdk/documentation) can be found on the DJI developer website.

The Onboard SDK can be cloned from GitHub - [Linux/Qt/STM32](https://github.com/dji-sdk/onboard-sdk) and [ROS](https://github.com/dji-sdk/onboard-sdk-ros). 

### How do I set up hardware for running the Onboard SDK?

The [Hardware Setup Guide](../hardware-setup/index.html) has detailed instructions for setting up the various parts of the system.

### Where can I get the DJI Onboard SDK Protocol Documentation?

The Open Protocol is documented [here](../introduction/index.html).

### If I have questions, where can I get help?

You can use the following methods to get help:

- StackOverFlow 

  Post questions in StackOverFlow with DJI SDK tag: <a href="http://stackoverflow.com/questions/tagged/dji-sdk" target="_blank">dji-sdk</a>

- DJI Onboard SDK Forum

  <a href="http://forum.dev.dji.com/forum-91-1.html" target="_blank">http://forum.dev.dji.com/forum-91-1.html</a>

- Github Issues
  
  <a href="https://github.com/dji-sdk/onboard-sdk/issues" target="_blank">Onboard SDK Issues</a>

  <a href="https://github.com/dji-sdk/onboard-sdk-ros/issues" target="_blank">Onboard SDK ROS Issues</a>
  
- Gitter Chat 

  [Onboard SDK Gitter Room](gitter.im/dji-sdk/Onboard-SDK)
  
- Send Email

  If you prefer email, please send to <dev@dji.com> for help.


### Why does activation fail?

The first time the application communicates with the drone/flight controller, it connects to a DJI Server to verify it's authorized to use the DJI Onboard SDK by sending the Application ID and Key. This process is called activation. 

Reasons for why it might fail include:

* DJI GO needs to be running on the mobile device, and needs internet connectivity the first time it is run after installation (successful activation is locally cached, so internet connectivity is not required after the first initialization).
* App ID/key is incorrect. Check in the <a href="https://developer.dji.com/user/apps/#all" target="_blank"> User Center </a> to confirm the application key.
* The serial port is not connected/opened correctly (baud rate, incorrect hardware connections etc). This might happen on ARM architectures since the Onboard SDK's serial driver does not implement sophisticated checks on this platform.
* The voltages on the UART line are incorrect. The electrical interface is 3.3V TTL.
* RC is not in Mode F. Activation can only happen in mode F.
* API Control is not enabled using DJI Assistant 2. Go to the SDK page on Assistant 2 and check the box marked Enable API Control.

## Product/Hardware Related

### Which DJI products are supported by the Onboard SDK?

The Matrice 100, Matrice 600 and the A3 flight controller are supported by the Onboard SDK.

### What does Onboard Embedded System (OES) mean?

In the context of DJI Onboard SDK documentation, Onboard Embedded System (OES) refers to any devices that can communicate with N1/A3 flight controller and supported by Onboard SDK.

### Which OES and Operating Systems are supported by Onboard SDK?
  
The [Hardware Setup Guide](../hardware-setup/index.html) talks about all supported combinations of OES and aircraft. Refer to the [Architecture Guide](../introduction/architecture-guide.html) for supported OS platforms.

### Is an OES with an OS running needed in the development of Onboard SDK?

Not necessarily, but preferred. We recommend a setup with Ubuntu and ROS but even a simple STM32 MCU without an OS running on it works.

### What are the communication ports between an OES and an N1 or A3 flight controller?
    
An OES can only communicate with N1/A3 flight controller via a UART port.

### Does M100 support third party video capturing devices? Can I use the M100's built-in ‘Lightbridge’ functionality?

Yes, M100 supports third party video capturing device. If you want to use the M100's built-in ‘Lightbridge’ functionality, all you need is the [N1 Video Encoder](http://store.dji.com/product/n1-video-encoder).

## Platform Related

### Manifold - Why does restoring system image cause issues?

If you're seeing blinking mouse cursors, changing text size or general issues with the display, please re-do the restore using Ubuntu 14.04 as the host computer.

### Manifold - How do I purchase a Manifold?

The Manifold is sold for university projects or for other research. Please send email to dev@dji.com stating the purpose of use.

### A3 - Do I need a LightBridge 2 RC to use Onboard SDK?

Currently, you do need a LightBridge 2 RC for first use (specifically, activation). This requirement will be removed in future A3 firmware.

### STM32 - Do all parts of the SDK work with low-power embedded systems?

We support low-power embedded systems for core SDK functionality - all funcitons in the osdk-core library are available with the STM32 (and potentially other low-power OESs). However, more complex functionality such as LiDAR logging and precision trajectory missions are unavailable on bare-metal systems due to insufficient compute power.

## General SDK

### What flight data of M100/M600/A3 can I get via the Onboard SDK?
     
You can get the full state estimate, timestamp and a lot of other information like gimbal data, state machine value etc. Refer to the [Receiving Flight Data](../application-development-guides/programming-guide.html#receiving-flight-data) section in the [Programming Guide](../application-development-guides/programming-guide.html). 

Bit-level protocol information about the state broadcast data can also be found in the [Open Protocol](../../appendix/index.html) Documentation 

### With the Open Protocol on UART port, what is the data output frequency of N1/A3?

The data output frequency for various kinds of state broadcast data (Position, Attitude, Timestamp etc.) can be set via DJI Assistant 2 in the [0, 100Hz] range.

### Can I encrypt data on the UART line?

Yes, AES encryption is available as a option. For more info, please refer to [Encryption](../introduction/index.html#open-protocol-encryption) in the Open Protocol.

### How do I get the camera's video feed on the OES?

You need to use the Manifold as your OES. There is no official support for using other OESs with the X3/X5 camera.

### Suppose some data onboard the drone needs to be transmitted to a mobile device. Can this functionality be supported by Onboard SDK?

Yes. Refer to [Data Transparent Transmission](../introduction/data-transparent-transmission.html).

### For the development of Onboard SDK, can I use some bandwidth from the remote controller to get my own data back to a ground station?
    
Unfortunately, the LightBridge 2 channel does now support transmitting arbitrary forms of data. If you have data in the form of a video stream, use N1 Video Encoder (M100) or HDMI (M600/A3) to stream it back to the RC. If you have some low-bandwidth data, consider using [Data Transparent Transmission](../introduction/data-transparent-transmission.html).

### Are there any simulators provided for the development of Onboard SDK with M100/M600/A3?
    
Yes. The [DJI Assistant 2](http://developer.dji.com/onboard-sdk/downloads/) has a built-in simulator that can be used with Onboard SDK.

### Can I set the initial height of the ‘take off’ function manually?

For now, no. The initial height is set to be about 1.2 meters.

### What is the recommended transmission rate for N1/A3 flight controller to receive external commands?
    
50Hz.
 
### If I choose 'Raw data' in DJI Assistant 2, Flight Data is incorrectly reported when using simulator. Is this a bug?
    
Because raw data is generated by actual sensors on UAV, raw data will not be available in simulator. Please choose fusion data when you use DJI simulator.

### How do I send commands to the drone when it is flying? Wireless keyboards or Wireless Serial Ports are impractical and unsafe.

We agree completely - so since Onboard SDK 3.1.8, we offer a [Mobile-Onboard SDK iOS app](../github-platform-docs/MobileOnboardSDK/Mobile-OSDK.html) that has triggers for all functionality available in the Linux Samples. You can look at the implementation and make triggers for your own commands as well.