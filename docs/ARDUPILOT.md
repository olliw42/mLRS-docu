# mLRS Documentation: ArduPilot Systems #

([back to main page](../README.md))

Further ArduPilot information is detailed below:

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

## RSSI

There are three RSSI metrics that are available to be displayed in Mission Planner when using mLRS:

1. rxrssi - the RSSI of the receiver, reported as a percentage.
    - This is provided by the receiver, the RSSI_TYPE parameter determines the method:
        - RSSI_TYPE = 3 (ReceiverProtocol): mLRS will send the RSSI dBm in the CRSF stream and ArduPilot will apply scaling using the following formula: rxrssi = 1 - ((Rx RSSI dBM - 50) / 70)
            - Note: When using RSSI_TYPE = 3, it is possible to replace the RSSI with Link Quality using the RC_OPTIONS bitmask.
        - RSSI_TYPE = 5 (TelemetryRadioRSSI): mLRS will provide the RSSI % in the MAVLink stream using the same formula listed above via the RADIO_STATUS message.
    - The rxrssi value is then sent back to the ground station via the RC_CHANNELS message.
2. rssi - the RSSI of the Tx module, reported as an unsigned 8-bit value.
    - This is provided by the Tx module when the parameter 'Tx Snd RadioStat' is set to 1 Hz via the RADIO_STATUS message.
    - mLRS will use the following formula: rssi = (1 - ((Tx RSSI dBM - 50) / 70)) * 255
3. remrssi - the RSSI of the receiver, reported as an unsigned 8-bit value.
    - This is provided by the Tx module when the parameter 'Tx Snd RadioStat' is set to 1 Hz via the RADIO_STATUS message.  
    - mLRS will use the following formula: remrssi = (1 - ((Rx RSSI dBM - 50) / 70)) * 255
        - Note: In theory, this should match the rxrssi value however due to scaling and timing this is not guaranteed.

### RSSI dBm

Given that the receive sensitivity limit will vary by RF mode it is often useful to know the exact RSSI dBm as opposed to RSSI as a percentage or an unsigned 8-bit value.  The RSSI dBm allows one to understand exactly how much margin there is in the link budget.  The table below provides conversions to RSSI dBm:  

| RSSI dBm | RSSI % | RSSI uint8_t | Notes            |
|----------|--------|--------------|------------------| 
| 90       | 43     | 77           |                  |
| 100      | 29     | 73           |                  |
| 105      | 21     | 55           | 50 Hz Mode Limit |
| 108      | 17     | 44           | 31 Hz Mode Limit |
| 112      | 11     | 29           | 19 Hz Mode Limit |

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
