# mLRS Documentation: ELRS Tx Modules (External and Internal) #

([back to main page](../README.md))

> [!IMPORTANT]
> 868/915 MHz ELRS Tx modules are only compatible with ELRS 868/915 and Frsky R9 receivers; they are incompatible with SX126x/STM32WLE hardware (MatekSys mR900, SeeedStudio Wio-E5, EBYTE E77 MBL, E77 Easy Solder)(see [here](SX126x_SX127x_INCOMPATIBILITY.md)).

> [!NOTE]
> mLRS only supports 400k baudrate, for external Tx modules navigate to MODEL SETTINGS->MODEL SETUP->External RF and select Mode = CRSF and Baudrate = 400k; for internal Tx modules navigate to SYS->HARDWARE and select Type = CRSF and Baudrate = 400k.

## External Modules ##

mLRS supports the following ELRS external modules:

| Module                   | Target                          | Frequency Band | Transmit Power   |
| ------------------------ | ------------------------------- | -------------- | ---------------- |
| BetaFPV Micro 1W         | tx-betafpv-micro-1w-2400        | 2.4 GHz        | 30 dBm (1000 mW) |
| RadioMaster Bandit       | tx-radiomaster-bandit-900       | 868/915 MHz    | 30 dBm (1000 mW) |
| RadioMaster Bandit Micro | tx-radiomaster-bandit-micro-900 | 868/915 MHz    | 30 dBm (1000 mW) |

### Flashing External Modules ###

> [!IMPORTANT]
> The BetaFPV Micro 1W requires specific dip switch settings to flash and operate, these are detailed in the 
> [BetaFPV section](https://github.com/olliw42/mLRS-docu/blob/elrs-tx-modules-update/docs/ELRS_TX_MODULES.md#betafpv-micro-1w-dip-switch-settings).

Flashing external modules is done using the mLRS Flasher Desktop App - this is found [here](https://github.com/olliw42/mLRS-Flasher).

Steps to flash:

1. Plug the module into the computer using USB
2. Launch the mLRS Flasher Desktop App
3. Select Tx Module (external) from the left menu
4. Select the Device Type, Firmware Version and Firmware File appropriate for your radio
5. Select the correct serial port
6. Click Flash Tx Module, wait for the flash to finish
7. Unplug the USB cable

### Flashing the Wireless Bridge on External Modules ###

> [!IMPORTANT]
> To flash the Wireless Bridge, you will need the mLRS firmware installed - this is done by following the steps outlined above.

1. Plug the module into the computer using USB
2. Launch the mLRS Flasher Desktop App
3. Select Tx Module (external) from the left menu
4. Select the Device Type, Firmware Version and Firmware File appropriate for your radio
5. Follow the instructions under 'Wireless Bridge' to allow flashing
6. Click Flash Wireless Bridge, wait for the flash to finish
7. Unplug the USB cable

### BetaFPV Micro 1W Dip Switch Settings ###

The BetaFPV Micro 1W has 7 dip switches which need to be set correctly depending on the operation mode, refer to the following table:

| Operation Mode                     | Dip Switches On | Dip Switches Off |
| ---------------------------------- | --------------- | ---------------- |
| Flash module or use USB for serial | 1,2             | 3,4,5,6,7        |
| Flash Wireless Bridge              | 5,6,7           | 1,2,3,4          |
| Use Wireless Bridge for serial     | 3,4             | 1,2,5,6,7        |

## Internal Modules ##

mLRS supports the ELRS internal modules on the following radios:

| Radio                                        | Target                             | Frequency Band | Transmit Power   |
| -------------------------------------------- | ---------------------------------- | -------------- | ---------------- |
| Jumper T20 V2, T15, T14, T-Pro S             | tx-jumper-internal-900             | 868/915 MHz    | 30 dBm (1000 mW) |
| Jumper T20 V1, T20 V2, T15, T14, T-Pro S     | tx-jumper-internal-2400            | 2.4 GHz        | 30 dBm (1000 mW) |
| RadioMaster Boxer                            | tx-radiomaster-internal-boxer-2400 | 2.4 GHz        | 30 dBm (1000 mW) |
| RadioMaster Pocket, MT12, TX12, TX16S, Zorro | tx-radiomaster-internal-2400       | 2.4 GHz        | 24 dBm (250 mW)  |

### Flashing Internal Modules ###

Flashing internal modules is done using the mLRS Flasher Desktop App - this is found [here](https://github.com/olliw42/mLRS-Flasher).

Steps to flash:

1. Power the radio on
2. Plug the radio into the computer using USB, select 'USB Serial (VCP)' from the menu
3. Launch the mLRS Flasher Desktop App
4. Select Tx Module (internal) from the left menu
5. Select the Device Type, Firmware Version and Firmware File appropriate for your radio
6. Click Flash Tx Module, wait for the flash to finish
7. Unplug the USB cable

### Flashing the Wireless Bridge on Internal Modules ###

> [!IMPORTANT]
> To flash the Wireless Bridge, you will need the mLRS firmware installed - this is done by following the steps outlined above.

1. Plug the radio into the computer using USB, select 'USB Serial (VCP)' from the menu
2. Launch the mLRS Flasher Desktop App
3. Select Tx Module (internal) from the left menu
4. Select the Device Type, Firmware Version and Firmware File appropriate for your radio
5. Click Flash Wireless Bridge, wait for the flash to finish
6. Unplug the USB cable