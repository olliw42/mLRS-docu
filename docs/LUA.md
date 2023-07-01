# mLRS Documentation: mLRS Configuration Lua Script #

([back to main page](../README.md))

The mLRS configuration Lua script provides the most convenient approach to set the Tx and Rx module's configuration settings.

The Lua script works on both OpenTx and EdgeTx radios.  There are two different versions of the Lua script which depends on your radio's display:
1. If your radio has a 480x272 color screen (e.g. Jumper T16, Radiomaster TX16S) then use the "mLRS.lua" file
2. If your radio has a 128x64 black and white screen (e.g. Radiomaster Zorro) then use the "mLRS-bw.lua" file

Two things need to be done to use the Lua script:

1. The Lua script "mLRS.lua" or "mLRS-bw.lua" located in the "lua" folder should be copied to the SD card of the radio into the "SCRIPTS/TOOLS" folder. Follow the common tutorials for how to do this.

2. The CRSF or mBridge protocol should be selected for the external RF module. Follow the common tutorials for how to do this.

You should then be able to run the Lua script by going to SYS->TOOLS in the radio, and selecting the tool "mLRS Configurator".

Note: For the script to work in the first place, the Tx module must have been set up for CRSF or mBrdige mode, by setting the parameter "Tx Ch Source" to  "crsf" or "mbridge" respectively. Since firmware version v0.2.13 "crsf" is the default setting, and the script thus should work with a fresh flash. Otherwise the CLI needs to be invoked and this parameter be set accordingly, as described in [CLI Commands](CLI.md)

Depending on the device, some parameters are not available for configuration or cannot be changed. For instance, for a device which doesn't support a buzzer the parameter "Buzzer" is not available, and for a device which doesn't support diversity the parameter "Diversity" cannot be changed. Parameters which are not available are not displayed on the screen (i.e. the list of shown parameters can vary depending on the device), and parameters which cannot be changed are displayed with the current selection but are greyed out and cannot be edited.
