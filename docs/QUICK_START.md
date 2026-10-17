# mLRS Documentation: Quick Start Guide #

([back to main page](../README.md))

This page provides hints, suggestions and links to help get new users started with mLRS quickly.

This guide covers the use case where mLRS is used to provide a single radio link to carry both RC control and full bi-directional MAVLink telemetry.  When we discuss configuration of your flight controller, we assume you are running ArduPilot.  We also assume you use EdgeTX or OpenTX and that you will connect a ground station and/or use the [Yaapu Telemetry App](CRSF.md).

We expect that you are starting fresh and that all ArduPilot and mLRS parameters not covered here still have their default settings.

The steps here should be followed in order and when practical, we provide a way to confirm a step was completed successfully.

Some notation and terminology:
- We use "Tx module" and "receiver" to refer to a mLRS module in the Tx/transmitter role and Rx/receiver role. In the use case assumed here, the Tx module will be installed in a EdgeTX or OpenTX radio handset, and the receiver will be mounted on the vehicle and connected to the flight controller.
- We use lower case "rx" and "tx" when referring to the receive and transmit pads or pins of a serial port connection.

## 1. Choose and purchase a Tx module and a compatible receiver

There are many supported choices of mLRS hardware, including off-the-shelf options and some DIY designs.
We cover here three popular, commercially available, off-the-shelf Tx module options. The RF chipset used by your Tx module will determine which receivers are compatible. Don't mix Tx module and receiver between these three options except as noted. We summarize some pros and cons below to help you choose. 

