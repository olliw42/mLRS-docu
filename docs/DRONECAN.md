# mLRS Documentation: DroneCAN for ArduPilot Systems #

([back to main page](../README.md))

DroneCAN can be utilized for RC and MAVLink with mLRS instead of the traditional serial communication if both flight controller and receiver have the hardware necessary to support it.

## Wiring & Powering

The DroneCAN connector and wiring specification is widely adopted by manufacturers. The DroneCAN micro connector standard is based on the 4-pin [JST-GH](https://www.jst.com/products/crimp-style-connectors-wire-to-board-type/gh-connector/) connector system with the following pinout:

| Pin | Use
| --- | ---
| Pin 1 | Bus power (5 V)
| Pin 2 | CANH
| Pin 3 | CANL
| Pin 4 | Ground

Ideally, the CANH and CANL wires should be twisted together, and the 5 V and ground wires should be twisted together as well. Care must be taken with the bus power supply, which is rated for a maximum of 1 A. High-power mLRS receivers can consume a substantial fraction of this limit.

Further technical details and recommendations are given in the [DroneCAN: Hardware design recommendations](https://dronecan.github.io/Specification/8._Hardware_design_recommendations).

<img src="images/DRONECAN_wiring.png" width="720px">

## mLRS Receiver Settings

#### RC

With a CAN-enabled firmware flashed, the mLRS receiver will output RC channels data on the CAN bus without any further settings.

#### MAVLink

In order to enable serial (MAVLink) communication via DroneCAN, one needs to set:

- "Rx Serial Port" = "can"

> [!NOTE] 
> Do not enable "rc_override" or "rc_channels" in the mLRS receiver settings when using MAVLink via DroneCAN as it adds substantial and unnecessary traffic on the CAN bus.

## ArduPilot Settings

The following parameters need to be set to enable RC and MAVLink over DroneCAN.

#### DroneCAN

Set up the CAN driver, the protocol and enable the virtual serial support:

- CAN_D1_PROTOCOL = 1 (is set to 1 by default)
- CAN_P1_DRIVER = 1
- CAN_D1_UC_SER_EN = 1 (only needed when MAVLink via DroneCAN is desired)

> [!NOTE]
> You need to reboot the flight controller after having adjusted CAN_P1_DRIVER, in order to see the parameter CAN_D1_UC_SER_EN.

Then reboot the flight controller (again).

#### RC

Enable RC channels via DroneCAN:

- RC_PROTOCOLS bitmask should have the 'DroneCAN' bit enabled

#### MAVLink

Configure the DroneCAN virtual serial port (mandatory settings):

- CAN_D1_UC_S1_BD = 57 (57600) (see also below in section Limitations)
- CAN_D1_UC_S1_IDX = 0 (Serial 0)
- CAN_D1_UC_S1_NOD = 68
- CAN_D1_UC_S1_PRO = 2 (MAVLink 2)

> [!NOTE]
> The setting "Serial 0" should not be confused with ArduPilot's SERIALx parameters or mLRS' serial and serial2 ports.   

Adjust DroneCAN stream rates (optional settings):

- CAN_D1_UC_NTF_RT = 1

Adjust MAVLink stream rates:

- Stream rates should be set as recommended on the [CRSF page](CRSF.md#stream-rates)

When configuring SRy/MAVy parameters for DroneCAN, 'y' corresponds to the number of serial ports that you have enabled for MAVLink (SERIALx parameters). For example, if you are using SERIAL0 for USB and SERIAL2 for MAVLink then you will have to modify the SR2/MAV2 parameters for the DroneCAN connection:

- SERIAL0 will use SR0/MAV0
- SERIAL2 will use SR1/MAV1
- DroneCAN will use SR2/MAV2

## Supported DroneCAN Services

- [protocol.NodeStatus](https://dronecan.github.io/Specification/7._List_of_standard_data_types/#nodestatus)
- [protocol.GetNodeInfo](https://dronecan.github.io/Specification/7._List_of_standard_data_types/#getnodeinfo)
- [protocol.dynamic_node_id.Allocation](https://dronecan.github.io/Specification/7._List_of_standard_data_types/#allocation)
- [sensors.rc.RCInput](https://github.com/dronecan/DSDL/blob/master/dronecan/sensors/rc/1140.RCInput.uavcan)
- [tunnel.Targetted](https://github.com/dronecan/DSDL/blob/master/uavcan/tunnel/3001.Targetted.uavcan)

> [!NOTE]
> Additional services, such as node configuration and firmware updates, are not supported.

## Limitations

Receivers using MAVLink via DroneCAN are a relatively new application of ArduPilot's DroneCAN, and issues not seen before may become exposed now. ArduPilot has been found to have these limitations:

#### All Versions of ArduPilot

- In MissionPlanner, on the DroneCAN/UAVCAN page, communication with the CAN nodes is not possible when connected via the mLRS link (mLRS has code to prevent this, as there is a critical bug in some ArduPilot versions which would lead to a crash of ArduPilot). This works normally when the flight controller is connected to MissionPlanner via e.g. USB.
- CRSF or SBus cannot be used in combination with DroneCAN RC.
- The MAVLink stream rates must not be set to too high values as this can lead to lost messages.

#### ArduPilot 4.6.x

- DroneCAN RC only provides RSSI and not LQ or SNR.
- OSD is limited to RSSI.

#### ArduPilot 4.5.x

- The baudrate of the DroneCAN virtual serial port ("CAN_D1_UC_S1_BD" parameter) should be set to 57600; otherwise the MAVLink flow control will not work properly.


