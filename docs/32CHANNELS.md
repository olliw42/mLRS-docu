# mLRS Documentation: 32 Channels Support #

([back to main page](../README.md))

mLRS can support 32 RC channels (since v1.4.04). In order to do so, the normal behavior in 16-channels operation mode is modified in various ways.

The 32-channel mode is selected automatically based on the CRSF frames sent to the Tx module. If the Tx module receives CRSF frames containing RC channel data for channels 17 - 32, it immediately switches to 32-channel mode, and the receiver follows along. The receiver output then changes according to the selected method: CRSF, MAVLink RADIO_RC_CHANNELS, MSP-RC, or DroneCAN (SBus does not support 32 channels).

## 32-Channel Layout

The channel layout changes as follows:

- CH1 - CH8: 8 channels with 11-bit resolution, full rate/no interlacing
- CH9 - CH16: 8 channels with 8-bit resolution, interlaced 1:2
- CH17 - CH20: 4 channels with 9-position resolution, interlaced 1:4
- CH21 - CH32: 12 channels with 3-position resolution, interlaced 1:4

The 11-bit channels are sent with every frame, and have a slightly higher reception probability than the other channels. The 8-bit channels are interlaced with a 1:2 ratio, meaning that the blocks of channels CH9 - CH12 and CH13 - CH16 are sent alternately, each block is sent every second frame. The nine- and three-position channels are interlaced with 1:4, with each block of four channels being sent every fourth frame. In 19 Hz mode, these channels are therefore updated every ca. 0.2 seconds, in 50 Hz mode every 80 ms.

## Receiver Output

In 32-channel mode, the receiver outputs are as follows:

- ***CRSF***: The RC Channels (0x16) CRSF frame carrying channels CH1 - CH16 is emitted as usual. In addition, Subset RC Channels (0x17) CRSF frames carrying channels CH17 - CH32 are emitted at a rate of 5 Hz.
- ***MAVLink***: The RADIO_RC_CHANNELS message contains the channel data for channels CH1 - CH32 instead of only CH1 - CH16 as normally. Please note that this makes it a large MAVLink frame of 85 bytes, which in 50 Hz mode would consume ca. 75% of the capacity of a 57600 baud serial connection. Using 230400 baud is therefore highly recommended. Furthermore, this message is emitted when "Rx Snd RcChannel" = "rc channels" is set. For "Rx Snd RcChannel" = "rc override", the RC_CHANNELS_OVERRIDE message is emitted, which contains only channels CH1 - CH1; 32 channels are then not available.
- ***MSP-RC***: The MSP_SET_RAW_RC (#200) MSP message carrying channels CH1 - CH16 are emitted as usual. In addition, the MSP2_INAV_SET_AUX_RC (#2230) message carrying channels CH17 - CH32 are emitted at the same rate as the MSP_SET_RAW_RC message. MSP2_INAV_SET_AUX_RC is only 15 bytes and the burden thus minimal.
- ***DroneCAN***: The RCInput message contains the channel data for channels CH1 - CH32 instead of only CH1 - CH16 as normally. While twice as long as in 16-channels mode, the effect on the available data rate on the CAN bus is minimal.

## Radio Lua Script

Since EdgeTx and Frsky radios do not natively support 32 channels via CRSF, mLRS provides some Lua scripts that can be installed on the radio. The scripts make the radio send the values of channels CH17 - CH32 to the Tx module. When enabled, this causes the Tx module, and consequently the receiver, to switch into 32-channel mode.

TODO: Describe scripts installation and usage

> [!NOTE]
> In a future version, EdgeTx may natively support 32 channels via CRSF. The Lua widget script would then no longer be needed.

