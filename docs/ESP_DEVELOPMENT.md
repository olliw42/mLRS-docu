# mLRS Documentation: Building and Flashing for ESP Devices #

([back to main page](../README.md))

Building the project for ESP platforms uses the Arduino Framework together with the [PlatformIO](https://platformio.org/) toolchain, which is an alternative to the original Arduino toolchain.

## Software ##

### Prerequisites ####

#### Windows ####

You need:
- An integrated development environment (IDE) to work with the code. The most popular choice on Windows is the [PlatformIO IDE](https://platformio.org/install/ide?install=vscode) which is nothing but a plugin for [Microsoft VSCode](https://code.visualstudio.com/).
- A recent [Python](https://www.python.org/downloads/windows/) installation.
- A recent [Tortoise Git](https://tortoisegit.org/) installation. Alternatively [Git for Windows](https://gitforwindows.org/) if you like to work in Git Bash.

#### Linux ####
Linux comes with Git and Python by default. The choice of IDE does not matter because we will use shell commands and explain the steps shortly.

1. Setup a virtual environment to not taint your system's python installation.
It does not matter where you create this but it makes sense to create it in the projects directory after you cloned it.

```
cd mLRS
python -m venv .venv
source .venv/bin/activate
```

2. Install the required python packages, empy and pexpect are named because modules like `dronecan` do not correctly specify
their dependencies.

```
pip install platformio dronecan setuptools empy==3.3.4 pexpect
```

### Clone the Sources ###

#### Windows ####
Both Git-for-Windows and Tortoise-Git come with Integration in Windows Explorer.
- Open Explorer and navigate to your workspace.
- Right Click and navigate throught the menu. Find Git -> Clone
- Paste the url `https://github.com/olliw42/mLRS.git` into the dialog and confirm.

Git Bash users follow the Linux section instead.

#### Linux ####
In Bash, navigate to your workspace and clone the repo recursively.
```
git clone --recursive https://github.com/olliw42/mLRS.git
```

### Preparing the Sources ###

In the mLRS directory, run the python setup script by entering the below command. This does three steps: initializes submodules (git submodule --init --recursive), copies ST drivers (not needed for ESP targets), and generates the MAVLink library files.
    - `python run_setup.py`
    - ***Note***: Ensure that the first and third steps are executed completely.

### Working with the Project in Platform IDE ###

In general, a project based on PlatformIO has a file called `platformio.ini` in the project directory.
Check out the [Quick Start Guide](https://docs.platformio.org/en/latest/integration/ide/vscode.html#quick-start).

Thus, the project is loaded into the IDE by selecting the base directory.
- Select `File->Open Folder`
- Navigate to the top directory of the repo where the `platformio.ini` file is located and confirm.
- Wait until the background tasks to finished. It may take a while as it installs compiler etc.

Interaction is done by the [Bottom Toolbar](https://docs.platformio.org/en/latest/integration/ide/vscode.html#ide-vscode-toolbar)
Find the [Project Environment Switcher](https://docs.platformio.org/en/latest/integration/ide/vscode.html#task-runner) which is the right-most item.
Environment in terms of PlatformIO is the target device.
It will show 'Default (mLRS)'. Select the appropriate environment for your device.

- To build the firmware, click the checkmark icon in the bottom bar.
    - ***Note***: When you hover over it should say 'PlatformIO: Build'
    - <img src="images/ESP_build.png">
- To prepare your receiver for flashing, you will need to connect it to a USB<>UART, follow the normal connections:
    - 5V to 5V
    - GND to GND
    - Tx to Rx
    - Rx to Tx
- When powering on the receiver you will need to have the bind button pushed down to enter into bootloader mode.
    - For receivers with a single (non-RGB) LED you can confirm the receiver is in bootloader mode if the LED is solid.
- To upload the firmware, click the right arrow icon in the bottom bar.
    - ***Note***: When you hover over it should say 'PlatformIO: Upload'
    - <img src="images/ESP_upload.png">
- Once the firmware has been written sucessfully, power cycle the receiver. The LED should blink to indicate that it is looking for a connection.
    - ***Note***: Binding can be done by holding down the button for four seconds.

### Building the Project from Console (LINUX) ###

The platformio package comes with the [pio](https://docs.platformio.org/en/latest/core/userguide/cmd_run.html) executable.
It is the build command of the toolchain. To verify your build environment does work, start building firmware for the most common ELRS 900Mhz receiver based on ESP32. Carefull, it does not use the same environment names as the ELRS project.

```
pio run --environment rx-generic-900
```

The trick is to find out what arguments to use for a specific task.
Browsing through the `platformio.ini` file usually finds the correct environment.
This one in particular builds and uploads to a specific serial port.

```
pio run --target upload --environment rx-generic-900 --upload-port /dev/ttyUSB0
```

