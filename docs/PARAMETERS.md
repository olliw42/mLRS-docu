# mLRS Documentation: Parameters (v0.3.24) #

([back to main page](../README.md))

Brief description of the parameters for configuring mLRS. The parameters fall into three categories: 

1. Parameters common to Tx and Rx. These need to be configured to be identical for Tx and Rx, in order for a connection to be possible. For an arbitrary receiver, this can be achieved by binding the receiver to the Tx module.

2. Parameters only for the Tx module (Tx parameters).

3. Parameters only for the receiver (Rx parameters).

All parameters are configured via the Tx module, by using the CLI or the mLRS configuration Lua script. If no receiver is connected, then the Rx parameters cannot be configured.

Depending on the specific mLRS hardware, it may happen that not all parameters are available, as well as that not all options for a parameter are available.

## Common Parameters ##

#### Bind Phrase ####
String of 6 characters. 
The characters can be 'a'-'z', '0'-'9', '_', '#', '-', '.', 

#### Mode ####
Operation mode. 
Can be "50 Hz", "31 Hz", "19 Hz".

#### RF Band ####
Frequency band. May not be selectable.

## Tx Parameters ##

#### Tx Power #### 
Transmission power in Watts.

#### Tx Diversity #### 
Diversity mode. 
Can be "enabled", "antenna1", "antenna2". 

#### Tx Ch Source #### 
Selects the source from which the rc data should be read. 
Can be "none", "mbridge", "in", "crsf".

#### Tx Ch Order #### 
Channel order of the rc data provided to the Tx module. 
Can be "AETR", "TAER", "ETAR".

#### Tx In Mode #### 
Selects the protocol of the rc data on the in port. Effective only when "Tx Ch Source" = "in". 
Can be "sbus", "sbus inv".

#### Tx Ser Dest #### 
Selects the destination/source of the serial data stream. 
Can be "serial", "mbridge", "serial2"

#### Tx Ser Baudrate #### 
Baudrate of the serial data stream. Effective only for "Tx Ser Dest" = "serial" or "serial2". 
Can be "9600", "19200", "38400", "57600", "115200", "230400".

#### Tx Buzzer #### 
Enables the buzzer, and selects what data it reflects. 
Can be "off", "LP", "rxLQ".

#### Tx Cli LineEnd ####
Determines the line termination character(s) used by the CLI. 
Can be "CR", "LF", "CRLF".

## Rx Parameters ##

#### Rx Power #### 
Transmission power in Watts.

#### Rx Diversity #### 
Diversity mode. 
Can be "enabled", "antenna1", "antenna2". 

#### Rx Ch Order #### 
Channel order of the rc data emitted by the receiver. 
Can be "AETR", "TAER", "ETAR".

#### Rx Out Mode #### 
Selects the protocol of the rc data emitted on the out port. 
Can be "sbus", "crsf", "sbus inv".

#### Rx Out Rssi Ch #### 
Determines if and on which channel the RSSI value is send out. 
Can be "off", "5" - "12".

#### Rx FailSafe Mode #### 
Determines the behavior upon a failsafe. 
Can be "no sig", "low thr", "by cnf", "low thr cnt", "ch1ch4 cnt".

#### Rx Ser Baudrate #### 
Baudrate of the serial data stream. 
Can be "9600", "19200", "38400", "57600", "115200", "230400".

#### Rx Ser Link Mode #### 
Selects how the serial data stream is processed. 
Can be "transp.", "mavlink".

The setting is also applied to the Tx module.

#### Rx Snd RadioStat #### 
Determines if a MAVLink RADIO_STATUS or RADIO_LINK_FLOW_CONTROL message is emitted by the receiver, and which flow control algorithm is used. Effective only when "Rx Ser Link Mode" = "mavlink". 
Can be "off", "ardu_1", "meth_b".

If "Rx Snd RcChannel" is set to "rc channels", then RADIO_LINK_FLOW_CONTROL messages are emitted instead of RADIO_STATUS.

#### Rx Snd RcChannel #### 
Determines if a MAVLink RC_CHANNELS_OVERRIDE or RADIO_RC_CHANNELS message is emitted by the receiver. Effective only when "Rx Ser Link Mode" = "mavlink". 
Can be "off", "rc override", "rc channels".

#### Rx Buzzer #### 
Enables the buzzer, and selects what data it reflects. 
Can be "off", "LP".

#### Rx FS Ch1 - Rx FS Ch16 #### 
Sets the rc channel value upon a failsafe. Effective only when "Rx FailSafe Mode" = "by cnf". 
Can be a value between -120% and +120%.
