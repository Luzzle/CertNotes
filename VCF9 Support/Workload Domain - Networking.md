#vcf9 

### Overview
##### Network Pool

A network pool is a range of IP addresses for specific services that VCF assigns to hosts that participate in a workload domain. VCF assigns IP addresses for the following network types:

- vMotion
- vSAN
- NFS
- iSCSI

You must provide the following information when creating a network pool:
- VLAN ID
- MTU settings
- Network for each network type
- Subnet for each network type
- Gateway settings
- Range of IPs

#### External Connectivity Types
There are two types of External Connections that serve different requirements.

**Distributed Network Connectivity**
- For this configuration all that is required is a VLAN that is available to all ESX hosts NICs. That VLAN requires access to the rest of the network.
- All of this connectivity is based on a "Default Project" in NSX. NSX provides multiple projects for per-tenant configuration, with each project having its own Transit Gateway.
- The transit gateway is then connected to a physical gateway to facilitate the connection assigned to this VLAN.
- The transit gateway will break out into multiple Virtual Private Cloud (VPC) gateways which house subnets for each VM.
- An external IP from the VLAN is required for internet access, which is then NAT'd 1:1 to VMs in the VPC subnets.

**Centralised Network Connectivity**
- For this configuration, a Tier 0 gateway is created by NSX, connected to each NSX projects transit gateway.
- The T0 gateway will have edge nodes that associate with the Physical Gateway to the rest of the network, which can provide BGP connectivity.
- This configuration allows for Advanced NAT and Load Balancing.
- Each subnet is automatically SNAT'd.

#### Prerequisites
**Distributed Network Connectivity**
- Configure a dedicated VLAN and subnet to connect the Transit Gateway with the ToR switch.
- On the physical gateway, disable ICMP redirect for the VLAN configured to connect the Transit Gateway with the external gateway. The external gateway must allow traffic between ESX host over that VLAN.
- Reserve an external IP block for VPC external connectivity. This must be the same or within the dedicated VLAN subnet.

**Centralised Network Connectivity**
- For all NSX Edge Nodes:
	- An available VLAN for Tunnel Endpoint (TEP) interfaces. You can reuse the same VLAN as the ESX host TEPs.
	- Enough CPU and memory in the workload domain cluster.
	- The NSX edge management network must have connectivity to the NSX Manager.
	- DNS entries for each of the NSX Edge nodes.
- Routing configuration:
	- If using dynamic routing, BGP must be configured on the ToR switch, which includes 2 BGP peers with its corresponding IP interfaces and local ASN.
- VPC:
	- Reserve an external IP block.

##### Active=Standby Mode
An active-standby Tier-0 gateway configuration is required for the following capabilities and use cases:
- vSphere Supervisor cluster
- VCF Autoamtion modern experience (IaaS)

**The vSphere Supervisor cluster activation fails if the Tier-0 gateway is configured in active-active mode.**