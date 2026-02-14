# mLRS Documentation: Parameters (v1.3.08) #

([back to main page](../README.md))

Brief description of the parameters for configuring mLRS. The parameters fall into three categories: 

1. Parameters common to the Tx module and receiver (common parameters). These parameters must be identical on both the Tx module and the receiver to establish a connection. For a receiver with unknown configuration, this can be achieved by binding the receiver to the Tx module.

3. Parameters only for the Tx module (Tx parameters).

4. Parameters only for the receiver (Rx parameters).

All parameters are configured through the Tx module using the CLI, the mLRS Lua script, or the OLED interface (if available). The Rx parameters can only be configured when a receiver is connected.

Depending on the specific mLRS hardware, it may happen that some parameters are not available or that for a parameter some options are not available.

> [!NOTE]
> - When the common parameters are identical on both the Tx module and the receiver, the devices are considered "bound." Once bound, they can establish a connection.
> - When the common parameters are not identical, i.e., Tx module and receiver are not bound, then they cannot establish a connection.

## Common Parameters ##

#### Bind Phrase ####
String of 6 characters. 
The characters can be 'a'-'z', '0'-'9', '_', '#', '-', '.'. 

For 2.4 GHz systems the last (6th) character of the bind phrase determines excluded frequencies. The exclude setting can be "\e-", "\e1", "\e6", "\e11", or "\e13". For details see [FHSS_SHAPING](FHSS_SHAPING.md).

#### Mode ####
Operation mode. May not be selectable (depends on hardware).
Can be: "50 Hz", "31 Hz", "19 Hz", "19 Hz 7x", "FLRC", "FSK".

#### RF Band ####
Frequency band. May not be selectable (depends on hardware).

#### RF Ortho ####
For 2.4 GHz and 915 MHz FCC RF bands allows one to constrain the used frequencies in the FHSS sequence, see [FHSS_SHAPING](FHSS_SHAPING.md).
Can be: "off", "1/3", "2/3", "3/3".

## Tx Parameters ##

#### Tx Power #### 
Transmission power in Watts.

#### Tx Diversity #### 
Diversity mode. 
Can be: "enabled", "antenna1", "antenna2", "r:en, t:ant1", "r:en, t:ant2".

The last two options enable receive diversity while allowing the transmit path to be restricted to a specific antenna.

#### Tx Ch Source #### 
Selects the source from which the RC data should be read. 
Can be: "none", "crsf", "in", "mbridge".

#### Tx Ch Order #### 
Channel order of the RC data provided to the Tx module. 
Can be: "AETR", "TAER", "ETAR".

#### Tx In Mode #### 
Selects the protocol of the RC data on the IN port. Effective only when "Tx Ch Source" = "in". 
Can be: "sbus", "sbus inv".

#### Tx Ser Dest #### 
Selects the destination/source of the serial data stream. 
Can be: "serial", "serial2", "mbridge". 

#### Tx Ser Baudrate #### 
Baudrate of the serial data stream. Effective only for "Tx Ser Dest" = "serial" or "serial2". 
Can be: "9600", "19200", "38400", "57600", "115200", "230400".

The default is 115200 bps, which is appropriate for almost all cases. Anything below 57600 bps is not recommended. 

#### Tx Snd RadioStat #### 
Determines if a RADIO_STATUS MAVLink message is emitted by the Tx module. Effective only when in the receiver "Rx Ser Link Mode" = "mavlink" or "mavlinkX" is set. 
Can be: "off", "1 Hz".

#### Tx Mav Component ####
Enables parameter configuration via the MAVLink parameter protocol.
Can be: "enabled", "off".

#### Tx Power Sw Ch ####
The channel used to control the RF output power of the Tx module. The power levels available on the device are linearly interpolated over the RC input range of −100% to +100%, where +100% corresponds to the power level defined by the Tx Power parameter and −100% corresponds to the minimum available power level.

#### Tx Buzzer #### 
Enables the buzzer, and selects what data it reflects. 
Can be: "off", "LP", "rxLQ".

