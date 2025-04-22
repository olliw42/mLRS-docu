# mLRS Documentation: Wireless Bridge #

([back to main page](../README.md))

mLRS supports a "wireless bridge" for providing wireless communication between the Tx module and a computer running GCS software such as Mission Planner. This allows for the operator to control the vehicle and have a GCS connection without being tethered to a computer.

The wireless bridge consists of an additional ESP32 or ESP8266/ESP8285 module, connected to one of the Tx module's serial port (often serial2), and additional hardware connections may exist for extended functionality. mLRS provides an Arduino sketch for creating the firmware to be loaded into the ESP32/ESP82xx chip (located [here](https://github.com/olliw42/mLRS/tree/main/esp/mlrs-wireless-bridge)).

The following wireless protocols are supported:

| chipset  | TCP | UDP | UDPCl | classic BT |
| ESP32 | x | x | x | x | x |
| ESP82xx | x | x | x | x | - |

For some Tx modules the wireless bridge can be configured from the Tx module, that is, via the CLI, Lua script or OLED (this depends on the specific hardware of the Tx module). Otherwise, the wireless bridge needs to be configured in the Arduino sketch and a new firmware be compiled and uploaded with each change.

## DIY Builds

### Hardware Selection & Configuration

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

In addition, any ESP8266 module will work. The sketch may have to be adapted slightly for a specific module however.

One of the serial ports of the Tx module will need to be connected to the ESP32/ESP82xx module using the pins specified in the boards.h file located [here](https://github.com/olliw42/mLRS/blob/main/esp/mlrs-wireless-bridge/mlrs-wireless-bridge-boards.h).

### Software Configuration

Configuration is done within the Arduino sketch, the following options can be set:

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

***Note***: The ESP8266/ESP8285 does not offer classic Bluetooth.