# mLRS Documentation: DroneCAN for ArduPilot Systems #

([back to main page](../README.md))

DroneCAN can be utilized for MAVLink and RC with mLRS instead of traditional serial communication if both the flight controller and receiver have the hardware necessary to support it.

## Wiring & Powering

TBD

## mLRS Receiver Settings

With a CAN-enabled firmware flashed, the receiver will output RC channel data on the CAN bus without any further settings.

In order to enable also the serial (MAVLink) communication via DroneCAN, one needs to set "Rx Serial Port = can".

## ArduPilot Settings

The following parameters need to be set to enable MAVLink and RC over DroneCAN.

Setup the CAN driver, protocol and enable the virtual serial port, then reboot the flight controller:

- CAN_P1_DRIVER = 1
- CAN_D1_PROTOCOL = 1 (set to 1 by default)
- CAN_D1_UC_SER_EN = 1

Configure the DroneCAN virtual serial port:

- CAN_D1_UC_S1_IDX = 0
- CAN_D1_UC_S1_NOD = 68
- CAN_D1_UC_S1_PRO = 2

Adjust the DroneCAN streams:

- CAN_D1_UC_NTF_RT = 1
- CAN_D1_UC_SRV_RT = 0

Note: This assumes that you are not using DroneCAN for servo outputs.

Enable RC Channels via DroneCAN:

- RC_PROTOCOLS bitmask should have the 'DroneCAN' bit enabled

Note: Do not enable rc_override or rc_channels in the mLRS configuration when using RC Channels via DroneCAN as it adds unnecessary traffic on the bus.

Adjust the Stream Rates:

Stream rates should be set based on the RF mode in use, they can be found on the ([CRSF Page](../CRSF.md#stream-rates))

Note: When configuring SRy parameters for DroneCAN, 'y' will correspond to the number of regular serial ports that have you enabled for MAVLink.  For example, if you are using Serial0 for USB and Serial2 for MAVLink then you'll have to modify the SR2 parameters for the DroneCAN connection.

- Serial0 will use SR0
- Serial2 will use SR1
- DroneCAN will use SR2
