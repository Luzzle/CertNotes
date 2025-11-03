#ManagingVNETs

### Definition
A Virtual Network (VNET) is a logical isolation of Azure resources. Each VNET has its own CIDR block and can be linked to other VNETs and on-premises networks.

[[Public IP Addresses]]
#### Subnets
- Each subnet has its own range of IP addresses that fall within the VNETs CIDR block. 
- Azure reserves 5 IP addresses within a subnet (example network 192.168.1.0/24):
	- `192.168.1.0` - Network address
	- `192.168.1.1` - Reserved as default gateway
	- `192.168.1.2` and `192.168.1.3` - Mapped to the VNET DNS IP addresses.
	- `182.168.1.255` - Broadcast
-