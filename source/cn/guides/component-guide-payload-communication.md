---
title: Payload - Onboard SDK communication
version: 3.8.1
date: 2019-05-24
keywords: [Payload Onboard SDK]
---

## Introduction
The Payload SDK offers a new set of protocols that let your payload device communicate with the aircraft’s internal systems such as flight controller, GPS module, transmission system and more.
The Onboard SDK allows developers to monitor and control the UAV from an onboard computer directly connected to the UAV through serial (UART) and USB interfaces.

The communication interface between the Payload SDK and Onboard SDK enables the communication link between payload device and onboard computer.

The upstream (payload device to onboard computer) bandwidth is approximately _4KB/s_ while the downstream (onboard computer to payload device) bandwidth is approximately _4KB/s_

![OSDK-PSDK](../../images/common/OSDK_PSDK_Comm.png)

## Uses

Communication between a Payload SDK application device and an Onboard SDK application can take full advantage of the capabilities of payload device and onboard computer.
Some example scenarios include:

* Onboard computer shares processed third party sensor information with the payload device.
* Payload device is able to send real-time data to onboard computer and hand over the data processing proscess to the onboard computer.

## Sample

As a way to demonstrate how to implement the communication between payload device and onboard computer, a [sample](./../sample-doc/psdk-comm.html) shows the basic usage of this interface.


