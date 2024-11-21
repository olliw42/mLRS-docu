# mLRS Documentation: DroneCAN for ArduPilot Systems #

([back to main page](../README.md))

DroneCAN can be utilized for MAVLink and RC with mLRS instead of traditional serial communication if both the flight controller and receiver have the hardware necessary to support it.

## Wiring & Powering

TBD

## mLRS Receiver Settings

#### RC

With a CAN-enabled firmware flashed, the receiver will output RC channels data on the CAN bus without any further settings.

#### MAVLink

In order to enable serial (MAVLink) communication via DroneCAN, one needs to set:

- "Rx Serial Port" = "can"

***Note***: Do not enable "rc_override" or "rc_channels" in the mLRS receiver settings when using MAVLink via DroneCAN as it adds substantial and unnecessary traffic on the CAN bus.

## ArduPilot Settings

The following parameters need to be set to enable RC and MAVLink over DroneCAN.

#### DroneCAN

Setup the CAN driver, protocol and enable the virtual serial support:

- CAN_P1_DRIVER = 1
- CAN_D1_PROTOCOL = 1 (is set to 1 by default)
- CAN_D1_UC_SER_EN = 1 (only needed when MAVLink via DroneCAN is desired)

Then reboot the flight controller.

#### RC

Enable RC channels via DroneCAN:

- RC_PROTOCOLS bitmask should have the 'DroneCAN' bit enabled

#### MAVLink

Configure the DroneCAN virtual serial port (mandatory settings):

- CAN_D1_UC_S1_BD = 57 (57600) (see also below in section Limitations)
- CAN_D1_UC_S1_IDX = 0
- CAN_D1_UC_S1_NOD = 68
- CAN_D1_UC_S1_PRO = 2

Adjust the DroneCAN streams (optional settings):

- CAN_D1_UC_NTF_RT = 1
- CAN_D1_UC_SRV_RT = 0

***Note***: This assumes that you are not using DroneCAN for servo outputs.

Adjust the MAVLink stream rates:

Stream rates should be set as recommended on the [CRSF page](CRSF.md#stream-rates).

***Note***: When configuring SRy parameters for DroneCAN, 'y' will correspond to the number of regular and virtual serial ports that you have enabled for MAVLink. For example, if you are using Serial0 for USB and Serial2 for MAVLink then you will have to modify the SR2 parameters for the DroneCAN connection:

- Serial0 will use SR0
- Serial2 will use SR1
- DroneCAN will use SR2

## Limitations

Receivers using MAVLink via DroneCAN are a relatively new application of ArduPilot's DroneCAN, and issues not seen before may be exposed now. ArduPilot has been found to have these limitations:

#### All Versions of ArduPilot

- In MissionPlanner, on the DroneCAN/UAVCAN page one cannot communicate with the CAN nodes when connected via the mLRS link (mLRS has code to prevent this, as there is a critical bug in some ArduPilot versions which would lead to a crash of ArduPilot). It works normally when the flight controller is connected to MissionPlanner e.g. via USB.
- RC out functionality for CRSF or SBus cannot be used in combination with DroneCAN RC. As DroneCAN RC only provides RSSI and not LQ or SNR, it might be tempting to use CRSF in addition but this will not work.
- OSD is limited to RSSI.
- The MAVLink stream rates cannot be set to too high values as this will lead to lost messages.

#### ArduPilot 4.5.x

- The baudrate of the DroneCAN virtual serial port ("CAN_D1_UC_S1_BD" parameter) should be set to 57600; otherwise the MAVLink flow control will not work properly.


