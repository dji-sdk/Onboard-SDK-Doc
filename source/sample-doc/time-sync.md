---
title: Time Sync sample
date: 2019-03-20
version: 3.8
keywords: [sample, timestamp, synchronization, gps, rtk, pps, nmea]
---

## Introduction

The Time Sync samples show how to access the data of time sync and the corresponding hardware pulse.
For more information on what Time Sync features, please consult the [time sync guide](../guides/component-guide-time-sync.html).

## Goals

Two samples are provided to show the example usage of how to access the data. 
Before you start, please ensure that your aircraft has good GPS/RTK reception.

The expected data are:

- NMEA GSA packets at 5Hz
- NMEA RMC packets at 5Hz
- UTC time tag for the upcoming hardware pulse at 1Hz
- PPS source information at 1Hz

The time sync sample is available on Linux.

## Output

The output of the time sync callback sample is shown below:
```
STATUS/1 @ PPSSourceCallback, L76: PPS pulse is coming from RTK
STATUS/1 @ NMEACallback, L46: $GPGSA,M,2,06,02,12,28,,,,,,,,,2.2,1.1,2.5*35
STATUS/1 @ NMEACallback, L46: $GLGSA,M,2,79,82,78,,,,,,,,,,2.2,1.1,2.5*2F
STATUS/1 @ NMEACallback, L46: $GAGSA,M,2,30,34,,,,,,,,,,,2.2,1.1,2.5*2D
STATUS/1 @ NMEACallback, L46: $BDGSA,M,2,,,,,,,,,,,,,2.2,1.1,2.5*29
STATUS/1 @ NMEACallback, L46: $GPRMC,003258.00,A,37.42162477,N,122.13716552,W,0.020,275.8,230319,108.6,E*4B
STATUS/1 @ NMEACallback, L46: $GPGSA,M,2,06,02,12,28,,,,,,,,,2.2,1.1,2.5*35
STATUS/1 @ NMEACallback, L46: $GLGSA,M,2,79,82,78,,,,,,,,,,2.2,1.1,2.5*2F
STATUS/1 @ NMEACallback, L46: $GAGSA,M,2,30,34,,,,,,,,,,,2.2,1.1,2.5*2D
STATUS/1 @ NMEACallback, L46: $BDGSA,M,2,,,,,,,,,,,,,2.2,1.1,2.5*29
STATUS/1 @ NMEACallback, L46: $GPRMC,003258.20,A,37.42162509,N,122.13716600,W,0.010,242.1,230319,108.5,E*48
STATUS/1 @ NMEACallback, L46: $GPGSA,M,2,06,02,12,28,,,,,,,,,2.2,1.1,2.5*35
STATUS/1 @ NMEACallback, L46: $GLGSA,M,2,79,82,78,,,,,,,,,,2.2,1.1,2.5*2F
STATUS/1 @ NMEACallback, L46: $GAGSA,M,2,30,34,,,,,,,,,,,2.2,1.1,2.5*2D
STATUS/1 @ NMEACallback, L46: $BDGSA,M,2,,,,,,,,,,,,,2.2,1.1,2.5*29
STATUS/1 @ NMEACallback, L46: $GPRMC,003258.40,A,37.42162539,N,122.13716644,W,0.015,281.4,230319,108.6,E*41
STATUS/1 @ UTCTimeCallback, L56: The UTC time for the next PPS pulse (ard 500ms) is...
STATUS/1 @ UTCTimeCallback, L57: UTC 190323 003259 3 
STATUS/1 @ NMEACallback, L46: $GPGSA,M,2,06,02,12,28,,,,,,,,,2.2,1.1,2.5*35
STATUS/1 @ NMEACallback, L46: $GLGSA,M,2,79,82,78,,,,,,,,,,2.2,1.1,2.5*2F
STATUS/1 @ NMEACallback, L46: $GAGSA,M,2,30,34,,,,,,,,,,,2.2,1.1,2.5*2D
STATUS/1 @ NMEACallback, L46: $BDGSA,M,2,,,,,,,,,,,,,2.2,1.1,2.5*29
STATUS/1 @ NMEACallback, L46: $GPRMC,003258.60,A,37.42162572,N,122.13716691,W,0.031,160.9,230319,108.6,E*43
STATUS/1 @ NMEACallback, L46: $GPGSA,M,2,06,02,12,28,,,,,,,,,2.2,1.1,2.5*35
STATUS/1 @ NMEACallback, L46: $GLGSA,M,2,79,82,78,,,,,,,,,,2.2,1.1,2.5*2F
STATUS/1 @ NMEACallback, L46: $GAGSA,M,2,30,34,,,,,,,,,,,2.2,1.1,2.5*2D
STATUS/1 @ NMEACallback, L46: $BDGSA,M,2,,,,,,,,,,,,,2.2,1.1,2.5*29
STATUS/1 @ NMEACallback, L46: $GPRMC,003258.80,A,37.42162607,N,122.13716737,W,0.032,280.1,230319,108.6,E*47
STATUS/1 @ FCTimeInUTCCallback, L64: Received Flight controller time in UTC reference...
STATUS/1 @ FCTimeInUTCCallback, L65: FC: 1925605442, UTC time: 003259, UTC date: 190323
STATUS/1 @ PPSSourceCallback, L76: PPS pulse is coming from RTK
STATUS/1 @ NMEACallback, L46: $GPGSA,M,2,06,02,12,28,,,,,,,,,2.2,1.1,2.5*35
STATUS/1 @ NMEACallback, L46: $GLGSA,M,2,79,82,78,,,,,,,,,,2.2,1.1,2.5*2F
STATUS/1 @ NMEACallback, L46: $GAGSA,M,2,30,34,,,,,,,,,,,2.2,1.1,2.5*2D
STATUS/1 @ NMEACallback, L46: $BDGSA,M,2,,,,,,,,,,,,,2.2,1.1,2.5*29
STATUS/1 @ NMEACallback, L46: $GPRMC,003259.00,A,37.42162645,N,122.13716783,W,0.032,309.7,230319,108.5,E*42
STATUS/1 @ NMEACallback, L46: $GPGSA,M,2,06,02,12,28,,,,,,,,,2.2,1.1,2.5*35
STATUS/1 @ NMEACallback, L46: $GLGSA,M,2,79,82,78,,,,,,,,,,2.2,1.1,2.5*2F
STATUS/1 @ NMEACallback, L46: $GAGSA,M,2,30,34,,,,,,,,,,,2.2,1.1,2.5*2D
STATUS/1 @ NMEACallback, L46: $BDGSA,M,2,,,,,,,,,,,,,2.2,1.1,2.5*29
STATUS/1 @ NMEACallback, L46: $GPRMC,003259.20,A,37.42162679,N,122.13716826,W,0.063,318.7,230319,108.5,E*4
```
An screenshot of the M210 V2 RTK hardware pulse and the data on serial line from the logic analyzer is shown below

![Time-sync-output](../images/samples/pps-uart-logic-analyzer.png)