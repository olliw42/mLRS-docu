# mLRS Documentation: FlySky FRM303 Transmitter Module #

([back to main page](../README.md))

The FlySky FRM303 transmitter module is a nearly perfect option for building mLRS equipment in the 2.4 GHz frequency range. Its main drawback is its price. It also has a small MCU which limits the available mLRS features. However, no hardware tweaking is required (although mods like the OLED mod are possible).

<table>
  <tbody>
    <tr>
      <td>Frequency Band</td>
      <td>2.4 GHz</td>
    </tr>
    <tr>
      <td>Max. RF Output Power</td>
      <td>30 dBm (1 W). The hardware should be capable of 33 dBm (2 W) but current mLRS firmware does not provide this option.</td>
    </tr>
    <tr>
      <td>Supported Modes</td>
      <td>50 Hz, 31 Hz, 19 Hz</td>
    </tr>
    <tr>
      <td>Weight</td>
      <td>65 grams without antenna</td>
    </tr>
  </tbody>
</table>

**Important: Never power up without an antenna connected! Otherwise you risk damaging the RF section.**

- [Product Page](https://www.flysky-cn.com/frm303description)

## As Tx Module ##

The description is for the default firmware version ('USB' version, indicated by a '-usb' label in the firmware file name).

The FRM303 provides two connectors, a 5-pin JST-GH connector at the bottom edge and a USB-C connector at top edge. In addition there is a 5-way button. Their usage is as follows:

JST-GH connector (from left to right when viewed from top):

- serial Rx
- serial Tx
- VCC
- GND
- in port

USB-C connector:

- com/cli port

5-way button:

- bind button (to enter bind mode, hold the button in the down direction for ca 4 seconds)

Notes:

- To enter the system bootloader for flashing, hold the button in the down direction during power up (or use the CLI, Lua script, or OLED if available)

## As Receiver ##

JST-GH connector (from left to right when viewed from top):

- serial Rx
- serial Tx
- VCC
- GND
- out port

USB-C connector:

- no function (except for firmware upgrade)

5-way button:

- bind button (to enter bind mode, hold the button in the down direction for ca 4 seconds)

Notes:

- To enter the system bootloader for flashing, hold the button in the down direction during power up
- The flight controller may not provide enough power for the FRM303 to run properly, choose a proper power source

## Flashing ##

### Initial Flashing ###

The first time that you flash the mLRS firmware to a FRM303 module you'll have to do the following:

- Download and install [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html)
- Connect your ST-Link programmer to the 3V3, GND, SWD, and SWCLK pins on the board
    - You need to remove the bottom part of the case to gain access to these pins
    - Some ST-Link programmer boards provide power and some do not - ensure the FRM303 is powered
- Launch STM32CubeProgrammer and select ST-Link as the connection method, click connect
- From the menu on the left select the Erase & Programming tile
- Click 'Full chip erase'
- From the menu on the left select the Download tile
- Select the correct firmware in the Download section, click Start Program
- Power cycle the board, the LEDs should start blinking

Note: If you are unable to to flash due to readout protection, perform the following steps after connecting to the device:
- From the menu on the left select the OB (Option Bytes) tile
- From the Read Out Protection section, change to AA, select Apply
    - This will erase the current firmware

### Subsequent Flashing ###

Subsequent flashing can be done in two ways:
1. Follow the initial flashing process using the ST-Link programmer
2. Boot into the system bootloader using the boot button, CLI, Lua script or the OLED display if available
    - This enables programming over the USB-C port using the DFU method
    - Launch STM32CubeProgrammer and select USB as the connection method, click connect 
    - Proceed as usual
   