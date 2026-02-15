# mLRS Documentation: INAV/MSP Support #

([back to main page](../README.md))

mLRS provides the MspX technology, which is designed to improve the over-the-air communication for systems using the MSP protocol, specifically INAV. It includes the following features:
- MSP to CRSF message conversion which provides telemetry elements to the radio and therefore enables Lua scripts on the radio such as the INAV Telemetry Widget, FM2M Toolbox or the Horus Mapping Widget to function.
- Provides comprehensive link statistics such as RSSI, LQ, SNR, etc. to the flight controller, enabling them to be shown on the OSD and recorded in the Blackbox.
- Option to have both RC and MSP serial data on a single UART. 
- Robust framing and parsing which reduces packet losses to a minimum, and compression of some very large MSP messages to increase probability of successful transmission.

In the following INAV 8 or 9 is assumed.

> [!NOTE]
> - It is highly recommended to use INAV 8 or later, although mLRS has also been tested with INAV 7.1.
> - For INAV 7.1 and earlier, several limitations exist. For the details please see the last chapter below, [Differences between INAV 8/9 and 7 when using MspX](#differences-between-inav-89-and-7-when-using-mspx).
> - MspX requires mLRS 1.3.04 or higher to be used.
> - An in-depth description of what is going on under the hood is given [here](https://discord.com/channels/1005096100572700794/1005268892437970945/1359794224349974608) and [here](https://discord.com/channels/1005096100572700794/1005268892437970945/1359795724056789002).

## mLRS Receiver Configuration

#### MspX

For enabling MspX set:

- "Rx Ser Link Mode" = "mspX"
- "Rx Ser Baudrate" = "115200"

***Note***: A baudrate of 230400 can also be used, but no change in performance or stability was noticed.

#### MSP-RC

For enabling MSP-RC set:

- "Rx Snd RcChannel" = "rc override" or "rc channels" (both have the same functionality in MspX mode)

> [!NOTE]
> - RC link statistics are only sent to the flight controller via MSP if "rc override" or "rc channels" is selected. 
> - MSP-RC messages will always override other RC inputs. If CRSF is connected and selected as the RC protocol in INAV, MSP-RC still has priority if enabled in mLRS and connected to a MSP enabled UART.
> - The RC update rate will be limited to 37 Hz in 2.4 GHz FLRC mode when using MspX (see [Differences between INAV 8/9 and 7 when using MspX](#differences-between-inav-89-and-7-when-using-mspx)).


## INAV Configuration

To use a mLRS receiver with INAV in MspX mode, the following settings have to be applied in INAV:
- Enable MSP for the Serial Port the mLRS receiver is connected to (UART 2 is recommended on most STM32 flight controllers; do not enable "Serial RX").
- Set the baudrate to 115200 or higher for consistent dataflow and RC control. Baudrates of less than 57600 can cause message loss on the INAV side and result in inconsistent RC control over MSP-RC (INAV limitation).
- INAV 8 also supports a baudrate of 230400 but no change in performance or stability was noticed.
  
<img src="images/MSPX_ports.png" width="720px">

- In the Receiver tab, change the Receiver Mode to 'MSP' and the RSSI Source to 'MSP' then save settings.
  
<img src="images/MSPX_receiver.png" width="720px">

- When connecting INAV 8/9 Configurator through mLRS for flight monitoring, it is recommended to enable the 'Wireless Mode' switch before connection, for better link reliability (do not use 'Wireless Mode' with versions lower than INAV 8).

<img src="images/MSPX_wirelessmode.png" width="360px">

If your radio is connected, you should now be able to see the channel values update when you move the radio sticks. No further settings are needed and telemetry will work for EdgeTX/OpenTX radios after scanning for sensors.

## Differences between INAV 8/9 and 7 when using MspX

Depending on the chosen connection and serial mode, the functionality will differ for INAV 8/9 and INAV 7. This is a quick overview, what options are available and what functions to expect. 

### INAV 8/9

Serial Mode:
- MspX
  - provides telemetry sensors to your radio
  - allows RC control over MSP
  - full MSP GCS functionality with INAV Configurator, MWP and other applications
  - comprehensive OSD and Blackbox link statistics with dedicated MSP messages provided by mLRS
  - RC update rate is limited to 37 Hz in 2.4 GHz FLRC mode
- Transparent
  - not recommended
  - see INAV 7 section

RC Out Mode (can be combined with serial if the mLRS receiver has 2 UARTs)
- CRSF
  - allows RC control
  - provides limited link statistics for OSD and Blackbox
  - RC update rate up to 111 Hz in 2.4 GHz FLRC mode
  - no downlink telemetry

 ***Recommendation***
 
Since INAV 8/9 in combination with mLRS can provide all features over MspX, it is recommended to only use a single UART MspX connection for most vehicles. The only exception is the 2.4 GHz FLRC mode that can provide 111 Hz RC rate over CRSF. Due to a performance limitation in INAV, this mode had to be limited to 37 Hz RC rate over MSP. Use a separate CRSF UART instead, to achieve full 111 Hz RC update rates in this mode. All other features will work as normal. 

### INAV 7

Serial Mode: 
- MspX
  - provides telemetry sensors to your radio
  - allows RC control over MSP
  - GCS use is limited to applications that can handle unrequested MSP messages (MWPTools only works in Monitor-Mode, INAV Configurator will be slow to load parameters, etc.)
  - no RC link statistics for OSD or Blackbox
  - RC update rate is limited to 37 Hz in 2.4 GHz FLRC mode
- Transparent
  - full functionality of GCS software but possibility of higher message loss (especially big MSP messages like ADS-B Data or Waypoint Mission transfers)
  - no RC control (needs CRSF for RC control) 
  - no link statistics for the OSD (needs CRSF for OSD link information)
  - no telemetry to the radio

RC Out Mode (can be combined with serial if the mLRS receiver has 2 UART)
- CRSF
  - allows RC control
  - provides limited link statistics for OSD and Blackbox
  - RC update rate up to 111 Hz in 2.4 GHz FLRC mode
  - no downlink telemetry

 ***Recommendation*** 
 
 For INAV 7 we recommend one of three options, depending on the usecase. 
 1. MspX+CRSF if you fly FPV, the separate CRSF for RC control enables OSD Link Statistics.
 2. MspX+MSP-RC if no OSD link statistics are needed (autonomous flights and LOS only) and if you use a GCS software that can handle passive MSP Message Monitoring with no 2-way communication (MWP).
 3. Transparent+CRSF for full 2-way GCS communication and RC control. However, in this case you will not have telemetry on your radio.

