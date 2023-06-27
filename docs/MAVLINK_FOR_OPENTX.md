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

Note: An ArduPilot flight controller is assumed. For PX4 it needs to be tested and seen. iNAV won't work AFAIK, as iNAV is not a proper MAVLink component.


## mLRS Tx Module Setup

- Tx Ch Source = mbridge
- Tx Ser Dest = mbridge
- Tx Snd RadioStat = off

Note: There are situations in which it can be usefull to enable "Tx Snd RadioStat", but you should do this only if you know what you are doing.


## ArduPilot Setup

Configuration of a serial for MAVLink v2

- SERIALx_BAUD = 57 
- SERIALx_OPTIONS = 0
- SERIALx_PROTOCOL = 2

Some further configurations are needed depending on the setup of the mLRS receiver.


## OpenTx Radio Setup

- MDL->MODEL SETUP->External RF->Mode = mBridge

For more details on other possible configurations, please consult the MAVLink for OpenTx project discussion channels.


## mLRS Rx Module Setup

These configurations are not strictly neccesary, but strongly recommended.

- Rx Ser Link Mode = mavlink
- Rx Snd RadioStat = ardu_1

It is also recommended to use the CRSF protocol instead of e.g. SBus if possible, i.e., set

- Rx Out Mode = crsf

To avoid needing a separate signal wire for rc data, it is possible to send the rc data via a MAVLink message to the flight controller. In this case set

- Rx Snd RcChannel = rc override

Note: It is recommended to use the CRSF protocol for rc data since you get benefits like better link statistics that aren't available when sending rc data via MAVLink.

