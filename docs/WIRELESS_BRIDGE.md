# mLRS Documentation: Wireless Bridge #

([back to main page](../README.md))

mLRS provides an Arduino sketch which enables ESP32 or ESP8266 development modules to be used as a wireless bridge providing communication between the Tx module and a computer running GCS software such as Mission Planner. This allows for the operator to control the vehicle and have a GCS connection without being tethered to the computer.

Sketch locations:
- esp32: [here](https://github.com/olliw42/mLRS/tree/main/esp/mlrs-wireless-bridge)
- esp8266: [here](https://github.com/olliw42/mLRS/tree/main/esp/mlrs-wireless-bridge-esp8266)

## Hardware Selection & Configuration

### ESP32

Any ESP32 module will work, however, several modules are pre-configured and available as options within the sketch. These include:

- Espressif ESP32-DevKitC V4
- NodeMCU ESP32-Wroom-32
- Espressif ESP32-PICO-KIT
- Adafruit QT Py S2
- Lilygo TTGO-MICRO32
- M5Stack M5Stamp C3 Mate
- M5Stack M5Stamp Pico
- M5Stack M5Stamp C3U Mate
- M5Stack ATOM Lite

The serial port (or one of the serial ports) of the Tx module will need to be connected to the ESP32 module using the pins specified in the boards.h file located [here](https://github.com/olliw42/mLRS/blob/main/esp/mlrs-wireless-bridge/mlrs-wireless-bridge-boards.h).

### ESP8266

Any ESP8266 module will work, the sketch may have to be adapted slightly for a specific module however.

## Software Configuration

Configuration is done within the sketch, the following options can be set:

- Module Type
- Serial Level
- Wireless Protocol
- WiFi SSID
- WiFI Password
- IP Address
- TCP Port
- UDP Port
- WiFi Channel
- WiFi Power
- Bluetooth Device Name
- Baudrate

Note: The ESP8266 and some EPS32 do not offer BlueTooth.