# mLRS Documentation: MAVLink for OpenTx #

([back to main page](../README.md))

This page describes how to set up a mLRS system for OpenTx radios running the MAVLink for OpenTx firmware.

Four steps need to be completed:
1. The OpenTx radio needs to be flashed with the MAVLink for OpenTx firmware.
2. The mLRS Tx module needs to be put into "mBridge mode".
3. The flight controller needs to be set up for MAVLink on a serial port.
4. The radio needs to be configured. 

Step 1. is beyond the scope of this article; please consult the project's discussion channels.

In principle, there is no specific configuration of the mLRS receiver neccessary. It is however recommended to set the receiver into "mavlink mode" and to use the CRSF protocol, as described below.

Note: An ArduPilot flight controller is assumed. For PX4 it needs to be tested and seen. INAV won't work AFAIK, as INAV is not a proper MAVLink component.

## OpenTx Radio Setup

- MDL->MODEL SETUP->External RF->Mode = mBridge

For more details on other possible configurations, please consult the MAVLink for OpenTx project discussion channels.

## mLRS Tx Module Setup

- Tx Ch Source = mbridge
- Tx Ser Dest = mbridge
- Tx Snd RadioStat = off

Note: There are situations in which it can be usefull to enable "Tx Snd RadioStat", but you should do this only if you know what you are doing.

## mLRS Receiver Setup

The configuration of the mLRS receiver can follow exactly the description in [CRSF Telemetry and Yaapu Telemetry App: mLRS Rx Module Setup](CRSF.md#mlrs-rx-module-setup).

It is possible to avoid the separate signal wire for the RC data, by sending the RC data via a MAVLink message to the flight controller. For this set

- Rx Snd RcChannel = rc override

Note: It is recommended to use the CRSF protocol for the RC data, since you get benefits like better link statistics that are not available when sending the RC data via MAVLink.

## ArduPilot Setup

The configuration of the ArduPilot flight controller can follow exactly the description in [CRSF Telemetry and Yaapu Telemetry App: ArduPilot Setup](CRSF.md#ardupilot-setup).



