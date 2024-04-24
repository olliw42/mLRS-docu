# mLRS Documentation: ArduPilot Systems #

([back to main page](../README.md))

Further ArduPilot information is detailed below:

## RC Channel Choices

mLRS supports several ways to send RC channel data from the mLRS receiver to the ArduPilot flight controller.

The traditional way is to send RC channel data on a dedicated signal wire using an RC protocol such as CRSF or SBUS. In this case the mLRS receiver will utilize two serial ports on the flight controller and will need to be connected with 5 wires: GND, 5V, OUT, TX, and RX. The OUT wire is for the RC channel data and the TX, RX wires are for the serial MAVLink data. The mLRS receiver parameter "Rx Out Mode" should be set to the desired RC protocol, e.g. "crsf", and the "Rx Snd RcChannel" parameter to "off" (note that a mLRS receiver might not support all RC protocols due to hardware restrictions). On the flight controller, the serial port connected to the OUT wire needs to be configured to SERIALx_PROTOCOL = 23 (RCin) and the serial port connected to the TX, RX wires needs to be configured to SERIALx_PROTOCOL = 2 (MAVLink V2).

Alternatively, the RC channel data can be sent via MAVLink to the flight controller. In that case only 4 wires need to be connected between the receiver and flight controller: GND, 5V, TX, RX. The mLRS receiver parameter "Rx Ser Link Mode" needs to be set to "mavlink" or "mavlinkX" and the parameter "Rx Snd RcChannel" should be set to based on the ArduPilot version of the flight controller:
- For ArduPilot >= 4.6.0 the "Rx Snd RcChannel" parameter should be set to "rc_channels". The serial port connected to the TX, RX wires needs to be configured to SERIALx_PROTOCOL = 2 (MAVLink V2) and the RC_PROTOCOLS bitmask needs to have "MavRadio" enabled.
- For ArduPilot <= V4.5.x, the parameter "Rx Snd RcChannel" should be set to "rc_override". The serial port connected to the TX, RX wires needs to be configured to SERIALx_PROTOCOL = 2 (MAVLink V2) and the RC_PROTOCOLS bitmask should have all protocols disabled.  Keep in mind, that this method should be considered legacy and should not be used if "rc_channels" is possible.

Note: When only using 4 wires, the "Rx Out Mode" parameter is irrelevant.

Each approach has pros and cons, which shall not be discussed here.

## CRSF Receiver

Setting up ArduPilot for a CRSF receiver can be a bit tricky, as it depends on the flight controller board, and might need BRD_ALT_CONFIG to be set to a specific value. It is best to consult the ArduPilot wiki, or ask in the ArduPilot discussion channel.

CRSF works best on serial ports that have DMA enabled.  This is only a concern on F4 and F7 flight controllers.  The serial ports that have DMA enabled can be found by using the MAVProxy command 'ftp get @SYS/uarts.txt -', an '*' will denote serial ports that have DMA enabled (example for Matek F405 VTOL):

<img src="images/Serial_DMA.png">

If you use a serial port without DMA, Mission Planner will show the message 'CRSF: running on non-DMA serial port' in the 'Messages' section.

For my Matek H743 board the configuration is:

- BRD_ALT_CONFIG = 1
- RC_PROTOCOLS = 536 or 512
- RSSI_TYPE = 3 or 5
- SERIAL7_BAUD = irrelevant (baud rate is determined by ArduPilot)
- SERIAL7_OPTIONS = 0
- SERIAL7_PROTOCOL = 23

Notes & References:
- [ArduPilot Docs for CRSF](https://ardupilot.org/copter/docs/common-tbs-rc.html)
- [ArduPilot Docs for RC_PROTOCOLS](https://ardupilot.org/plane/docs/parameters.html#rc-protocols-rc-protocols-enabled)
- [ArduPilot Docs for RSSI_TYPE](https://ardupilot.org/plane/docs/parameters.html#rssi-type-rssi-type)
- There are more RC options available in the 'RC_OPTIONS' parameter. ([ArduPilot Docs for RC_OPTIONS](https://ardupilot.org/plane/docs/parameters.html#rc-options-rc-options)) 

## Stream Rates

When configuring the SRx parameters, the 'x' does not correspond to the serial port number  but to the number of serial ports set to MAVLink.

Example with MAVLink on serial ports 0 and 3:

- Serial 0: SR0_
- Serial 3: SR1_

To understand how stream rates affect the MAVLink data rate, you can use this [calculator](https://github.com/ArduPilot/pymavlink/blob/master/tools/mavtelemetry_datarates.py)  (requires Python).

## mLRS Rx Module

- Rx Snd RadioStat:
    - ardu_1: optimizes for ArduPilot usage
    - brad: optimizes for PX4 usage
