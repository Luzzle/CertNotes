#AzureCompute

### Availability Zones

|Category|Description|Examples|
|---|---|---|
|**Zonal services**|Azure _zonal_ services pin each resource to a specific zone.|- Azure Virtual Machines   <br>- Azure managed disks   <br>- Standard IP addresses|
|**Zone-redundant services**|For Azure services that are zone-redundant, the platform replicates automatically across all zones.|- Azure Storage that's zone-redundant   <br>- Azure SQL Database

### Availability Plan
An availability plan needs to include strategies for the following maintenance / downtime definitions.

**Unplanned Maintenance** - occurs when the Azure platform predicts that the hardware or any platform component associated to a physical machine is about to fail. Azure uses Live Migration technology to migrate your virtual machines from the failing hardware to a healthy physical machine.

**Unexpected downtime** - occurs when the hardware or the physical infrastructure for your virtual machine fails unexpectedly.

**Planned maintenance** - periodic updates made by Microsoft to the underlying Azure platform to improve overall reliability, performance, and security of the platform infrastructure that your virtual machines run on.

### Availability Set
An availability set is a logical feature you can use to ensure a group of related virtual machines are deployed together. The grouping helps to prevent a single point of failure from affecting all of your machines. 

The grouping ensures that not all of the machines are upgraded at the same time during a host operating system upgrade in the datacenter.

###### Characteristics
- All virtual machines in an availability set should perform the identical set of functionalities.
- All virtual machines in an availability set should have the same software installed.
- Azure ensures that virtual machines in an availability set run across multiple physical servers, compute racks, storage units, and network switches.

#### Fault Domain
A fault domain is a group of nodes that represent a physical unit of failure. Think of a fault domain as nodes that belong to the same physical rack.

- A fault domain defines a group of virtual machines that share a common set of hardware (or _switches_) that share a single point of failure. An example is a server rack serviced by a set of power or networking switches.
- Two fault domains work together to mitigate against hardware failures, network outages, power interruptions, or software updates.

#### Update Domain
An update domain is a group of nodes that are upgraded together during the process of a service upgrade (or _roll out_). 

An update domain allows Azure to perform incremental or rolling upgrades across a deployment. Here are some other characteristics of update domains.

- During planned maintenance, only one update domain is rebooted at a time.
- By default, there are five (non-user-configurable) update domains.    
- You can configure up to 20 update domains.

![[Pasted image 20251207133648.png]]