# mLRS Documentation: MspX #

([back to main page](../README.md))

**Important: MSP support is experimental and currently only available in the branch 'dev-mspx'.**

MspX is a technology designed to improve the over-the-air communication for systems using the MSP protocol, such as INAV. It includes the following features:
- Robust framing and parsing which reduces packet losses to a minimum.
- Compression of some very large MSP messages to increase probability of successful transmission.
- MSP to CRSF message conversion which provides telemetry elements to the radio and therefore enables Lua scripts on the radio such as the INAV app to function.

MspX is currently tested for INAV 7.1.

## Configuration

MspX is enabled by setting the "Rx Ser Link Mode" parameter in the receiver to "mspX".

Further parameter settings:
- "Rx Snd RcChannel": When set to "rc override" or "rc channels", SET_RAW_RC MSP messages are sent to the flight controller. In the flight controller configure the receiver to the MSP protocol. This allows one to avoid the extra wire for CRSF.
- "Rx Snd RadioStat": has no effect.



