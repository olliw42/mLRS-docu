# mLRS Documentation: CRSF Telemetry and Yaapu Telemetry App #

([back to main page](../README.md))

This page describes how to set up an mLRS system for EdgeTX/OpenTX radios, so you get CRSF telemetry sensors and can use the Yaapu telemetry app.

Three steps need to be completed:
1. The transmitter needs to be setup for the CRSF protocol
2. The mLRS Tx module needs to be put into "CRSF mode"
3. The flight controller needs to be set up to send a MAVLink stream with the desired MAVLink messages

Optional but recommended steps:
- Install the mLRS Lua script on the transmitter to configure Tx and Rx parameters: [Lua Script](LUA.md)
- Set the receiver into "mavlink mode" (described below)
- Install the Yaapu app (described below)

Notes:
- Any radio which supports the CRSF protocol should work, this should include many brands besides EdgeTX/OpenTX radios.
- An ArduPilot flight controller is assumed. PX4 and INAV needs to be tested and validated.

## Transmitter Setup

In EdgeTX/OpenTX, navigate to MDL->MODEL SETUP and configure the external RF module for CRSF protocol with 400K baud rate. 

## mLRS Tx Module Setup

Set the following parameters using the CLI or Lua script:

- Tx Ch Source = crsf
- Tx Ser Dest = serial or serial2 (not mbridge!)
- Tx Ser Link Mode = mavlink

## ArduPilot Setup

- SERIALx_BAUD = 57 
- SERIALx_PROTOCOL = 2 (important, do not use MAVLink v1!)

Note: Further ArduPilot specific parameters are detailed here: [ArduPilot Setup](docs/ARDUPILOT.md)

## mLRS Rx Module Setup

Set the following parameters using the CLI or Lua script:

- Rx Out Mode = crsf
- Rx Ser Link Mode = mavlink

Note: Rx Ser Baudrate must match the baudrate that the FC's MAVLink serial port is configured for.

## Yaapu Telemetry App Setup for EdgeTX/OpenTX

In EdgeTX/OpenTX go to MDL->TELEMETRY and select "Discover new sensors". You should see sensors appearing; mLRS currently provides 28 sensors. ([CRSF Sensors](docs/CRSF_SENSORS.md))

Install the Yaapu app exactly as described in its wiki. Note: You need to install the dev version, the stable release version will not work. You need to enable the CRSF support: Start the "Yaapu Config" script in SYS->TOOLS, and set "enable CRSF support: yes" (then repower the radio). You can check if all is good by running the "Yaapu Debug CRSF" script in SYS->TOOLS.

## Demo

[![mLRS: Yaapu Telemetry App and wireless Mavlink forwarding to MissionPlanner](https://img.youtube.com/vi/m1uDWcwcknM/0.jpg)](https://www.youtube.com/watch?v=m1uDWcwcknM "mLRS: Yaapu Telemetry App and wireless Mavlink forwarding to MissionPlanner")
