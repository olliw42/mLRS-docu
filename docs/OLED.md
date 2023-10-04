# mLRS Documentation: OLED Display #

([back to main page](../README.md))

mLRS allows for a 0.96", 128x64, SSD1306 OLED display to be connected to a Tx module using I2C.  When paired with a 5-way joystick (4 directions + select) this allows for one to update parameters and display link statistics.

## Hardware Configuration

Instructions for adding an OLED display to the FRM303 module [here](https://github.com/olliw42/mLRS-docu/blob/master/docs/FLYSKY_FRM303.md#oled-display-addition).

## OLED Screens & Navigation

From the main screen, you can navigate the through 4 main screens using the up and down directions, these contain the following information:

<table border="1">
    <tr>
        <th>Main</th>
        <th>Main/2</th>
        <th>Main/3</th>
        <th>Main/4</th>
    </tr>
    <tr>
        <td>Config ID</td>
        <td>Mode</td>
        <td>Tx, Rx data rate</td>
        <td>Tx, Rx hardware</td>
    </tr>
    <tr>
        <td>Mode</td>
        <td>Sensitivity</td>
        <td>Tx, Rx active antenna3</td>
        <td>Tx, Rx firmware version</td>
    </tr>
    <tr>
        <td>Tx, Rx output power</td>
        <td>Tx, Rx output power</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>Tx, Rx LQ</td>
        <td>Tx, Rx diversity mode</td>
        <td></td>
        <td></td>
    </tr>
</table>


From the main screen, you can navigate to the setting and action screens using the right and left directions, these contain the following settings:

<table border="1">
    <tr>
        <th>Common</th>
        <th>Tx</th>
        <th>Rx</th>
        <th>Actions</th>
    </tr>
    <tr>
        <td>Bind Phrase</td>
        <td>Power</td>
        <td>Power</td>
        <td>Store</td>
    </tr>
    <tr>
        <td>Mode</td>
        <td>Diversity</td>
        <td>Diversity</td>
        <td>Bind</td>
    </tr>
    <tr>
        <td>Band</td>
        <td>Ch Source</td>
        <td>Ch Order</td>
        <td>Boot</td>
    </tr>
    <tr>
        <td></td>
        <td>Ch Order</td>
        <td>Out Mode</td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td>In Mode</td>
        <td>Failsafe Mode</td>
        <td></td>
    </tr>
        <tr>
        <td></td>
        <td>Ser Dest</td>
        <td>Ser Baudrate</td>
        <td></td>
    </tr>
        <tr>
        <td></td>
        <td>Ser Baudrate</td>
        <td>Ser Link Mode</td>
        <td></td>
    </tr>
        <tr>
        <td></td>
        <td>Snd RadioStat</td>
        <td>Snd RadioStat</td>
        <td></td>
    </tr>
        <tr>
        <td></td>
        <td>Buzzer</td>
        <td>Snd RcChannel</td>
        <td></td>
    </tr>
        <tr>
        <td></td>
        <td>Cli LineEnd</td>
        <td>Buzzer</td>
        <td></td>
    </tr>
    </tr>
        <tr>
        <td></td>
        <td>Cli LineEnd</td>
        <td>Out Rssi Ch</td>
        <td></td>
    </tr>
     </tr>
        <tr>
        <td></td>
        <td>Cli LineEnd</td>
        <td>Out LQ Ch</td>
        <td></td>
    </tr>
        </tr>
        <tr>
        <td></td>
        <td>Cli LineEnd</td>
        <td>FS Ch1-16</td>
        <td></td>
    </tr>
</table>