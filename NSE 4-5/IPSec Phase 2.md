#NSE4 

### Overview
Phase 2 negotiates two unidirectional IPsec SA's for ESP.

Phase 2 does not end when ESP begins, but instead periodically renegotiates IPsec SA's to maintain security. If you enable **Perfect Forward Secrecy (PFS)**, everytime P2 expires, FortiGate uses DH to recalculate new secret keys. In this way, new keys are not derived from older keys.

Each P1 can have multiple P2's, in case you want to use different encryption keys for each subnet whos traffic is crossing th tunnel. FortiGate selects a P2 based on what matches the traffic.

### Configuration
**Auto Negotiate** - The Fortigate wll automatically negotiate new SA's right before the current SA's expire. This prevents traffic disruptiuon by the IPsec SA registration.

**Autokey Keep Alive** - The Fortigate will periodically send keep alive packets over the tunnel to keep it up, even if there is no traffic flow.

