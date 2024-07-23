# mLRS Documentation: MatekSys mR24-30 #

([back to main page](../README.md))
([back to MatekSys page](MATEKSYS.md))

The MatekSys mLRS receivers and Tx modules are specifically designed for mLRS, and are currently simply the best options available. 

This page describes the MatekSys mR24-30 device for the 2.4 GHz band.

<table>
  <tbody>
    <tr>
      <td>Frequency Band</td>
      <td>2.4 GHz</td>
    </tr>
    <tr>
      <td>Max. RF Output Power</td>
      <td>+30 dBm (1 W)</td>
    </tr>
    <tr>
      <td>Supported Modes</td>
      <td>50 Hz, 31 Hz, 19 Hz, FLRC (111 Hz)</td>
    </tr>
    <tr>
      <td>LoRa Chipset</td>
      <td>SX128x</td>
    </tr>
    <tr>
      <td>Compatibility</td>
      <td>Compatible with all 2.4 GHz mLRS gear, including the ELRS 2.4 GHz receivers</td>
    </tr>
  </tbody>
</table>


## mR24-30 ##

- [Product Page](https://www.mateksys.com/?page_id=12174)

The mR24-30 device can be used in three ways:
- as receiver
- as transmitter
- in combination with a Tx carrier board it can be used as a Tx module

The mR24-30 provides a 8-pin pin header, a USB-C port, and a good number of solder pads on the bottom side for additional use.


### As Transmitter ###

Connections (name in respect to board print-ons, otherwise please refer to graphic):

<table>
  <tbody>
    <tr>
      <td>V:</td><td>power supply, 4.5 V - 13 V</td>
    </tr><tr>
      <td>serial:</td><td>Tx1, Rx1</td>
    </tr><tr>
      <td>com / cli:</td><td>LT1, LR1</td>
    </tr><tr>
      <td>JRPin5 / in:</td><td>Tx2</td>
    </tr><tr>
      <td>bind:</td><td>button</td>
    </tr>
  </tbody>
</table>

Notes:
- To enter the system bootloader for flashing, hold the button down during power up.
- The USB-C port can be used for powering as well as for flashing (per DFU).
- The Rx2 pin has no function.


### As Receiver ###

Connections (name in respect to board print-ons, otherwise please refer to graphic):

<table>
  <tbody>
    <tr>
      <td>V:</td><td>power supply, 4.5 V - 13 V</td>
    </tr><tr>
      <td>serial:</td><td>Tx1, Rx1</td>
    </tr><tr>
      <td>OUT:</td><td>Tx2</td>
    </tr><tr>
      <td>bind:</td><td>button</td>
    </tr>
  </tbody>
</table>

Notes:
- To enter the system bootloader for flashing, hold the button down during power up.
- The USB-C port can be used for powering as well as for flashing (per DFU).
- The Rx2 pin has no function.


### As Tx Module ###

TODO


## Flashing ##

**Important: Every time that you power a board you should ensure that there is an antenna connected otherwise you risk damaging the RF section.**

### DFU via USB-C ###

- Download and install [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)
- Hold down the button while powering up
- Connect the device via USB-C to your PC
- Launch STM32CubeProgrammer and select USB as the connection method, click connect
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

