# mLRS Documentation: E77 Easy Solder Boards #

([back to main page](../README.md))

The E77 Easy Solder Boards are designed to be an allow one with minimal soldering skills to build their own mLRS hardware. All of the parts except for the E77 module are through-hole parts to aid in assembly.  These boards are flexible in that they can be used as a Tx module, Rx module or a SiK replacement. Additionally, these boards support diversity when paired with an additional E22 module.

<table>
  <tbody>
    <tr>
      <td>Frequency Bands</td>
      <td>868 MHz/915 MHz (E77-900M22S) or 433 MHz/70 cm (E77-400M22S)</td>
    </tr>
    <tr>
      <td>Max. RF Output Power</td>
      <td>22 dBm (158 mW)</td>
    </tr>
    <tr>
      <td>Supported Modes</td>
      <td>31 Hz, 19 Hz</td>
    </tr>
  </tbody>
</table>

### As Tx Module ###

Connections (name in respect to board print-ons, otherwise please refer to graphic):

- serial: Tx, Rx
- com/cli: Tx, Rx
- debug: STx
- JR pin 5: S
- button: cli / BIND

Notes:

- To enable the cli, hold down the button during boot

<img src="images/E77_Tx_Wiring.png" width="720">

### As Rx Module ###

Connections (name in respect to board print-ons, otherwise please refer to graphic):

- serial: Tx, Rx
- out: S
- debug: STx
- button: BIND

<img src="images/E77_Rx_Wiring.png" width="720">

## Flashing ##

**Important: Every time that you power a board you should ensure that there is an antenna connected otherwise you risk damaging the RF section.**

- Download and install [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)
- Connect your ST-Link to the 3V3, GND, SWD, and SWCLK pins on the board
    - Refer to the diagrams above
    - Some ST-Link boards provide power and some do not - ensure the board is powered
- Launch STM32CubeProgrammer and select ST-Link as the connection method, click connect
- From the menu on the left select the Download tile
- Select the correct firmware in the Download section, click Start Program
- Power cycle the board, the red LED should blink which indicates that the board is disconnected

Notes:

If you are unable to to flash due to readout protection, perform the following steps after connecting to the device:
- From the menu on the left select the OB (Option Bytes) tile
- From the Read Out Protection section, change to AA, select Apply
    - This will erase the current firmware