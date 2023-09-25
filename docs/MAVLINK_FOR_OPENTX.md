# mLRS Documentation: MAVLink for OpenTx #

([back to main page](../README.md))

This page describes how to set up a mLRS system for OpenTx radios running the MAVLink for OpenTx firmware.

Five steps need to be completed:
1. The OpenTx radio needs to be flashed with the MAVLink for OpenTx firmware.
2. The radio needs to be configured. 
3. The mLRS Tx module needs to be put into "mBridge mode".
4. The mLRS system needs to be put into "MAVLink mode".
5. The flight controller needs to be set up for MAVLink on a serial port.

Step 1. is beyond the scope of this article; please consult the project's discussion channels.

Note: An ArduPilot flight controller is assumed. For PX4 it needs to be tested and seen. INAV won't work AFAIK, as INAV is not a proper MAVLink component.

## OpenTx Radio Setup

- MDL->MODEL SETUP->External RF->Mode = mBridge

For more details on other possible configurations, please consult the MAVLink for OpenTx project discussion channels.

## mLRS Tx Module Setup

- Tx Ch Source = mbridge
- Tx Ser Dest = mbridge
- Tx Snd RadioStat = off

Note: There are situations in which it can be useful to enable "Tx Snd RadioStat", but you should do this only if you know what you are doing.

## mLRS Receiver Setup

The configuration of the mLRS receiver can follow exactly the description in [CRSF Telemetry and Yaapu Telemetry App: mLRS Rx Module Setup](CRSF.md#mlrs-rx-module-setup).

It is possible to avoid the separate signal wire for the RC data, by sending the RC data via a MAVLink message to the flight controller. For this set:

- Rx Snd RcChannel = rc override

Note: It is recommended to use the CRSF protocol for the RC data, since you get benefits like better link statistics that are not available when sending the RC data via MAVLink.

## ArduPilot Setup

### MAVLink Serial Port

- SERIALx_BAUD:
    - 57 for 31 Hz, 50 Hz
    - 38 for 19 Hz (57 works very well too, only parameter download is slower)
    - 230 for FLRC
- SERIALx_PROTOCOL = 2 (important, do not use MAVLink v1!)
- SERIALx_OPTIONS = 0

Note: 'x' refers to the serial port of your flight controller used for MAVLink

### Stream Rates

In contrast to the other setups, the SRy parameters for the stream rates do not need to be configured here (i.e., can be left at zero). The MAVLink for OpenTx firmware requests the required streams itself.

Only if the settings by the MAVLink for OpenTx firmware should be overruled, the SRy parameters can be configured as described in [CRSF Telemetry and Yaapu Telemetry App: ArduPilot Setup](CRSF.md#ardupilot-setup).

Note: While the MAVLink for OpenTx radio is a full-fledged GCS in MAVLink terminology, it is not recognized by ArduPilot as its GCS, since the MY_GCS parameter is set by default to MissionPlanner/QGC. Accordingly, setting e.g. SERIALx_OPTIONS = 4096 has no effect.

### CRSF Receiver

The configuration of the receiver settings in the ArduPilot flight controller can follow exactly the description in [CRSF Telemetry and Yaapu Telemetry App: ArduPilot Setup](CRSF.md#ardupilot-setup).


