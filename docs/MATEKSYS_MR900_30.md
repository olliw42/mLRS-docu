# mLRS Documentation: MatekSys mR900-30 #

([back to main page](../README.md))
([back to MatekSys page](MATEKSYS.md))

The MatekSys mLRS receivers and Tx modules are specifically designed for mLRS, and are currently simply the best options available. 

This page describes the MatekSys mR900-30 device for the 868/915 MHz band.

<table>
  <tbody>
    <tr>
      <td>Frequency Band</td>
      <td>868 MHz/915 MHz</td>
    </tr>
    <tr>
      <td>Max. RF Output Power</td>
      <td>+30 dBm (1 W)</td>
    </tr>
    <tr>
      <td>Supported Modes</td>
      <td>31 Hz, 19 Hz, FSK (50 Hz)</td>
    </tr>
    <tr>
      <td>LoRa Chipset</td>
      <td>SX126x</td>
    </tr>
    <tr>
      <td>Compatibility</td>
      <td>Compatible with SeeedStudio Wio-E5, EBYTE E77 MBL, E77 Easy Solder. Incompatible with all SX127x hardware (Frsky R9 and ELRS 900 Mhz).</td>
    </tr>
  </tbody>
</table>


## mR900-30 ##

- [Product Page](https://www.mateksys.com/?page_id=12174)

The mR900-30 device can be used in three ways:
- as receiver
- as transmitter
- in combination with a Tx carrier board it can be used as a Tx module

The mR900-30 provides a 8-pin pin header, a USB-C port, and a good number of solder pads on the bottom side for additional use.


### As Receiver ###

Connections (name in respect to board print-ons, otherwise please refer to graphic):

<table>
  <tbody>
    <tr>
      <td>V</td><td>Power supply, 4.5 - 13 V</td>
    </tr><tr>
      <td>G</td><td>Ground</td>
    </tr><tr>
      <td>Tx1, Rx1</td><td>Serial</td>
    </tr><tr>
      <td>Tx2</td><td>Out (CRSF, SBus, SBUs inv.)</td>
    </tr><tr>
      <td>button</td><td>Bind, and for firmware upgrade</td>
    </tr><tr>
      <td>USB-C</td><td>Power & firmware upgrade</td>
    </tr>
  </tbody>
</table>

Notes:
- To enter bind mode, press the button for ca 4 sec.
- To enter the system bootloader for firmware upgrade, press the button during power up.
- The USB-C port can be used for powering as well as for firmware upgrade (per DFU).
- The Rx2, LT1, LT2 pins have no function.


### As Transmitter ###

Connections (name in respect to board print-ons, otherwise please refer to graphic):

<table>
  <tbody>
    <tr>
      <td>V</td><td>Power supply, 4.5 - 13 V</td>
    </tr><tr>
      <td>G</td><td>Ground</td>
    </tr><tr>
      <td>Tx1, Rx1</td><td>Serial</td>
    </tr><tr>
      <td>LT1, LR1</td><td>Com / Cli</td>
    </tr><tr>
      <td>Tx2</td><td>JRPin5 / In</td>
    </tr><tr>
      <td>button</td><td>Bind, and for firmware upgrade</td>
    </tr><tr>
      <td>USB-C</td><td>Power & firmware upgrade</td>
    </tr>
  </tbody>
</table>

Notes:
- To enter bind mode, press the button for ca 4 sec.
- To enter the system bootloader for firmware upgrade, press the button during power up.
- The USB-C port can be used for powering as well as for firmware upgrade (per DFU).
- The Rx2 pin has no function.


### As Tx Module ###

TODO


## Flashing ##

**Important: Every time that you power a board you should ensure that there is an antenna connected otherwise you risk damaging the RF section.**

### DFU via USB-C ###

- Download and install [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)
- Hold down the button while powering up
- Connect the device via USB-C to your PC
- Launch STM32CubeProgrammer and select USB as the connection method, click connect. If the Port field does not show "USB1", the click the buttun right to it.
- From the menu on the left select the Download tile
- Select the correct firmware in the Download section, click Start Program
- Power cycle the board, the red LED should blink which indicates that the board is disconnected


### ST-Link via SWD ###

- Download and install [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)
- Connect your ST-Link programmer to the 3V3, GND, SWD, and SWCLK pins on the board (images below)
    - The SWD and SWCLK pins are labeled 'SWD' and 'SWC' respectively
    - Some ST-Link programmers provide power and some do not - ensure the board is powered
- Launch STM32CubeProgrammer and select ST-Link as the connection method, click connect
- From the menu on the left select the Download tile
- Select the correct firmware in the Download section, click Start Program
- Power cycle the board, the red LED should blink which indicates that the board is disconnected

