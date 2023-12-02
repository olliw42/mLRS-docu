# mLRS Documentation: mLRS Lua Script #

([back to main page](../README.md))

The mLRS Lua script provides the most convenient way to change the Tx and Rx module's settings.

The Lua script works on both OpenTx and EdgeTx radios but there are two different versions depending on the display of your radio:
1. If your radio has a 480x272 color screen (e.g. Jumper T16, Radiomaster TX16S) then use the "mLRS.lua" file
2. If your radio has a black and white screen (e.g. Frsky Taranis X9E, Radiomaster Zorro) then use the "mLRS-bw.lua" file

Depending on the device, some parameters are not available for configuration or cannot be changed. For instance, for a device which doesn't support a buzzer the parameter "Buzzer" is not available, and for a device which doesn't support diversity the parameter "Diversity" cannot be changed. Parameters which are not available are not displayed on the screen (i.e. the list of shown parameters can vary depending on the device), and parameters which cannot be changed are displayed with the current selection but are greyed out and cannot be edited.

## Setup

Three things need to be done in order to use the Lua script:

1. The Tx module must be configured for CRSF or mBridge mode, by setting the parameter "Tx Ch Source" to "crsf" or "mbridge" respectively. Since firmware version v0.2.13 "crsf" is the default setting, so this will be already completed after an initial flash. If not, the CLI needs to be used to set this parameter accordingly, as described in [CLI Commands](CLI.md).

2. In EdgeTX/OpenTX, navigate to MDL->MODEL SETUP and configure the external RF module for CRSF or mBridge protocol with 400K baud rate.

    - Note: mLRS only officially supports 400K baud rate.

3. The Lua script "mLRS.lua" or "mLRS-bw.lua" located in the "lua" folder of the repository needs to be copied to the "SCRIPTS/TOOLS" folder of the radio's SD card. One can follow the common tutorials for how to do this.

You should then be able to run the Lua script by going to SYS->TOOLS on the radio, and selecting "mLRS Configurator".

## BW Lua Limitations

The Lua script for radios with a black and white screen is limited in functionality and only allows for 5 parameters to be configured.  By default, these are BindPhrase, Mode, TxPwr, RxPwr, and RxOutMode.

If one wants to be able to change a different parameter, this [section](https://github.com/olliw42/mLRS/blob/main/lua/mLRS-bw.lua#L25-L28) in the Lua can be updated to reference a different parameter.  The parameter numbers are zero-based and can be determined from the list [here](https://github.com/olliw42/mLRS/blob/main/mLRS/Common/setup_list.h#L80-L127).

For example, if one wanted to replace Mode with RF Band then 'param_idx_list[1] = 1' needs to be updated to 'param_idx_list[1] = 2'