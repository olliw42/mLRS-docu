# mLRS Documentation: Building and Flashing for STM32 Devices #

([back to main page](../README.md))

mLRS uses STM32CubeIDE for STM32 targets. The following procedure should work.

In case of issues with this procedure, don't hesitate to join the discussion thread at rcgroups or the discord channel.

## Software: Installation Bits and Bops ##

Let's assume that the project should be located in the folder `C:/Me/Documents/Github/mlrs`.

### Dependencies ###

For the first step (step I) you need to have git and Python3 installed. Depending on the Python3 distribution you may need to install further libraries.

### Clone and setup the project files (Step I) ###

1. open a command line processor
2. cd into `C:/Me/Documents/Github` (not C:/Me/Documents/Github/mlrs !)
3. `git clone https://github.com/olliw42/mLRS.git mlrs`
4. `cd mlrs`
5. run `run_setup.py`. This does four steps: Initializes submodules (git submodule --init --recursive), copies ST HAL and LL drivers to the target folders, generates the MAVLink library files, and finally generates the DroneCAN library files.
    - ***Note***: Ensure that all four steps are executed completely.

For cloning you of course can use any other tool you like.

### STM32CubeIDE (Step II) ###

1. download and install STM32CubeIDE
    - ***Note***: Install into the default folder if possible.
2. start STM32CubeIDE
3. in Launcher select Workspace by hitting [Browse...] button, and browse to `C:/Me/Documents/Github/mlrs/mLRS`. Hit [Launch] button.
    - ***Note***: It is not C:/Me/Documents/Github/mlrs but C:/Me/Documents/Github/mlrs/mLRS! If you proceed with the wrong path then there will be a compile error "undefined reference to main_main()"!
4. in the IDE's top bar go to `File->Open Projects from File System`
5. in the Importer select Import source by hitting [Directory...] button, and browse to the desired project. E.g. select `C:/Me/Documents/Github/mlrs/mLRS/rx-diy-board01-f103cb`. Hit [Finish] button.
6. change from Debug to Release configuration: Go to the 'hammer' icon in the top icon bar, click on the down arrow right to it, and select `Release`.
    - ***Note***: If you don't do that then there will be a compile error "undefined reference to main_main()"!
7. open the file `mlrs-rx.cpp` or `mlrs-tx.cpp` into the editor
8. compiling should work now: Go to the green 'right-pointing triangle' icon in the top icon bar and click it
9. repeat steps 4. - 8. for each board you are interested in

<img src="https://user-images.githubusercontent.com/6089567/154903396-25f62bf6-573a-4b80-9720-a0ad4a21f291.jpg" width="480">

The STM32CubeIDE has its weirdness, so you may have to get used to it. 




