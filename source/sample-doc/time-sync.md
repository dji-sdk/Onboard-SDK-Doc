---
title: Time Sync sample
date: 2020-01-20
version: 4.0
keywords: [sample, timestamp, synchronization, gps, rtk, pps, nmea]
---

## Introduction

The Time Sync samples show how to access the data of time sync and the corresponding hardware pulse.
For more information on what Time Sync features, please consult the [time sync guide](../guides/component-guide-time-sync.html).

## Goals

Two samples are provided to show the example usage of how to access the data. 
Before you start, please ensure that your aircraft has good GPS/RTK reception.

The expected data are:

- NMEA GNGSA packets at 5Hz
- NMEA GNRMC packets at 5Hz
- UTC time tag for the upcoming hardware pulse at 1Hz
- PPS source information at 1Hz

The time sync sample is available on Linux.

## Output

The output of the time sync callback sample is shown below:
```
STATUS/1 @ PPSSourceCallback, L76: PPS pulse is coming from RTK
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,26,14,16,34,31,35,32,,,,,,3.8,1.4,3.5,1*31
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,69,,,,,,,,,,,,3.8,1.4,3.5,2*39
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,09,,,,,,,,,,,,3.8,1.4,3.5,3*3E
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,16,06,07,09,14,,,,,,,,3.8,1.4,3.5,4*3A
STATUS/1 @ NMEACallback, L46: $GNRMC,071859.00,A,2231.52026169,N,11356.15491846,E,0.254,353.5,160120,2.9,W,A,V*40
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,26,14,16,31,32,,,,,,,,3.8,1.5,3.5,1*31
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,69,,,,,,,,,,,,3.8,1.5,3.5,2*38
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,09,,,,,,,,,,,,3.8,1.5,3.5,3*3F
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,16,06,07,09,14,,,,,,,,3.8,1.5,3.5,4*3B
STATUS/1 @ NMEACallback, L46: $GNRMC,071859.20,A,2231.52026141,N,11356.15491113,E,0.212,189.5,160120,2.9,W,A,V*46
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,26,14,16,31,,,,,,,,,4.2,1.7,3.9,1*33
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,69,,,,,,,,,,,,4.2,1.7,3.9,2*3B
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,09,24,,,,,,,,,,,4.2,1.7,3.9,3*3A
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,16,06,07,09,14,,,,,,,,4.2,1.7,3.9,4*38
STATUS/1 @ NMEACallback, L46: $GNRMC,071859.40,A,2231.52025688,N,11356.15491514,E,0.251,56.2,160120,2.9,W,A,V*71
STATUS/1 @ UTCTimeCallback, L56: The UTC time for the next PPS pulse (ard 500ms) is...
STATUS/1 @ UTCTimeCallback, L57: UTC 200116 071900 5 
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,26,14,16,31,,,,,,,,,4.2,1.7,3.9,1*33
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,69,,,,,,,,,,,,4.2,1.7,3.9,2*3B
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,09,24,,,,,,,,,,,4.2,1.7,3.9,3*3A
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,16,06,07,09,14,,,,,,,,4.2,1.7,3.9,4*38
STATUS/1 @ NMEACallback, L46: $GNRMC,071859.60,A,2231.52025782,N,11356.15491893,E,0.048,89.8,160120,2.9,W,A,V*78
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,26,16,31,,,,,,,,,,4.4,2.1,3.9,1*35
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,69,,,,,,,,,,,,4.4,2.1,3.9,2*38
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,09,24,,,,,,,,,,,4.4,2.1,3.9,3*39
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,16,06,07,09,14,,,,,,,,4.4,2.1,3.9,4*3B
STATUS/1 @ NMEACallback, L46: $GNRMC,071859.80,A,2231.52024528,N,11356.15491295,E,0.361,201.4,160120,2.9,W,A,V*4F
STATUS/1 @ FCTimeInUTCCallback, L64: Received Flight controller time in UTC reference...
STATUS/1 @ FCTimeInUTCCallback, L65: FC: 310878558, UTC time: 71900, UTC date: 200116
STATUS/1 @ PPSSourceCallback, L76: PPS pulse is coming from RTK
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,26,16,31,,,,,,,,,,4.4,2.1,3.9,1*35
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,69,,,,,,,,,,,,4.4,2.1,3.9,2*38
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,09,24,,,,,,,,,,,4.4,2.1,3.9,3*39
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,16,06,07,09,14,,,,,,,,4.4,2.1,3.9,4*3B
STATUS/1 @ NMEACallback, L46: $GNRMC,071900.00,A,2231.52024521,N,11356.15489939,E,0.350,339.8,160120,2.9,W,A,V*43
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,26,16,31,,,,,,,,,,4.4,2.1,3.9,1*35
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,69,,,,,,,,,,,,4.4,2.1,3.9,2*38
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,09,24,,,,,,,,,,,4.4,2.1,3.9,3*39
STATUS/1 @ NMEACallback, L46: $GNGSA,M,3,16,06,07,09,14,,,,,,,,4.4,2.1,3.9,4*3B
```
An screenshot of the M210 V2 RTK hardware pulse and the data on serial line from the logic analyzer is shown below

![Time-sync-output](../images/samples/pps-uart-logic-analyzer.png)