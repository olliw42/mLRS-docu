# mLRS Documentation: Diagnosing Common Problems #

([back to main page](../README.md))

This page attempts to provide a step by step guide to isolate and correct some common problems.  It covers only a core use case where an EdgeTX or OpenTX radio with a mLRS Tx module is used to communicate with a mLRS receiver connected to an ArduPilot flight controller to provide both RC control and MAVLink telemetry to a ground station and/or [Yaapu Telemetry App](CRSF.md).  Users with other use cases in mind may still find some parts of this page helpful.

Numbered topics here assume correct verification of previous functionality so don't skip ahead.  You must establish correct operation for each numbered topic in turn or the deductions we make later may not be correct.  Each numbered topic also assumes the state and configuration established in previous topics.  For example, topic 3 instructs you to power on both your Tx module and receiver and verify the connection.  All subsequent topics assume they are powered on and connected.

Each numbered topic is structured as a test procedure with expected results followed by a list of things to check or tests to perform to help locate the problem if the expected test results are not observed.

Some notation and terminology:

- We use "Tx module" and "receiver" to refer to a mLRS module in the Tx/transmitter role and Rx/receiver role. In the use case assumed here, the Tx module will be installed in a EdgeTX or OpenTX radio handset, and the receiver will be mounted on the vehicle and connected to the flight controller.
- We use lower case "rx" and "tx" when refering to the receive and transmit pads or pins of a serial port connection.

## 1. Confirm successful firmware install

In most cases, you can confirm that mLRS firmware is installed by observing the LED.  When either a Tx module or receiver is powered on by itself, a LED (usually red) should flash at 2 Hz (twice per second, on for 1/4 second then off for 1/4 second repeatedly).

- If you don't see any LED activity, check power connections and voltage.
- If you don't see the expected LED pattern, follow the mLRS firmware install [documentation](https://github.com/olliw42/mLRS-docu?tab=readme-ov-file#stm32-hardware) for your hardware.
- If you have trouble reliably flashing via ST-Link, try shorter wires, 20 cm or less.

## 2. Confirm operation of the mLRS Lua script

Carefully install your Tx module into your EdgeTX or OpenTX radio.  Some Tx modules can be fussy on pin alignment; don't use excessive force or you may break something.  Follow the [instructions](LUA.md) to configure your radio and install the mLRS Lua script. Then, confirm you can talk to the Tx module via the Lua script.  You should see the TX module firmware version reported at the top of the screen.

