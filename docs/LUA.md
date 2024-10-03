# mLRS Documentation: mLRS Lua Script #

([back to main page](../README.md))

The mLRS Lua script provides a convenient way to change the Tx module and receiver settings.

The Lua script works on both OpenTx and EdgeTx radios but there are two different versions depending on the display of your radio:
1. If your radio has a 480x272 color screen (e.g. Jumper T16, Radiomaster TX16S) then use the "mLRS.lua" file
2. If your radio has a black and white screen (e.g. Frsky Taranis X9E, Radiomaster Zorro) then use the "mLRS-bw.lua" file

***Note***: The mLRS Lua script requires EdgeTx version 2.9.x or later.

## Setup

Three things need to be done in order to use the Lua script:

1. The Tx module must be configured for CRSF or mBridge mode, by setting the parameter "Tx Ch Source" to "crsf" or "mbridge" respectively. Since firmware version v0.2.13 "crsf" is the default setting, so this will be already completed after an initial flash. If not, the CLI needs to be used to set this parameter accordingly, as described in [CLI Commands](CLI.md).

2. In EdgeTX/OpenTX, navigate to MDL->MODEL SETUP and configure the external RF module for CRSF or mBridge protocol with 400K baud rate.

    - ***Note***: mLRS only officially supports 400K baud rate.

3. The Lua script "mLRS.lua" or "mLRS-bw.lua" located in the "lua" folder of the mLRS github repository needs to be copied to the "SCRIPTS/TOOLS" folder of the radio's SD card. One can follow the common tutorials for how to do this.

You should then be able to run the Lua script by going to SYS->TOOLS on the radio, and selecting "mLRS Configurator".

## Usage

Parameters are changed by:
- Highlighting a parameter
- Pressing the enter button
- Scrolling through the available settings
- Pressing the enter button on the setting
- Selecting 'Save' to store

***Note***: Parameter changes are stored permanently in the devices only when a 'Save' has been executed.

## Color Lua Script Notes

Parameters which are not available are not displayed on the screen (i.e. the list of shown parameters can vary depending on the device). For instance, on a device which does not support a buzzer the parameter "Buzzer" will not be displayed. Parameters which cannot be changed are displayed with the current selection but are greyed out and cannot be edited. For instance, on a device which does not support diversity the parameter "Diversity" is displayed but cannot be changed.

## BW Lua Script Notes

The Lua script for radios with a black and white screen is limited in functionality and only allows for 5 parameters to be configured.  By default, these are BindPhrase, Mode, TxPwr, RxPwr, and RxOutMode.

If one wants to be able to change a different parameter, the 'custom param list' section in the Lua script can be updated to reference a different parameter. The parameter numbers are zero-based and can be determined from the 'Setup parameter list' section located in [setup_list.h](https://github.com/olliw42/mLRS/blob/main/mLRS/Common/setup_list.h).

For example, if one wanted to replace "Mode" with "RF Band" then 'param_idx_list[1] = 1' needs to be updated to 'param_idx_list[1] = 2'
