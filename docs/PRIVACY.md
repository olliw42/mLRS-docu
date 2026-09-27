# mLRS Documentation: Privacy #

([back to main page](../README.md))

mLRS provides encryption and authentication mechanisms to secure the over-the-air (OTA) communication using ChaCha20 and Poly1305 (since v1.4.04). These features are enabled through the common parameter "Privacy", which provides three settings with increasing security level:
 
| | encryption<br>nonce size | authentication<br>MAC size | serial data rate<br>reduction | secured<br>data | comment |
| --- | --- | --- | --- | --- | --- |
| level 1 | 3 bytes / 24 bits | --- | -3 bytes / -4.7% uplink / -3.7% downlink | serial data | only encryption |
| level 2 | 3 bytes / 24 bits | 3 bytes / 24 bits | -6 bytes / -9.4% uplink / -7.3% downlink | serial data | encryp. + auth. |
| level 3 | 4 bytes / 32 bits | 8 bytes / 64 bits | -12 bytes / -18.8% uplink / -14.6% downlink | RC + serial data | encryp. + auth. |

It should be noted that encryption alone does not prevent an attacker from spoofing or injecting messages and potentially taking control of the vehicle. Encryption does, however, prevent adversaries from eavesdropping on the data. For instance, it makes it practically impossible to determine GPS positions or other sensitive "personal" data. For most applications, the protection provided by level 1 should be sufficient, while the associated reduction in available data rate remains acceptable. Level 3, on the other hand, is intended to provide a similar level of security to that offered by signing MAVLink messages (signing messages takes a large toll on the data rate, might not be necessary).

> [!IMPORTANT]
> The mLRS privacy features are relatively new. We therefore do not claim that the current implementation is fully mature or free of vulnerabilities. The description on this page should be understood as a description of the design and its intended security properties, not as a security guarantee. We believe that the encryption implementation is sound. The integration of authentication is considerably more complex, and the current implementation should be expected to contain weaknesses or attack vectors (for instance, the current implementation does not yet include protection against replay attacks). Competent contributions aimed at identifying and closing such gaps are highly welcome.

> [!IMPORTANT]
> mLRS privacy features are not intended to meet the security requirements of high-security applications.

## Technical Details

ChaCha20-Poly1305 uses a key, a nonce, and a message authentication code (MAC). The key must remain secret, whereas the nonce and MAC can be public. In mLRS, the nonce and MAC are transmitted with each frame (reducing the usable payload). The nonce is incremented for each frame. Since a nonce must never be reused with the same key, the size of the nonce limits the maximum duration of a session. In 50 Hz mode, a 3-byte nonce implies a maximum runtime of 2^24 / 50 sec or 3.9 days; a 4-byte nonce provides a runtime of 2.7 years.

The key used in a session is 32 bytes (256 bits) in size and is constructed as follows:

Upon binding, a 32-byte key (static key) is constructed from the bind phrase, the hardware UIDs of the Tx module and receiver, and a 64-bit random number. This makes the static key specific to the user's configuration and particular pair of devices. Furthermore, each binding process results in a new static key. Importantly, because the material used for constructing the static key is exchanged during binding, the binding process must be performed in a secure environment. If there is any suspicion that the static key has been compromised, a new binding should be performed.

The actual key used in the communication - the session key - is created after power-up, when the Tx module and receiver establish their first connection. Another, fresh 64-bit random number is exchanged between the Tx module and receiver and protected using the static key, albeit with always the same nonce. This random number, which is specific to the session, is then used with the secrets established before during binding (bind phrase, Tx module and receiver UIDs, 64-bit random number) to derive the 256-bit session key. Consequently, each session uses a fresh secret key. 

Therefore, a new binding is not needed for each session. Furthermore, since the exchange of the session random number at first connection is secured with the static key, it can usually be considered secure. However, in this startup exchange the same nonce is always used, and an attacker who manages to spy several startups may compromise the static key.

mLRS uses the [Monocypher](https://monocypher.org/) cryptographic library.


