# mLRS Documentation: INAV/MSP Support #

([back to main page](../README.md))

mLRS provides the MspX technology, which is designed to improve the over-the-air communication for systems using the MSP protocol, specifically INAV. It includes the following features:
- MSP to CRSF message conversion which provides telemetry elements to the radio and therefore enables Lua scripts on the radio such as the INAV Telemetry Widget, FM2M Toolbox or the Horus Mapping Widget to function.
- Robust framing and parsing which reduces packet losses to a minimum, and compression of some very large MSP messages to increase probability of successful transmission.
- Providing of comprehensive mLRS link statistics and information to the Flight-Controller, to show them on the OSD and in blackbox recordings.
- Possibility of RC-Control, serial data communication and Radio Telemetry through a single UART. 

***Notes***: 
- For INAV Versions before 8.0 RC1 MspX is not strictly compliant with the MSP protocol, and softwares which require strict compliance may not work properly. This includes e.g. MWPT. In these cases, mLRS can be set into transparent mode by setting "Rx Ser Link Mode" = "transp." (the below features of MspX will then not be avaiable).
- MspX is tested and verified for INAV 7.1 and newer (it may also work with older INAV releases, but this has not been tested).
- INAV Configurator is assumed as ground control station, and INAV Lua app on the radio.
- Link statistics and information such as RSSI, LQ, SNR, etc. are provided to the FC on INAV 8.0 and higher (not available on earlier versions, RC Control over CRSF on a second UART are necessary, to recieve link statistics). More info can be found [here](https://github.com/iNavFlight/inav/pull/10451).

## mLRS Receiver Configuration

#### MspX

MspX is enabled by this setting in the receiver:

- "Rx Ser Link Mode" = "mspX"

#### MSP-RC

For enabling MSP-RC set:

- "Rx Snd RcChannel" = "rc override" or "rc channels"

With MSP-RC enabled, SET_RAW_RC messages are sent to the flight controller. In the flight controller configure the receiver to the MSP protocol. This allows one to avoid the extra wire for CRSF or SBus. MspX needs to be enabled.

***Notes***:
RC Link Statistics are only send to the Flight controller via MSP, if "rc override" or "rc channels" is enabled. 

## INAV Configuration

The baudrate should be set to 115200 or higher for consistent dataflow and RC control. Baudrates of less than 57600 can cause message loss on the INAV side and result in a inconsistent RC control at 50Hz RC Rate, if MSP-RC is used (INAV Limitation). 

INAV 8.0 and later will also support a baudrate of 230400 but no change in performance or stability was noticed. Additionally with INAV 8.0 the performance of the serial link to a ground control station will be increased, due to some optimizations in INAV. 

To use a mLRS receiver with INAV in MspX mode, the following settings have to be applied in INAV:
- Enable MSP for the Serial Port the mLRS receiver is connected to (UART 2 is recommended on most STM32 flight controllers; do not enable "Serial RX").
- Set the baudrate to 115200 or higher.
  
<img src="images/MSPX_ports.png" width="720px">

- In the Receiver tab, select the Receiver Type in the Receiver Mode panel to MSP, and save settings.
  
<img src="images/MSPX_receivermode.png" width="720px">

- When connecting INAV 8.0 Configurator through mLRS it is highly recommended to enable the Wireless Mode switch before connection, for better link reliability (do not use Wireless Mode with versions earlier than 8.0, such as INAV 7.1).

<img src="images/MSPX_wirelessmode.png" width="360px">

If your radio is connected, you should now be able to see the channel values update when you move the radio sticks. No further settings are needed and telemetry will work for EdgeTX/OpenTX radios after scanning for sensors.




