#vcf9 

### Architecture

VMware Cloud Foundation (VCF) integrates [[Troubleshooting New Deployment - vSphere Foundation|compute]], storage, networking, operations and automation into a unified software-defined data center platform.

VMware Cloud Foundation offers the following benefits:
- Allows you to build a private cloud model
- Provides a central interface to manage licensing certificates and other critical workflows.
- Automates the life cycle management of all VCF components
- Enables users to consume IaaS as and platform services through a unified cloud experience.

#### Private Cloud Components
A VCF private cloud is the highest level of management and consumption for the underlying software-defined data center resources.

A VCF private cloud contains of one or more VCF fleets.
- A VCF fleet is an environment managed by a single set of fleet-level management components (VCF Operations and VCF automation).
- This is comprised of:
	- A single VCF operations instance
	- A single VCF automation instance
	- One of more VCF instances

![[Pasted image 20260124142149.png]]

Everything is build and deployed through the VMware Cloud Foundation Installer.

##### VCF Installer Main Screen
Before you proceed you must:
1. Review the prerequisites
2. Download the vSphere Foundation Binary Files from an online or offline depot.
	- To download an offline depot, use the VCF download tool to download the binaries to a computer with access to the internet.

#### Management Domain Storage Options
The management domain can be configured with one of the following storage types:

1. **vSAN**
	- Software-defined storage built into the hypervisor.
2. **VMFS over Fibre Channel**
	- high-speed protocol that sends SCSI commands across a SAN.
3. **Network File System (NFS)**
	- File-sharing protocol to access files on NAS devices.

#### NSX
NSX provides consistent networking across private clouds, public clouds and containers.

NSX offers a complete layer 2 to layer 7 software-defined networking stack, including switching, routing and other services such as NAT and VPN.

#### VCF Operations
The VCF Operations layer includes the following components.

- SDDC Manager provides API access to the VCF infrastructure.
- Appliances:
	- The VCF operations appliance is the administrative console for the VCF environment.
	- The Operations Collector appliance collects and ingests inventory and performance data, providing insights into the health, capacity and performance of VCF components.
- VCF Operations fleet management is responsible for configuring VCF unified SSO certificate, password management, licensing and life cycle management of all VCF instances.

#### VCF Automation
VCF Automation enables a flexible self-service consumption of VCF infrastructure. This allow us to automate IaaS.

#### Deployment Models
The VCF installer provides 2 deployment models for the NSX Manager, VCF Operations and VCF Automation appliances.

- **Simple (single node)**: deploys only one NSX manager node, one VCF operations node and a VCF Automation node. Each are given a virtual ip (except the operations node), even if only one node is deployed.
- **High Availability (three nodes)**: Deploys in a 3 node cluster for high availability, each cluster assigned a virtual IP, with the VCF Operations cluster using an external load balancer.

### Installation Process
1. ESX Hosts Preparation
2. vCenter Deployment
3. SDDC Manager Deployment
4. Configuring the vSphere Cluster
5. NSX Deployment and Configuration
6. VCF Fleet Management Deployment and Configuration
7. VCF Operations Deployment and Configuration
8. VCF Automation Deployment and Configuration


### Log Locations
![[Pasted image 20260124150658.png]]
![[Pasted image 20260124150732.png]]

