# mLRS Documentation: 32 Channels Support #

([back to main page](../README.md))

mLRS supports 32 RC channels (since v1.4.04), with the following differences compared to the normal behavior in 16-channel operation mode.

The 32-channel mode is selected automatically based on the CRSF frames sent to the Tx module. If the Tx module receives CRSF frames containing RC channel data for channels 17 – 32, it immediately switches to 32-channel mode, and the receiver follows accordingly. The receiver output then changes according to the selected protocol: CRSF, MAVLink RADIO_RC_CHANNELS, MSP-RC, or DroneCAN. SBus does not support 32 channels.

## 16-Channel Layout

For comparision, the channel layout in 16-channel mode is recalled:

<table><tr>
<td>CH1 - CH8</td><td>8 channels with 11-bit resolution</td>
</tr><tr>
<td>CH9 - CH12</td><td>4 channels with 8-bit resolution</td>
</tr><tr>
<td>CH13 - CH16</td><td>4 channels with 3-position resolution</td>
</tr></table>

All channels are sent with every over-the-air (OTA) frame and are update at full rate. Channels CH1 - CH4 and CH13, CH14 have a slightly higher reception probability than the other channels.

## 32-Channel Layout

The channel layout in 32-channel mode is as follows:

<table><tr>
<td>CH1 - CH8</td><td>8 channels with 11-bit resolution</td><td>full rate/no interlacing</td>
</tr><tr>
<td>CH9 - CH16</td><td>8 channels with 8-bit resolution</td><td>interlaced 1:2</td>
</tr><tr>
<td>CH17 - CH20</td><td>4 channels with 9-position resolution</td><td>interlaced 1:4</td>
</tr><tr>
<td>CH21 - CH32</td><td>12 channels with 3-position resolution</td><td>interlaced 1:4</td>
</tr></table>

The 11-bit channels are sent with every OTA frame, and have a slightly higher reception probability than the other channels. The 8-bit channels are interlaced with a 1:2 ratio, meaning that the blocks of channels CH9 - CH12 and CH13 - CH16 are sent alternately, each block is sent every second frame. The nine- and three-position channels are interlaced with 1:4, with each block of four channels being sent every fourth frame. In 19 Hz mode, these channels are therefore updated at a rate of ca. 5 Hz, and in 50 Hz mode at a rate of 12.5 Hz.

## Receiver Output

In 32-channel mode, the receiver outputs are as follows:

- ***CRSF***: The RC Channels (0x16) CRSF frame carrying channels CH1 - CH16 is emitted as usual. In addition, Subset RC Channels (0x17) CRSF frames carrying channels CH17 - CH32 are emitted at a rate of 5 Hz.
- ***MAVLink***: The RADIO_RC_CHANNELS message is emitted at the full rate, with either channel data for CH1 – CH16 or CH1 – CH32, where the 16-channel variant is replaced by the 32-channel variant at a rate of 5 Hz. Note that this message is emitted when "Rx Snd RcChannel" = "rc channels" is set. For "Rx Snd RcChannel" = "rc override", the RC_CHANNELS_OVERRIDE message is emitted, which contains only channels CH1 - CH16; 32 channels are then not available.
- ***MSP-RC***: The MSP_SET_RAW_RC (#200) message carrying channels CH1 - CH16 is emitted as usual. In addition, the MSP2_INAV_SET_AUX_RC (#2230) message carrying channels CH17 - CH32 are emitted at the same rate as the MSP_SET_RAW_RC message. MSP2_INAV_SET_AUX_RC is only 15 bytes and the burden thus minimal. Note: The 9-position channels are broken down to 3-position values.
- ***DroneCAN***: The RCInput message type contains the channel data for channels CH1 - CH32 instead of only CH1 - CH16 as normally. While twice as long as in 16-channels mode, the effect on the available data rate on the CAN bus is minimal.

## FrSky/ETHOS Radios

FrSky ETHOS radios support mLRS' 32-channel mode natively since ETHOS firmware 26.1.3. Go to the "RF systems" page and set the channel range to CH32.

For those who prefer to update their radio later, or not at all, mLRS provides a Lua script that enables 32-channel support. For installation, copy the file main.lua from Ethos/mLRS32Ch/ to SD:/scripts/mlrs32/ on the radio's SD card, and restart the radio. Enable the task per model under Model setup -> Lua -> Lua tasks -> "mLRS 32Ch".

mLRS thanks FrSky for the swift and great cooperation in bringing 32 channels to life in ETHOS.

## EdgeTx Radios

EdgeTx does not natively support 32 channels via CRSF, therefore mLRS provides Lua scripts that can be installed on the radio. The scripts make the radio send the values of channels CH17 - CH32 to the Tx module. When enabled, this causes the Tx module, and consequently the receiver, to switch into 32-channel mode.

Two Lua scripts are provided, a [mixes script](https://luadoc.edgetx.org/overview/script-types/mixes-scripts) and a [widget script](https://luadoc.edgetx.org/overview/script-types/widget-scripts). There is no fundamental advantage of the one over the other; which one to use is largely a matter of preference.

> [!NOTE]
> In a future version, EdgeTx may natively support 32 channels via CRSF. The Lua script would then no longer be needed.

#### Mixes Lua Script

For installation, copy the file mlrs32.lua located in the folder mLRS32ChM to the folder /SCRIPTS/MIXES/ on the radio's SD card. In order to run the script, add it to the mixer (custom) scripts (see EdgeTx/OpenTx instructions for [mixer scripts](https://manual.edgetx.org/color-radios/model-settings/custom-scripts)).

#### Widget Lua Script

For installation, copy the folder mLRS32ChW with its content to the folder /WIDGETS/ on the radio's SD card (there should be then a folder /WIDGETS/mLRS32ChW/). In order to run the script, place the widget as usual (see EdgeTx/OpenTx instructions for [widgets](https://manual.edgetx.org/color-radios/screen-settings)). The widget has options to set the color of the text, and enable or disable it. When enabled, it sends the CH17 - CH32 CRSF frames.

