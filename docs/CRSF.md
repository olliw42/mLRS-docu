# mLRS Documentation: CRSF Telemetry and Yaapu Telemetry App #

([back to main page](../README.md))

This page describes how to set up a mLRS system for EdgeTX/OpenT radios, so that you get the usual CRSF telemetry sensors and can use the Yaapu telemetry app.

Two things need to be done:
1. The mLRS Tx module needs to be put into "CRSF mode"
2. The flight controller needs to be set up to send a MAVLink stream with the desired MAVLink messages

Optional but recommended steps:
- Set the receiver into "mavlink mode" (described below)
- Install the LUA script on the radio which allows you to change the Tx and Rx parameters: ([LUA Script](LUA.md))

Notes:
- Any radio which supports the CRSF protocol should work, this includes many brands besides EdgeTX/OpenTX radios.
- An ArduPilot flight controller is assumed. PX4 and INAV needs to be tested and validated.


## mLRS Tx Module Setup

- Tx Ch Source = crsf
- TX Ser Baudrate = 57600
- Tx Ser Dest = serial or serial2 (not mbridge!)
- Tx Ser Link Mode = mavlink
- Tx Snd RadioStat = off (yes, off!)

Note: There are situations in which it can be useful to enable "Tx Snd RadioStat", but you should do this only if you know what you are doing. You really should not need it for this setup.


## ArduPilot Setup

Configuration of a Serial Port for MAVLink v2:

- SERIALx_BAUD = 57 
- SERIALx_OPTIONS = 0
- SERIALx_PROTOCOL = 2

Configuration of MAVLink Stream Rates:

- SRx_EXT_STATS = 1 (or 2 if you use 31 Hz or 50 Hz mode)
- SRx_EXTRA1 = 4
- SRx_EXTRA2 = 4
- SRx_EXTRA3 = 1 (or 2 if you use 31 Hz or 50 Hz mode)
- SRx_POSITION = 2
- SRx_RAW_SENS = 0 (for most of you this one is unimportant, keep it at 0 unless you really need it)

Configuration for CRSF Receiver:

Setting up ArduPilot for a CRSF receiver can be a bit tricky, as it depends on the flight controller board, and might need BRD_ALT_CONFIG to be set to a specific value. It is best to consult the ArduPilot wiki, or ask in the ArduPilot discussion channel.

For my Matek H743 board the configuration is:

- BRD_ALT_CONFIG = 1
- RC_PROTOCOLS = 536 or 512
- RSSI_TYPE = 3
- SERIAL7_BAUD = Irrelevant (Baud Rate is autodetected by Ardupilot)
- SERIAL7_OPTIONS = 0
- SERIAL7_PROTOCOL = 23

There are more options available in the 'RC_OPTIONS' parameter: https://ardupilot.org/plane/docs/parameters.html#rc-options-rc-options

## mLRS Rx Module Setup

These configurations are not strictly neccesary, but recommended for Ardupilot:

- Rx Out Mode = crsf
- RX Ser Baudrate = 57600
- Rx Ser Link Mode = mavlink
- Rx Snd RadioStat = ardu_1


## Yaapu Telemetry App

The External RF module needs to be set up for CRSF protocol with 400K Baud Rate. In EdgeTX/OpenTX, this is done in MDL->MODEL SETUP.

In EdgeTX/OpenTX go to MDL->TELEMETRY and select "Discover new sensors". You should see sensors appearing, mLRS currently supports 27 sensors.

Install the Yaapu app exactly as described in its wiki. Note: You need to install the dev version, the stable release version will not work. You can check if all is good by running the "Yaapu Debug CRSF" script in SYS->TOOLS.