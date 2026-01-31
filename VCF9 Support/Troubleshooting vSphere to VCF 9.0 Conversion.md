#vcf9 

### SKUs and Components

| SKU                | Components                                                                                                                                                             | Notes                                                                                                                                                                                                                                                                                                   |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| VCF                | Core:<br>- VC<br>- NSX<br>- SDDC Manager<br><br>Management:<br>- VCF Operations fleet management<br>- VCF Operations<br>- VCF Operations collector<br>- VCF Automation | - VCF Installer deploys VC, SDDC Manager, NSX and VCF Operations fleet manager.<br><br>- VCF Installer instructs VCF Operations fleet management to deploy the management components.<br><br>- VCF Operations collector is a dependent component of VCF Operations that is requiredfor each deployment. |
| vSphere Foundation | Core:<br>- VC<br><br>Management:<br>- VCF Operations<br>- VCF Operations Collector                                                                                     | - VCF Installer deploys all of the products.<br><br>- VCF Operations Fleet Management is not available.                                                                                                                                                                                                 |
Two options are available for the SDDC Manager: either deploy a new one or reuse the VCF installer to become an SDDC Manager (called a flip).

#### Environment Prerequisites

**ESX Hosts**:
- Four hosts for Management domain plus additional if needed.
- Images with ESX 9.0.0.0
- 32 vCPUs require for the hosts in the management domain
- RAM: 64GB

**Networks**:
- Management, VM management, vSAN, vMotion, NSX TEP

**Existing vCenter**:
- Must be non-ELM (Enhanced Linked Mode)

**If NSX exists**:
- Should be connected to the given vCenter
- Should not be federated

**If VCF Operations exists**:
- Input specification should always state `vcfCloudProxy -> useExistingDeplyment -> false`

**VCF Installer VM**:
- Either predeployed in the existing vCenter or deployed on infrastructure outside the existing vCenter, but with network connectivity to the VC/NSX/ESX/VCF Operations products.

**DNS and NTP configuration**:
- Must be correct or this can cause failures in resolving host names.

**vSAN File Services**:
- Must be disabled in the cluster.

**Certificates**:
- Existing vCenter system should not have any expired or untrusted certificates before convert/import operation.

### Upgrade Phases

##### Phase 1

Phase 1 is to do an inplace upgrade to upgrade the existing vSphere to version 9.0.

##### Phase 2

Phase 2 is to deploy VCF 9.0 with the existing vSphere 9.0 using the VCF Installer in a specific sequence.

1. Connect existing infrastructure
2. Validation
3. Depot configuration
4. Installation

### Services for VCF Installer and SDDC Manager


| Service            | Location                                   | Responsibilities                                                    |
| ------------------ | ------------------------------------------ | ------------------------------------------------------------------- |
| Common Service     | `/opt/vmware/vcf/commonsvcs`               | Inventory, Credentials, Certificates, Passwords                     |
| Domain Manager     | `/opt/vmware/vcf/domainmanager`            | VCF Installer validation and deployment workflows, Day 2 workflows. |
| Operations Manager | `/opt/vmware/vcf/operationsmanager`        | Security Operations, Data Aggregation, Host Commissioning           |
| LCM                | `/opt/vmware/vcf/lcm/lcm-app`              | Upgrade planning, Patching, Upgrades, Prechecks, Bundle Management  |
| SoS                | `/opt/vmware/sddc-support`                 | Support Logs generation, health                                     |
| UI                 | `/var/log/vmware/vcf/sddc-manager-ui-app.` | UI for VCF Installer / SDDC Manager                                 |
