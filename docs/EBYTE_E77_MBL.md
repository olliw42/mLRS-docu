# mLRS Documentation: EBYTE E77 MBL Boards #

([back to main page](../README.md))

EBYTE E77 MBL Boards are an option for building mLRS equipment. These boards use the EBYTE E77 module and are available in both 868/915 MHz and 433 MHz/70 cm versions. However, these boards are not perfect since their pins are not ready-made for the purposes of mLRS. So, some tweaking and (easy) soldering is required.

## EBYTE E77 MBL Boards ##

- [E77-400MBL-01](https://www.cdebyte.com/products/E77-400MBL-01)
- [E77-900MBL-01](https://www.cdebyte.com/products/E77-900MBL-01)

### As Tx Module ###

Connections (name in respect to board print-ons, otherwise please refer to graphic):

- serial: TxD,RxD and on-board USB plug
- com/cli: TxD,RxD and on-board USB plug
- debug: PA5
- button1: BOOT
- button2: cli / BIND

Notes:

- To communicate with the radio via the JR bay (pin 5 in the JR bay), you need to solder a Schottky diode (e.g. BAT42) between pads PB7 and PB6 (see graphic)
- To enable the cli, hold down button2 during boot
- To enter system bootloader, hold down button1 during boot

<img src="images/mLRS-EByte-E77-MBLKit-Tx.jpg" width="900px">

### As Rx Module ###

Connections (name in respect to board print-ons, otherwise please refer to graphic):

- serial: TxD,RxD and on-board USB plug
- out: PB6
- debug: PA5
- button1: BOOT
- button2: BIND

Notes:

- To enter system bootloader, hold down button1 during boot

<img src="images/mLRS-EByte-E77-MBLKit-Rx.jpg" width="900px">