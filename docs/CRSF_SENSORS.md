# mLRS Documentation: CRSF Sensors #

([back to main page](../README.md))

([back to CRSF page](CRSF.md))

mLRS provides the following telemetry sensors when using CRSF:

Num | Datapoint | Description                                                              | Data Source |
--- | --------- | ------------------------------------------------------------------------ | ----------- |
1   | 1RSS       | Receiver RSSI                                                           | mLRS        |
2   | 2RSS       | Not supported                                                           |             |
3   | Alt        | Altitude                                                                | FC          |
4   | ANT        | Not supported                                                           |             |
5   | Bat%       | Battery percent remaining                                               | FC          |
6   | Capa       | Current consumption                                                     | FC          |
7   | Curr       | Current draw                                                            | FC          |
8   | FM         | Flight mode                                                             | FC          |
9   | GPS        | GPS coordinates                                                         | FC          |
10  | GSpd       | Ground speed                                                            | FC          |
11  | Hdg        | Heading                                                                 | FC          |
12  | Ptch       | FC pitch angle                                                          | FC          |
13  | RFMD       | Receiver update rate (19, 31, 50)                                       | mLRS        |
14  | Roll       | FC roll angle                                                           | FC          |
15  | RQly       | Receiver link quality                                                   | mLRS        |
16  | RRSP       | Receiver RSSI percentage                                                | mLRS        |
17  | RSNR       | Not supported                                                           |             |
18  | RxBt       | Battery Voltage                                                         | FC          |
19  | Sats       | GPS satellites acquired                                                 | FC          |
20  | TFPS       | Transmitter update rate (20, 30, 50 - use RFMD instead)                 | mLRS        |
21  | TPWR       | Transmitter power                                                       | mLRS        |
22  | TPw2*      | Transmitter power                                                       | mLRS        |
23  | TQly       | Tramsmitter link quality                                                | mLRS        |
24  | TRSP       | Transmitter RSSI percentage                                             | mLRS        |
25  | TRSS       | Transmitter RSSI                                                        | mLRS        |
26  | TSNR       | Transmitter signal to noise ratio                                       | mLRS        |
27  | VSpd       | Vertical speed (barometer)                                              | FC          |
28  | Yaw        | FC yaw angle                                                            | FC          |

\*Shows up as a 2nd 'TPWR' on EdgeTX