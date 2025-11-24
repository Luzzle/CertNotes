#ManagingVNETs

### Definition
A Virtual Network (VNET) is a logical isolation of Azure resources. Each VNET has its own CIDR block and can be linked to other VNETs and on-premises networks.

[[Public IP Addresses]]
[[Network Security]]
[[Network Virtual Appliance (NVA)]]
[[Azure DNS]]
#### Subnets
- Each subnet has its own range of IP addresses that fall within the VNETs CIDR block. 
- Azure reserves 5 IP addresses within a subnet (example network 192.168.1.0/24):
	- `192.168.1.0` - Network address
	- `192.168.1.1` - Reserved as default gateway
	- `192.168.1.2` and `192.168.1.3` - Mapped to the VNET DNS IP addresses.
	- `182.168.1.255` - Broadcast

- Every subnet has the following default system routes:

| Address prefix                | Next hop type   |
| ----------------------------- | --------------- |
| Unique to the virtual network | Virtual network |
| 0.0.0.0/0                     | Internet        |
| 10.0.0.0/8                    | None            |
| 172.16.0.0/12                 | None            |
| 192.168.0.0/16                | None            |
| 100.64.0.0/10                 | None            |

### Hub and Spoke
When you deploy a hub-and-spoke network, the hub virtual network can host infrastructure components like a network virtual appliance (NVA) or Azure VPN gateway. 

All the spoke virtual networks can then peer with the hub virtual network. Traffic can flow through NVAs or VPN gateways in the hub virtual network.
![[Pasted image 20251123144950.png]]


### User Defined Routes (UDRs)
Virtual network peering enables the next hop in a user-defined route to be the IP address of a virtual machine in the peered virtual network, or a VPN gateway

When creating user-defined routes, you can specify these next hop types:

- **Virtual appliance**: A virtual appliance is typically a firewall device used to analyze or filter traffic that is entering or leaving your network. You can specify the private IP address of a Network Interface Card (NIC) attached to a virtual machine so that IP forwarding can be enabled. Or you can provide the private IP address of an internal load balancer.
- **Virtual network gateway**: Use to indicate when you want routes for a specific address to be routed to a virtual network gateway. The virtual network gateway is specified as a VPN for the next hop type.
- **Virtual network**: Use to override the default system route within a virtual network.
- **Internet**: Use to route traffic to a specified address prefix that is routed to the internet.
- **None**: Use to drop traffic sent to a specified address prefix.

### BGP
Typically, you use BGP to advertise on-premises routes to Azure when you're connected to an Azure datacenter through Azure ExpressRoute. You can also configure BGP if you connect to an Azure virtual network by using a VPN site-to-site connection.

If there are multiple routes with the same address prefix, Azure selects the route based on the type in the following order of priority:

1. User-defined routes
2. BGP routes
3. System routes