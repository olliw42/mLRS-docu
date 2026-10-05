# mLRS Documentation: 32 Channels Support #

([back to main page](../README.md))

mLRS supports 32 RC channels (since v1.4.04), with the following differences compared to the normal behavior in 16-channel operation mode.

The 32-channel mode is selected automatically based on the CRSF frames sent to the Tx module. If the Tx module receives CRSF frames containing RC channel data for channels 17 – 32, it immediately switches to 32-channel mode, and the receiver follows accordingly. The receiver output then changes according to the selected method: CRSF, Sbus, MAVLink RADIO_RC_CHANNELS, MSP-RC, or DroneCAN.

## 32-Channel Layout

The channel layout changes as follows:

- CH1 - CH8: 8 channels with 11-bit resolution, full rate/no interlacing
- CH9 - CH16: 8 channels with 8-bit resolution, interlaced 1:2
- CH17 - CH20: 4 channels with 9-position resolution, interlaced 1:4
- CH21 - CH32: 12 channels with 3-position resolution, interlaced 1:4

The 11-bit channels are sent with every frame, and have a slightly higher reception probability than the other channels. The 8-bit channels are interlaced with a 1:2 ratio, meaning that the blocks of channels CH9 - CH12 and CH13 - CH16 are sent alternately, each block is sent every second frame. The nine- and three-position channels are interlaced with 1:4, with each block of four channels being sent every fourth frame. In 19 Hz mode, these channels are therefore updated at a rate of ca. 5 Hz, and in 50 Hz mode at a rate of 12.5 Hz.

## Receiver Output

In 32-channel mode, the receiver outputs are as follows:

- ***CRSF***: The RC Channels (0x16) CRSF frame carrying channels CH1 - CH16 is emitted as usual. In addition, Subset RC Channels (0x17) CRSF frames carrying channels CH17 - CH32 are emitted at a rate of 5 Hz.
- ***SBus***: The SBus frame carrying channels CH1 - CH16 (start marker 0x0F) is emitted as usual. In addition, SBus frames with start marker 0x2F carrying channels CH17 - CH32 are emitted at the same rate.
- ***MAVLink***: The RADIO_RC_CHANNELS message contains the channel data for channels CH1 - CH32 instead of only CH1 - CH16 as normally. Please note that this makes it a large MAVLink frame of 85 bytes, which in 50 Hz mode would consume ca. 75% of the capacity of a 57600 baud serial connection. Using 230400 baud is therefore highly recommended. Furthermore, this message is emitted when "Rx Snd RcChannel" = "rc channels" is set. For "Rx Snd RcChannel" = "rc override", the RC_CHANNELS_OVERRIDE message is emitted, which contains only channels CH1 - CH1; 32 channels are then not available.
- ***MSP-RC***: The MSP_SET_RAW_RC (#200) MSP message carrying channels CH1 - CH16 are emitted as usual. In addition, the MSP2_INAV_SET_AUX_RC (#2230) message carrying channels CH17 - CH32 are emitted at the same rate as the MSP_SET_RAW_RC message. MSP2_INAV_SET_AUX_RC is only 15 bytes and the burden thus minimal. Note: The 9-position channels are broken down to 3-position values.
- ***DroneCAN***: The RCInput message type contains the channel data for channels CH1 - CH32 instead of only CH1 - CH16 as normally. While twice as long as in 16-channels mode, the effect on the available data rate on the CAN bus is minimal.

## Radio Lua Script

Since EdgeTx and Frsky radios do not natively support 32 channels via CRSF, mLRS provides some Lua scripts that can be installed on the radio. The scripts make the radio send the values of channels CH17 - CH32 to the Tx module. When enabled, this causes the Tx module, and consequently the receiver, to switch into 32-channel mode.

> [!NOTE]
> In a future version, EdgeTx may natively support 32 channels via CRSF. The Lua script would then no longer be needed.

### EdgeTx/OpenTx Radios

mLRS provides two Lua scripts, a [mixes script](https://luadoc.edgetx.org/overview/script-types/mixes-scripts) and a [widget script](https://luadoc.edgetx.org/overview/script-types/widget-scripts). There is no fundamental advantage of the one over the other; which one to use is largely a matter of preference.

#### Mixes Lua Script

For installation, copy the file mlrs32.lua LOCATED in the folder mLRS32ChM to the folder /SCRIPTS/MIXES on the radio's SD card. This also activates the script.

#### Widget Lua Script

For installation, copy the folder mLRS32ChW with its content to the folder /SCRIPTS/WIDGETS/ on the radio's SD card (there should be then a folder /SCRIPTS/WIDGETS/mLRS32ChW). In order to run the script, place the widget as usual (see EdgeTx/OpenTx instructions for [widgets](https://manual.edgetx.org/color-radios/screen-settings)). The widget has options to set the color of the text, and enable or disable it. When enabled, it sends the CH17 - CH32 CRSF frames.

### Frsky/ETHOS Radios

mLRS provides also a Lua script for ETHOS radios. For installation, copy the file main.lua located in the folder Ethos/mLRS32Ch to the folder SD:/scripts/mlrs32/ on the radio's SD card, and restart the radio. Enable the task per model: Model setup -> Lua -> Lua tasks -> "mLRS 32Ch".

