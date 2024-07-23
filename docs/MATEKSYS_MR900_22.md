# mLRS Documentation: MatekSys mR900-22 #

([back to main page](../README.md))
([back to MatekSys page](MATEKSYS.md))

The MatekSys mLRS receivers and Tx modules are specifically designed for mLRS, and are currently simply the best options available. 

This page describes the MatekSys mR900-22 device for the 868/915 MHz band.

<table>
  <tbody>
    <tr>
      <td>Frequency Band</td>
      <td>868 MHz/915 MHz</td>
    </tr>
    <tr>
      <td>Max. RF Output Power</td>
      <td>+22 dBm (158 mW)</td>
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



## mR900-22 Receiver ##

- [Product Page](https://www.mateksys.com/?page_id=12174)

Connections (name in respect to board print-ons, otherwise please refer to graphic):

<table>
  <tbody>
    <tr>
      <td>V</td><td>power supply, 4 - 9 V</td>
    </tr><tr>
      <td>G</td><td>ground</td>
    </tr><tr>
      <td>Tx2, Rx2</td><td>serial, also for firmware flashing</td>
    </tr><tr>
      <td>Tx1</td><td>OUT (CRSF, SBus, SBus inv.)</td>
    </tr><tr>
      <td>BIND button</td><td>bind</td>
    </tr><tr>
      <td>Boot button</td><td>system bootloader</td>
    </tr>
  </tbody>
</table>


Notes:
- To enter bind mode, press the bind button for ca 4 sec. Alternatively, power up the device quickly 4 times.</td>
- To enter the system bootloader for firmware upgrade, hold the boot button down during power up (not bind button!).
- The Rx1 pin has no function.


## Flashing ##

**Important: Every time that you power a board you should ensure that there is an antenna connected otherwise you risk damaging the RF section.**

### Uart via Tx2, Rx2 Pins ###

- Download and install [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)
- Hold down the boot button while powering up
- Connect the device via a USB-TTL adapter, wired to the Tx2, Rx2 pins, to your PC
- Launch STM32CubeProgrammer and select UART as the connection method, select the correct COM port, click connect
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

