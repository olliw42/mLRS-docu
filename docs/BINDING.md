# mLRS Documentation: Binding #

([back to main page](../README.md))

For a Tx module and a receiver to be able to connect to each other, some parameters (the common parameters) need to be set to equal values in both the Tx module and the receiver. For an arbitrary receiver this can be achieved by binding.

The binding procedure is as follows:

1. On the Tx side you have three options: (i) press the bind button (for ca. 4 seconds) on the Tx module, (ii) initiate the binding via a CLI command, or (iii) initiate the binding via the mLRS configuration Lua script. If available, the binding can also be initiated via the OLED display.
2. Press the bind button (for ca 4 seconds) on the receiver.

The sequence doesn't matter, i.e., one also can first press the bind button on the receiver and then set the Tx module into binding mode.

When in binding mode, the green and red LEDs will blink alternatively with ca 2.5 Hz.

When a receiver is connected to a Tx module, the common parameters (as well as all other parameters) can be changed and stored permanently by issuing a save command either via the CLI (pstore; command) or the mLRS configuration Lua script (Save button), or the OLED display if available (STORE option).

The following video shows the various LED blink pattern: 

[![mLRS: LED Blink Patterns](https://img.youtube.com/vi/M_49QP8oxBk/0.jpg)](https://www.youtube.com/watch?v=M_49QP8oxBk "mLRS: LED Blink Patterns")
