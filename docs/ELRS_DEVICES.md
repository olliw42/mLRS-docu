# mLRS Documentation: ELRS Devices #

([back to main page](../README.md))

## Receivers ##

As of April 2024, ELRS receivers running the ESP82xx chipset are experimentally supported by mLRS.  The following receiver modules are recommended because they offer at least 100 mW transmit power.

Note: ELRS receivers using an ESP32 chipset are currently not (yet) supported.

<table>
  <thead>
    <tr>
      <th>Frequency</th>
      <th>Product Name</th>
      <th>Transmit Power</th>
      <th>Target</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>868/915 MHz</td>
      <td>Bayck 915M Nano Pro</td>
      <td>500 mW, 27 dBm</td>
      <td>Generic 900 PA</td>
      <td>Unverified</td>
    </tr>
    <tr>
      <td>868/915 MHz</td>
      <td>iFlight ELRS 500mW</td>
      <td>500 mW, 27 dBm</td>
      <td>Generic 900 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>iFlight ELRS 500mW</td>
      <td>500 mW, 27 dBm</td>
      <td>Generic 2400 PA</td>
      <td>Needs custom power levels</td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>Anyleaf ELRS Single</td>
      <td>200 mW, 23 dBm</td>
      <td>Generic 2400 PA Diversity</td>
      <td>Antenna 2 Only</td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>Matek R24D</td>
      <td>200 mW, 23 dBm</td>
      <td>Generic 2400 PA Diversity</td>
      <td>Antenna 2 only</td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>NewBeeDrone BeeCeiver Diversity</td>
      <td>200 mW, 23 dBm</td>
      <td>Generic 2400 PA Diversity</td>
      <td>Antenna 2 only</td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>Radiomaster RP3</td>
      <td>200 mW, 23 dBm</td>
      <td>Generic 2400 PA Diversity</td>
      <td>Antenna 2 only</td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>Skystars Supreme 2.4GHz</td>
      <td>200 mW, 23 dBm</td>
      <td>Generic 2400 PA Diversity</td>
      <td>Antenna 2 only</td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>ATOMRC 2.4G ELRS</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>BAYCKRC ELRS 2.4G NANO</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>BETAFPV ELRS Nano</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>EMAX Aeris Link 2.4G</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>GEPRC ELRS Nano 2.4G PA100</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>HiYOUNGER RX24T</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>JHEMCU RX24T</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>Jumper ELRS AION-RX-NANO</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>Matek R24S</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>SpeedyBee Nano 2.4G</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>Sub250 ELRS Nano</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
    <tr>
      <td>2.4 GHz</td>
      <td>VANTAC 2.4GHz ELRS Nano Pro</td>
      <td>158 mW, 22 dBm</td>
      <td>Generic 2400 PA</td>
      <td></td>
    </tr>
  </tbody>
</table>

## Transmitter Modules ##

ELRS transmitter modules are currently not (yet) supported.
