#NSE4 

### Overview

IPsec is a suite of separate protocols:

| Protocol                                 | Description                                                                                                                        |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **[[Internet Key Exchange (IKE)]]**      | Used to authenticate peers, exchange keys and negotiate the encryption and checksums that are used. This is the *control channel*. |
| **Authentication Header (AH)**           | Checksums that verify the integrity of the data. This is not used by FortiGate                                                     |
| **Encapsulating Security Payload (ESP)** | The encapsulated security payload. The data channel.                                                                               |
##### Ports
**[[Internet Key Exchange (IKE)|IKE]]** - UDP 500
**[[Internet Key Exchange (IKE)|IKE]] NAT-T** - UDP 4500

### Modes
**Transport Mode** - Directly encapsulates and protects the 4th layer and above. It does not protect the original IP header and does nto add an additional IP header.

**Tunnel Mode** - It encapsulates the entire IP packet and adds a new IP header at the beginning.