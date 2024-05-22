# mLRS Documentation: MspX #

([back to main page](../README.md))

**Important: MSP support is experimental and currently only available in the branch 'dev-mspx'**

MspX is a technology designed to improve the over-the-air communication for systems using the MSP protocol, such as INAV systems. It introduces more robust framing and parsing which reduces packet losses to the minimum, and adds features such as compression of some very large MSP messages. It also converts MSP message into CRSF telemetry messages to the radio, thus providng telemetry to the radio and Lua scripts running on the radio.

MspX is currently under test with INAV 7.1.

MspX is enabled by setting the "Rx Ser Link Mode" parameter in the receiver to "mspX".

Further parameter settings of relevance:
- "Rx Snd RcChannel": when set to "rc override" or "rc channels", a MSP SET_RAW_RC message is sent to the flight controller. In the fligh controller configure the receiver to the MSP protocol. This allows avoiding an extra wire for CRSF.
- "Rx Snd RadioStat": has no effect



