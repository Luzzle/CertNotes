#NetworkFundamentals #ccna-day53 

### Overview
**CE** - Customer Edge Router
**PE** - Provider Edge Router
**P** - Provider Router

MPLS networks are shared infrastructure many customers connect to and share to make WAN connections.

When the PE routers receive frames from the CE routers, they add a label to the frame.
These labels are used to make forwarding decisions within the provider network.
![[Pasted image 20250531162907.png]]

### Peerings
#### Layer 3 VPN
The CE and PE routers will peer using OSPF, and will learn about each others routes using this peering.

#### Layer 2 VPN
The service provider network is entirely transparent in this case, in effect it is like the 2 CE routers are directly connected. 
	The 2 WAN interfaces are in the same subnet.

If a [[Dynamic Routing]] protocol is used, they will directly peer with each other.