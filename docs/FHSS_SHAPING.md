# mLRS Documentation: FHSS Shaping #

([back to main page](../README.md))

mLRS uses frequency hopping. 

The number of frequencies which are used in the hopping depend on the RF band and the selected mode. For instance, in the 2.4 GHz band and for the 50 Hz mode, the FHSS sequence consists of 24 different frequencies. The frequency values and their sequence however are determined by the bind phrase. This allows for one to operate several mLRS systems in the same RF band with minimized mutual interference, by choosing different bind phrases for each system.

In addition to this "bind phrase" mechanism for affecting the frequencies used in the FHSS sequence, mLRS also provides the "except" and "ortho" mechanisms.


## "Except" Mechanism ##

This feature is available only in the 2.4 GHz band.

The 2.4 GHz band is crowded and especially used by WiFi. Often, in a local area, the WiFi communication occupies predominantly only one of the several possible Wifi bands, e.g., WiFi band #6. The "except" mechanism allows for one to configure mLRS such that it is *****not***** using frequencies which are in a particular WiFi band. mLRS so to say stays outside of this WiFi band. This can help with reducing interference with WiFi.

The "except" setting can be:
- "\e-": normal behavior, no frequencies excluded
- "\e1": WiFi band #1 excluded
- "\e6": WiFi band #6 excluded
- "\e11: WiFi band #11 excluded
- "\e13: WiFi band #13 excluded

The WiFi band which is excluded is determined by the last (6th) character of the bind phrase as follows: 'a' -> "\e-", 'b' -> "\e1", 'c' -> "\e6", 'd' -> "\e11", 'e' -> "\e13", and with 'f' the cycle starts over.


## "Ortho" Mechanism ##

The feature is available only for wide RF bands, such as the 2.4 GHz and FCC 915 MHz bands.

The bind phrase mechanism minimizes interference between different mLRS systems operating in the same RF band. However, the possibility of mutual interference is not strictly ruled out since the set of frequencies generated from different bind phrases can overlap. The "ortho" mechanism modifies the set of frequencies generated from a bind phrase such that for up to three mLRS systems the frequencies are guaranteed to be strictly different (orthogonal). The mLRS systems then so to say stay out of each others way.

The "ortho" setting can be:
- "off": normal behavior
- "1/3": the 1st out of the three available frequency sets is used
- "2/3": the 2nd out of the three available frequency sets is used
- "3/3": the 3rd out of the three available frequency sets is used

In order to use the "ortho" mechanism, the two or three mLRS systems need to be configured with equal bind phrases, but differ in their setting for the "Ortho" parameter (and "Ortho" should not be set to "off" for any of them).

For systems operating in the 2.4 GHz band, the "ortho" mechanism can be combined with the "except" mechanism.

