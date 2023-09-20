# mLRS Documentation: Configuration ID #

([back to main page](../README.md))

mLRS allows for 10 different configurations to be stored on the Tx module.  This is useful for when you want to use a single Tx module with multiple receivers and want to use different settings for each receiver.  For example, you may prefer to use 50 Hz mode on your copter but prefer to use 19 Hz mode on your rover. The active configuration ID is set based on the receiver number that is assigned on the MODEL SETUP page within the 'External RF' page/section of EdgeTx/OpenTx. This option is only available when using CRSF or mBridge protocols, SBUS will only use configuration ID 0.

## Changing the Receiver Number

Within EdgeTx/OpenTx, navigate to the MDL->MODEL SETUP page and then select the 'External RF' Section:

<img src="images/configIDModelSetup.bmp" width="360px">

Change the receiver number to the slot you want to use:

<img src="images/configIDExternalRF.bmp" width="360px">

The configuration ID currently in use is also available in the Lua script:

<img src="images/configIDLua.bmp" width="360px">