#SecurityFundamentals #ccna-day53 

### Overview
A 'site to site' VPN is a VPN between 2 devices and is used to connect 2 sites together over the internet.

A VPN 'tunnel' is created between the two devices by encapsulating the original IP packet with a VPN header and a new IP header.
The original packet is fully encrypted before encapsulation.

The tunnel is only formed between 2 tunnel endpoints, meaning each device does not need to configure a VPN. The routers will automatically encrypt the packets.
### Process
1) Sending router combines the original packet and session key and runs through an encryption formula.
2) Sending device encapsulates the packet.
3) Packet is sent over the internet to the other side of the tunnel.
4) Receiving router decrypts the data to get the original packet and then forwards the original packet to its destination.

### GRE over IPsec
Generic Routing Encapsulation (GRE) creates tunnels like IPsec, however does not encrypt the original packet so it is not secure.

However it can encapsulate a wider variety of L3 protocols as well as broadcast and multicast packets.

### DMVPN
Dynamic Multipoint VPN (DMVPN) is a cisco-developed solution that allows routers to dynamically create a full mesh of IPsec tunnels without having to manually configure each tunnel.

1) Configure IPsec tunnels to hub site.
2) The hub router gives each router info to form an IPsec tunnel with each other router.