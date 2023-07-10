# mLRS Documentation: Link Statistics #

([back to main page](../README.md))

This page provides details around the three types of link statistics that mLRS reports (as of version 0.3.27).  The three types are:

1. LQ (Link Quality) 
2. RSSI (Raw / Received Signal Strength Indicator)
3. SNR (Signal to Noise Ratio)

## LQ (Link Quality) ##

- Link Quality represents the percentage of valid packets that are received.  
    - For example, in the 50 Hz mode if 2 packets are corrupted due to interference then the Link Quality will be reported as 96% (48 / 50).  
- Link Quality is available in the following locations when using mLRS:
    - The radio will show the LQ of the receiver (RQly) and the transmitter (TQly) when using CRSF for JR Pin 5.
        - RQly measures the percentage of packets for the receiver that were valid up to the first CRC (this includes the status and RC channels 1-4, 13, 14).
        - TQly measures the percentage of packets for the transmitter in which the entire frame was valid. 
    - ArduPilot will be able to show the LQ of the receiver when using CRSF for RC.
        - See the definition of RQly above.
- Link Quality is measured by code within mLRS.

## RSSI (Raw / Received Signal Strength Indicator) ##

- RSSI represents the strength of the received signal and is measured in two ways:
    1. RSSI dBm, which is an absolute value. This value can be compared to the sensitivity limit of the RF mode in use. For example, the 50 Hz mode has a sensitivity limit of -105 dBm, so if RSSI dBm is reported as -100 dBm then you are said to have 5 dBm of link budget before signal will be lost.
    2. RSSI percentage, which scales the RSSI dBm to a percentage between 0 and 100 with larger values representing a stronger signal.
- RSSI dBm is available in the following locations when using mLRS:
    - The radio will be able to show the RSSI dBm of both the transmitter (TRSS) and the receiver (1RSS) when using CRSF for JR Pin 5. There will also be a 2RSS telemetry element (designed for diversity receivers) but this is not supported by mLRS.
- RSSI percentage is available in the following locations when using mLRS:
    - The radio will show the RSSI percentage of the transmitter (TRSP) and the receiver (RRSP) when using CRSF for JR Pin 5. 
    - ArduPilot will be able to show the RSSI percentage of the receiver (rxrssi) and the transmitter (rssi).
        - In order to see rxrssi, RSSI will need to be enabled and configured.
        - In order to see rssi, the Tx Snd RadioStat parameter needs to be set to 1 Hz.
- While the RSSI dBm is a more useful value to understand, as ArduPilot only reports RSSI percentage here's a table that provides the corresponding percentages to the sensitivity limits of the mLRS RF modes:

    - <table>
        <thead>
            <tr>
            <th>RSSI dBm</th>
            <th>RSSI %</th>
            <th>RF Mode</th>
            </tr>
        </thead>
        <tbody>
            <tr>
            <td>-105</td>
            <td>21</td>
            <td>50 Hz</td>
            </tr>
            <tr>
            <td>-108</td>
            <td>17</td>
            <td>31 Hz</td>
            </tr>
            <tr>
            <td>-112</td>
            <td>11</td>
            <td>19 Hz</td>
            </tr>
        </tbody>
        </table>
- RSSI dBm is measured by the SX12xx RF chipset and RSSI percentage is determined by code within both mLRS and ArduPilot using the measured RSSI dBm.

## SNR (Signal to Noise Ratio) ##

- SNR represents the the RSSI dBm level to the RF noise level of the environment.  This is an absolute value and can have both positive and negative values. Positive values means that there is more signal than noise and negative values indicate that there is less signal than noise.
- SNR is available in the following locations when using mLRS:
    - The radio will show the SNR of the transmitter (TSNR) when using CRSF for JR Pin 5.  There will also be a RSNR telemetry element but this is not supported by mLRS.
- SNR is measured by the SX12xx RF chipset.