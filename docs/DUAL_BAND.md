# mLRS Documentation: Dual Band #

([back to main page](../README.md))

mLRS allows for a dual-band setup, where the Tx module and receiver both transmit and receive in the 2.4 GHz and 868/915 MHz (or 433 MHz/70 cm) bands simultaneously.

This operation mode is very simlar to a full-diversity setup, except that the hardware of course needs to provide two RF stages operating in the two different RF bands. An example is given by the dual-band version of the easy-to-solder boards, which can be eqipped with E77 modules working at 868/915 MHz and E28 modules working at 2.4 GHz. See [here]( https://github.com/olliw42/mLRS-hardware/tree/master/olliw-stm32-based/rx-tx-E77-E28-dualband-easysolder). The "normal" easy-to-solder boards can be eqipped with E77 modules working at 868/915 MHz and E22 modules working at 433 MHz, allowing to build a dual-band setup working in the 868/915 MHz and 433 MHz bands. This is possible also for a number of other DIY options which use a E22 module as second RF stage.

Similar to a full-diversity setup, dual band uses FHSS and the receiver will choose the packet on the best band. 

In contrast to a full-diversity setup, however, the dual-band setup transmits simultaneously on both RF bands. This means that even if one RF band is blocked, packets will not be missed.

## Configuration

Configuration is the same as a single band 868/915 MHz system.

## Demo Video

[![mLRS: Dual Band Demo](https://img.youtube.com/vi/ZhJaliL_N-M/0.jpg)](https://youtu.be/ZhJaliL_N-M "mLRS: Dual Band Demo")
