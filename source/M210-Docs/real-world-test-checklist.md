---
title: M210 Real-world Tests Checklist
date: 2017-10-10
keywords: [M210, linux, ros, onboard computer, OES, USB, libusb, udev, configuration]
---

DJI flight controller has a safety feature to prevent users accidentally take off aircraft while developing their applications. Unless in simulation, the flight controller does not allow aircraft to arm the motors when USB is connected. An example of the warning message is shown in below picture. 

The [Advanced Sensing](../guides/component-guide-advanced-sensing-stereo-camera.html) feature on M210 contradicts with this safety feature since it requires USB to receive image data. A configuration tool located inside `utility/bin/` is provided to disable it. This configuration requires OSDK activated and does not persist through power cycles for safety concern, please configure it before every flight. Please choose the right executable depending on your processor. Example usage is shown below.
````
./M210ConfigTool --usb-port /dev/ttyACM0 --config-file UserConfig.txt --usb-connected-flight on
````


![m210_usb_connected_flight](../images/workflow/m210_usb_connected_flight_app.PNG)
