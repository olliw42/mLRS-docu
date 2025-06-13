# mLRS Documentation: Flashing / Upgrading Firmware #

([back to main page](../README.md))

Depending on the device, a confusing number of methods can exist for flashing and upgrading the firmware. Here is provided a general overview of some of the methods.

> [!TIP]
> Flashing for a specific device is described in more depth on the hardware specific pages, please check those out for step by step instructions.

> [!IMPORTANT]
> Firmware with version numbers which end in a odd number (like v1.3.05) are developer versions (dev versions in slang). You should ***not*** use them unless you understand clearly what this implies. Firmware versions which end in an even number are safe to use (like v1.3.00 or v1.3.04).

## mLRS Web Flasher

The easiest way to flash firmware can be the [mLRS Web Flasher](https://mlrs.xyz/flash). 

***Notes***:
- Only few devices are supported currently (currently only DFU mode is supported, which covers the MatekSys mLRS devices).
- It does not run on all browsers (specifically not on Firefox).

## mLRS-Flasher Desktop App

The [mLRS-Flasher](https://github.com/olliw42/mLRS-Flasher) desktop app also makes it easy to flash firmware but requires installation of the app on your computer. 

It provides support for substantially more mLRS devices, and can run on Win, MacOS, and Linux systems. If the mLRS Web Flasher is not suitable for you, mLRS-Flasher might be the go-to tool.  

## STM32CubeProgrammer

The STM32CubeProgrammer is the go-to tool for flashing STM32 devices. Any STM32 based mLRS device can be flashed by at least one of the three protocols, UART, DFU mode via USB, or STLink via SWD.

***Note***: Sometimes one can find the "ST-LINK Utility" software being suggested. This software is totally outdated, and fully replaced by STM32CubeProgrammer. Please use STM32CubeProgrammer.

The STM32CubeProgrammer can be downloded from ST's website: https://www.st.com/en/development-tools/stm32cubeprog.html. If you have installed the STM32CubeIDE for building/compiling the firmware yourself, it is usually included already.

## STLink Programmer

In many cases a STLink programmer is needed for flashing STM32 devices. It might be tempting to buy one of the cheap STLink/V2 clones, but these may cause issues or may not even work. The [STLINK-V3MINIE](https://www.st.com/en/development-tools/stlink-v3minie.html) is a genuine inexpensive STLink/V3 programmer from STMicroelectronics, which can be recommended.
