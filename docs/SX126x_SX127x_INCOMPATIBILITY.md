# mLRS Documentation: Compatibility Chart #

([back to main page](../README.md))

mLRS hardware uses several Semtech RF chipsets that are not fully compatible with one another. As a result, not all mLRS devices can bind to each other (see the subsection below for details).

## Compatibility Chart

Whenever two devices say ✅ to a mode, they can work together in that mode.

<table>
  <tbody>
    <tr>
      <th>Mode \ Chipset</th>
      <th>SX128x</th>
      <th>SX126x</th>
      <th>SX127x</th>
      <th colspan="2">LR1121</th>
    </tr><tr>
      <th></th>
      <th><strong>2.4 GHz</strong></th>
      <th><strong>868/915 MHz</strong></th>
      <th><strong>868/915 MHz</strong></th>
      <th><strong>2.4 GHz</strong></th>
      <th><strong>868/915 MHz</strong></th>
    </tr><tr align="center">
       <th align="left">50 Hz       </th><td> ✅ </td><td> ❌ </td><td> ❌ </td><td> ✅ </td><td> ❌ </td>
    </tr><tr align="center">
       <th align="left">31 Hz       </th><td> ✅ </td><td> ✅ </td><td> ❌ </td><td> ✅ </td><td> ✅ </td>
    </tr><tr align="center">
       <th align="left">19 Hz       </th><td> ✅ </td><td> ✅ </td><td> ❌ </td><td> ✅ </td><td> ✅ </td>
    </tr><tr align="center">
       <th align="left">19 Hz 7x    </th><td> ❌ </td><td> ❌ </td><td> ✅ </td><td> ❌ </td><td> ✅ </td>
    </tr><tr align="center">
       <th align="left">FSK 50 Hz   </th><td> ❌ </td><td> ✅ </td><td> ❌ </td><td> ❌ </td><td> ✅ </td>
    </tr><tr align="center">
       <th align="left">FLRC 111 Hz </th><td> ✅ </td><td> ❌ </td><td> ❌ </td><td> ❌ </td><td> ❌ </td>
    </tr>
  </tbody>
</table>

## SX126x and SX127x Incompatibility

mLRS hardware using the SX126x/STM32WLE and SX127x LoRa chipsets are ***not*** compatible with each other and will not bind.

This is for two reasons:
- The 31 Hz mode uses spreading factor 5 (SF5), which is only available on the SX126x/STM32WLE chipset.
- The 19 Hz and 19 Hz 7x modes use spreading factor 6 (SF6), which was modified on the SX126x/STM32WLE chipset making it incompatible with the SX127x chipset.

This is the relevant part in the datasheet of the SX126x chipset:

<img src="images/SX126x_SF6_incompatibility.png" width="900px">
