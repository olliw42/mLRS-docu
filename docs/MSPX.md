# mLRS Documentation: MspX #

([back to main page](../README.md))

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

## INAV Configuration

To use a mLRS Receiver with INAV in MspX mode, the following settings have to be applied:
- Enable MSP for the Serial Port the mLRS receiver is conencted to (do not enable Serial RX)
- Set the Baud-Rate to 115200 or higher (Only INAV 7.1 and 8.0-dev are tested, Version 6.0 and newer should also work)
- INAV 8.0 and later will also support Baud 230400 but with no noticeable difference in performance or stability 
![image](https://github.com/user-attachments/assets/c359f819-66dd-453c-8883-f2498103c7a6)

- In the Receiver Tab, select the Receiver Mode Type to MSP and save settings
![image](https://github.com/user-attachments/assets/75cb76b9-6487-4d64-a538-b46d4ca446bf)

You should now be able to detect channel values, if your radio is connected. No further settings are needed and telemetry will work for OpenTX/EdgeTX radios after Scanning for sensors. 
