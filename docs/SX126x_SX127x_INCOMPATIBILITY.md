# mLRS Documentation: SX126x and SX127x Incompatibility #

([back to main page](../README.md))

mLRS hardware using the sx126x and sx127x LoRa chipsets are not compatible with each other, and cannot be operated together (they don't bind).

This is for two reasons:
- the SF6 spreading factor, which is used by mLRS for the 19 Hz mode, is incompatible for the sx126x and sx127x chipsets. 
- the SX127x does not support the SF5 spreading factor which is used for the mLRS 31 Hz mode.

This is the relevant part in the datasheet of the sx126x chip set:

<img src="images/SX126x_SF6_incompatibility.png" width="900px">
