# mLRS Documentation: ELRS Receivers #

([back to main page](../README.md))

## Supported ELRS Receivers ##

As of April 2024, ELRS receivers with an ESP8285 MCU are experimentally supported by mLRS. The following targets are supported:

- Generic 900
- Generic 900 PA
- Generic 2400
- Generic 2400 PA
- Generic 2400 PA-D

To determine if your receiver hardware is supported, go to [ELRS Targets](https://github.com/ExpressLRS/targets/blob/master/targets.json) and find the layout file of your hardware.

Note: ELRS receivers that use an ESP32 MCU are under active development.

## Recommended ELRS Receivers ##

The following receivers are recommended as they support >= 100 mW transmit power and have been validated by the mLRS team.

<table>
  <tbody>
    <tr>
      <td>Product Name</td>
      <td>Frequency Band</td>
      <td>Transmit Power</td>
    </tr>
    <tr>
      <td>BayckRC 915M Nano Pro</td>
      <td>868/915 MHz</td>
      <td>27 dBm (500 mw)</td>
    </tr>
    <tr>
      <td>SpeedyBee Nano</td>
      <td>2.4 GHz</td>
      <td>20 dBm (100 mw)</td>
    </tr>
  </tbody>
</table>

## Connections ##

All ELRS receivers have a standardized pinout and will need to be connected to the FC as follows:

<img src="images/ELRS_fc_wiring.png" width="600px">

Note: In order to send RC channels over the serial connection, change the Rx Snd RcChannel parameter to 'rc override'.

## Flashing ##

- To prepare your receiver for flashing, you will need to connect it to a USB<>UART, follow the normal connections:
    - 5V to 5V
    - GND to GND
    - Tx to Rx
    - Rx to Tx
- When powering on the receiver you will need to have the bind button pushed down to enter into bootloader mode.
    - For receivers with a single (non-RGB) LED you can confirm the receiver is in bootloader mode if the LED is solid.
- Open a supported browser (Chrome, Edge, Opera) and navigate [here](https://esp.huhn.me/).
- Click connect and select the serial port of your USB<>UART.
- Upload the .bin file for your receiver and click program.
- Once the firmware has been written sucessfully, power cycle the receiver. The LED should blink to indicate that it is looking for a connection.
    - ***Note***: Binding can be done by holding down the button for four seconds.