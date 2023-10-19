# mLRS Documentation: Dual Band #

([back to main page](../README.md))

**Important: Dual band functionality is experimental and currently only available in the branch 'dev-dualband2'. Firmware binaries need to be compiled manually for the specific hardware.**

mLRS allows for a dual-band setup, where the Tx module and receiver both transmit and receive in the 2.4 GHz and 868/915 MHz bands (also the combination 2.4 GHz and 433 MHz/70 cm is possible). 

This operation mode is very simlar to a full-diversity setup, except that the hardware of course needs to provide two RF chains operating in the two different RF bands. An example is given by the dual-band version of the easy-to-solder boards, which can be eqipped with E77 modules working at 868/915 MHz and E28 modules working at 2.4 GHz. See [here]( https://github.com/olliw42/mLRS-hardware/tree/master/olliw-stm32-based/rx-tx-E77-E28-dualband-easysolder). Like full diversity, dual band also uses FHSS, and receiving depends on which packet in which band is best according to a full-diversity principle.

In contrast to full diversity however, in the dual-band setup the modules are each transmitting simultaneously in the two RF bands. Therefore no packets are missed when one frequency band is blocked. 

## Configuration

Configuration is equal to a single band 868/915 MHz (or 433 MHz/70 cm) system.

## Demo Video

[![mLRS: Dual Band Demo](https://img.youtube.com/vi/ZhJaliL_N-M/0.jpg)](https://youtu.be/ZhJaliL_N-M "mLRS: Dual Band Demo")
