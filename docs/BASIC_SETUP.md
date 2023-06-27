# mLRS Documentation: Basic Setup #

([back to main page](../README.md))

mLRS can work with any radio which provides an SBus output, which should be really every radio. This page describes this most basic setup.

In this setup, the radio only feeds the rc data to the mLRS Tx module (via SBus) but there is no communication between radio and mLRS Tx module with regards to the serial/MAVLink data stream. There is thus no thing such as telemetry in the radio. The serial/MAVLink data stream is available via a UART port on the mLRS Tx module, and it is up to you how to make use of it.

For this basic setup, the mLRS Tx module needs to be put into "SBUS mode". Of course, in addition, the radio needs to be set up for SBus, but this proceeds exactly as described in common tutorials. Also, if a MAVLink serial stream is used, it is recommended to set the Tx module into "mavlink mode".

In principle, there is no specific configuration of the mLRS receiver neccessary. It is however recommended to also set the receiver into "mavlink mode" if a MAVLink serial stream is used. It is also recommended to set it up for CRSF instead of SBus if possible.

Note: An ArduPilot flight controller is assumed. For PX4 and iNav it needs to be tested and seen.


## mLRS Tx Module Setup

- Tx Ch Source = sbus
- Tx Ser Dest = serial or serial2 (not mbridge!)

If the serial data stream is MAVLink then it is recommended to set the respective parameter in the receiver (see below), as well as:

- Tx Snd RadioStat = off


## mLRS Rx Module Setup

If your flight controller supports CRSF, then it is recommended to choose it, i.e., set

- Rx Out Mode = crsf

Else set "Rx Out Mode" to "sbus" or "sbus inv".

These configurations are not strictly neccesary, but highly recommended if the serial data stream is MAVLink:

- Rx Ser Link Mode = mavlink
- Rx Snd RadioStat = ardu_1


## ArduPilot Setup

Setting up ArduPilot for a SBus or CRSF receiver can be a bit tricky by times, and there can be more than one way to achieve it. It is best to consult the ArduPilot wiki, or ask in the ArduPilot discussion channel.

Configuration of a serial for MAVLink v2

- SERIALx_BAUD = 57 
- SERIALx_OPTIONS = 0
- SERIALx_PROTOCOL = 2

Depending on your setup, you may also want to set MAVLink stream rates (SRx parameters).


