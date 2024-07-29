# mLRS Documentation: Parameters (v1.3.00) #

([back to main page](../README.md))

Brief description of the parameters for configuring mLRS. The parameters fall into three categories: 

1. Parameters common to the Tx module and receiver. These need to be configured to be identical for both, in order for a connection to be possible. For an arbitrary receiver, this can be achieved by binding the receiver to the Tx module.

2. Parameters only for the Tx module (Tx parameters).

3. Parameters only for the receiver (Rx parameters).

All parameters are configured via the Tx module, by using the CLI or the mLRS configuration Lua script (or the OLED if available). If no receiver is connected, then the Rx parameters cannot be configured.

Depending on the specific mLRS hardware, it may happen that some parameters are not available or that for a parameter some options are not available.

## Common Parameters ##

#### Bind Phrase ####
String of 6 characters. 
The characters can be 'a'-'z', '0'-'9', '_', '#', '-', '.'. 

For 2.4 GHz systems the last (6th) character of the bind phrase determines excluded frequencies. The exclude setting can be "\e-", "\e1", "\e6", "\e11", or "\e13". For details see [FHSS_SHAPING](FHSS_SHAPING.md).

#### Mode ####
Operation mode. May not be selectable.
Can be "50 Hz", "31 Hz", "19 Hz", "FLRC", "FSK".

#### RF Band ####
Frequency band. May not be selectable.

#### RF Ortho ####
For 2.4 GHz and 915 MHz FCC RF bands allows one to constrain the used frequencies in the FHSS sequence, see [FHSS_SHAPING](FHSS_SHAPING.md).
Can be "off", "1/3", "2/3", "3/3".

## Tx Parameters ##

#### Tx Power #### 
Transmission power in Watts.

#### Tx Diversity #### 
Diversity mode. 
Can be "enabled", "antenna1", "antenna2", "r:en, t:ant1", "r:en, t:ant2".

The last two options allow for having receive diversity while choosing to transmit on a specific antenna.

#### Tx Ch Source #### 
Selects the source from which the rc data should be read. 
Can be "none", "crsf", "in", "mbridge".

#### Tx Ch Order #### 
Channel order of the rc data provided to the Tx module. 
Can be "AETR", "TAER", "ETAR".

#### Tx In Mode #### 
Selects the protocol of the rc data on the in port. Effective only when "Tx Ch Source" = "in". 
Can be "sbus", "sbus inv".

#### Tx Ser Dest #### 
Selects the destination/source of the serial data stream. 
Can be "serial", "serial2", "mbridge". 

#### Tx Ser Baudrate #### 
Baudrate of the serial data stream. Effective only for "Tx Ser Dest" = "serial" or "serial2". 
Can be "9600", "19200", "38400", "57600", "115200", "230400".

#### Tx Snd RadioStat #### 
Determines if a MAVLink RADIO_STATUS message is emitted by the Tx module. Effective only when in the receiver "Rx Ser Link Mode" = "mavlink" or "mavlinkX" is set. 
Can be "off", "1 Hz".

#### Tx Buzzer #### 
Enables the buzzer, and selects what data it reflects. Can be "off", "LP", "rxLQ".

LP stands for Lost Packet, and here the buzzer emits a short beep for any lost packet. rxLQ stands for receiver Link Quality, and here the buzzer beeps every second, with the beep length reflecting LQ (longer beep equals lower LQ).

#### Tx Mav Component ####
Enabled parameter configuration using the MAVLink parameter service.
Can be "enabled", "off".

#### Tx Cli LineEnd ####
Determines the line termination character(s) used by the CLI. 
Can be "CR", "LF", "CRLF".

## Rx Parameters ##

#### Rx Power #### 
Transmission power in Watts.

#### Rx Diversity #### 
Diversity mode. 
Can be "enabled", "antenna1", "antenna2", "r:en, t:ant1", "r:en, t:ant2".

The last two options allow for having receive diversity while choosing to transmit on a specific antenna.

#### Rx Ch Order #### 
Channel order of the rc data emitted by the receiver. 
Can be "AETR", "TAER", "ETAR".

#### Rx Out Mode #### 
Selects the protocol of the rc data emitted on the out port. 
Can be "sbus", "crsf", "sbus inv".

#### Rx Out Rssi Ch #### 
Determines if and on which channel the RSSI value is send out. 
Can be "off", "5" - "16".

#### Rx Out Lq Ch #### 
Determines if and on which channel the LQ value is send out. 
Can be "off", "5" - "16".

#### Rx FailSafe Mode #### 
Determines the behavior upon a failsafe. 
Can be "no sig", "low thr", "by cnf", "low thr cnt", "ch1ch4 cnt".

#### Rx Ser Baudrate #### 
Baudrate of the serial data stream. 
Can be "9600", "19200", "38400", "57600", "115200", "230400".

#### Rx Ser Link Mode #### 
Selects how the serial data stream is processed. 
Can be "transp.", "mavlink", "mavlinkX".

The setting is also applied to the Tx module. For MAVLinkX see [here](MAVLINKX.md).

#### Rx Snd RadioStat #### 
Determines if a MAVLink RADIO_STATUS or RADIO_LINK_FLOW_CONTROL message is emitted by the receiver, and which flow control algorithm is used. Effective only when "Rx Ser Link Mode" = "mavlink" or "mavlinkX". 
Can be "off", "ardu_1", "meth_b".

If "Rx Snd RcChannel" is set to "rc channels", then RADIO_LINK_FLOW_CONTROL messages are emitted instead of RADIO_STATUS.

#### Rx Snd RcChannel #### 
Determines if a RC_CHANNELS_OVERRIDE or RADIO_RC_CHANNELS MAVLink message is emitted by the receiver. Effective only when "Rx Ser Link Mode" = "mavlink" or "mavlinkX". 
Can be "off", "rc override", "rc channels".

If using ArduPilot V4.6.0-dev on a 2 MB flight controller, the "rc channels" setting is strongly recommended. Otherwise, "rc override" must be used. (ArduPilot V4.6.0-dev supports the RADIO_RC_CHANNELS message, older versions do not)

#### Rx Buzzer #### 
Enables the buzzer, and selects what data it reflects. Can be "off" or "LP".

LP stands for Lost Packet, and here the buzzer emits a short beep for any lost packet.

#### Rx FS Ch1 - Rx FS Ch16 #### 
Sets the rc channel value upon a failsafe. Effective only when "Rx FailSafe Mode" = "by cnf". 
Can be a value between -120% and +120%.
