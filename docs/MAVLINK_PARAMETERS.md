# mLRS Documentation: MAVLink Parameters #

([back to main page](../README.md))

When enabled, the Tx module and receiver can also be configured via MAVLink parameters using a ground control station (GCS) such as MissionPlanner. This can be useful in cases in which the other methods for configuration, i.e., the CLI, Lua script, or OLED, are not (easily) accessible, such as in some stand-alone applications.

Using the MAVLink parameters for configuration has its inconveniences however, due to the limitations of the MAVLink parameter system and support in GCSes.

When enabled, the Tx module presents itself as MAVLink component with system id 51 (like the SiK radios) and component id 68 (= MAV_COMP_ID_TELEMETRY_RADIO). That is, it emits a [HEARTBEAT](https://mavlink.io/en/services/heartbeat.html) MAVLink message which allows a GCS to discover the component, and provides the [parameter microservice](https://mavlink.io/en/services/parameter.html). A GCS can thus connect to this component and read & write its parameters.

This MAVLink component is available only under certain conditions:
- in the Tx module the setting "Tx Mav Component" must be set to "enabled". This is usually the default setting. If not, when it must be configured using one of the other methods (CLI, Lua script, OLED). 
- a receiver is connected for which the setting "Rx Ser Link Mode" is configured to "mavlink" or "mavlinkX".
- if no receiver is connected then the MAVLink component is available if the last receiver which the Tx module "remembers" was configured with "Rx Ser Link Mode" = "mavlink" or "mavlinkX". This is usually the last receiver which was connected to the Tx module and for which a parameter store operation was done. 

As for the other methods, if a receiver is connected, then the parameters of both the Tx module and the receiver can be configured. If no receiver is connected, then only the parameters of the Tx module can be configured. Note however that the receiver parameters are nevertheless shown.

The MAVLink parameters are identical to those described in [Configuration Parameters](PARAMETERS.md), but have different names which conform to the MAVLink standard. They should be easy to recognize however, for instance, the parameter "Rx Ser Link Mode" shows up as "RX_SER_LNK_MODE". Four exceptions exist:
- the bind phrase is presented as an uint32_t number instead of a string of 6 chars as in the other methods, and the parameter is called "BIND_PHRASE_U32" (setting a bind phrase is thus a bit inconvenient, but the MAVLink parameter system does not allow us to do better).
- the parameter "TX_MAV_COMPONENT" (= "Tx Mav Component") cannot be set or modified and will always be 1. This is to prevent unintentional disabling of the MAVLink component.
- the parameter "RX_SER_LNK_MODE" (= "Rx Ser Link Mode") cannot be set to 0. This is to prevent unintentional disabling of the MAVLink component.
- the additional parameter "PSTORE" is available. Parameter changes are not permanently stored in the Tx module or receiver when written. In order to store them permanently, the parameter PSTORE must be set to 1 and written to the component. This is somewhat similar to the CLI's pstore command or the Lua script's "Store" button. 

Some GCSes, such as MissionPlanner, do not update the parameter values to the actual values taken by the component upon a write operation. This can result in situations where the parameter values shown in the GCS are invalid, i.e., do not reflect the setting in the Tx module or reciever (the available parameter settings can be specific to a particular mLRS system). It is thus recommended practice to do a parameter refresh after parameter writes, and to double check the resulting setting before a PSTORE.

A major painpoint of the MAVLink parameter system is that the parameter settings are only available as numerical values, and not as plain text, as with the other methods. There is unfortunately nothing mLRS can do about this. The meaning of the parameter values need to be inferred from the information given in [Configuration Parameters](PARAMETERS.md).

This all may sound a bit complicated, but it is less complicated than it may read now. The MAVLink parameter system can be a working alternative for configuration.

 


