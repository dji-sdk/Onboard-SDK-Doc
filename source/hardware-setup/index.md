---
title: Hardware setup
date: 2016-06-24
keywords: [hardware setup，M100 UART Connector, A3 UART Connector]
---

# Hardware Setup guide
This guide will help you connect your onboard embedded system (OES) with the M100 vehicle, M600 vehicle, or A3 flight controller. You may need to build or buy your own cable to connect your OES to a DJI product. Reference the M100 or A3 UART connector diagrams below to build a cable to interface with your OES UART port. The M600 uses an A3 flight controller, which is accessable through the top cover.  See the M600 user manual for details.
> The M100/600/A3 UART electrical interface is 3.3 volt TTL. You must ensure that your OES UART port is compatible to avoid damaging the flight controller.

## M100 UART Connector

![M100UARTConnector](../images/hardwaresetup/Connecter.jpg) 

## A3 UART Connector  

![A3UARTConnector](../images/hardwaresetup/A3UARTPort.png) 

**Note: Do NOT use the Vcc pin to power your own devices. You might damage your OES, A3 or both.**

## M100 + Manifold

The diagram below shows the hardware connection between an M100 and Manifold. Note that: 
- UART cable is provided with the Manifold. 
- M100 to PC connection can be used to run DJI Assistant 2. 
- With DJI Assistant you can enable API, set baudrate and/or run the Simulator.


![M100Manifold](../images/hardwaresetup/M100Manifold.png)

## M100 + PC/Linux machine

The diagram below shows the hardware connection between an M100 and a PC or Linux machine. Note that: 
- M100 UART cable is provided in the box and is also [sold](http://store.dji.com/product/matrice-100-uart-cable) separately. 
- USB to TTL cable can be purchased on [Amazon](https://www.amazon.com/ADAFRUIT-INDUSTRIES-954-SERIAL-RASPBERRY/dp/B00DJUHGHI/ref=sr_1_5?s=electronics&ie=UTF8&qid=1466208644&sr=1-5&keywords=usb+to+ttl).
- The two cables need to be connected on the TTL end to establish communication between M100 and PC/Linux. 
- M100 to PC connection is used to run DJI Assistant 2. 
- With DJI Assistant you can enable API, set baudrate and/or run the Simulator.


![M100PCLinux](../images/hardwaresetup/M100PCLinux.png)


## M100 + STM32

The diagram below shows the hardware connection between an M100 and STM32. Note that: 
- M100 UART cable is provided in the box and is also [sold](http://store.dji.com/product/matrice-100-uart-cable) separately. 
- USB to TTL cable can be purchased on [Amazon](https://www.amazon.com/ADAFRUIT-INDUSTRIES-954-SERIAL-RASPBERRY/dp/B00DJUHGHI/ref=sr_1_5?s=electronics&ie=UTF8&qid=1466208644&sr=1-5&keywords=usb+to+ttl).
- M100 UART cable connects to USART3 connector on STM32. 
- USB-TTL cable connects to USART2 connector on STM32. 
- PC is used for STM32 development. 
- In the STM32 sample App, users can send commands and receive feedback on a Computer. 


![M100STM32](../images/hardwaresetup/M100STM32.png)


## A3 + Manifold

The diagram below shows the hardware connection between an A3 and Manifold. Note that: 
- UART cable referenced in the image is a cable with 0.1 inch female headers on both sides going from Tx port on A3 to Rx port on Manifold and vice-versa. 
- Tx pin on Expansion I/O of the Manifold is pin 15. 
- Rx pin on Expansion I/O of the Manifold is pin 13. 
- Ground pin on Expansion I/O of the Manifold is pin 16. 
- A3 to PC connection is used to run DJI Assistant 2. 
- With DJI Assistant you can enable API, set baudrate and/or run the Simulator.

![A3Manifold](../images/hardwaresetup/A3Manifold.png)


## A3 + PC/Linux machine

The diagram below shows the hardware connection between an A3 and a PC or Linux machine. Note that:
- USB to TTL cable can be purchased on [Amazon](https://www.amazon.com/ADAFRUIT-INDUSTRIES-954-SERIAL-RASPBERRY/dp/B00DJUHGHI/ref=sr_1_5?s=electronics&ie=UTF8&qid=1466208644&sr=1-5&keywords=usb+to+ttl).
- A3 to PC connection is used to run DJI Assistant 2. 
- With DJI Assistant you can enable API, set baudrate and/or run the Simulator. 

![A3PCLinux](../images/hardwaresetup/A3PCLinux.png)


## A3 + STM32

The diagram below shows the hardware connection between an A3 and STM32. Note that:
- UART cable referenced in the image is a cable with 0.1 inch female headers on both sides going from Tx port on A3 to Rx port on the STM32 and vice-versa.  
- USB to TTL cable can be purchased on [Amazon](https://www.amazon.com/ADAFRUIT-INDUSTRIES-954-SERIAL-RASPBERRY/dp/B00DJUHGHI/ref=sr_1_5?s=electronics&ie=UTF8&qid=1466208644&sr=1-5&keywords=usb+to+ttl).
- UART cable betweenn A3 and STM32 connects to USART3 connector on STM32. 
- USB-TTL cable connects to USART2 connector on STM32. 
- PC is used for STM32 development. 
- In the STM32 sample App, users can send commands and receive feedback on a Computer.


![A3STM32](../images/hardwaresetup/A3STM32.png)
