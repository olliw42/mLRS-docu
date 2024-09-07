# mLRS Documentation: Configuration ID #

([back to main page](../README.md))

mLRS allows for 10 different configurations to be stored on the Tx module.  This is useful for when you want to use a single Tx module with multiple receivers and want to use different settings for each receiver.  For example, you may prefer to use 50 Hz mode on your copter but prefer to use 19 Hz mode on your rover. The active configuration ID is set based on the receiver number that is assigned on the MODEL SETUP page within the 'External RF' page/section of EdgeTx/OpenTx or via the 'setconfigid' CLI command.

Notes:
- By default, each configuration ID has a unique bind phrase associated with it and will therefore require you to bind with the receiver that you want to use after changing the configuration ID.
- Any receiver number greater than 9 will use configuration ID 9.

## Changing the Receiver Number on the Radio

Within EdgeTx/OpenTx, navigate to the MDL->MODEL SETUP page and then select the 'External RF' Section:

<img src="images/configIDmodelSetup.bmp" width="360px">

Change the receiver number to the slot you want to use:

<img src="images/configIDExternalRF.bmp" width="360px">

The configuration ID currently in use will be displayed in the Lua script and on the OLED display.

<img src="images/configIDLua.bmp" width="360px">

<img src="images/configIDOLED.png" width="360px">