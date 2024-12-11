# mLRS Documentation: ELRS Tx Modules #

([back to main page](../README.md))

mLRS supports a few ELRS Tx modules, but only for SiK telemetry use. 

> [!IMPORTANT]
> Only for SiK telemetry use means that RC control is not supported, neither via the JR bay nor via an IN port. This also means that the mLRS Lua script cannot be used, nor can the Yaapu app.

> [!IMPORTANT]
> 868/915 MHz ELRS Tx modules are only compatible with ELRS 868/915 and Frsky R9 receivers; they are incompatible with SX126x/STM32WLE hardware (MatekSys mR900, SeeedStudio Wio-E5, EBYTE E77 MBL, E77 Easy Solder)(see [here](SX126x_SX127x_INCOMPATIBILITY.md)).

The Tx modules below allow for convenient configuration through the OLED.

## BetaFPV 1W Micro Tx Module (2.4 GHz) ##

TBD

## RadioMaster Micro Bandit (868/915 MHz) ##

TBD

## RadioMaster Bandit (868/915 MHz) ##

TBD

## Flashing ##

- Download the firmware for your Tx module.
    - The latest official release or latest pre-release is found [here](https://github.com/olliw42/mLRS/releases).
    - The latest dev release is found [here](https://github.com/olliw42/mLRS/tree/main/firmware/pre-release-esp).
