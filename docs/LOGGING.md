# mLRS Documentation: Logging #

([back to main page](../README.md))

Logging radio link statistics can be helpful to understand performance and potentially debug any problems you are having. Two logging methods are described below:

1. EdgeTx/OpenTx Logging
2. ArduPilot Lua

## EdgeTx/OpenTx Logging ##

### Setup & Validation ###

1. Ensure that you have the link setup correctly and have completed the step to discover telemetry sensors.
2. Go to go to MDL->SPECIAL FUNCTIONS, click '+'.
3. Select the special function to assign, for example SF1.
4. For Trigger, it is typical to have the same switch used for arming, although any switch can be chosen.
5. For Function, select 'SD Logs'.
6. For Interval, 1.0 seconds is fine, this can be increased or decreased based on your preference.
7. Enable the special function.
8. To validate, enable logging using the switch previously assigned.  Wait a few seconds, then turn use the switch again to disable.  
9. Navigate to SYS->SD CARD, then choose the 'LOGS' folder.  If working as expected, you will see a CSV file with the model name and timestamp.

### Analysis ###

The logs are stored as CSV files on the SD card in the 'LOGS' folder, they can be extracted and and analyzed using your preferred tool - Excel, Python, Sheets, etc.

A good option is to use this browser based solution [here](https://maxbl4.github.io/otx/index.html).

## ArduPilot Logging ##

An ArduPilot Lua script has been developed which records link statistics as part of the flight controller log.  Note that this requires a flight controller with 2 MB of flash and 80 kB of memory (H7 and some F7 flight controllers).

### Setup & Validation ###

1. Download the Lua file from [here](https://github.com/olliw42/mLRS/blob/main/ardupilot_tools/mlrs_mavlink_link_stats.lua) and place in the /APM/SCRIPTS/ folder on the SD Card of your flight controller. If the /APM/SCRIPTS/ folder doesn't exist, you will need to create it.
2. On your flight controller, enable scripting by setting the parameter SCR_ENABLE to 1, then reboot the flight controller.
3. Set the following two parameters in mLRS:
    1. 'Rx Ser Link Mode' = 'mavlink' or 'mavlinkX' ('mavlinkX' should be preferred)
    2. 'Rx Snd RcChannel' = 'rc channels' (NOT 'rc override'!)
4. To validate, arm your flight controller for a few seconds, then disarm.
5. Check the /APM/LOGS/ folder on the SD Card of your flight controller, you should see a BIN file.

### Analysis ###

Analysis can be done in Mission Planner by following the steps [here](https://ardupilot.org/copter/docs/common-downloading-and-analyzing-data-logs-in-mission-planner.html#downloading-logs-via-mavlink).