LP stands for Lost Packet, and here the buzzer emits a short beep for any lost packet. rxLQ stands for receiver Link Quality, and here the buzzer beeps every second, with the beep length reflecting LQ (longer beep equals lower LQ).

#### Tx Wifi Protocol #### 
Protocol used by the wireless bridge. 
Can be: "TCP", "UDP", "BT", "UDP STA", "BLE".

#### Tx Wifi Channel #### 
Wifi channel used by the wireless bridge.
Can be: "1", "6", "11", "13".

#### Tx Wifi Power #### 
RF power used by the wireless bridge. 
Can be: "low", "med", "max".

## Rx Parameters ##

#### Rx Power #### 
Transmission power in Watts.

#### Rx Diversity #### 
Diversity mode. 
Can be: "enabled", "antenna1", "antenna2", "r:en, t:ant1", "r:en, t:ant2".

The last two options enable receive diversity while allowing the transmit path to be restricted to a specific antenna.

#### Rx Ch Order #### 
Channel order of the RC data emitted by the receiver. 
Can be: "AETR", "TAER", "ETAR".

#### Rx Out Mode #### 
Selects the protocol of the RC data emitted on the OUT port. 
Can be: "sbus", "crsf", "sbus inv".

#### Rx FailSafe Mode #### 
Determines the behavior upon a failsafe. 
Can be: "no sig", "low thr", "by cnf", "low thr cnt", "ch1ch4 cnt".

#### Rx Ser Baudrate #### 
Baudrate of the serial data stream. 
Can be: "9600", "19200", "38400", "57600", "115200", "230400".

The default is 57600 bps. Anything below 57600 bps is not recommended. 

#### Rx Ser Link Mode #### 
Selects how the serial data stream is processed. 
Can be: "transp.", "mavlink", "mavlinkX", "mspX".

This setting is also applied to the Tx module. For MAVLinkX see [here](MAVLINKX.md). For MspX see [here](MSPX.md).

#### Rx Mav System ID #### 
Determines the MAVLink system ID used by the mLRS system. Effective only when "Rx Ser Link Mode" = "mavlink" or "mavlinkX". This setting is also applied to the Tx module. 
Can be: "51", "52", "53", "54", "55".

A system ID of 51 has become a defacto standard for telemetry links (it is e.g. used by SiK devices).

#### Rx Snd RadioStat #### 
Determines if a RADIO_STATUS MAVLink message is emitted by the receiver, and which flow control algorithm is used. Effective only when "Rx Ser Link Mode" = "mavlink" or "mavlinkX". 
Can be: "off", "ardu_1", "meth_b".

#### Rx Snd RcChannel #### 
Determines if either a RC_CHANNELS_OVERRIDE or a RADIO_RC_CHANNELS MAVLink message is emitted by the receiver. Effective only when "Rx Ser Link Mode" = "mavlink" or "mavlinkX". 
Can be: "off", "rc override", "rc channels".

If using ArduPilot 4.6.0 and higher on a 2 MB flight controller, the "rc channels" setting is strongly recommended. Otherwise, "rc override" must be used. For details see the [ArduPilot configuration page](ARDUPILOT.md).

#### Rx Out Rssi Ch #### 
Determines if and on which channel the RSSI value is send out. 
Can be: "off", "5" - "16".

#### Rx Out LQ Ch #### 
Determines if and on which channel the LQ value is send out. 
Can be: "off", "5" - "16".

#### Rx Power Sw Ch ####
The channel used to control the RF output power of the Tx module. The power levels available on the device are linearly interpolated over the RC input range of −100% to +100%, where +100% corresponds to the power level defined by the Tx Power parameter and −100% corresponds to the minimum available power level.

#### Rx FS Ch1 - Rx FS Ch16 #### 
Sets the RC channel values upon a failsafe. Effective only when "Rx FailSafe Mode" = "by cnf". 
Can be a value between -120% and +120%.
