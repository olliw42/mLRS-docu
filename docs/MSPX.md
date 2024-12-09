# mLRS Documentation: INAV/MSP Support #

([back to main page](../README.md))

mLRS provides the MspX technology, which is designed to improve the over-the-air communication for systems using the MSP protocol, specifically INAV. It includes the following features:
- MSP to CRSF message conversion which provides telemetry elements to the radio and therefore enables Lua scripts on the radio such as the INAV Telemetry Widget, FM2M Toolbox or the Horus Mapping Widget to function.
- Robust framing and parsing which reduces packet losses to a minimum, and compression of some very large MSP messages to increase probability of successful transmission.
- Providing of comprehensive mLRS link statistics and information to the Flight-Controller, to show them on the OSD and in blackbox recordings.
- Possibility of RC-Control, serial data communication and Radio Telemetry through a single UART. 

***Notes***: 
- For INAV Versions before 8 RC1 MspX is not strictly compliant with the MSP protocol, and softwares which require strict compliance may not work properly. This includes e.g. MWPT. In these cases, mLRS can be set into transparent mode by setting "Rx Ser Link Mode" = "transp." (the below features of MspX will then not be avaiable).
- MspX is tested and verified for INAV 7.1 and newer (it may also work with older INAV releases, but this has not been tested).
- INAV Configurator is assumed as ground control station, and INAV Lua app on the radio.
- Link statistics and information such as RSSI, LQ, SNR, etc. are provided to the FC on INAV 8 and higher (not available on earlier versions, RC Control over CRSF on a second UART are necessary, to recieve link statistics). More info can be found [here](https://github.com/iNavFlight/inav/pull/10451).

## mLRS Receiver Configuration

#### MspX

MspX is enabled by this setting in the receiver:

- "Rx Ser Link Mode" = "mspX"

#### MSP-RC

For enabling MSP-RC set:

- "Rx Snd RcChannel" = "rc override" or "rc channels" (both have the same functionality in mspX mode)

With MSP-RC enabled, SET_RAW_RC messages are sent to the flight controller. In the flight controller configure the receiver to the MSP protocol. This allows one to avoid the extra wire for CRSF or SBus. MspX needs to be enabled.

***Notes***:
RC Link Statistics are only send to the Flight controller via MSP, if "rc override" or "rc channels" is enabled. 
MSP-RC messages will always override other RC Link inputs. If CRSF is connected and CRSF selected as the RC Protocol in INAV, MSP-RC still has priority if enabled in mLRS and connected to a MSP Enabled UART.

## INAV Configuration

The baudrate should be set to 115200 or higher for consistent dataflow and RC control. Baudrates of less than 57600 can cause message loss on the INAV side and result in a inconsistent RC control at 50Hz RC Rate, if MSP-RC is used (INAV Limitation). 

INAV 8 and later will also support a baudrate of 230400 but no change in performance or stability was noticed. Additionally with INAV 8 the performance of the serial link to a ground control station will be increased, due to some optimizations in INAV. 

To use a mLRS receiver with INAV in MspX mode, the following settings have to be applied in INAV:
- Enable MSP for the Serial Port the mLRS receiver is connected to (UART 2 is recommended on most STM32 flight controllers; do not enable "Serial RX").
- Set the baudrate to 115200 or higher.
  
<img src="images/MSPX_ports.png" width="720px">

- In the Receiver tab, select the Receiver Type in the Receiver Mode panel to MSP and also set the RSSI Source to MSP (INAV 8 and later) and save settings.
  
<img src="images/MSPX_receiver.png" width="720px">

- When connecting INAV 8 Configurator through mLRS for flight monitoring, it is recommended to enable the Wireless Mode switch before connection, for better link reliability (do not use Wireless Mode with versions earlier than 8, such as INAV 7.1).

<img src="images/MSPX_wirelessmode.png" width="360px">

If your radio is connected, you should now be able to see the channel values update when you move the radio sticks. No further settings are needed and telemetry will work for EdgeTX/OpenTX radios after scanning for sensors.

## Connection Types with different INAV Versions

Depending on the chosen connection and serial mode, the functionality will slightly differ, especially in INAV versions before 8.0. This is a quick overview, what options are available and what functions to expect. 

### INAV 7

Serial Mode: 
- mspX
  - provides telemetry sensors to your radio
  - allows RC Control over MSP (rc override)
  - Ground control station use is limited to applications that can handle unrequested MSP messages (MWPTools only works in Monitor-Mode, INAV Configurator will be slow to load parameters, etc.)
  - Will not provide RC Link Statistics for OSD or Blackbox
- Transparent
  - Full functionality of GCS Software but possibility of higher message loss (Especially big MSP Messages like ADS-B Data or Waypoint Mission transfers)
  - No RC Control, No Telemetry to the radio (needs CRSF for RC control) 
  - No link statistics for the OSD (Needs CRSF for OSD Link Information)

RC Out Mode (Can be combined with Serial if the Rx has 2 UART)
- CRSF
  - allows RC Control
  - provides link statistics for OSD and Blackbox
  - No Telemetry

 ***Recommendation*** 
 For INAV 7 we recommend one of three options, depending on the usecase. 
 - mspX+CRSF if mLRS is only used as a radio control system for FPV. The separate CRSF for RC Control is recommended, to have OSD Link Statistics available
 - mspX+MSP-RC if no OSD link statistics are needed (autonomous flights and LOS only) and if you use a GCS Software that can handle passive MSP Message Monitoring with no 2-way communication (MWP)
 - Transparent+CRSF for full 2-Way GCS Communication and RC Control. In this case you will not have telemetry on your radio.

### INAV 8

Serial Mode:
- mspX
  - provides telemetry sensors to your radio
  - allows RC Control over MSP (rc override)
  - Full MSP GCS Functionality with INAV Configurator, MWP and other applications
  - comprehensive OSD and Blackbox Link Statistics with dedicated MSP messages provided by mLRS
  - limited to 50Hz RC Rate (Only relevant for 2.4GHz FLRC Mode with 111Hz Packet rate, Will be limited to 37Hz RC rate)
- Transparent
  - See INAV 7 section
  - Not recommended

RC Out Mode (Can be combined with Serial if the Rx has 2 UART)
- CRSF
  - allows RC Control
  - RC Rate up to 111Hz in 2.4GHz FLRC mode

 ***Recommendation***
Since INAV 8 in combination with mLRS can provide all features over mspX, it is recommended to only use a single UART mspX connection for most vehicles. The only exception is the 2.4GHz FLRC mode that can provide 111Hz packet and RC rate. 
Due to a performance limitation in INAV, this mode had to be limited to 37Hz RC Rate over MSP. Use a separated CRSF UART instead, to achieve full 111Hz RC Update Rates in this mode. All other features will work as normal. 


