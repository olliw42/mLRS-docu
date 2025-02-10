# mLRS Documentation: Simple SBUS Relay #

([back to main page](../README.md))

If you want to mount your Tx module on a tripod or other structure away from your radio, you can configure the Tx module to accept an SBus signal from a seperate receiver to provide the RC channel information.

## mLRS Tx Module Setup

You will have to update the following parameter:

- Tx Ch Source = in

***Note***: Changing this setting is best done with the CLI or OLED as this will cause the CRSF communication over the JRPin5 to no longer function.  The CLI commands are:

- `p tx_ch_source=2`
- `pstore`

## Relay Receiver Setup

No additional configuration is needed if your receiver already outputs an SBus signal.  ELRS receivers can be configured to output SBus via their Tx pin using the ELRS Lua script:

- Ensure your ELRS receiver is connected
- Select 'Other Devices' in the ELRS Lua
- Select the connected receiver
- Change 'Protocol' to 'SBUS'

## Wiring

In addition to a common ground, wire the SBus signal from your relay receiver to your Tx Module using the following table:

| Tx Module       | SBus Connection |
| --------------- | ----------------|
| Matek mR900-30  | JRPin5, TX2     |
| Matek mR2400-30 | JRPin5, TX2     |
| FrSky R9M       | JRPin1          |
| FlySky FRM303   | JRPin5          |
