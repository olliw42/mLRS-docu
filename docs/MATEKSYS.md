# mLRS Documentation: MatekSys mLRS Tx Modules & Receivers #

([back to main page](../README.md))

The MatekSys mLRS Tx modules and receivers are specifically designed for mLRS and are the best options available. If you are new to mLRS, then it is highly recommended to start with this hardware.

They are available for the 2.4 GHz band and the 868/915 MHz band. 

Links to the MatekSys website are found below, which include product specifications, excellent instructions, and more information:

- [Product Page](https://www.mateksys.com/?page_id=12174)

> [!IMPORTANT]
> MatekSys mLRS gear in the 868/915 MHz band use the SX126x/STM32WLE RF chipset and are only compatible 
with SX126x/STM32WLE and LR1121 hardware; they are incompatible with SX127x hardware providing the '19 Hz 7x' mode (Frsky R9 system and ELRS 900 MHz gear)(see [here](SX126x_SX127x_INCOMPATIBILITY.md)).

## 2.4 GHz Hardware ##

- [mR24-30 Tx Module Kit](https://www.mateksys.com/?portfolio=mr24-30-tx)
- [mR24-30 Receiver](https://www.mateksys.com/?portfolio=mr24-30)

## 868 MHz  / 915 MHz Hardware ##

- [mR900-30 Tx Module Kit](https://www.mateksys.com/?portfolio=mr900-30-tx)
- [mR900-30 Receiver](https://www.mateksys.com/?portfolio=mr900-30)
- [mR900-22 Receiver](https://www.mateksys.com/?portfolio=mr900-22)

## Video Tutorial ##

[![mLRS Tx Setup & Overview | Mavlink Telemetry & RC Input for Develop Air & Other Arducopter Drones](https://img.youtube.com/vi/ej5qcmaGqNE/0.jpg)](https://www.youtube.com/watch?v=ej5qcmaGqNE "mLRS Tx Setup & Overview | Mavlink Telemetry & RC Input for Develop Air & Other Arducopter Drones")

## Flashing / Upgrading Firmware ##

The most convenient way of flashing the Matek mLRS devices is via their USB-C port and using the [mLRS Web Flasher](https://www.olliw.eu/mlrsflasher) app.

Plug in the USB-C cable while pressing the bind button. This puts the mLRS device into DFU mode (LEDs are not flashing). Then follow the instructions provided by the mLRS Web Flasher app.

## Tx Module, HC-04 Bluetooth Notes ##

To use the HC-04 Bluetooth module on Matek mLRS Tx modules, you need to set in the Tx module:

- ["Tx Ser Dest"](PARAMETERS.md#tx-ser-dest) = "serial"

You can do this via the [mLRS Lua script](LUA.md) on your radio or the [CLI](CLI.md).

Additional configuration of the HC-04 module should not be needed as mLRS will automatically configure all of the necessary settings on the module. However, if you are having problems you can check the following items:

- Ensure that the 3 dip switches are all in the 'ON' / left position when looking at the Tx module with the antenna pointing up.
    - <img src="images/Matek_HC04.png">
- If you are using Windows 11 and are unable to see the device being broadcasted, ensure that 'Advanced' is selected within the 'Bluetooth devices discovery' option that is located on the Bluetooth & devices pages.
    - <img src="images/Win11_BT.png">
