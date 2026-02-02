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

### Monitoring Compute

**VCF Health** - provide detailed information about VCF compoentns grouped per component.

**VCF Storage Operations** - Provides a single console to view the entire storage infrastructure regardless of storage type.

**VCF Operations** - provides a centralized log location across all components.
	- **Diagnostic Findings** provides a graphical representation of alerts categorized by severity. Within this *findings catalog* lists potential issues that can impact your environment with guidance for remediation.
		- This can also be used for providing diagnostic reports for vSphere clusters using health checks against known issues.
	- VCF Operations provides reports that display the overall health and utilization of ESX hosts as well as VM level monitoring.

[[ESX Host Troubleshooting]]
[[vCenter Monitoring & Troubleshooting]]
[[Virtual Machine Troubleshooting]]