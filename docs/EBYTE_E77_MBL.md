# mLRS Documentation: EBYTE E77 MBL Boards #

([back to main page](../README.md))

EBYTE E77 MBL Boards are an option for building mLRS equipment. These boards use the EBYTE E77 module and are available in both 868/915 MHz and 433 MHz/70 cm versions. However, these boards are not perfect since their pins are not ready-made for the purposes of mLRS. So, some tweaking and (easy) soldering is required.

**Important: If you are planning to use the SMA connector for the antenna, ensure that a 0 Ohm resistor is populated. Multiple users have reported that it is not present on their modules. Refer to the red square next to the SMA connector in the diagrams below for the location.**

<table>
  <tbody>
    <tr>
      <td>Frequency Bands</td>
      <td>868 MHz/915 MHz (E77-900MBL-01) or 433 MHz/70 cm (E77-400MBL-01)</td>
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
      <td>9.35 grams without antenna</td>
    </tr>
  </tbody>
</table>

Note: EByte silently changed the hardware of the E77 module around the beginning of 2024. These newer modules use a (better) TCXO, whereas the older modules use a ceramic crystal oscillator. According to the datasheet, newer modules can be identified by serial number SN &#8805; 3202995. The new and old modules require different firmware. The old modules will need firmware with the label "-xtal" in the name. Also, some reports suggest that one needs to use NRST (reset) for flashing via SWD.

## EBYTE E77 MBL Boards ##

- [E77-400MBL-01](https://www.cdebyte.com/products/E77-400MBL-01)
- [E77-900MBL-01](https://www.cdebyte.com/products/E77-900MBL-01)

### As Tx Module ###

Connections (name in respect to board print-ons, otherwise please refer to graphic):

- serial: TxD,RxD and on-board USB plug
- com/cli: TxD,RxD and on-board USB plug
- JRPin5/in: PB7
- button1: boot
- button2: bind / cli
- debug: PA5

Notes:

- To enable the cli, hold down button2 during boot
- To enter system bootloader, hold down button1 during boot

<img src="images/mLRS-EByte-E77-MBLKit-Tx.jpg" width="900px">

*The Schottky diode between the PB6 and PB7 pins is not needed with the default firmware. If you are having communication issues between the radio and the Tx module then you can install the Schottky diode and use the 'sdiode' firmware ('sdiode' will be included in the file name, e.g. tx-E77-MBLKit-wle5cc-400-**sdiode**-vX.X.XX.hex).  

### As Rx Module ###

Connections (name in respect to board print-ons, otherwise please refer to graphic):

- serial: TxD,RxD and on-board USB plug
- out: PB6
- button1: boot
- button2: bind
- debug: PA5

Notes:

- To enter system bootloader, hold down button1 during boot

<img src="images/mLRS-EByte-E77-MBLKit-Rx.jpg" width="900px">

## Flashing the Modules ##

**Important: Every time that you power a board you should ensure that there is an antenna connected otherwise you risk damaging the RF section.**

### Initial Flashing ###

The first time that you flash the mLRS firmware to an E77 MBL board you'll have to do the following:

- Download and install [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)
- Connect your ST-Link to the 3V3, GND, SWD, and SWCLK pins on the board
    - Refer to the diagrams above
    - Some ST-Link boards provide power and some do not - ensure the E77 MBL board is powered
- Launch STM32CubeProgrammer and select ST-Link as the connection method, click connect
- From the menu on the left select the Download tile
- Select the correct firmware in the Download section, click Start Program
- Power cycle the board, the red LED should blink which indicates that the board is disconnected

Notes:

If you are unable to to flash due to readout protection, perform the following steps after connecting to the device:
- From the menu on the left select the OB (Option Bytes) tile
- From the Read Out Protection section, change to AA, select Apply
    - This will erase the current firmware

### Subsequent Flashing ###

Subsequent flashing can be done in two ways:
1. Follow the initial flashing process
2. Boot into the system bootloader using the boot button, cli, lua or the OLED display
    - This enables programming over the USB port which is connected to UART2 (PA2, PA3)
    - Alternatively, use UART1 (PA9, PA10) with a USB-TTL adapter and the Serial connection option in STM32CubeProgrammer