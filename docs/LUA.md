# mLRS Documentation: mLRS Lua Script #

([back to main page](../README.md))

The mLRS Lua script provides a convenient way to change the Tx module and receiver settings.

The Lua script works on OpenTx, EdgeTx, and Ethos radios but there are different versions depending on the display and OS of your radio:
1. If your radio runs OpenTx/EdgeTx and has a 480x272 (e.g. Jumper T16, Radiomaster TX16S) or 480x320 (e.g. Jumper T15) color screen then use the "mLRS.lua" file
2. If your radio runs OpenTx/EdgeTx and has a black and white screen (e.g. FrSky Taranis X9E, Radiomaster Zorro) then use the "mLRS-bw.lua" file
3. If your radio runs Ethos (e.g. FrSky X18, X20) then use the "mlrs.lua", "main.lua", and "icon.png" files located in the 'Ethos' folder

## Module Setup

The Tx module must be configured for CRSF mode, by setting the parameter "Tx Ch Source" to "crsf". This is the default setting after an initial flash. If this parameter was changed, you can set it using the OLED interface (if available) or the CLI. See [CLI Commands](CLI.md) for more details.

## OpenTx/EdgeTx Setup

> [!IMPORTANT]
> The mLRS Lua script requires EdgeTx version 2.9.x or later.

1. In OpenTx/EdgeTx, navigate to MDL->MODEL SETUP (or SYS->HARDWARE for internal modules) and configure the RF module for CRSF or mBridge protocol with 400K baud rate.

    - ***Note***: mLRS only officially supports 400K baud rate.

2. The Lua script "mLRS.lua" or "mLRS-bw.lua" needs to be copied to the "SCRIPTS/TOOLS" folder of the radio's SD card. One can follow the common tutorials for how to do this.

    - ***Note***: The correct Lua version needs to be selected based on your firmware version:
        - You can download the Lua scripts from the [mLRS Web Flasher](https://www.olliw.eu/mlrsflasher) when using v1.3.04 or newer (for older versions they are found [here](https://github.com/olliw42/mLRS/tree/v1.3-release/lua))

You should then be able to run the Lua script by going to SYS->TOOLS on the radio, and selecting "mLRS Configurator" or "mLRS-bw".

## Ethos Setup

1. In Ethos, navigate to Model->RF System and configure the External RF module for Crossfire protocol with 400K baud rate.

    - ***Note***: mLRS only officially supports 400K baud rate.

2. The files "mlrs.lua", "main.lua" and "icon.png" need to be copied to the "/scripts/mLRS/" folder of the radio's SD card.

    - ***Note***: The correct Lua version needs to be selected based on your firmware version:
        - You can download the Lua scripts from the [mLRS Web Flasher](https://www.olliw.eu/mlrsflasher)

You should then be able to run the Lua script by going to System->MLRS.

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

The Lua script for radios with a black and white screen also supports editing all parameters. But because of screen and memory limitations it looks and behaves slightly differently than the color Lua script.

The starting page contains [common parameters](PARAMETERS.md#mlrs-documentation-parameters-v1300), status information, and commands such as bind and save. Seven additional parameters appear on each subsequent page and page navigation is linear via the "prev" and "next" commands.

Parameters which are not available are still displayed, but with a "-" character in the value position. Parameters which cannot be changed are displayed as normal. Unused lines on the last page contain a blank name and a value of ".". The cursor can be moved to unavailable or unchangeable parameters and unused lines, but they can not be selected for edit; pressing enter on them will provide haptic feedback to indicate they can't be edited.

***Note***:  If you receive a "not enough memory" error, please try the pre-compiled mLRS-bw-luac.lua file.  You can also try reducing the file size by running the code through a Lua minifier tool such as the one [here](https://mothereff.in/lua-minifier) and install the minified version as a workaround.  If neither solution works, please report this to the mLRS developers.
