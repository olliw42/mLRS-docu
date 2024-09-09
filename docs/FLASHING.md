# mLRS Documentation: Flashing / Upgrading Firmware #

([back to main page](../README.md))

Depending on the device, a confusing number of options can exist for flashing and upgrading the firmware.

## mLRS Web Flasher

The easiest way to flash can be the [mLRS Web Flasher](https://mlrs.xyz/flash). Only few devices are supported currently however (currently only DFU mode is supported, which covers the MatekSys mLRS devices).

## STM32CubeProgrammer

The STM32CubeProgrammer is the goto tool for flashing STM32 devices. Any STM32 based mLRS device can be flashed by at least one of the three protocols, UART, DFU mode via USB, or STLink via SWD.

Note: Sometimes one can find the "ST-LINK Utility" software being suggested. This software is totally outdated, and replaced by STM32CubeProgrammer.

The STM32CubeProgrammer can be downloded from the ST website: https://www.st.com/en/development-tools/stm32cubeprog.html. If you have installed the STM32CubeIDE for building/compiling the firmware yourself, it is usually included already.