- If the Lua script does not work, ensure you have installed the correct version.  There is a separate version for radios with a lower resolution black and white screens.
- Inspect the Tx module connector and ensure your Tx module is fully seated in the bay.
- Check that the external CRSF baud rate is set to 400k; this is the only speed supported by mLRS.
- If your Tx module is the older version of the [R9M](FRSKY_R9.md#r9m-versions), don't forget to do the Inverter Mod.

## 3. Confirm radio link between Tx module and receiver

When custom firmware with the same bind phrase or the pre-compiled firmware is installed on new or freshly erased Tx modules and receivers, they should connect as they will already be bound with the same bind phrase.

Power up a single Tx module and compatible receiver.

When the Tx module and receiver are bound and powered on, a LED (usually green) should flash more slowly at 1 Hz (once per second, on for 1/2 second then off for 1/2 second repeatedly) to indicate they are connected and exchanging radio messages.

You should also use the [mLRS Lua script](LUA.md) to confirm the radio link and firmware versions.  It is HIGHLY recommended to use the same firmware version on both the receiver and Tx module. The latest released firmware is also recommended, especially for new installs.

- If the radio link does not connect, follow the [Binding](BINDING.md) procedure.
- If the binding procedure doesn't establish the connection, verify that both the receiver and Tx module are compatible, which means they must be on the same band (2.4 GHz, 915/868 MHz or 433 MHz). In the case of 915/868 MHz, also check that the LoRa chipsets are [compatible](SX126x_SX127x_INCOMPATIBILITY.md).  For example, the FrSky R9 series and ELRS 900 MHz receivers are not compatible with the MatekSys 900 MHz hardware.
- Be sure you have flashed the correct [firmware file](https://github.com/olliw42/mLRS#firmware-flashing).  Files which start with tx are only for modules functioning in the Tx role and files which start with rx are only for modules functioning in the receiver role.  Also, pay attention to the variants for different use cases and hardware configurations.  For example, there are 3 separate files for different hardware and use case options for the MatekSys mR900-30 when used as a Tx module and a 4-th file for when the same hardware is used as a receiver.  A module with rx firmware flashed won't connect with any other module with rx firmware flashed and tx firmware won't connect with tx firmware.

## 4. Confirm MAVLink message flow from flight controller to receiver and Tx module

In EdgeTx/OpenTX go to MDL->TELEMETRY and select "Discover new sensors".  Then, scroll up using the scroll wheel and you should find a sensor named FM among several other sensors.  It should have a star flashing next to it indicating it is updating about once per second.  See the [CRSF](CRSF.md) documentation page for background info.

Above, you have already confirmed the radio link and communication between the Tx module and Edgetx/OpenTX.  So, if you don't see the FM sensor updating, this very likely indicates that the HEARTBEAT MAVLink message which is sent once per second by ArduPilot on all MAVLink interfaces is not reaching the receiver.

- Check your serial port wiring between the flight controller and the receiver to ensure you have connected serial rx on one board to serial tx on the other board in both directions and ground to ground.
- Use the mLRS Lua script or another configuration method to check your [mLRS receiver setup](CRSF.md#mlrs-rx-module-setup) to be sure "mavlinkX" or "mavlink" is selected for the "Rx Ser Link Mode" and that ["Rx Ser Baudrate"](PARAMETERS.md#rx-ser-baudrate) is correct and matches what you set in the following bullet.
- Use a USB connected ground control station to check your ArduPilot serial [configuration](CRSF.md#ardupilot-setup) to be sure the SERIALx_PROTOCOL is set to MAVLink2 and the SERIALx_BAUD are set for the correct serial port number (x), and ensure that the baud rate matches what you set the receiver to use in the previous bullet.
- If it is still not working, use a volt meter or oscilloscope to verify that both serial port wires between the mLRS receiver and flight controller have a voltage with respect to ground that is constantly changing.  If either wire has no changing signal, you have probably still missed something above.

## 5. Confirm MAVLink message flow from Tx module to ground station

Start your ground station software and connect to your Tx module by whatever method you have chosen.  You should see (MP) or hear (QGC) the flight mode.  If the parameter download also completes successfully, you can skip the next two topics.

This is a complex topic since there are so many ways to connect a Tx module to a ground station.

- Use the [mLRS Lua script](LUA.md#usage) or [CLI](CLI.md) to check that "Tx Ser Dest" is correct and that "Tx Ser Baudrate" matches your wireless bridge or ground control setting.
- If the data path between your Tx module and ground station includes a serial port, double check your serial port wiring between the Tx module and the ground station or wireless bridge; ensure you have connected serial rx on one board to serial tx on the other board in both directions and ground to ground.
- If your Tx module is the [R9M](FRSKY_R9.md#r9m-tx-module), don't forget to account for the inverted serial port and set dip switch 1 to "on" before powering up.
- If the ground station runs on a mobile device and is connected via USB, an OTG adapter may be required.
- If you want to connect via Bluetooth to the original [MatekSys mLRS Tx Module Kit](MATEKSYS.md), don't forget to enable the HC04 Bluetooth module by moving all three [dip switches](https://www.mateksys.com/?portfolio=mr900-30-tx#tab-id-2) to the "on" position.
- If the connection is via Bluetooth, the devices need to be paired by your operating system first.
- If the connection is via UDP or TCP over WiFi, connect to the WiFi access point before starting the ground station.

## 6. Confirm MAVLink message flow from receiver to flight controller

Use the mLRS Lua script or another configuration method to temporarily set ["Rx Snd RcChannel"](PARAMETERS.md#rx-snd-rcchannel) to "rc override".  If you use the mLRS Lua script there is no need to store; just press the RTN button after selecting "rc override".

Connect a ground station via USB directly to your flight controller and view the MAVLink messages.
With QGroundControl, use "Analyze Tools" -> "MAVLink Inspector" and select System 255 in the upper right.
With Mission Planner, Press Ctrl-F, select "MAVLink Inspector" and expand "Vehicle 255" -> "Comp 68" -> "RC\_CHANNELS\_OVERRIDE".

You should see the RC\_CHANNELS\_OVERRIDE message is being received at the same rate as your configured mLRS mode.  Note that this also confirms your Tx module is receiving RC channel data from your radio and sending it to the receiver.

- If you don't see these messages, double check your wiring to ensure that the correct serial tx output on the receiver module is connected to the correct rx input on your flight controller.

## 7. Confirm MAVLink message flow from ground station to flight controller

Using your ground station connected to your Tx module, verify that you can change flight modes (using the ground station, not the radio) or successfully download parameters.

- If you can't change flight modes or download parameters or issue other commands via the ground station, check your wiring to ensure that the correct serial tx output on your ground control device or wireless module or serial adapter is connected to the correct serial rx input on your Tx module.
- If flight mode changes initiated by the ground control system are correctly reported back to the ground control system and FM sensor, but parameter download fails, see [Confirm reliable message delivery](TROUBLE.md#Confirm reliable message delivery) below.

## 8. Confirm RC control is passed from the radio to the flight controller

Use the radio calibration page of your ground station (connected either via your Tx module or directly to USB) to verify all RC controls are working as expected.

- If you use "Rx Snd RcChannel" = "rc overwrite" setting instead of connecting a CRSF receiver output and are testing with QGroundControl, switch to Mission Planner or APM Planner 2.0 since QGroundControl doesn't show data from RC\_CHANNELS\_OVERRIDE MAVLink messages on this page.
- If the display doesn't follow stick movement and you use a CRSF connection between your receiver and your flight controller, check that you have connected the wire to the correct pins/pads on both your receiver and flight controller.
- For CRSF, check that you have correctly [configured ArduPilot](ARDUPILOT.md#crsf-receiver) to use this input.
- For CRSF, check that you have correctly [configured your receiver](CRSF.md#mlrs-rx-module-setup) for CRSF output with "Rx Out Mode" = "crsf".
- If your receiver [doesn't provide an RC output](ELRS_RECEIVERS.md#connections) or you don't want to use it, check that you have set ["Rx Snd RcChannel"](PARAMETERS.md#rx-snd-rcchannel) to "rc override".

## 9. Confirm reliable message delivery

Use your ground control station connected to your Tx module to examine the message loss rate both during parameter download and for a few minutes after it completes.

For QGroundControl, select "Application Settings" -> "MAVLink" and scroll down to "MAVLink Link Status".

For Mission Planner, select "Stats" in the upper right, move the windows so you can see both and then refresh parameters from the "full parameters" page.

You should see very few or no messages lost.

- If you see more than the occasional lost message or if parameter download takes more time than expected (8 to 60 seconds, depending on mode and ArduPilot version), check that the ["Rx Ser Link Mode"](PARAMETERS.md#rx-ser-link-mode) parameter is set to "mavlinkX" or "mavlink" and that ["Rx Snd Radiostat"](PARAMETERS.md#rx-snd-radiostat) is set to "ardu_1" or "meth_b".
- Depending on your ArduPilot version, it may help to adjust your [ArduPilot setup](CRSF.md#ardupilot-setup) to use the recommended baud rate between the receiver and flight controller; also adjust your configured stream rates as appropriate for your radio mode.
- Upgrade to a newer version of ArduPilot which may have fixed flow control issues.

## Range issues

If you don't see the range you expect, consider the following.

- Powering up a Tx module or receiver without an antenna connected may cause damage, especially at high output levels.
- When choosing and connecting antennas be aware of the difference between SMA and RP-SMA.  It is unfortunately possible to attach an RP-SMA antenna to an SMA jack but there will be no electrical connection of the signal (see previous bullet).
- If your vehicle allows, always use a vertical antenna orientation on both the Tx module and the receiver.  Especially with non-diversity systems.
- Be aware that calculated/estimated maximum ranges are free-space line of sight numbers and don't take into account obstructions or near-by objects such as trees and buildings.  Nor do they take into account RF noise from electronics on the craft or other users of the band.
- Not all antennas are created equal and some are surprisingly bad or just plain defective.
- Directional antennas, especially on the Tx module can increase or decrease range depending on antenna orientation.
- Metal, body parts, CF frames and wires near the antenna can cause reduced range.

## Fail-safe testing

It is critical to check and test your failsafe behavior and configuration ***before*** you experience a connection loss in flight.

- The "no signal" method is highly recommended.
- See ["Rx Failsafe Mode"](PARAMETERS.md#rx-failsafe-mode).
- See ArduCopter [Radio failsafe](https://ardupilot.org/copter/docs/radio-failsafe.html) documentation.

## Misc problems and non-problems

This section contains Frequently Answered Questions.

- There is no standard interpretation of RSSI values in MAVLink messages.
