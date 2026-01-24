#vcf9

### Architecture
vSphere Foundation is the workload engine that provides an enterprise class hyper-converged infrastructure solution. The solution combines compute (vSphere) and storage (vSAN) virtualisation with built in Kubernetes orchestration (VKS) and intelligent [[Troubleshooting New Deployment - VMware Cloud Foundation#VCF Operations|operations (VCF Operations)]].

The VCF installer is used for the initial deployment of the vSphere Foundation. This accepts manual configuration data entry using a UI wizard, or using a pre-populated deployment specification JSON file as input.

#### Components
- ESX - Compute platform in which you create and run VMs and other workloads.
- vCenter - The service used to manage multiple ESX hosts and provide capabilities such as vSphere vMotion, HA and DRS.

vSAN is a policy based storage management solution to create storage pools for use in virtualisation.

vSphere Kubernetes Service (VKS) is an enterprise-grade Kubernetes platform that allows you to easily deploy, manage and scale containerised applications. VKS has the following benefits:
- Simplified cluster deployment and management.
- Consistency for different on-prem environments.
- Allows the team to focus on the applications rather than the infrastructure.
- Foundation for deploying cloud-native technologies.

![[Pasted image 20260124132857.png]]

### Troubleshooting New Deployment

#### Installation Process
1. **ESX Hosts preparation**
	- Perform an interactive ESX 9.0 installation.
	- Configure VLAN ID of the ESX host management network.
	- Configure VLAN ID of the VM network.
	- Configure NTP.
	
	*Troubleshooting vSAN preparation:*
	Search for `PrepareEsxiContractAction` in domain manager log.
	
	*Troubleshooting ESX DNS configuration*
	Search for `ReconfigureHostDNSAction` in domain manager log.
	
	*Troubleshooting Network Port Group configuration*
	Search for `CreateVmPortGroupAction` in domain manager log.

2. **vCenter deployment**
	- The vCenter appliance is deployed to the **first ESX host** of the vSphere cluster.
	- vCenter is connected to the VM network port group on the ESX host VSS.
	- A vSAN data store is configured on the ESX host to store the vCenter appliance files.
	- First boot scripts are run on the vCenter appliance.
	
	*Troubleshooting vCenter deployment*
	Search for `DeployVcAction` in the domain manager log.

3. Configuring the vSphere cluster
	- A new data centre and vSphere cluster are created on the vCenter system.
	- All ESX hosts are added to the vSphere cluster.
	- A vSphere Distributed Switch is created for all hosts in the vSphere cluster.
	- VMs are migrated to the VM Management distributed port group.
	- ESX host management NICs are migrated to the vSphere Distributed Switch.
	- vSAN data store is expanded to all host in the vSphere cluster.
	- HA and DRS are configured in the cluster.
	
	*Troubleshooting Distributed Switch Creation*
	Search for `CreateDVSAction` in the domain manager log.
	
	*Troubleshooting vSAN cluster creation*
	Search for `CreateVsanClusterAction` in the domain manager log.
	
	*Troubleshooting Distributed Switch creation*
	Search for `CreateDvsAction` in the domain manager log.
	
	*Troubleshooting Portgroup creation*
	Search for `BaseCreatePortGroupAction` in the domain manager log.
	
	*Troubleshooting VM migration*
	Search for `MigrateVmsToDifferentPortGroup` in domain manager log.

4. VCF Operations Deployment and Configuration
	*Troubleshooting VCF Operations deployment*
	Search for `VcfOpsDeployAction` in domain manager log.

#### Log Files

ID is usually a timestamp.

| Stage                         | Log Location                                                                                                                                        |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| VVF Installation              | `/var/log/vmware/vcf/domainmanager/domainmanager.log`                                                                                               |
| vCenter Deployment            | `/var/log/vmware/vcf/domainmanager/domainmanager.log`<br>`/var/log/vmware/vcf/domainmanager/ci-installer-[id]/workflow_[id]/vcsa-cli-installer.log` |
| vSphere Cluster Configuration | `/var/log/vmware/vcf/domainmanager/domainmanager.log`                                                                                               |
| VCF Operations                | `/var/log/vmware/vcf/domainmanager/domainmanager.log`<br>`/var/log/vmware/vcf/domainmanager/vcf-ops-ovf-tool-[id].log`                              |
