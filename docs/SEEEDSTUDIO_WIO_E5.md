# mLRS Documentation: SeeedStudio Wio-E5 Boards #

([back to main page](../README.md))

The SeeedStudio [Wio-E5 module](https://wiki.seeedstudio.com/LoRa-E5_STM32WLE5JC_Module) is a highly attractive module for building mLRS equipment. SeeedStudio provides a number of boards which are based on this module, and which are quite interesting hardware for mLRS. However, these boards are not perfect since their pins are not ready-made for the purposes of mLRS. So, some tweaking and (easy) soldering is required.


## SeeedStudio Wio-E5 mini dev Board ##

https://wiki.seeedstudio.com/LoRa_E5_mini/

This board is well suited for building a Tx mLRS module, and - if the somewhat larger weight and size is no concern - also for building a Rx module.

### As Tx Module ###

Connections (name in respect to board print-ons):

- serial: Tx2,Rx2
- in: Rx1
- com/cli: Tx,Rx and on-board USB plug
- debug: A3
- led green: SDA (solder a green LED with resistor > 300 Ohm to GND, you can use pad SCL as intermediate post)
- led red: on-board
- button: on-board (BOOT button)

If you want to communicate with the radio via the JR bay (pin 5 in the JR bay), then you in addition need to do:

- solder a Schottky diode (e.g. BAT42) between pads RX1 and TX1 (RX1 - |<| - TX1, |<| represents the diode)
- use firmware with DEVICE_HAS_JRPIN5 enabled (this is the default)

Example Wiring using JR bay with CRSF:

<img src="images/E5_Mini_Tx_Wiring.png" width="800px">

### As Rx Module ###

Connections (name in respect to board print-ons):

- serial: Tx2,Rx2
- out: Tx1
- debug: Tx, and on-board USB plug
- led green: SDA (solder a green LED with resistor > 300 Ohm to GND, you can use pad SCL as intermediate post)
- led red: on-board
- button: on-board (BOOT button)

Example Wiring:

<img src="images/E5_Mini_Rx_Wiring.png" width="800px">

## SeeedStudio Grove Wio-E5 Board ##

https://wiki.seeedstudio.com/Grove_LoRa_E5_New_Version/

### As Tx Module ###

not recommended

### As Rx Module ###

Connections (name in respect to board print-ons):

- serial: Tx,Rx on connector, and solder pads on bottom
- out: none
- debug: none
- led green: none
- led red: on-board (solder jumper on the bottom of the board needs to be closed)
- button: BOOT solder pad (solder a button between the BOOT pad and GND)

Note: There is no convenient way to connect a green LED, and you thus won't get the information conveyed by it (like connection). It is possible to work around this but it would require some more sophisticated solder work.

Example Wiring:

<img src="images/E5_Grove_Rx_Wiring.png" width="800px">
