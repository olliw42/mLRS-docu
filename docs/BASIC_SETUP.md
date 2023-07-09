# mLRS Documentation: Basic Setup #

([back to main page](../README.md))

mLRS can work with any radio which provides an SBus output, which should be really every radio. This page describes this most basic setup.

In this setup, the radio only feeds the RC data to the mLRS Tx module (via SBus) but there is no communication between radio and mLRS Tx module otherwise. There is thus no such thing as telemetry in the radio. The serial/MAVLink data stream is available via the serial/UART port on the mLRS Tx module, and it is up to you how to make use of it. Also, there is no such thing as a Lua script for configuration, configuration of the mLRS sytem has to be done via the CLI (or OLED if available).

For this basic setup, the mLRS Tx module needs to be put into "SBUS mode". In addition, the radio needs to be set up for SBus, but this proceeds exactly as described in common tutorials. In principle, there is no specific configuration of the mLRS receiver neccessary. It is however recommended to set it up for CRSF instead of SBus if possible. If a MAVLink serial stream is used, then it is strongly recommended to also set the system into "mavlink mode".

Note: An ArduPilot flight controller is assumed. For PX4 and iNav it needs to be tested and seen.

<img src="images/mLRS-docu-setup-basic-for-sbus-radios-02.jpg" width="800px">

## mLRS Tx Module Setup

- Tx Ch Source = sbus
- Tx Ser Dest = serial or serial2 (not mbridge!)

If the serial data stream is MAVLink then it is recommended to set the respective parameter in the receiver (see below).

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

Depending on your setup, you may also want to set MAVLink stream rates (SRx parameters). You can follow the settings described in [CRSF Telemetry and Yaapu Telemetry App](CRSF.md).
