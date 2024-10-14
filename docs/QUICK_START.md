# mLRS Documentation: Quick Start Guide #

([back to main page](../README.md))

This page provides hints, suggestions and links to help get new users started with mLRS quickly.

This guide covers the use case where mLRS is used to provide a single radio link to carry both RC control and full bi-directional MAVLink telemetry.  When we discuss configuration of your flight controller, we assume you are running ArduPilot.  We also assume you use EdgeTX or OpenTX and that you will connect a ground station and/or use the [Yaapu Telemetry App](CRSF.md).

We expect that you are starting fresh and that all ArduPilot and mLRS parameters not covered here still have their default settings.

The steps here should be followed in order and when practical we provide a way to confirm a step was completed successfully.

Some notation and terminology:
- We use "Tx module" and "receiver" to refer to a mLRS module in the Tx/transmitter role and Rx/receiver role. In the use case assumed here, the Tx module will be installed in a EdgeTX or OpenTX radio handset, and the receiver will be mounted on the vehicle and connected to the flight controller.
- We use lower case "rx" and "tx" when referring to the receive and transmit pads or pins of a serial port connection.

## 1. Choose and purchase a Tx module and a compatible receiver

There are many supported choices of mLRS hardware, including off-the-shelf options and many DIY designs.
We cover here three popular but mutually incompatible commercially available off-the-shelf options.  We summarize some pros and cons below to help you choose. Don't mix Tx module and receiver between these options.

