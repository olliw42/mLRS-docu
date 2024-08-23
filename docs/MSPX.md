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

MspX is tested and verified with INAV 7.1 as well as 8.0 development builds but should also work with INAV 6.0 and newer. The baudrate should be set to 115200 as lower baud rates have shown irregular telemetry update rates on the radio due to the lack of flow control on the INAV side. INAV 8.0 and later will also support a baud rate of 230400 but no change in performance or stability was noticed. Additionally with INAV 8.0 the performance of the serial link to a Ground Control Station (GCS) will be increased, due to some optimizations in INAV. 

To use a mLRS Receiver with INAV in MspX mode, the following settings have to be applied:
- Enable MSP for the Serial Port the mLRS receiver is conencted to (UART 2 is recommended on most STM32 Flight-Controllers; do not enable "Serial RX")
- Set the Baud-Rate to 115200 or higher
  
![image](https://github.com/user-attachments/assets/e4263b21-f3c5-40b5-a498-bf3c4906fdc2)


- In the Receiver Tab, select the Receiver Mode Type to MSP and save settings
  
![image](https://github.com/user-attachments/assets/d3f9adb4-3438-4552-989b-dea2ab1c044e)


- When connecting INAV 8.0 Configurator through mLRS it is highly recommended to enable the Wireless Mode switch before connection, for better link reliability. (Do not use Wireless Mode with versions older than 8.0).

![image](https://github.com/user-attachments/assets/2291187a-5d27-4857-a4d6-454f6b0f5e30)



If your radio is connected, you should now be able to see the channel values update. No further settings are needed and telemetry will work for OpenTX/EdgeTX radios after scanning for sensors. 
