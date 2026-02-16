# mLRS Documentation: Setup as SiK Telemetry Replacement #

([back to main page](../README.md))

This page describes how to use mLRS as a bi-directional MAVLink telemetry link similar to a SiK telemetry unit. This setup doesn't require a radio and will only transmit and receive MAVLink data. The only unique aspect of "SiK Telemetry" method of operation is that RC over MAVLink is not utilized.

<img src="images/mLRS-docu-setup-sik-telemetry-02.jpg" width="800px">

## Firmware

- Tx module (ground module): needs to be flashed with a "tx-xxxx" firmware
- Receiver (vehicle module): needs to be flashed with a "rx-xxxx" firmware

## mLRS Tx Module Setup

No changes from the default should be necessary.

## mLRS Receiver Setup

- "Rx Ser Baudrate" = must match the baudrate of the flight controller's serial port
- "Rx Snd RcChannel" = off

## ArduPilot Setup

Configure the serial port that is connected to the mLRS receiver:

- SERIALx_PROTOCOL = 2 (important, do not use MAVLink v1!)
- SERIALx_BAUD = must match the baudrate of the mLRS receiver's serial port
- SERIALx_OPTIONS = 4096 (ignore commands from GCS to change stream rates)

> [!NOTE]
> 'x' refers to the serial port of your flight controller used for connecting with the mLRS receiver's serial port.

If you are using a separate RC system (e.g. ELRS, Crossfire, FrSky, etc.), configure it according to that system's documentation.

### Stream Rates

For MAVLink telemetry, stream rates must be enabled by setting the SRy/MAVy parameters in ArduPilot (ground control stations typically set stream rates upon connection). The exact stream rate values are not critical, as mLRS regulates the message flow when necessary. For recommended settings, see the [CRSF Telemetry](CRSF.md#stream-rates) page.

## Ground Control Station Connection

Since there is no radio in the loop, the ground control station connects directly to the mLRS Tx module. Several connection methods are available:

- **USB**: Some Tx modules provide USB serial access. The "siktelem" firmware variant enables this on MatekSys Tx modules.
- **Wired serial**: A TTL level USB serial adapter can be used to connect a Tx module serial port directly to a PC or mobile device.
- **Wireless bridge (WiFi/Bluetooth)**: An ESP or HC04 module connected to the Tx module serial port can provide a WiFi or Bluetooth link to the ground control station. Some Tx modules include a built-in wireless bridge. See [Wireless Bridge](WIRELESS_BRIDGE.md) for details.
