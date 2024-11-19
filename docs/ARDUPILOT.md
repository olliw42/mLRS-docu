# mLRS Documentation: Additional Configuration for ArduPilot Systems #

([back to main page](../README.md))

***Note***: This page contains additional detail on certain configuration options that are applicable only to ArduPilot systems. Initial configuration should follow the process described within the [CRSF Telemetry and Yaapu Telemetry App](CRSF.md) page. If you are using a separate RC system and only want to have SiK functionality then you can refer to the [SiK Telemetry Replacement](docs/SETUP_SIK.md) page.

## CRSF Receiver

Setting up ArduPilot for a CRSF receiver can be a bit tricky, as it depends on the flight controller board, and might need BRD_ALT_CONFIG to be set to a specific value. It is best to consult the ArduPilot wiki, or ask in the ArduPilot discussion channel.

CRSF works best on serial ports that have DMA enabled. This is only a concern on F4 and F7 flight controllers. The serial ports that have DMA enabled can be found by using the MAVProxy command 'ftp get @SYS/uarts.txt -', an '*' will denote serial ports that have DMA enabled (example for Matek F405 VTOL):

<img src="images/Serial_DMA.png">

If you use a serial port without DMA, Mission Planner will show the message 'CRSF: running on non-DMA serial port' in the 'Messages' section.

For a Matek H743 board the configuration is:

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

## RSSI

RSSI is a relatively confusing topic with ArduPilot, since there are so many ways.

First a comment on how RSSI is represented by ArduPilot. ArduPilot converts any RSSI value which it reads in into the range [0.0...1.0], where 0.0 represents the weakest and 1.0 the strongest signal. The conversion law which is used for this scaling depends on the source of the RSSI value. In the dataflash log this value is available as RSSI:RXRSSI. For most output purposes, this internal RSSI value is then again converted into whatever the outpt format demands. For instance, for the OSD it is multiplied by 100 and displayed as 0% ... 100%. For MAVLink it is converted into the range [0...254] (0 = weakest signal, 254 = strongest signal, 255 = undefined)(this could be called the MAVLink units for RSSI).

The source of the RSSI value (and thus applied conversion law) is determined by the ArduPilot parameter RSSI_TYPE. With mLRS these settings can be relevant:
- RSSI_TYPE = 3 (ReceiverProtocol): mLRS will send RSSI in dBm in the CRSF stream and ArduPilot will apply scaling using the following formula: RSSI = 1 - ((RSSI_dBM - 50) / 70). That is -120 dBm is mapped to 0.0 and -50 dBm to 1.0.
    - ***Note***: When using RSSI_TYPE = 3, it is possible to replace the RSSI with LQ using the RC_OPTIONS bitmask.
- RSSI_TYPE = 5 (TelemetryRadioRSSI): mLRS will send RSSI in the MAVLink stream to the ArduPilot via the RADIO_STATUS message, in MAVLink units. mLRS applies the formula RSSI = (1 - ((RSSI_dBM - 50) / 70))*254 to convert to MAVLink units.
- RSSI_TYPE = 2 (RCChannelPwmValue): mLRS can be configured to send RSSI (and LQ) as a channel value to ArduPilot. This option is not recommended and not further described.

MissionPlanner in turn gets RSSI data from ArduPilot via MAVLink messages (usually via the RC_CHANNELS message), and hence in the range [0...254] (or 255 for undefined). This value is available in MissionPlanner as "rxrssi".

In addition a Tx module may send RADIO_STATUS MAVLink messages to MissionPlanner, and RSSI is hence again represented as [0...254] (some older Tx module implementations may scale to [0...255]). The data from the Tx module is available in MissionPlanner as "rssi" and "remrssi" (also "noise" and "remnoise" are avilable).

With mLRS these data is provided when the parameter 'Tx Snd RadioStat' is set to '1 Hz'. mLRS will use the following formula to convert from RSSI in dBm to MAVLink uints: RSSI = (1 - ((RSSI_dBM - 50) / 70)) * 254.

Therefore in Mission Planner three RSSI metrics are available when using mLRS (all in MAVLink units):

1. rxrssi - the RSSI of the mLRS receiver, as seen by ArduPilot
2. rssi - the RSSI of the mLRS Tx module
3. remrssi - the RSSI of the mLRS receiver, as seen by the mLRS Tx module
    - ***Note***: In theory, this value should match the rxrssi value however due to scaling and timing this is not guaranteed.

### RSSI dBm

Given that the receiver sensitivity will vary with the mLRS mode it is often useful to know the exact RSSI dBm as opposed to RSSI as a percentage or in MAVLink units. The RSSI dBm allows one to understand exactly how much margin there is in the link budget. The table below provides conversions to RSSI dBm:

| RSSI dBm | RSSI % | RSSI MAVLink units | Notes            |
|----------|--------|--------------|------------------|
| -90       | 43     | 77           |                  |
| -100      | 29     | 73           |                  |
| -105      | 21     | 55           | 50 Hz Mode receiver sensitivity |
| -108      | 17     | 44           | 31 Hz Mode receiver sensitivity |
| -112      | 11     | 29           | 19 Hz Mode receiver sensitivity |

## Stream Rates

When configuring SRy parameters, 'y' does not necessarily correspond to the number 'x' of the SERIALx port but to the count of serial ports using the MAVLink protocol.  SERIAL0, and thus SR0, will nearly always be reserved for the USB connection and set to use the MAVLink protocol (which should not be modified). Therefore, as an example, in a setup with SERIAL1 and SERIAL2 not set to the MAVLink and with the mLRS receiver connected to SERIAL3, then SR1 should be used to configured the stream rates for the mLRS receiver.

To understand how stream rates affect the MAVLink data rate, you can use this [calculator](https://github.com/ArduPilot/pymavlink/blob/master/tools/mavtelemetry_datarates.py) (requires Python).

## mLRS Receiver

- Rx Snd RadioStat:
    - ardu_1: optimizes for ArduPilot usage
    - meth_b: optimizes for PX4 usage
