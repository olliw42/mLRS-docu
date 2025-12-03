# mLRS Documentation: ELRS Tx Modules (External and Internal) #

([back to main page](../README.md))

mLRS supports a number of external ELRS modules as well as the internal ELRS modules in a number of popular radios.

> [!IMPORTANT]
> 868/915 MHz ELRS Tx modules using the SX127x RF chipset are only compatible with ELRS 868/915 SX127x receivers, ELRS LR1121 receivers and Frsky R9 receivers using the 19 Hz 7x mode; they are incompatible with SX126x/STM32WLE hardware (MatekSys mR900, SeeedStudio Wio-E5, EBYTE E77 MBL, E77 Easy Solder)(see [here](SX126x_SX127x_INCOMPATIBILITY.md)).

> [!NOTE]
> mLRS only supports CRSF for 400k baudrate. For external Tx modules navigate to MODEL SETTINGS->MODEL SETUP->External RF and select Mode = CRSF and Baudrate = 400k; for internal Tx modules navigate to SYS->HARDWARE and select Type = CRSF and Baudrate = 400k.

## External Tx Modules ##

mLRS supports the following external ELRS modules:

| Module                   | Target                          | Frequency Band       | RF Chipset | Transmit Power   |
| ------------------------ | ------------------------------- | -------------------- | ---------- |----------------- |
| BetaFPV Micro 1W         | tx-betafpv-micro-1w-2400        | 2.4 GHz              | SX128x     | 30 dBm (1000 mW) |
| RadioMaster Bandit       | tx-radiomaster-bandit-900       | 868/915 MHz          | SX127x     | 30 dBm (1000 mW) |
| RadioMaster Bandit Micro | tx-radiomaster-bandit-micro-900 | 868/915 MHz          | SX127x     | 30 dBm (1000 mW) |
| RadioMaster Bandit Nano  | tx-radiomaster-bandit-micro-900 | 868/915 MHz          | SX127x     | 30 dBm (1000 mW) |
| RadioMaster Nomad        | tx-radiomaster-nomad            | 868/915 MHz, 2.4 GHz | LR1121     | 30 dBm (1000 mW) |
| RadioMaster Ranger       | tx-radiomaster-ranger-2400      | 2.4 GHz              | SX128x     | 30 dBm (1000 mW) |

### Flashing External Tx Modules ###

> [!IMPORTANT]
> The BetaFPV Micro 1W requires specific dip switch settings to flash and operate, these are detailed in the 
> [BetaFPV section](https://github.com/olliw42/mLRS-docu/blob/elrs-tx-modules-update/docs/ELRS_TX_MODULES.md#betafpv-micro-1w-dip-switch-settings).

Flashing external Tx modules is done using the mLRS Flasher Desktop App - this is found [here](https://github.com/olliw42/mLRS-Flasher).

Steps to flash:

1. Plug the module into the computer using USB
2. Launch the mLRS Flasher Desktop App
3. Select Tx Module (external) from the left menu
4. Select the Device Type, Firmware Version and Firmware File appropriate for your radio
5. Select the correct serial port
6. Click Flash Tx Module, wait for the flash to finish
7. Unplug the USB cable

### Flashing the Wireless Bridge on External Tx Modules ###

> [!IMPORTANT]
> To flash the Wireless Bridge, you will need the mLRS firmware installed - this is done by following the steps outlined above.

> [!NOTE]
> The mLRS wireless bridge uses the "backpack" ESP8285 chip available on these ELRS Tx modules.

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

## Internal Tx Modules ##

mLRS supports the internal ELRS modules on the following radios:

| Radio                                        | Target                             | Frequency Band       | RF Chipset | Transmit Power.     |
| -------------------------------------------- | ---------------------------------- | -------------------- | ---------- | ------------------- |
| Jumper<br>T20 V2, T15, T14, T-Pro S             | tx-jumper-internal-900             | 868/915 MHz          | SX127x     | 30 dBm<br>(1000 mW) |
| Jumper<br>T20 V1, T20 V2, T15, T14, T-Pro S     | tx-jumper-internal-2400            | 2.4 GHz              | SX128x     | 30 dBm<br>(1000 mW) |
| RadioMaster Boxer                            | tx-radiomaster-internal-boxer-2400 | 2.4 GHz              | SX128x     | 30 dBm<br>(1000 mW) |
| RadioMaster<br>Pocket, MT12, TX12, TX16S, Zorro | tx-radiomaster-internal-2400       | 2.4 GHz              | SX128x     | 24 dBm<br>(250 mW)  |
| RadioMaster TX15                             | tx-radiomaster-internal-tx15       | 868/915 MHz<br>2.4 GHz | LR1121     | 30 dBm<br>(1000 mW) |
| RadioMaster GX12                             | tx-radiomaster-internal-gx12       | 868/915 MHz<br>2.4 GHz | LR1121     | 30 dBm<br>(1000 mW) |

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

> [!NOTE]
> The mLRS wireless bridge uses the "backpack" ESP8285 chip available on these ELRS Tx modules.

1. Plug the radio into the computer using USB, select 'USB Serial (VCP)' from the menu
2. Launch the mLRS Flasher Desktop App
3. Select Tx Module (internal) from the left menu
4. Select the Device Type, Firmware Version and Firmware File appropriate for your radio
5. Click Flash Wireless Bridge, wait for the flash to finish
6. Unplug the USB cable
