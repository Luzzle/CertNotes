#vcf9 

### Overview
**Prerequisites for ESX host commissioning**
- Hosts must be pre-imaged with the correct ESX version.
- Host names must be resolvable in DNS.
- Storage type cannot be change after the host is commissioned.
- Network pools must exist before you commission hosts.
- Hosts can be commissioned individually or in bulk.
- NTP and Syslog must be enabled.

The following must be provided:
- FQDN
- Storage Type
- Network pool name
- Host root password

[[vMotion and DRS]]
[[vSphere HA]]

[[ESX Host Troubleshooting]]
[[vCenter Monitoring & Troubleshooting]]
[[Virtual Machine Troubleshooting]]

### Monitoring Compute
**VCF Health** - provide detailed information about VCF components grouped per component.

**VCF Storage Operations** - Provides a single console to view the entire storage infrastructure regardless of storage type.

**VCF Operations** - provides a centralized log location across all components.
	- **Diagnostic Findings** provides a graphical representation of alerts categorized by severity. Within this *findings catalog* lists potential issues that can impact your environment with guidance for remediation.
		- This can also be used for providing diagnostic reports for vSphere clusters using health checks against known issues.
	- VCF Operations provides reports that display the overall health and utilization of ESX hosts as well as VM level monitoring.

### Virtual Machines
You can use `vim-cmd vmsvc/[command]` to perform commands on virtual machines on a host.

In vCenter a VM can have one of several connectivity states:
- **Connected** - vCenter can access the VM.
- **Disconnected** - VM host is disconnected.
- **Inaccessible** - One of more VM configuration files are inaccessible.
- **Invalid** - The VM configuration file is invalid.
- **Orphaned** - The VM exists in the vCenter database but is no longer present in the ESX host inventory.

A VM includes a set of files located in a datastore, controlled by the ESX host it is registered to.
- **.vmx** - configuration file
- **.nvram** - bios file
- **-rdm.vmdk** - Raw device map file
- **.vmdk** - Disk descriptor file
- **-flat.vmdk** - Disk data file
You can use `vim-cmd vmsvc/get.filelayout <vmid>` to list all files for the VM

#### Snapshots
If a VM has snapshots, the content ID (CID) and parent CID values in the disk description file help ensures the integrity of the VM snapshot chain.

Some products require file systems to be quiesced before a snapshot operation for purposes of backup and data integrity.

Quiescing is the process of suspending all IO operations to the file system to ensure the snapshot is consistent and stable, this can be performed by the Microsoft VSS service.

#### Templates
A template is a static image of a VM that can be used to provision new VMs. They can specify the following:
	- Guest OS
	- Applications
	- Hardware Configuration
	- VMware Tools

### Content Libraries
Content Libraries are repositories of OVF templates and other file types that can be synchronised across vCenter systems globally.

Content Libraries can be one of the following types:
- **Local** - Content controlled by the administrator.
- **Published** - A local library that is available for subscription.
- **Subscribed** - A library that synchronises with a published library.