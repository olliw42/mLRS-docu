# mLRS Documentation: INAV/MSP Support #

([back to main page](../README.md))

mLRS provides the MspX technology, which is designed to improve the over-the-air communication for systems using the MSP protocol, specifically INAV. It includes the following features:
- MSP to CRSF message conversion which provides telemetry elements to the radio and therefore enables Lua scripts on the radio such as the INAV app or telemetry widgets to function.
- Robust framing and parsing which reduces packet losses to a minimum, and compression of some very large MSP messages to increase probability of successful transmission.

***Notes***: 
- MspX is not strictly compliant with the MSP protocol, and softwares which require strict compliance may not work properly. This includes e.g. MWP. In these cases, mLRS can be set into transparent mode by setting "Rx Ser Link Mode" = "transp." (the below features of MspX will then not be avaiable).
- MspX is tested and verified for INAV 7.1. It has been successfully tested with INAV 8.0 development builds (it may also work with INAV 6.0 and newer, but this has not been tested).
- INAV Configurator is assumed as ground control station, and INAV Lua app on the radio.
- 'Link statistics and information such as RSSI, LQ, SNR, etc. are provided to the FC on INAV 8.0 and higher (not available on earlier versions). More info can be found [here](https://github.com/iNavFlight/inav/pull/10451).

## mLRS Receiver Configuration

#### MspX

MspX is enabled by this setting in the receiver:

- "Rx Ser Link Mode" = "mspX"

#### MSP-RC

For enabling MSP-RC set:

- "Rx Snd RcChannel" = "rc override" or "rc channels"

With MSP-RC enabled, SET_RAW_RC messages are sent to the flight controller. In the flight controller configure the receiver to the MSP protocol. This allows one to avoid the extra wire for CRSF or SBus. MspX needs to be enabled.

## INAV Configuration

The baudrate should be set to 115200 as lower baudrates have shown irregular telemetry update rates on the radio due to the lack of flow control on the INAV side. 

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
