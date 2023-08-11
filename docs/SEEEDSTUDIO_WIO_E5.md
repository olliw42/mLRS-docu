# mLRS Documentation: SeeedStudio Wio-E5 Boards #

([back to main page](../README.md))

The SeeedStudio [Wio-E5 module](https://wiki.seeedstudio.com/LoRa-E5_STM32WLE5JC_Module) is a highly attractive module for building mLRS equipment. SeeedStudio provides a number of boards which are based on this module, and which are quite interesting hardware for mLRS. However, these boards are not perfect since their pins are not ready-made for the purposes of mLRS. So, some tweaking and (easy) soldering is required.

<table>
  <tbody>
    <tr>
      <td>Frequency Bands</td>
      <td>868 MHz/915 MHz</td>
    </tr>
    <tr>
      <td>Max. RF Output Power</td>
      <td>22 dBm (158 mW)</td>
    </tr>
    <tr>
      <td>Supported Modes</td>
      <td>31 Hz, 19 Hz</td>
    </tr>
    <tr>
      <td>Weight</td>
      <td>Wio-E5 Mini: ~7 grams without antenna</td>
    </tr>
  </tbody>
</table>

## SeeedStudio Wio-E5 Mini dev Board ##

- [Product Page](https://wiki.seeedstudio.com/LoRa_E5_mini/)
- [3D Model](https://www.thingiverse.com/thing:6108814)

This board is well suited for building a Tx mLRS module, and - if the somewhat larger weight and size is no concern - also for building a receiver.

### As Tx Module ###

Connections (name in respect to board print-ons):

- serial: Tx2,Rx2
- in: Rx1
- com/cli: Tx,Rx and on-board USB plug
- debug: A3
- led green: SDA (solder a green LED with resistor > 300 Ohm to GND, you can use pad SCL as intermediate post)
- led red: on-board
- bind button: BOOT button, hold for 4 seconds to initiate bind mode

Example Wiring using JR bay with CRSF:

<img src="images/E5_Mini_Tx_Wiring.png" width="600px">

*The Schottky diode between the TX1 and RX1 pins is not normally needed and this configuration uses the default firmware (labeled tx-Wio-E5-Mini-wle5jc-vX.X.XX.hex).  If you are having communication issues between the radio and the module then you can install the Schottky diode and use the sdiode firmware (labeled tx-Wio-E5-Mini-wle5jc-sdiode-vX.X.XX.hex).  

### As Receiver ###

Connections (name in respect to board print-ons):

- serial: Tx2,Rx2
- out: Tx1
- debug: Tx, and on-board USB plug
- led green: SDA (solder a green LED with resistor > 300 Ohm to GND, you can use pad SCL as intermediate post)
- led red: on-board
- bind button: BOOT button, hold for 4 seconds to initiate bind mode

Example Wiring:

<img src="images/E5_Mini_Rx_Wiring.png" width="800px">

## SeeedStudio Grove Wio-E5 Board ##

- [Product Page](https://wiki.seeedstudio.com/Grove_LoRa_E5_New_Version/)
- [Printable Cases](https://www.printables.com/model/535202-wio-e5-grove-case)

### As Tx Module ###

not recommended

### As Receiver ###

Connections (name in respect to board print-ons):

- serial: Tx,Rx on connector, and solder pads on bottom
- out: none
- debug: none
- led green: none
- led red: on-board (solder jumper on the bottom of the board needs to be closed)
- bind button: BOOT solder pad (solder a button between the BOOT pad and GND or a wire between the two to ground out the BOOT pad, hold for 4 seconds to initiate bind mode)

Note: There is no convenient way to connect a green LED, and you thus won't get the information conveyed by it (like connection). It is possible to work around this but it would require some more sophisticated solder work.

Example Wiring:

<img src="images/E5_Grove_Rx_Wiring.png" width="800px">

## Flashing the Modules ##

**Important: Every time that you power a board you should ensure that there is an antenna connected otherwise you risk damaging the RF section.**

### Initial Flashing ###

The first time that you flash the mLRS firmware to either the Wio-E5 Mini or Wio-E5 Grove you'll have to do the following:

- Download and install [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)
- Connect your ST-Link programmer to the 3V3, GND, SWD, and SWCLK pins on the board
    - The SWD and SWCLK pins are labeled 'DIO' and 'CLK' respectively
    - Some ST-Link programmers provide power and some do not - ensure the Wio-E5 is powered
- Hold down the boot button and then press the reset button, boot button can then be released.
- Launch STM32CubeProgrammer and select ST-Link as the connection method, click connect
- From the menu on the left select the OB (Option Bytes) tile
- From the Read Out Protection section, change to AA, select Apply
    - This will erase the factory firmware
- From the menu on the left select the Download tile
- Select the correct firmware in the Download section, click Start Program
- Power cycle the board, the red LED should blink which indicates that the board is disconnected

### Subsequent Flashing ###

Subsequent flashing can be done in two ways:
1. Follow the initial flashing process using the ST-Link programmer
    - There is no need to change the read out protection after the initial flash
    - If a full erase is desired, go to the Erase & Programming page and click 'Full chip erase'
2. Boot into the system bootloader using the CLI, Lua script or the OLED display
    - This enables programming over UART1 (pins PA9, PA10, labeled 'D9' and 'MOSI') or UART2 (pins PA2, PA3, labeled 'Tx2' and 'Rx2') with a USB-TTL adapter using the Serial connection option in STM32CubeProgrammer. The on-board USB connector cannot be used.
