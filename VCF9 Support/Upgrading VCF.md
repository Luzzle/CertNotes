#vcf9 

[[VCF - Use Cases and Limitations]]
[[VCF vs vSphere]]

### Overview

**Key considerations - Upgrade vs New Deployment**

| Requirements        | Upgrade                                                                                      | New Deployment                                                                                            |
| ------------------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Compatibility**   | Compatibility with existing hardware must be considered.                                     | The latest hardware and software can be used.                                                             |
| **Complexity**      | Deployments tend to be complex as they require integration with existing systems.            | Deployments are less complex as you start from scratch. Predicting resource utilisation can be difficult. |
| **Risk Assessment** | A risk assessment must be performed to determine the impact of new systems on existing ones. | You must predict potential risks before deployment.                                                       |
| **Time Frame**      | Deployments take longer due to requiring integration with existing systems.                  | Deployments can be done quicker as you start from scratch.                                                |
| **Scalability**     | Scalability might be limited by existing platforms and systems.                              | Considerations can be designed into the infrastructure from the start.                                    |
|                     |                                                                                              |                                                                                                           |
#### Prerequisities

![[Pasted image 20260125075127.png|1000]]

![[Pasted image 20260125075341.png|1000]]

![[Pasted image 20260125075415.png]]

### Upgrade Path - vSphere 8.0 to VCF 9.0
This is split into 2 phases:
1. In place upgrade from vSphere 8.0 to vSphere 9.0
	- Before upgrade:
		- Check vCenter infrastructure compatibility with vCenter 9.0.
		- Backup all critical infrastructure.
		- Take a snapshot of the vCenter VM.
		- Remove vCenter HA.
	
	- Starting with VCF 9.0, only vSphere Lifecycle Manager image clusters are supported. ESX clusters using vSphere Baseline must switch to using vLCM.
	
	- Before you start upgrading vSAN on-disk format versions ensure that:
		- ESX and vCenter upgrades are complete.
		- The disks are healthy.
		- ESX hosts are not in maintenance mode.
		- No component rebuilding tasks are currently in progress in the vSAN cluster.
	- Upgrade the vSAN ondisk format version to use features that are only available in later versions.
	- You **must** upgrade ESX and vCenter before upgrading the vSphere Distributed Switch to use features from later versions.
	
2. Conversion to VCF 9.0


#### VCF Installer Deployment Wizard

After the vSphere Foundation component binaries are downloaded, you can start the deployment using the deployment wizard.
- You must review the prerequisites.
- Confirm a depot.
- Then deploy from Deployment Wizard -> VMware vSphere Foundation.

*When you select an existing vCenter infrastructure, the storage, hosts, networks and distributed switch pages of the wizard are not available as compared to New Deployment*.

You deploy VCF using a deployment specification JSON file by clicking `DEPLOY USING JSON SPEC` in the VCF installer menu.

##### VCF Operations

As part of the VCF Operations configuration, you provide details for the VMware Cloud Foundations Operations appliance.

- Operations Appliance Size (vCPUs and Memory)
- FQDN
- Admin password
- Root password

##### vCenter

As part of the vCenter configuration you provide the FQDN, SSO user name and password.

You then validate and accept the thumbprint of the existing vCenter.

---

After everything is configured, you can then download a JSON file of the configuration, this can be uploaded to create a portable installation file.

Before proceeding, the VCF installer validates the parameters provided. If validation errors occur, you must navigate back and rectify them before rerunning validations.

### Accessing the VCF Operations Appliance

1. Log in to the VCF Operations appliance for the initial configuration.
2. Create a vCenter account from `Administration - Integrations`, provide details about the existing vCenter FQDN and credential, and save.
3. Start collecting information about inventory objects from the vCenter system.
