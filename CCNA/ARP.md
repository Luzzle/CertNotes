#NetworkFundamentals #ccna-day6 #ccna-day29

### Definition
Used to find Layer 2 address from a known layer 3 address. 
If an ARP address is static in an ARP table it is a default entry.
If it is dynamic it is learnt from an ARP request.

ARP requests are **broadcast**
ARP replies are **unicast**

### Gratuitous ARP
ARP replies are sent without being requested. The frames are **broadcast** to `FFFF.FFFF.FFFF`.
