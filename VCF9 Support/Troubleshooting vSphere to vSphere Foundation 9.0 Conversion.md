#vcf9 

### Supportability and Serviceability Utility (SoS)

The SoS utility is not a debug tool, but it provides health check operations that can facilitate debugging a failed deployment.

To run, open an SSH connection to the VCF installer appliance using the admin account and `su`.

Navigate to `/opt/vmware/sddc-support` and enter `./sos` followed by the options required for your desired operation.

```
sos - Supportability and Serviceability Utility

Usage: ./sos [options]
	--help -h: Provides a summary of the available SoS tool options
	--version -v: Provides the Sos tools version number
	--debug-mode: Runs the SoS tool in debug mode
	--enable-stats: Enables collection of Sos execution stats
	--force: Allows SoS operations while workflows are running
	--history: Displays the last 20 SoS operations performed
	--log-dir <LOGDIR>: Specifies the directory to store logs
	--setup-json <SETUP_JSON>: Custom setup-json file for log collection
	--short: Displays health results only for failures and warnings
	--skip-known-host-check: Skips the specified check for SSL thumbprints for hosts in the known hosts file
	--zip: Creates a zipped tar file for the output
	
	Log File Operations
	--api-logs: Collects output from APIs
	--vcf-installer-logs: Collects VCF Installer appliance support logs
	--esx-logs: Collects logs from the ESX hosts only
	--no-clean-old-logs: Use this option to prevent the tool from removing any output from a previous collection run.
	--no-health-check: Skips the health check executed as part of log collection
	--sddc-manager-logs: Collects logs from the SDDC Manager only
	--vc-logs: Collect logs from the vCenter instances only
	--vm-screenshots: Collects screenshots from all VMs
```

SoS writes the output to `/var/log/vmware/vcf/sddc-support`. This can be used to generate a log bundle for detailed diagnosis and troubleshooting purposes.

##### Log Identifiers

Logs can get intermingled, meaning it can be difficult to seperate logs of system and user initiated events.

Log identifiers allow you to identify the logs of a particular event, such as the creation of a workload domain. Log identifiers are consistent across all log files.

### Log Files

| Stage                           | Appliance Log Location | Location                                                                                                                                                |
| ------------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| vSphere Foundation Installation | VCF Installer          | `/var/log/vmware/vcf/domainmanager/domainmanager.log`                                                                                                   |
| vCenter Deployment              | VCF Installer          | `/var/log/vmware/vcf/domainmanager/ci-installer-[id]/workflow_[id]/vcsa-cli-installer.log`<br><br>`/var/log/vmware/vcf/domainmanager/domainmanager.log` |
| vSphere Cluster Configuration   | VCF Installer          | `/var/log/vmware/vcf/domainmanager/domainmanager.log`                                                                                                   |
| VCF Operations Deployment       | VCF Installer          | `/var/log/vmware/vcf/domainmanager/domainmanager.log`<br><br>`/var/log/vmware/vcf/domainmanager/vcf-ops-ovf-tool-[id].log`                              |

---

The `domainmanager.log` file provides information about the VCF Operations appliance deployment. The information includes details such as power on, disk provisioning state, portgroup connectivity, appliance IP, DNS, gateway etc...

The `vcf-ops-ovf-tool-<id>.log` file tracks information about on which ESX host the VCF Operations appliance has been deployed, as well as information about the appliance such as OS Name, VMware Tools Status, IP, MAC and so on.
