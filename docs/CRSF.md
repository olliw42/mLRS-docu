# mLRS Documentation: CRSF Telemetry and Yaapu Telemetry App #

([back to main page](../README.md))

This page describes how to set up a mLRS system for EdgeTX/OpenTX radios, so that you get the usual CRSF telemetry sensors and can use the Yaapu telemetry app.

Two things need to be done:
1. The mLRS Tx module needs to be put into "CRSF mode"
2. The flight controller needs to be set up to send a MAVLink stream with the desired MAVLink messages

Optional but recommended steps:
- Set the receiver into "mavlink mode" (described below)
- Install the mLRS LUA script on the radio which allows you to change the Tx and Rx parameters: ([LUA Script](LUA.md))

Notes:
- Any radio which supports the CRSF protocol should work, this should include many brands besides EdgeTX/OpenTX radios.
- An ArduPilot flight controller is assumed. PX4 and INAV needs to be tested and validated.


## mLRS Tx Module Setup

- Tx Ch Source = crsf
- Tx Ser Dest = serial or serial2 (not mbridge!)
- Tx Ser Link Mode = mavlink
- Tx Snd RadioStat = off (yes, off!)

Notes: 
- There are situations in which it can be useful to enable "Tx Snd RadioStat", but you should do this only if you know what you are doing. You really should not need it for this setup.
- The choice of Tx Ser Baudrate is uncritical and really determined by the user's need. It is recommended to set it to 57600 or higher, as this will provide enough speed for all operation modes (19 Hz, 31 Hz, 50 Hz).


## ArduPilot Setup

Configuration of a serial port for MAVLink v2:

- SERIALx_BAUD = 57 
- SERIALx_OPTIONS = 0
- SERIALx_PROTOCOL = 2 (important, do not use MAVLink v1!)

Configuration of MAVLink stream rates:

- SRx_EXT_STATS = 1 (or 2 if you use 31 Hz or 50 Hz mode)
- SRx_EXTRA1 = 4
- SRx_EXTRA2 = 4
- SRx_EXTRA3 = 1 (or 2 if you use 31 Hz or 50 Hz mode)
- SRx_POSITION = 2
- SRx_RAW_SENS = 0 (for most of you this one is unimportant, keep it at 0 unless you really need it)

Configuration for CRSF receiver:

Setting up ArduPilot for a CRSF receiver can be a bit tricky, as it depends on the flight controller board, and might need BRD_ALT_CONFIG to be set to a specific value. It is best to consult the ArduPilot wiki, or ask in the ArduPilot discussion channel.

For my Matek H743 board the configuration is:

- BRD_ALT_CONFIG = 1
- RC_PROTOCOLS = 536 or 512
- SERIAL7_BAUD = irrelevant (baud rate is determined by ArduPilot)
- SERIAL7_OPTIONS = 0
- SERIAL7_PROTOCOL = 23

Notes:
- There are more RC options available in the 'RC_OPTIONS' parameter. ([ArduPilot Docs for RC_OPTIONS](https://ardupilot.org/plane/docs/parameters.html#rc-options-rc-options)) 
- RSSI_TYPE should be set to either 3 or 5. ([ArduPilot Docs for RSSI_TYPE](https://ardupilot.org/plane/docs/parameters.html#rssi-type-rssi-type)) 


## mLRS Rx Module Setup

These configurations are not strictly neccesary, but recommended for ArduPilot:

- Rx Out Mode = crsf
- Rx Ser Baudrate = 57600
- Rx Ser Link Mode = mavlink
- Rx Snd RadioStat:
    - mLRS version >= v0.3.13 = ardu_1
    - mLRS version <  v0.3.13 = w txbuf

Notes:

- It is strongly recommended to set Rx Ser Baudrate to 57600.

## Yaapu Telemetry App Setup for EdgeTX/OpenTX

The external RF module needs to be set up for CRSF protocol with 400K baud rate. In EdgeTX/OpenTX, this is done in MDL->MODEL SETUP.

In EdgeTX/OpenTX go to MDL->TELEMETRY and select "Discover new sensors". You should see sensors appearing; mLRS currently provides 28 sensors. ([CRSF Sensors](docs/CRSF_SENSORS.md))

Install the Yaapu app exactly as described in its wiki. Note: You need to install the dev version, the stable release version will not work. You need to enable the CRSF support: Start the "Yaapu Config" script in SYS->TOOLS, and set "enable CRSF support: yes" (then repower the radio). You can check if all is good by running the "Yaapu Debug CRSF" script in SYS->TOOLS.

## Demo

[![mLRS: Yaapu Telemetry App and wireless Mavlink forwarding to MissionPlanner](https://img.youtube.com/vi/m1uDWcwcknM/0.jpg)](https://www.youtube.com/watch?v=m1uDWcwcknM "mLRS: Yaapu Telemetry App and wireless Mavlink forwarding to MissionPlanner")
