# mLRS Documentation: ArduPilot Setup #

([back to main page](../README.md))

([back to CRSF page](CRSF.md))

Further parameters can be configured to optimize peformance for ArduPilot and the RF mode (19Hz, 31Hz or 50Hz) selected.

## mLRS Rx Module Setup

- Rx Snd RadioStat= ardu_1

## Serial Port Setup

- SERIALx_BAUD:
    - 57 for 31Hz, 50Hz
    - 38 for 19Hz
- SERIALx_OPTIONS = 4096 (ignore commands from GCS to change stream rates)

Note: These baud rates enable MAVFTP parameter download

## Stream Rates Setup

- SRx_ADSB = 0
- SRx_EXT_STAT:
    - 2 for 31Hz, 50Hz
    - 1 for 19Hz
- SRx_EXTRA1 = 4
- SRx_EXTRA2 = 4
- SRx_EXTRA3:
    - 2 for 31Hz, 50Hz
    - 1 for 19Hz
- SRx_PARAMS = 50
- SRx_POSITION = 2
- SRx_RAW_CTRL = 0
- SRx_RAW_SENS = 0 (for most of you this one is unimportant, keep it at 0 unless you really need it)
- SRx_RC_CHAN = 0

## CRSF Receiver Setup

Setting up ArduPilot for a CRSF receiver can be a bit tricky, as it depends on the flight controller board, and might need BRD_ALT_CONFIG to be set to a specific value. It is best to consult the ArduPilot wiki, or ask in the ArduPilot discussion channel.

For my Matek H743 board the configuration is:

- BRD_ALT_CONFIG = 1
- RC_PROTOCOLS = 536 or 512
- RSSI_TYPE = 3 or 5
- SERIAL7_BAUD = irrelevant (baud rate is determined by ArduPilot)
- SERIAL7_OPTIONS = 0
- SERIAL7_PROTOCOL = 23

Notes:
- [ArduPilot Docs for RC_PROTOCOLS](https://ardupilot.org/plane/docs/parameters.html#rc-protocols-rc-protocols-enabled)
- [ArduPilot Docs for RSSI_TYPE](https://ardupilot.org/plane/docs/parameters.html#rssi-type-rssi-type)
- There are more RC options available in the 'RC_OPTIONS' parameter. ([ArduPilot Docs for RC_OPTIONS](https://ardupilot.org/plane/docs/parameters.html#rc-options-rc-options)) 