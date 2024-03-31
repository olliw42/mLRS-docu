# mLRS Documentation: Compiling and Flashing for ESP82xx and ESP32 Devices #

([back to main page](../README.md))

For ESP82xx and ESP32 devices, the project is using [PlatformIO](https://platformio.org/) in combination with [VSCode](https://code.visualstudio.com/).

## Software: Installation Bits and Bops

Let's assume that the project should be located in the folder C:/Me/Documents/Github/mlrs.

### Opening the mLRS Project

- in the VSCode IDE top bar go to 'File->Open Folder'. ***Note***: it is 'Open Folder', not 'Open File' or any other option
- in the Open Folder dialog browse to `C:/Me/Documents/Github/mlrs`. Hit [Select Folder] button. ***Note***: it is not C:/Me/Documents/Github/mlrs/mLRS but C:/Me/Documents/Github/mlrs! If you proceed with the wrong path then there will be all sorts of issues which you want to avoid. As a general rule: It's always the folder which contains the 'platformio.ini' file.
- wait until PlatformIO/VSCode have done their thing. ***Note***: be patient, this can take a while. You may need internet connection. You will see plenty of notifcation boxes showing up. Most of them are irrelevant and you can just close them (or wait until they disappear).
- in the bottom bar find the field which shows 'Switch PlatformIO Project Environment' when you hover over it. Click on it, which will open a menu in to top, and select the environment you want.

## Firmware: Flashing