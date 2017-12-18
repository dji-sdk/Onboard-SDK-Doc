---
title: Running your DJI OSDK Application
date: 2017-11-23
version: 3.4
keywords: [write apps, run apps, SDK, integrate, DJI]
---

## Onboard Computer Checklist

- Provide your DJI OSDK App ID and Key to your application. In the samples, this is done in the form of a config file parsed before activation.
- Set your serial port and baudrate in your application. In the samples, this is done in the form of a config file parsed before opening the serial port.
- Make sure you have permissions to read from and write to the serial and USB port. Follow the [Environment Setup Guide](environment-setup.html) for instructions on how to do this.
- For M210, extra steps are required. Please check out [M210 Onboard Computer checklist](../M210-Docs/oes-checklist.html).

## Aircraft Checklist

- Consult the [Hardware Setup Guide](hardware-setup.html) to check your API port connections.
- Make sure your Aircraft/FC has more than 50% battery power.
- If you are using LightBridge 2/ S-BUS, make sure your remote controller is powered on and paired. If you are using A3/N3 without an RC, consult the [Environment Setup](environment-setup.html) for more.
- Connect your Aircraft/FC's USB port to a computer running DJI Assistant 2
- On the SDK Page confirm that
    - The box titled `Enable API Control` is checked.
    - The baudrate is the same as the one provided on the onboard computer. If you had to change this setting, re-start the FC/Aircraft.
    - **Not all** the broadcast telemetries are set to `Do Not Send`, i.e. at least something is broadcasting.
- Upgrade to the newest firmware that is [officially supported](../appendix/versioning.html) by the OSDK version you are using.
- For M210, extra steps are required. Please check out [M210 aircraft checklist](../M210-Docs/aircraft-checklist.html).

## Simulation Checklist

- On the Simulator page,
    - Set your desired GPS location.
    - If your version of Assistant allows you to toggle `Battery Simulation`, set it to `OFF`.
    - Start the Simulator.
- For M210, extra steps are required. Please check out [M210 simulation checklist](../M210-Docs/simulation-checklist.html).

## Real-world Tests Checklist

- Please make sure you are in compliance with the flight laws in effect at your chosen flight location.
- Follow the setup instructions in your aircraft's user manual to ensure your aircraft is in good condition for a flight.
- Make sure you have tested your application in simulation before you try a real-world flight test.
- For M210, extra steps are required. Please check out [M210 real-world flight checklist](../M210-Docs/real-world-test-checklist.html).