### MatekSys mLRS [mR900-30-TX](https://www.mateksys.com/?portfolio=mr900-30-tx) module kit with their [mR900-30](https://www.mateksys.com/?portfolio=mr900-30) receiver
- These 900 MHz band modules were designed specifically for mLRS and arrive pre-flashed with mLRS.
- This option should provide the longest range of the three discussed here.
- The mR900-30-TX module kit includes an HC04 module for a convenient Bluetooth serial connection to your ground station software running on a computer or Android device.
- These modules are especially easy to flash via DFU over their USB-C connection using the [mLRS Web Flasher](https://olliw.eu/mlrsflasher) app.
- These use the SX126x LoRa chip and support 19 Hz, 31 Hz and FSK(50 Hz) modes.
- This option does not work with SX127x or SX128x based ELRS receivers, but it does work with LR1121 based receivers.
- The Tx module kit does not include an antenna or a JR bay case which must be 3D printed.  If you don't have access to a 3D printer, you can purchase a print from a number of 3D printing services and also from some vendors.

### MatekSys mLRS [mR24-30-TX](https://www.mateksys.com/?portfolio=mr24-30-tx) module kit with their [mr24-30](https://www.mateksys.com/?portfolio=mr24-30) receiver or any [Selected 2.4 GHz ELRS](ELRS_RECEIVERS.md#selected-elrs-receivers) receiver
- These 2.4 GHz band modules were also designed specifically for mLRS and arrive pre-flashed with mLRS.
- The mR24-30-TX module also includes the HC04 module.
- These modules are also especially easy to flash via DFU over their USB-C connection.
- 2.4 GHz is a wider band which might support more simultaneous users.  But this band can also be noisy so you may notice some interference including potentially from the HC04 if you use it.
- These modules support 19 Hz, 31 Hz, 50, and FLRC(111 Hz) modes.
- The Tx module kit does not include an antenna or JR bay case which must be 3D printed.  If you don't have access to a 3D printer, you can purchase a print from a number of 3D printing services and also from some vendors.
- If you don't need as much range, you can flash mLRS on one of the smaller and lighter [Selected 2.4 GHz ELRS](ELRS_RECEIVERS.md#selected-elrs-receivers) receivers such as the RadioMaster [RP4TD](ELRS_RADIOMASTER_RP4TD.md#mlrs-documentation-radiomaster-rp4td-receiver).
- This TX module will work with mLRS flashed on many 2.4 GHz ELRS modules including some AIO flight controller boards with a 2.4 GHz ELRS serial receiver.

### An ELRS TX module such as the [RadioMaster Nomad](ELRS_TX_MODULES.md##external-tx-modules) with a compatible receiver such as the [Bayck 915M Nano Pro](ELRS_RECEIVERS.md#selected-elrs-receivers) 900 MHz ELRS receiver
- This option is recommended for users who already have a supported [ELRS Tx module](ELRS_TX_MODULES.md) and [receiver](ELRS_RECEIVERS.md).  It is also recommended if you want a complete off-the-shelf, no assembly, solution.
- The Nomad is a fairly compact, low cost, 1 Watt external Tx module using the LR1121 LoRa chip.  It supports ELRS 900 MHz and 2.4GHz band receivers as well as the MatekSys receivers discussed above.  An LR1121 based internal Tx module found in some newer EdgeTX radio handsets can also be used.
- ELRS Tx modules can be [flashed](ELRS_TX_MODULES.md#flashing-external-tx-modules) via USB using the [mLRS Web Flasher](https://olliw.eu/mlrsflasher) app.
- The Bayck 915M Nano Pro, like most ELRS receivers, is not quite as easy to flash as the full power MatekSys.

## 2. Assemble your Tx module if required, and install antennas on both the receiver and Tx module

If you are using one of the MatekSys Tx module kits, print or purchase a JR bay case from the STL download available from [MatekSys](https://www.mateksys.com/?portfolio=mr900-30-tx#tab-id-1).

If you will use the MatekSys HC04 module to connect your ground station via Bluetooth, set all three [dip switches](MATEKSYS.md#tx-module-hc-04-bluetooth-notes) to the on position before assembling your Tx module.

When choosing and connecting antennas, be aware of the difference between SMA and RP-SMA.  It is, unfortunately, possible to attach an RP-SMA antenna to an SMA jack but there will be no electrical connection of the signal which could damage your module.

## 3. Connect your receiver to your flight controller

For the 1 Watt [MatekSys mLRS receivers](https://www.mateksys.com/?portfolio=mr24-30#tab-id-2):
- connect the receiver rx1 to a FC UART Tx.
- connect the receiver tx1 to the corresponding FC UART rx.
- Connect the receiver V pin to a 5 volt output on your FC.
- Connect the receiver G pin to a ground pad on your FC.
- If you will use CRSF for RC channels, connect the receiver tx2 to a different UART rx on your FC.

For most ELRS receivers, the [connections](ELRS_RECEIVERS.md#connections) are similar to those above except CRSF is not available.

Directly connect your ground station to your ArduPilot flight controller via a USB cable and configure the serial port (x) you wired to your receiver serial port.  Don't forget to press "Write Parameters" if your ground station requires this step.
- Set SERIALx\_PROTOCOL to "MAVLink2" (2).
- Set SERIALx\_BAUD to "57600" (57) (default mLRS "Rx Ser Baudrate").

If you will use CRSF or SBUS for RC channels, use your ground station to configure the serial port (x) you wired to your receiver RC output.
- Set SERIALx_PROTOCOL to "RCIN" (23).
- Set RC_PROTOCOLS to 536.
- Set RSSI_TYPE to 3.

## 4. Install firmware if required

If both your receiver and Tx modules came pre-installed with mLRS firmware as with the MatekSys mLRS modules, you can use the existing firmware unless you need a bug fix or feature which was added in a newer firmware version.

Carefully install your Tx module into the bay of your EdgeTX or OpenTX radio.  Some Tx modules can be fussy about pin alignment; don't use excessive force or you may break something.

Flashing Firmware is best done using the [mLRS Web Flasher](https://www.olliw.eu/mlrsflasher) on a Chromium based browser.

Once the firmware is installed, you can confirm operation by observing the LED.
- When either a receiver or Tx module is powered on alone, a LED (usually red) should flash at 2 Hz (twice per second, on for 1/4 second then off for 1/4 second repeatedly).
- When the Tx module and receiver are both powered on and bound, they will connect and a LED (usually green) should flash more slowly at 1 Hz (once per second, on for 1/2 second then off for 1/2 second repeatedly) to indicate they are connected and exchanging radio messages.

## 5. Install the mLRS Configurator Lua script and configure your mLRS system

Use the 'Lua Script' page on the [mLRS Web Flasher](https://www.olliw.eu/mlrsflasher) and follow the instructions to install the Lua script on your radio.

Start the mLRS Lua script from the SYS->TOOLS menu and confirm you can talk to the Tx module.  You should see the Tx module firmware version reported at the top of the screen.

Use the mLRS Lua script to confirm the receiver is connected and the firmware versions are recent enough to support the features you need.
- If the radio link does not connect, follow the [Binding](BINDING.md) procedure.
- It is HIGHLY recommended to use the same firmware version on both the receiver and Tx module. The latest released firmware is also recommended, especially for new installs.  If your receiver and Tx module firmware versions don't match or are very much out of date, return to the previous step and install the latest mLRS firmware release.

Use the mLRS Configurator Lua script to configure your mLRS system:
- Leave your receiver powered on and connected while you complete the following steps.
- Set the correct ["RF Band"](PARAMETERS.md#rf-band) for your region (if using 900 MHz hardware).
- You can change the ["Bind Phrase"](PARAMETERS.md#bind-phrase) if desired.
- Set your desired ["Mode"](PARAMETERS.md#mode).
- If you didn't connect the SBUS or CRSF RC output from your receiver to your flight controller, enter the "Edit Rx" page and set ["Rx Snd RcChannels"](PARAMETERS.md#rx-snd-rcchannel) to "rc override" (or "rc channels" for ArduPilot 4.6 with MAVLink RC receiver support).
- If your radio has a color screen, return to the main page and select Save. If you have a black and white screen, you will need to save before leaving the page. After saving, verify that your receiver reconnects.
- You may wish to review and adjust other settings at this time, but the defaults should be OK to get started.

## 6. Optionally, Install the Yaapu Telemetry script

You may wish to install the [Yaapu Telemetry script](https://github.com/yaapu/FrskyTelemetryScript) which uses the CRSF telemetry messages which mLRS generates on your Tx module from the MAVLink data it receives when the ["Rx Ser Link Mode"](PARAMETERS.md#rx-snd-radiostat) is set to "mavlinkX" or "mavlink".
- If you won't always use a ground station to set MAVLink stream rates when it starts up, be sure to set your ArduPilot [Stream Rate](CRSF.md#stream-rates) parameters.
- See the [Yaapu Wiki](https://github.com/yaapu/FrskyTelemetryScript/wiki) and [mLRS CRSF Telemetry](CRSF.md) page for details.

## 7. Connect a ground station to your mLRS Tx module

There are MAVLink ground station applications available for all common platforms including Windows, MacOS, Linux, Android, and iOS. We won't cover selecting a platform or installing a ground station here.  But we will provide some hints and suggestions for popular connection methods.

Wireless links are possible for all three of the recommended Tx modules.

Bluetooth is very handy for mobile devices and is recommended for the MatekSys Tx modules since they include an HC04 module which is automatically configured by mLRS.
- The [HC04](MATEKSYS.md#tx-module-hc-04-bluetooth-notes) support clasic Bluetooth Serial Profile and will be discoverable soon after being powered on.
- First, pair your HC04 (pin: 1234) or ESP32 with your device or computer.  Look for a device which includes "mLRS" in its name.
- Bluetooth LE is supported by some ELRS Tx modules which use the ESP32C3 for their backpack; this works with newer versions of QGroundControl on mobile platforms.
- QGroundControl works with clasic Bluetooth SP on Linux or Windows.  Create a new Bluetooth type connection via Application Settings -> Comm Links -> Add.
- Mission Planner is recommended for Windows.  Connect to the COM port associated with the Clasic Bluetooth SP connection after pairing.

UDP or TCP over WiFi is another popular wireless option.
- Most ELRS Tx modules support UDP or TCP over WiFi.
- All popular ground stations can connect via UDP.
- The standard ports for MAVLink are 14550 for UDP and 5760 for TCP.
- It is also possible to connect the MatekSys Tx module to an external ESP32 board such as the M5 Stamp boards running the [Wireless Bridge](WIRELESS_BRIDGE.md) sketch, but it must be configured in the sketch and compiled.

Some external Tx modules include serial ports which may be used to connect to your ground station.
- Standard PC serial ports and RS232 serial USB adapters use higher voltage levels than the logic level required for serial connections on Tx modules.  You will need a TTL level USB serial adapter to connect your Tx serial port to a PC or mobile device.
- The [MatekSys Tx modules](https://www.mateksys.com/?portfolio=mr24-30-tx#tab-id-2) provide 1 or 2 TTL level serial ports depending on the dip switch settings.

Direct USB connection is another useful option for both PCs and mobile devices which support OTG USB.
- This option is recommended for external 2.4 GHz ELRS modules to reduce RF interference.
- If you do this, you will want to use the mLRS lua Configurator script to set "Ser Port" to "com"
- This option does not work out of the box with the recommended MatekSys Tx modules for this use case because the USB port on these modules is not accessible when installed in a radio JR bay.
- It is possible to solder a type A USB cable directly to the USB pads on the back of the MatekSys Tx modules.
- If you solder a cable to these pads, you must then also use the soldered USB cable for flashing and not connect anything to the built-in USB-C jack.

## 8. Radio calibration

There are many calibration and setup steps required for ArduPilot on a new aircraft.  Here, we mention just the RC calibration step.  Not only because RC calibration needs to be repeated when switching to mLRS from a different RC system, but also because of a quirk you may encounter with older versions of QGroundControl.

- If you did not connect SBUS or CRSF RC output from your receiver to your flight controller and are using ["rc\_override"](PARAMETERS.md#rx-snd-rcchannel) for your RC, you can't use older versions of QGroundControl to calibrate your radio. You will need to use a newer version of QGroundControl or another ground station such as Mission Planner or APM Planner 2.0 to perform radio calibration.
- You can connect any of these ground stations via your mLRS Tx module or directly via USB to your flight controller for radio calibration.
- This is a good time to configure and check the operation of any flight modes and switches you might want.

## 9. Bench and range testing

Before your first flight with mLRS, it is good to do some additional testing to ensure everything is working as expected.

- Remove props and power everything up.
- Verify the receiver and Tx modules connect by observing the LEDs.
- Use the mLRS Lua script or CLI to set the ["Rx Power"](PARAMETERS.md#rx-power) and ["Tx Power"](PARAMETERS.md#tx-power) to the lowest setting.
- Start your ground station and verify that parameters download in a reasonable time depending on the mLRS mode (6-60 seconds).
- Verify that everything you expect such as attitude, GPS position, battery voltage, etc is being displayed correctly by both the ground station and Yaapu telemetry if you use it.  If you don't use Yaapu or don't see what you expect, check that you see the expected telemetry sensors on your radio (MDL -> TELEMETRY -> Discover new sensors)
- Ensure you can change flight modes and arm/disarm the aircraft from both your RC radio and your ground station.
- Perform a "walking range test" by leaving the aircraft behind while you walk away with the transmitter and ground station.
- If mLRS doesn't work as expected, see the [Troubleshooting](TROUBLE.md) page.
- Don't forget to set "Rx Power" and "Tx Power" back to a reasonable level before your first flight.

## 10. Failsafe configuration

Check and test your failsafe behavior and configuration ***before*** you experience a connection loss in flight.

- You may choose to configure ArduPilot for failsafe actions for loss of either MAVLink telemetry or radio control or both.
- Note that even though both MAVLink and RC are transported by mLRS in the same radio frames, the design is such that loss of radio control may occur at a slightly greater distance than loss of telemetry at the receiver.
- Note also that, of course, loss of MAVLink telemetry messages at the ground station may not occur at the same range as loss of MAVLink telemetry messages at the receiver, depending on the transmit power and RF conditions at either end of the radio link.  Thus, your ground station may report "communication lost" before or after ArduPilot initiates failsafe actions.
- The "no signal" method is highly recommended for RC failsafe.
- See ["Rx Failsafe Mode"](PARAMETERS.md#rx-failsafe-mode).
- See ArduCopter [Radio failsafe](https://ardupilot.org/copter/docs/radio-failsafe.html) documentation.

## 11. Optimizing mLRS

The above 10 steps should get you started with mLRS.  If something doesn't work, try the [Troubleshooting](TROUBLE.md) page.

Here are some additional things you should consider to improve your experience:
- Check your ArduPilot [Stream Rate](CRSF.md#stream-rates) parameters.  When you don't use a ground station, these may have to be set to get the MAVLink messages which radio telemetry sensors and Yaapu need.
- mLRS is constantly improving.  Update your firmware to get the latest features and bug fixes.  Your mLRS configuration parameters will normally be retained across firmware upgrade as long as you don't explicitly erase all flash.
- Upgrade ArduPilot; the latest release of ArduPilot may well work better with mLRS than older versions did.  The mLRS team and others contribute features and fixes to ArduPilot to improve operation with mLRS.
- Visit the mLRS [Discord server](https://discord.gg/vwjzCD6ws5) for help or to read about how others are using mLRS.
