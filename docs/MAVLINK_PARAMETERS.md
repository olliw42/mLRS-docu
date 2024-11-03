# mLRS Documentation: MAVLink Parameters #

([back to main page](../README.md))

The Tx module and receiver can also be configured via MAVLink parameters using ground control station (GCS) software such as Mission Planner. However, due to the limitations of the MAVLink parameter system, this method is only recommended when other configuration methods (CLI, Lua script, or OLED) are not easily accessible. 

The Tx module will present itself as a MAVLink component with a system id 51 (like SiK radios) and component id 68 (MAV_COMP_ID_TELEMETRY_RADIO). For instance, in MissionPlanner it will show up as "COMxx-51-TELEMETRY RADIO". The Tx module emits MAVLink [HEARTBEAT](https://mavlink.io/en/services/heartbeat.html) messages which allows a GCS to discover the Tx module and provide the [parameter microservice](https://mavlink.io/en/services/parameter.html). The GCS can connect to this component and edit its parameters.

In order to utilize this functionality, one must do the following:
- In the Tx module, the parameter "Tx Mav Component" must be set to "enabled". This is the default setting; if it has been changed, then this parameter must be configured using one of the other methods (CLI, Lua script, OLED).
- Be connected to a receiver with the parameter "Rx Ser Link Mode" configured to "mavlink" or "mavlinkX". "mavlinkX" is the default setting; if it has been changed, then this parameter must be configured using one of the other methods (CLI, Lua script, OLED).
- If no receiver is connected then the MAVLink component is only available if the last receiver which the Tx module "remembers" was configured with "Rx Ser Link Mode" = "mavlink" or "mavlinkX". This should be the last receiver which was connected to the Tx module for which a parameter store operation was done. 

***Note***: If no receiver is connected, then only the parameters of the Tx module can be configured. However, the receiver parameters are always shown.

The MAVLink parameters are identical to those described in [Configuration Parameters](PARAMETERS.md), but have different names which conform to the MAVLink standard. They should be easy to recognize. For instance, the parameter "Rx Ser Link Mode" shows up as "RX_SER_LNK_MODE". 

These exceptions exist:
1. An additional parameter "PSTORE" is available. Parameter changes are not permanently stored in the Tx module or receiver when written. In order to store them permanently, the parameter PSTORE must be set to 1 and written to the component. This is somewhat similar to the CLI's pstore command or the Lua script's "Store" button.
2. The bind phrase is presented as an uint32_t number instead of a string of 6 chars as in the other methods, and the parameter is called "BIND_PHRASE_U32". This means that setting a bind phrase is a bit inconvenient, as the MAVLink parameter system only allows numeric values.
3. The parameter "TX_MAV_COMPONENT" ("Tx Mav Component") cannot be set or modified and will always be 1. This is to prevent unintentional disabling of the MAVLink component.
4. The parameter "RX_SER_LNK_MODE" ("Rx Ser Link Mode") cannot be set to 0. This is to prevent unintentional disabling of the MAVLink component.
5. An additional parameter "CONFIG ID" is available, which allows one to set the [configuration ID](CONFIGID.md).

A major painpoint of the MAVLink parameter system is that the parameter settings are only available as numeric values, and not as plain text, as with the other methods. There is unfortunately nothing mLRS can do about this. The meaning of the parameter values need to be inferred from the information given in [Configuration Parameters](PARAMETERS.md).

Here are the steps that one should take to update a parameter in Mission Planner:

1. Change the value of the parameter you wish to update
2. Click Write, to temporarily set the parameter
3. Click Refresh, to check that the parameter was updated
4. Set PSTORE to 1
5. Click Write to permanently store the parameter

This all may sound a bit complicated, but it is less complicated than it may read now. Those who are already comfortable editing parameters should be able to find this method a valid option for configuration.

***Note***: MAVLink supports two [parameter encodings](https://mavlink.io/en/services/parameter.html#parameter-encoding). mLRS is using byte-wise encoding, and announces this properly by setting the respective flag in the capabilities field of the [AUTOPILOT_VERSION](https://mavlink.io/en/messages/common.html#AUTOPILOT_VERSION) MAVLink message. Most GCSes can handle both encodings, but some do not (for instance, pymavlink does not).
