#vcf9 

### Overview

Upgrading from VCF 5.2 to 9.0 involves 2 phases.

1. Upgrading Aria components to the VCF Fleet 9.0 management component.
2. Upgrading VCF 5.2 components.
	- SDDC Manager
	- NSX Manager
	- vCenter
	- ESXI

The following components are **not** automatically upgraded to VCF 9.0:
- VMware Tools
- Telegraf Agents
- VM Hardware
- Distributed Switch

### Using SoS

To collect all logs use the `--collect-all-logs` option.

Mentioning the `--domain-name` option is very important otherwise SoS is only performed on the management domain.

SoS log collection can time out after 60 minutes.

### Failed Upgrade

You can check the log files for failed upgrades to help troubleshoot and resolve issues.

1. Open an SSH connection to the VCF Installer (flip) or SDDC manager appliance with the VCF username and password.
2. To access upgrade logs, navigate to `/var/log/vmware/vcf/lcm`
	- `lcm-activity.log`: Contains information level logging.
	- `lcm-debug.log`: Contains debug-level logging information.