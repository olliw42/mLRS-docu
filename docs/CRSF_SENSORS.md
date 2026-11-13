# mLRS Documentation: CRSF Sensors #

([back to main page](../README.md))

([back to CRSF page](CRSF.md))

mLRS provides the following telemetry sensors when using CRSF:

Num | Datapoint   | Description                                                             | Data Source |
--- | ----------- | ----------------------------------------------------------------------- | ----------- |
1   | 1RSS        | Receiver RSSI                                                           | mLRS        |
2   | 2RSS        | not supported (repurposed to show MAVLink link quality)                 |             |
3   | RQly        | Receiver link quality                                                   | mLRS        |
4   | RSNR        | not supported (shows -1 dB)                                             |             |
5   | ANT         | Active receiver antenna                                                 | mLRS        |
6   | RFMD        | Receiver update rate (19, 31, 1 - 50Hz)                                 | mLRS        |
7   | TPWR*       | Transmitter power (CRSF power level in mW)                              | mLRS        |
8   | TRSS        | Transmitter RSSI                                                        | mLRS        |
9   | TQly        | Tramsmitter link quality                                                | mLRS        |
10  | TSNR        | Transmitter signal to noise ratio                                       | mLRS        |
11  | TRSP        | Transmitter RSSI percentage                                             | mLRS        |
12  | RPWR        | Receiver power (dBm)                                                    | mLRS        |
13  | TFPS        | Transmitter update rate (20, 30, 50)                                    | mLRS        |
14  | RRSP        | Receiver RSSI percentage                                                | mLRS        |
15  | TPWR        | Transmitter power (dBm)                                                 | mLRS        |
16  | RxBt        | Battery voltage                                                         | FC          |
17  | Curr        | Current draw                                                            | FC          |
18  | Capa        | Current consumption                                                     | FC          |
19  | Bat%        | Battery percent remaining                                               | FC          |
20  | GPS         | GPS coordinates                                                         | FC          |
21  | GSpd        | GPS ground speed                                                        | FC          |
22  | Hdg         | Heading                                                                 | FC          |
23  | GAlt        | GPS altitude                                                            | FC          |
24  | Sats        | GPS satellites acquired                                                 | FC          |
25  | Date        | GPS time                                                                | FC          |
26  | Ptch        | FC pitch angle                                                          | FC          |
27  | Roll        | FC roll angle                                                           | FC          |
28  | Yaw         | FC yaw angle                                                            | FC          |
29  | FM          | Flight mode                                                             | FC          |
30  | Alt         | Barometer altitude                                                      | FC          |
31  | VSpd        | Vertical speed                                                          | FC          |
32  | ASpd        | Air speed                                                               | FC          |
33  | Temp        | Temperature                                                             | FC          |

\*Shows up as a 'TPw2' on OpenTX

The numbering of the sensors can vary. Not all sensors may show up.