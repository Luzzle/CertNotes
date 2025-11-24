#ManagingVNETs

### Definition
Azure Load Balancer is an Azure service that allows you to evenly distribute incoming network traffic across a group of Azure VMs, or across instances in a Virtual Machine Scale Set. Load Balancer delivers high availability and network performance in the following ways:
- Load-balancing rules determine how traffic is distributed to instances that comprise the back end.
- Health probes ensure the resources in the back end are healthy and that traffic isn't directed to unhealthy back-end instances.

Azure Load Balancer operates at Layer 4.

You can deploy **public** load balancers and **internal** (or _private_) load balancers in Azure:

- _Public load balancers_ are used to load balance internet traffic to your virtual machines (VMs). A public load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the back-end pool VMs. For example, you can spread the load of incoming web-request traffic from the internet across multiple web servers. A public load balancer can also provide outbound connections for VMs inside your virtual network.
- An _internal load balancer_ directs traffic to resources that are inside a virtual network or that use a VPN to access Azure infrastructure. Internal load balancer front-end IP addresses and virtual networks are never directly exposed to an internet endpoint. Internal line-of-business (LOB) applications run in Azure and are accessed from within Azure or from on-premises resources. An internal load balancer is used where private IPs are needed at the front end only. Internal load balancers are often used to balance traffic from the front-end web tier infrastructure as a service (IaaS) VMs across a set of secondary VMs that perform tasks such as performing calculations or data processing.

#### Internal Load Balancer
An internal load balancer enables the following types of load balancing:

- **Within a virtual network**: Load balancing from VMs in the virtual network to a set of VMs that reside within the same virtual network.
- **For a cross-premises virtual network**: Load balancing from on-premises computers to a set of VMs that reside within the same virtual network.
- **For multi-tier applications**: Load balancing for internet-facing multi-tier applications where the back-end tiers aren't internet-facing. The back-end tiers require traffic load balancing from the internet-facing tier.
- **For LOB applications**: Load balancing for LOB applications that are hosted in Azure without added load balancer hardware or software. This scenario includes on-premises servers that are in the set of computers whose traffic is load balanced.

### Components
Load Balancer has several elements that work together to ensure an application's high availability and performance:

- Front-end IP
- Load balancer rules
	-  A load balancer rule defines how traffic is distributed to the back-end pool. The rule maps a given front-end IP and port combination to a set of back-end IP addresses and port combination.
- Back-end pool
	- The back-end pool is a group of VMs or instances in a Virtual Machine Scale Set that responds to the incoming request.
- Health probes
	- A health probe is used to determine the health status of the instances in the back-end pool. This health probe determines if an instance is healthy and can receive traffic. You define what is considered a healthy threshold.    
- Inbound NAT rules
	- You can use load balancing rules in combination with Network Address Translation (NAT) rules.
- High availability ports
	- A load balancer rule configured with `protocol - all and port - 0` is known as a _high availability (HA) port rule_. This rule enables a single rule to load balance all TCP and UDP flows that arrive on all ports of an internal standard load balancer.
- Outbound rules
	- An outbound rule configures Source Network Address Translation (SNAT) for all VMs or instances identified by the back-end pool.
- Session persistence
	- When you use session persistence, connections from the same client go to the same back-end instance within the back-end pool.

### Load Balancer Usage
#### When to use Azure LB
Azure Load Balancer is best suited for applications that require ultra-low latency and high performance. 
Load Balancer is suitable for your organization's needs because you're replacing existing network hardware devices that load balance traffic across applications.

#### When to not use Azure LB
Azure Load Balancer isn't appropriate if you have a web application that doesn't require load balancing running on a single IaaS VM instance.

Azure provides other load-balancing solutions as alternatives to Azure Load Balancer, including Azure Front Door, Azure Traffic Manager, and [[Azure Application Gateway]].