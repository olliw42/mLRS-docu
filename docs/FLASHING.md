# mLRS Documentation: Flashing / Upgrading Firmware #

([back to main page](../README.md))

Depending on the device, a confusing number of methods can exist for flashing and upgrading the firmware. Here is provided a general overview of some of the methods.

***Note***: Flashing for a specific device is described in more depth on the hardware specific pages, please check those out for step by step instructions.

## mLRS Web Flasher

The easiest way to flash firmware can be the [mLRS Web Flasher](https://mlrs.xyz/flash). 

***Notes***:
- Only few devices are supported currently (currently only DFU mode is supported, which covers the MatekSys mLRS devices).
- It does not run on all browsers (specifically not on Firefox).

## STM32CubeProgrammer

The STM32CubeProgrammer is the go-to tool for flashing STM32 devices. Any STM32 based mLRS device can be flashed by at least one of the three protocols, UART, DFU mode via USB, or STLink via SWD.

***Note***: Sometimes one can find the "ST-LINK Utility" software being suggested. This software is totally outdated, and fully replaced by STM32CubeProgrammer. Please use STM32CubeProgrammer.

The STM32CubeProgrammer can be downloded from ST's website: https://www.st.com/en/development-tools/stm32cubeprog.html. If you have installed the STM32CubeIDE for building/compiling the firmware yourself, it is usually included already.

