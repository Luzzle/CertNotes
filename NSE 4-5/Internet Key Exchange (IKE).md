#NSE4 

### Overview

| Feature                    | IKEv1                                                                                                                       | IKEv2                                                                                       |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Exchange Modes             | - Main: Total messages: 9 (6 for phase 1, 3 for phase 2).<br>- Aggressive: Total messages: 6 (3 for phase 1, 3 for phase 2) | Single exchange procedure: Total messages - 4 (one child SA only).                          |
| Authentication Methods     | Symmetric:<br>- Pre-shared key (PSK)<br>- Certificate signature<br>- Extended authentication (XAuth)                        | Asymmetric:<br>- PSK<br>- Certificate signature<br>- EAP (pass-through - no client support) |
| NAT-T                      | Supported as extension                                                                                                      | Native support                                                                              |
| Reliability                | Unrealiable - messages are not acknowledged                                                                                 | Reliable - messages are acknowledged                                                        |
| Dial-up phase 1            | - Peer ID + aggressive mode + PSK<br>- Peer ID + main mode + certificate signature                                          | - Peer ID<br>- Network ID                                                                   |
| Traffic selector narrowing | Not supported                                                                                                               | Supported                                                                                   |