### MatekSys mLRS [mR900-30-TX](https://www.mateksys.com/?portfolio=mr900-30-tx) module kit with their [mR900-30](https://www.mateksys.com/?portfolio=mr900-30) receiver
- These 900 MHz band modules were designed specifically for mLRS and arrive pre-flashed with mLRS.
- This option should provide the longest range of the three discussed here.
- The mR900-30-TX module kit includes an HC04 module for a convenient Bluetooth serial connection to your ground station software running on a computer or Android device.
- These modules are especially easy to flash via DFU over their USB-C connection.
- These use the SX126x LoRa chip and support 19 Hz, 31 Hz and FSK(50 Hz) modes.
- This option does not work with any ELRS receivers.
- The Tx module kit does not include an antenna or a JR bay case which must be 3D printed.  If you don't have access to a 3D printer, you can purchase a print from a number of 3D printing services and also from some vendors.
- The [mR900-22](https://www.mateksys.com/?portfolio=mr900-22) is a compatible lower power receiver which is appropriate for smaller vehicles.  But it is not currently recommended for new users because it is not yet easy to flash without disconnecting it from your flight controller.

### MatekSys mLRS [mR24-30-TX](https://www.mateksys.com/?portfolio=mr24-30-tx) module kit with their [mr24-30](https://www.mateksys.com/?portfolio=mr24-30) receiver or any [Selected 2.4 GHz ELRS](ELRS_RECEIVERS.md#selected-elrs-receivers) receiver
- These 2.4 GHz band modules were also designed specifically for mLRS and arrive pre-flashed with mLRS.
- The mR24-30-TX module also includes the HC04 module.
- These modules are also especially easy to flash via DFU over their USB-C connection.
- 2.4 GHz is a wider band which might support more simultaneous users.  But this band can also be noisy so you may notice some interference including potentially from the HC04 if you use it.
- These modules support 19 Hz, 31 Hz, 50, and FLRC(111 Hz) modes.
- The Tx module kit does not include an antenna or JR bay case which must be 3D printed.  If you don't have access to a 3D printer, you can purchase a print from a number of 3D printing services and also from some vendors.
- If you don't need quite as much range, you can flash mLRS on one of the smaller and lighter [Selected 2.4 GHz ELRS](ELRS_RECEIVERS.md#selected-elrs-receivers) receivers such as the RadioMaster RP4TD.
- Some AIO flight controller boards include a low power 2.4 GHz ELRS serial receiver which can also be flashed with mLRS for use with this Tx module.

### FrSky [R9M Tx module](FRSKY_R9.md#r9m-tx-module) with the [Bayck 915M Nano Pro](ELRS_RECEIVERS.md#selected-elrs-receivers) 900 MHz ELRS receiver
- This option is not highly recommended for new users as it is more complicated and slightly less flexible, but is included here since it allows use of 900 MHz ELRS receivers you may already have.
- This Tx module uses the SX1276 LoRa chip and supports only 19 Hz mode.  It works with many 900 MHz ELRS receivers but is incompatible with the MatekSys gear above.
- The FrSky R9M can be flashed using your EdgeTX or OpenTX radio.
- No 3D printer is required, but transmit power should be limited to less than 500 mW unless you add a fan.
- The Bayck 915M Nano Pro ELRS receiver can be [flashed](ELRS_RECEIVERS.md#flashing) with mLRS firmware without removing it from your vehicle by using ArduPilot serial passthrough.
- If you already have a R9MX or R9MM receiver, they are also compatible, but have lower power and are more difficult to [flash](FRSKY_R9.md#flash-r9-receivers-with-elrs-bootloader).
- Unfortunately, the R9M has inverted serial port signals; if you choose this option you will probably also want to purchase an [ESP32 module](FRSKY_R9.md#esp32-wireless-bridge) such as the [M5 Stamp Pico Mate](https://shop.m5stack.com/products/m5stamp-pico-diy-kit) to use as a wireless bridge and handle the inverted serial port.

## 2. Assemble your Tx module if required and install antennas on both the receiver and Tx module

If you are using one of the MatekSys Tx module kits, print or purchase a JR bay case from the STL download available from [MatekSys](https://www.mateksys.com/?portfolio=mr900-30-tx#tab-id-1).

If you will use the MatekSys HC04 module to connect your ground station via Bluetooth, set all three [dip switches](MATEKSYS.md#tx-module-hc-04-bluetooth-notes) to the on position before assembling your Tx module.

If you are using the [R9M Tx module](FRSKY_R9.md#r9m-tx-module):
- Set [dip switch 1](FRSKY_R9.md#r9m-tx-module) to the on position to configure it for serial data.
- Install the [Arduino IDE](https://www.arduino.cc/en/software) and use it to build and flash [firmware](WIRELESS_BRIDGE.md) on your ESP32 module.  Be sure to select the R9M variant for your module when you edit the mlrs-wireless-bridge.ino.
- Connect your [ESP32 wireless bridge](https://FRSKY_R9.md#esp32-wireless-bridge) module to the serial and power pins of your R9M.

When choosing and connecting antennas be aware of the difference between SMA and RP-SMA.  It is, unfortunately, possible to attach an RP-SMA antenna to an SMA jack but there will be no electrical connection of the signal.

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

[Flashing firmware](https://www.mateksys.com/?portfolio=mr24-30-tx#tab-id-3) to MatekSys mLRS modules with USB is especially easy via the [mLRS Web Flasher](https://mlrs.xyz/flash/) on a Chromium based browser.

For the R9M Tx module, it is recommended to [Flash via EdgeTx/OpenTx](FRSKY_R9.md#flash-the-r9m-module-with-elrs-bootloader) which is a 2 step process:

- First, [Flash the ELRS Bootloader](FRSKY_R9.md#flash-the-elrs-bootloader).
- Next, use your EdgeTX/OpenTX radio to [Flash the mLRS Firmware](FRSKY_R9.md#flashupdate-the-mlrs-firmware).

To flash ELRS receivers, you can use esptool or a Chromium based browser as instructed [here](ELRS_RECEIVERS.md#flashing).

Once the firmware is installed, you can confirm operation by observing the LED.
- When either a receiver or Tx module is powered on alone, a LED (usually red) should flash at 2 Hz (twice per second, on for 1/4 second then off for 1/4 second repeatedly).
- When the Tx module and receiver are both powered on and bound, they will connect and a LED (usually green) should flash more slowly at 1 Hz (once per second, on for 1/2 second then off for 1/2 second repeatedly) to indicate they are connected and exchanging radio messages.

## 5. Install the mLRS Lua script and configure your mLRS system

Follow the [instructions](LUA.md) and copy the correct mLRS Lua script to the SCRIPTS\TOOLS folder on your SD card and setup your RC radio external module.

Start the mLRS Lua script from the SYS->TOOLS menu and confirm you can talk to the Tx module.  You should see the Tx module firmware version reported at the top of the screen.

Use the mLRS Lua script to confirm the receiver is connected and the firmware versions are recent enough to support the features you need.
- If the radio link does not connect, follow the [Binding](BINDING.md) procedure.
- It is HIGHLY recommended to use the same firmware version on both the receiver and Tx module. The latest released firmware is also recommended, especially for new installs.  If your receiver and Tx module firmware versions don't match or are very much out of date, return to the previous step and install the latest mLRS firmware release.

Use the mLRS Lua script to configure your mLRS system:
- Leave your receiver powered on and connected while you complete the following steps.
- Set the correct ["RF Band"](PARAMETERS.md#rf-band) for your region (if using 900 MHz hardware).
- You can change the ["Bind Phrase"](PARAMETERS.md#bind-phrase) if desired.
- Set your desired ["Mode"](PARAMETERS.md#mode).
- If you didn't connect the SBUS or CRSF RC output from your receiver to your flight controller, enter the "Edit Rx" page and set ["Rx Snd RcChannels"](PARAMETERS.md#rx-snd-rcchannel) to "rc override" (or "rc channels" for ArduPilot 4.6 with MAVLink RC receiver support).  Return to the main page.  If your radio has a black and white screen, you will need to use the [CLI](CLI.md) for this.
- Select "Save" and verify that your receiver reconnects.
- You may wish to review and adjust other settings at this time, but the defaults should be OK to get started.

## 6. Optionally, Install the Yaapu Telemetry script

You may wish to install the [Yaapu Telemetry script](https://github.com/yaapu/FrskyTelemetryScript) which uses the CRSF telemetry messages which mLRS generates on your Tx module from the MAVLink data it receives when the ["Rx Ser Link Mode"](PARAMETERS.md#rx-snd-radiostat) is set to "mavlinkX" or "mavlink".
- If you won't always use a ground station to set MAVLink stream rates when it starts up, be sure to set your ArduPilot [Stream Rate](CRSF.md#stream-rates) parameters.
- See the [Yaapu Wiki](https://github.com/yaapu/FrskyTelemetryScript/wiki) and [mLRS CRSF Telemetry](CRSF.md) page for details.

## 7. Connect a ground station to your mLRS Tx module

There are MAVLink ground station applications available for all common platforms including Windows, MacOS, Linux, Android, and iOS. We won't cover selecting a platform or installing a ground station here.  But we will provide some hints and suggestions for popular connection methods.

Wireless links are possible for all three of the recommended Tx modules.

Bluetooth is very handy for mobile devices and is recommended for the MatekSys Tx modules since they include an HC04 module which is automatically configured by mLRS.
- The [HC04](MATEKSYS.md#tx-module-hc-04-bluetooth-notes) will be discoverable soon after being powered on.
- Bluetooth is also supported by some ESP32 boards such as the [M5 Stamp Pico Mate](https://shop.m5stack.com/products/m5stamp-pico-diy-kit) which is recommended for use with the [FrSky R9M Tx module](FRSKY_R9.md#esp32-wireless-bridge).
- First, pair your HC04 (pin: 1234) or ESP32 with your device or computer.  Look for a device which includes "mLRS" in its name.
- iOS devices do not support the Bluetooth Serial Port Profile and QGroundControl does not support Bluetooth LE so QGroundControl will not connect over Bluetooth on iOS.  It has been reported that the SidePilot App works on iOS.
- QGroundControl works well with Bluetooth on Android, Linux or Windows.  Create a new Bluetooth type connection via Application Settings -> Comm Links -> Add.
- Mission Planner is recommended for Windows.  Connect to the COM port associated with the Bluetooth connection after pairing.

UDP or TCP over WiFi is another popular wireless option.
- All three of the recommended Tx modules could be connected to an external ESP32 board such as the M5 Stamp boards running the [Wireless Bridge](WIRELESS_BRIDGE.md) sketch.
- All popular ground stations can connect via UDP.
- The standard ports for MAVLink are 14550 for UDP and 5760 for TCP.

All three of the recommended Tx modules include serial ports which may be used to connect to your ground station.
- PC serial ports and RS232 serial USB adapters use higher voltage levels than the logic level required for serial connections on Tx modules.  You will need a TTL level USB serial adapter to connect your Tx serial port to a PC or mobile device.
- The [MatekSys Tx modules](https://www.mateksys.com/?portfolio=mr24-30-tx#tab-id-2) provide 1 or 2 TTL level serial ports depending on the dip switch settings.
- The FrSky R9M shares its single inverted serial port between CLI and MAVLink based on the position of [dip switch 1](FRSKY_R9.md#r9m-tx-module) at power on.  A [method](FRSKY_R9.md#diy-inverter-dongle) to invert the signals will be required.

Direct USB connection is another useful option for both PCs and mobile devices which support OTG USB.
- Unfortunately this option is not available with the FrSky R9M.
- This option does not work out of the box with the recommended MatekSys Tx modules for this use case because the USB port on these modules is not accessible when installed in a radio JR bay.
- It is possible to solder a type A USB cable directly to the USB pads on the back of the MatekSys Tx modules.
- If you do this, you will need to flash the "siktelem" version of the firmware for your MatekSys Tx module.
- If you solder a cable to these pads, you must then also use the soldered USB cable for flashing and not connect anything to the built-in USB-C jack.

## 8. Radio calibration

There are many calibration and setup steps required for ArduPilot on a new aircraft.  Here, we mention just the RC calibration step.  Not only because RC calibration needs to be repeated when switching to mLRS from a different RC system, but also because of a quirk you may encounter.

- If you did not connect SBUS or CRSF RC output from your receiver to your flight controller and are using ["rc\_override"](PARAMETERS.md#rx-snd-rcchannel) for your RC, you can't use QGroundControl to calibrate your radio. You will need to use another ground station such as Mission Planner or APM Planner 2.0 to perform radio calibration.
- You can, of course, connect any of these ground stations via your mLRS Tx module or directly via USB to your flight controller.
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
- Note that even though both MAVLink and RC are transported by mLRS in the same radio frames, the design is such that loss of radio control will probably occur at a slightly greater distance than loss of telemetry at the receiver.
- Note also that, of course, loss of MAVLink telemetry messages at the ground station may not occur at the same range as loss of MAVLink telemetry messages at the receiver, depending on the transmit power and RF conditions at either end of the radio link.  Thus, your ground station may report "communication lost" before or after ArduPilot initiates failsafe actions.
- The "no signal" method is highly recommended for RC failsafe.
- See ["Rx Failsafe Mode"](PARAMETERS.md#rx-failsafe-mode).
- See ArduCopter [Radio failsafe](https://ardupilot.org/copter/docs/radio-failsafe.html) documentation.

## 11. Optimizing mLRS

The above 10 steps should get you started with mLRS.  If something doesn't work, try the [Troubleshooting](TROUBLE.md) page.

Here are some additional things you should consider to improve your experience:
- Check your ArduPilot [Stream Rate](CRSF.md#stream-rates) parameters.  When you don't use a ground station, these have to be set to get the MAVLink messages which radio telemetry sensors and Yaapu need.
- mLRS is constantly improving.  Update your firmware to get the latest features and bug fixes.  Your mLRS configuration parameters will normally be retained across firmware upgrade as long as you don't explicitly erase all flash.
- Upgrade ArduPilot; the latest release of ArduPilot may well work better with mLRS than older versions did.  The mLRS team and others contribute features and fixes to ArduPilot to improve operation with mLRS.
- Visit the mLRS [Discord server](https://discord.gg/vwjzCD6ws5) for help or to read about how others are using mLRS.
