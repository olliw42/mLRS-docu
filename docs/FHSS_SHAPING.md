# mLRS Documentation: FHSS Shaping #

([back to main page](../README.md))

mLRS uses frequency hopping spread spectrum (FHSS) techniques. 

The number of frequencies used in the FHSS sequence depend on the RF band and the selected mode. For instance, in the 2.4 GHz band and for the 50 Hz mode, the FHSS sequence consists of 24 different frequencies. The frequency values and sequence are determined by the bind phrase. Choosing different bind phrases for each mLRS system allows one to operate several systems in the same RF band with minimized mutual interference.

In addition to the "bind phrase" mechanism, mLRS also provides the "except" and "ortho" mechanisms for altering the frequencies used in the FHSS sequence.

## "Except" Mechanism ##

This feature is available only in the 2.4 GHz band.

The 2.4 GHz band is crowded, especially by WiFi. Often, in a local area, WiFi predominantly occupies only one of the several possible Wifi channels, e.g., WiFi channel #6. The "except" mechanism allows for one to configure mLRS to *****exclude***** using the frequencies of a specific WiFi channel. Therefore, mLRS will not use this WiFi channel, which can help with reducing interference with WiFi.

The "except" setting can be:
- "\e-": normal behavior, no frequencies excluded
- "\e1": WiFi channel #1 excluded
- "\e6": WiFi channel #6 excluded
- "\e11: WiFi channel #11 excluded
- "\e13: WiFi channel #13 excluded

The WiFi channel which is excluded is determined by the last (6th) character of the bind phrase as follows: 'a' -> "\e-", 'b' -> "\e1", 'c' -> "\e6", 'd' -> "\e11", 'e' -> "\e13", and with 'f' the cycle starts over.


## "Ortho" Mechanism ##

The feature is available only for wide RF bands, such as the 2.4 GHz and 915 MHz FCC bands.

The "bind phrase" mechanism minimizes interference between different mLRS systems operating in the same RF band. However, the possibility of mutual interference is not strictly ruled out since the set of frequencies generated from different bind phrases can overlap. The "ortho" mechanism modifies the set of frequencies generated from a bind phrase into three further sets which are guaranteed to be strictly different (orthogonal). This allows for up to three mLRS systems to say stay out of each others way.

The "ortho" setting can be:
- "off": normal behavior
- "1/3": the 1st out of the three available frequency sets is used
- "2/3": the 2nd out of the three available frequency sets is used
- "3/3": the 3rd out of the three available frequency sets is used

In order to use the "ortho" mechanism, mLRS systems need to be configured with the same bind phrase, but use different settings for the "Ortho" parameter. "Ortho" should not be set to "off" for any of them.

Note: For systems operating in the 2.4 GHz band, the "ortho" mechanism can be combined with the "except" mechanism.

