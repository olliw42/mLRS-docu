# mLRS Documentation: ELRS Receivers #

([back to main page](../README.md))

## Supported ELRS Receivers ##

As of April 2024, the following ELRS receiver targets are supported:

<table>
  <tbody>
    <tr>
      <td>Target</td>
      <td>Transmit Power</td>
    </tr>
    <tr>
      <td>Generic 900</td>
      <td>17 dBm (50 mw)</td>
    </tr>
    <tr>
      <td>Generic 900 PA</td>
      <td>27 dBm (500 mw)</td>
    </tr>
    <tr>
      <td>Generic 2400</td>
      <td>12.5 dBm (18 mw)</td>
    </tr>
      <td>Generic 2400 PA</td>
      <td>20 dBm (100 mw)</td>
    </tr>
      </tr>
      <td>Generic 2400 True Diversity PA</td>
      <td>20 dBm (100 mw)</td>
    </tr>
  </tbody>
</table>

To determine if your receiver hardware is supported, go to [ELRS Targets](https://github.com/ExpressLRS/targets/blob/master/targets.json) and find the layout file of your hardware.

Note: 868/915 MHz ELRS receivers cannot connect with 868/915 MHz mLRS Tx modules using the SX126x LoRa chipset. This is because the 868/915 MHz ELRS receivers use the SX127x LoRa chipset, which is incompatible with the SX126x LoRa chipset for the spreading factor used by the mLRS 19 Hz mode. In addition, the SX127x does not support the spreading factor which is used for the mLRS 31 Hz mode.

## Selected ELRS Receivers ##

The following receivers are good choices. They support &#8805; 100 mW, are affordable, and have been validated by the mLRS team.

<table>
  <tbody>
    <tr>
      <td>Product Name</td>
      <td>Frequency Band</td>
      <td>Transmit Power</td>
    </tr>
    <tr>
      <td>Bayck 915M Nano Pro</td>
      <td>868/915 MHz</td>
      <td>27 dBm (500 mw)</td>
    </tr>
    <tr>
      <td>BetaFPV SuperD 2.4G</td>
      <td>2.4 GHz</td>
      <td>20 dBm (100 mw)</td>
    </tr>
    <tr>
      <td>SpeedyBee Nano 2.4G</td>
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

- Download the firmware for your receiver.
    - The latest pre-release is found [here](https://github.com/olliw42/mLRS/tree/main/firmware/pre-release-esp).
    - The latest official release is found [here](https://github.com/olliw42/mLRS/releases).
- To prepare your receiver for flashing, you will need to connect it to a USB<>UART, follow the normal connections:
    - 5V to 5V
    - GND to GND
    - Tx to Rx
    - Rx to Tx
- When powering on the receiver you will need to have the bind button pushed down to enter into bootloader mode.
    - For receivers with a single (non-RGB) LED you can confirm the receiver is in bootloader mode if the LED is solid.
- Open a supported browser (Chrome, Edge, Opera, not Firefox) and navigate [here](https://esp.huhn.me/).
- Click connect and select the serial port of your USB<>UART.
- Upload the .bin file for your receiver and click program.
- Once the firmware has been written sucessfully, power cycle the receiver. The LED should blink to indicate that it is looking for a connection.
    - Note: Binding can be done by holding down the button for four seconds.