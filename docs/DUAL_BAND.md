# mLRS Documentation: Dual Band #

([back to main page](../README.md))

mLRS allows for a dual-band setup, where the Tx module and receiver both transmit and receive in the 2.4 GHz and 868/915 MHz (or 433 MHz/70 cm) bands simultaneously.

Operation is similar to a full-diversity setup, except that the hardware uses two RF stages operating in the two different RF bands. Two examples are provided:
- To use 868/915 MHz and 2.4 GHz simultaneously there is a dual-band version of the E77 Easy-Solder board, which has an E77 module working at 868/915 MHz and an E28 module working at 2.4 GHz. More details can be found [here](https://github.com/olliw42/mLRS-hardware/tree/master/olliw-stm32-based/rx-tx-E77-E28-dualband-easysolder).
- To use 868/915 MHz and 433 MHz simultaneously one can use the "normal" E77 Easy-Solder board, when equipped with an E77 module working at 868/915 MHz and an E22 module working at 433 MHz.

Same as a full-diversity setup, dual band uses FHSS and the receiver will select the packet on the best band.

In contrast to a full-diversity setup, however, the dual-band setup transmits simultaneously on both RF bands. This means that even if there is strong interference on one RF band then packets will continue to be received on the other band.

## Configuration

Configuration is the same as a single band 868/915 MHz system.

## Demo Video

[![mLRS: Dual Band Demo](https://img.youtube.com/vi/ZhJaliL_N-M/0.jpg)](https://youtu.be/ZhJaliL_N-M "mLRS: Dual Band Demo")
