# mLRS Documentation: Binding #

([back to main page](../README.md))

For a Tx module and a receiver to be able to connect to each other, some parameters (the common parameters) need to be set to equal values in both the Tx module and the receiver. For an arbitrary receiver this can be achieved by binding.

Both the Tx module and the receiver will need to be put into bind mode, there are multiple ways to do this:

- For the Tx module you have four options: 
    1. Press the bind button (for ca. 4 seconds) on the Tx module.
    2. Enter bind mode via the 'bind' CLI command.
    3. Enter bind mode via the mLRS Lua script.
    4. If available, enter bind mode via the OLED display.
- For the receiver you have two options:
    1. Press the bind button (for ca. 4 seconds) on the receiver.
    2. Power cycle the receiver quickly 3 times, the receiver will then enter bind mode.

The sequence doesn't matter, i.e., one can first press the bind button on the receiver and then set the Tx module into bind mode.

When in bind mode, the green and red LEDs will blink alternatively with ca 2.5 Hz.

When a receiver is connected to a Tx module, the common parameters as well as all other parameters can be changed and stored permanently by issuing a save command either via the CLI (pstore; command), the mLRS Lua script (Save button), or the OLED display if available (STORE option).

Note: When flashing mLRS to new hardware or after performing a factory reset (e.g. by a full chip erase) the Tx module and receiver should usually connect immediately as they will be bound already (i.e. both have the default bind phrase of 'mlrs.0', default mode and default frequency band).

The following video shows the various LED blink pattern: 

[![mLRS: LED Blink Patterns](https://img.youtube.com/vi/M_49QP8oxBk/0.jpg)](https://www.youtube.com/watch?v=M_49QP8oxBk "mLRS: LED Blink Patterns")