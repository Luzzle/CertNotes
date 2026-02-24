#vcf9 

### Configurating Centralized Network Connectivity
[[Workload Domain - Networking#External Connectivity Types|Centralized network connectivity]] is compulsory for environments with the following requirements:
	- Supervisor cluster or VCF Automation
	- Advanced NAT configuration
	- DHCP
	- ESX hosts that do not share the same L2 VLAN

This requires the deployment of an NSX Edge cluster to host the T0 gateway and BGP or static routing configuration in the physical fabric.

This mode can be configured after the creation of a workload domain.

**Node** - The Tier 0 gateway is purely software based and exists to be a programmable entry to create edge nodes, grouped into edge clusters.

### N-VDS Configuration in VMware Cloud Foundation
When creating an NSX Edge cluster for a VMware Cloud Foundation VI workload, NSX Edge nodes are created with the following characteristics.

- A single N-VDS in each VM edge node.
- It carries both overlay and VLAN uplink traffic.
- Two TEPs are configured to provide load balancing for the overlay traffic.
- The management interface is connected to a distributed port group selected by the user during the deployment wizard.

### Validating the NSX Edge Cluster Deployment Status
You can monitor the NSX Edge cluster deployment from the vSphere Client.

On successful completion, the connectivity status must be Up and the status must be Success for each of the NSX Edge nodes.

If you need more details about the NSX Edge interface state and statistics, these detailsc an be viewed from the NSX UI.

Navigate to **System** > **Fabric** > **Nodes** > **Edge Transport Nodes** and select the edge.

##### CLI
SSH to edge node as **admin** user and run `get edge-cluster status` . This will not be available as root user.
Cluster state history can be viewed through running `get edge-cluster history state`.

Checking edge connectivity can be found by running `get interface fp-eth0 (example)`.
Edge performance can be viewed by running `get process`.

### Log Files
You can run the `get log-file <log_name>` command from the CLI to retrieve logging outputs that are available.

| Log Name | Log Type and Location                 |
| -------- | ------------------------------------- |
| auth.log | Authorization Log `/var/log/auth.log` |
| kern.log | Kernel log `/var/log/kern.log`        |
| syslog   | System log `/var/log/syslog`          |
