# mLRS Documentation: Setup as SiK Telemetry Replacement #

([back to main page](../README.md))

This page describes how to use mLRS as a bi-directional MAVLink telemetry link similar to a SiK telemetry unit. This setup doesn't require a radio and will only transmit and receive MAVLink data.

<img src="images/mLRS-docu-setup-sik-telemetry-01.jpg" width="800px">

## Setup

The configuration for this mode is similar to others, except that one can ignore the RC settings on both the mLRS Tx module and receiver, and the RC input and output pins on the devices are not used.

For this setup, the mLRS Tx module should be set to "Tx Ch Source = none". There is no specific configuration of the mLRS receiver neccessary. 

With the exception of "Tx Ch Source = none", the configuration can exactly follow the settings described in [CRSF Telemetry and Yaapu Telemetry App](CRSF.md). If you are using a separate RC system (e.g. ELRS, Crossfire, FrSky, etc.), the sub chapter [Setup ArduPilot: CRSF receiver](CRSF.md/#crsf-receiver) will need to be modified for the system you are using, otherwise it can be ignored.




