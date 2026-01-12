#NSE4

[[FortiGate Interfaces]]
[[FortiGate Monitoring]]

### Life of a Packet
![[Pasted image 20251214093221.png]]

### Modes
#### NAT Mode
- FortiGate acts as a router
- Interfaces have IP Addresses
- Packets are routed by IP

Interfaces cannot be used until they have an IP address.

[[FortiGate Routing|Routing]]

#### Transparent Mode
- FortiGate is a layer 2 switch or bridge
- Interfaces do not have IP Addresses
- Cannot route packets, only forward or block

### Default Settings
- **Default Management IP**: 192.168.1.99/24
- Ping, SSH and HTTPS is open by default
- Built in DHCP enabled on port1

Testing123


