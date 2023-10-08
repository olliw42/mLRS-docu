# mLRS Documentation: MavlinkX #

([back to main page](../README.md))

MavlinkX is a technology which weeds out deficiencies of the original MAVLink protocol and makes the over-the-air MAVLink communication significantly more robust, reducing packet losses to the minimum. Furthermore, it can provide per-message compression of the MAVLink data stream.

A major deficiancy of the MAVLink protocol is that, in the presence of data loss, it is prone to miss MAVLink packets which are actually valid, i.e., which are correctly and fully recieved and thus provide valid data, but are missed in the parsing of the stream (for a deeper discussion of such topics see [here](https://github.com/mavlink/mavlink/issues/1347)).

Loosing valid packets for "no reason" is obviously highly undesirable, especially given that the bandwidth of long-range links is generally constraint and should be used in the best possible manner. MavlinkX overcomes this issue by reframing the MAVLink messages and using parsing strategies which enables the parser to recover any valid packet from the lossy data stream.

Moreover, MavlinkX provides compression of the MAVLink data stream. Given the nature of the MAVLink data, the average compression rate cannot be huge (simple theoretical best-case estimates suggest ca 20%), but for low-bandwith links this can be sufficient to be significant.

Example: In the 19 Hz mode, the data rate of the telemetry stream might be typically 1150 bytes/s. With MavlinkX enabled, it would typically allow to send 1300 bytes/sec. This correspond to ca 4 additional ATTITUDE MAVLink messages per sec, and the rate for ATTITUDE messages could be increased from e.g. 2 Hz to 5 Hz, which would yield a substantially smoother HUD display.

MavlinkX is enabled by setting the "Rx Ser Link Mode" parameter in the receiver to "mavlinkx". Note: The compression is enabled only in the 19 Hz mode. 