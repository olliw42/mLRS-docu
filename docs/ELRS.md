# mLRS Documentation: ExpressLRS Devices #

([back to main page](../README.md))

In principle, any ELRS receiver which uses the ESP8285 chipset is supported. This page does not list all of them, but just some which are considered particularly useful for being used as mLRS receiver, e.g., because their transmit power is >= 100 mW. 

ELRS receivers using a EPS32 chipset or ELRS transmitter modules are currently not (yet) supported.

## Receivers ##

### SpeedyBee Nano 2.4G ExpressLRS ELRS Receiver
- https://www.speedybee.com/speedybee-nano-2-4g-expresslrs-elrs-receiver/
- 2.4 GHz, 100 mW
- ESP8285
- xtal: ??
- PA/LNA: Skyworks RFX2401C (tx gain 24 dB, max 22 dBm) ?

### Bayck 915M Nano Pro Receiver
- 868/915 MHz, 500 mW
- ESP8255
- xtal: TXCO ?
- PA/LNA: ??
- additional RF filter

### BetaFPV ELRS Nano Receiver
- https://betafpv.com/collections/expresslrs-series-accessories/products/elrs-nano-receiver
- 2.4 GHz, 100 mW or 868/915 MHz, 100 mW
- ESP8285
- xtal: ??
- PA/LNA: ??

### BetaFPV ELRS SuperD Diversity Receiver
- https://betafpv.com/collections/expresslrs-series-accessories/products/superd-elrs-2-4g-diversity-receiver
- 2.4 GHz, 2x 100 mW or 868/915 MHz, 2x 50 mW
- ESP32-PICO-D4
- xtal: TXCO shared by both RF chips
- PA/LNA: ??
- RGB Led
- NOT YET SUPPORTED

### MatekSys ExpressLRS/ELRS 2.4 GHz Receiver ELRS-R24-D
- https://www.mateksys.com/?portfolio=elrs-r24
- 2.4 GHz, 200 mW (22.5 dBm)
- ESP8285
- xtal: ??
- PA/LNA: Skyworks SE2431L (tx gain 23 dB, max 24 dBm)
- RF switch: ??
- antenna diversity (default antenna = 2)

### RadioMaster RP4TD ExpressLRS 2.4GHz True Diversity Receiver 
- https://www.radiomasterrc.com/collections/rp-series-receivers/products/rp4td-expresslrs-2-4ghz-diversity-receiver
- 2.4 GHz, 2x 100 mW 
- ESP32 ?
- xtal: dual TCXO
- PA/LNA: ??
- RGB Led
- NOT YET SUPPORTED

## Transmitter Modules ##



