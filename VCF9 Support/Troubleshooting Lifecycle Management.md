#vcf9 

### Patching VCF Core Components
You can use **Plan Patching** from VCF Operations for patching VCF core components. To minimize interruption during upgrades, you can run a precheck to identify and resolve potential issues.

You can monitor life cycle management tasks in VCF Operations. You can review the status of failed, pending and completed tasks, including the task duration. This can be accessed under **VCF Management > Tasks**

### Live Patch
In ESX 9.0, Live Patch extends support for the VMkernel and NSX components of the ESX image, enabling more patches to use Live Patch updates.

### Configuration Templates
A configuration template is a set of configurations representing a desired state. A configuration template enables an administrator to define and monitor the configurations. The configuration schema defines the settings for the desired state.

You define a desired state based on your current environment using configuration templates. You create, edit, or delete configuration templates in VCF Operations.

Ensure that the vCenter user account has administrator privileges.
Verify that the user has the required Configuration Drifts roles:
	- **Manage Privilege**: For creating templates, assigning them to policy, and running configuration drift checks.
	- **View Privilege**: For viewing template content and viewing existing configuration drifts.

Verify that a collector group or a collector is assigned to your cloud account.

The ***vpxd*** and ***infraprofile*** services on the vCenter appliance handle the vCenter profile configuration requests.

You can view the drift status of your vSphere clusters in VCF Operation. Drift status is visible only for vSphere clusters that have configuration profiles enabled.

Integrating the VCF Operations Configuration Drift Templates with a source control repository enables you to control the versioning, auditing, and management of your configuration templates.

You can automate drift detection by creating a scheduled job to run at a defined interval.

##### Configuration Drift
Possible drift statuses:
- **Not Drifted**: This state shows vCenter instances and vSphere clusters with no drifts from the desired state.
- **Drift Detected**: This state shows when vCenter instances or vSphere clusters have deviated from the desired standard configurations.
- **Drift Check Failed**: vCenter instances or vSphere clusters data has not been collected.
- **Unavailable**: The instance version might not be supported or registered.

You can detect configuration drifts for each configuration template that you created for a specific vCenter instance. You can click **Detect Drift** or **Download Drift Status Report** to get details of the drift.

### Developer Center
In the VCF Operations console, the **Developer Center** tab provides documentation and access to the SDDC Manager API.

**Features**:
- Execute RESTful API with the interactive API Explorer.
- You can execute PowerCLI commands.
- Integrate workflows and partner solutions with VMware and community code samplels for common development languages.
- Obtain open-source SDK and links to guides and documentation on Operations API.

### Logs
On the vCenter VM, vSphere Lifecycle Manager (vLCM) manages the patches and performs prechecks to ensure that the patch is compatible.

- VPXD:
	- `/var/log/vmware/vpxd/vpxd.log`
- vLCM:
	- `/var/log/vmware/vmware-updatemgr/vum-server/vmware-vum-server.log`
- vSAN:
	- `/var/log/vmware/vsan-health/vsanvcmgmtd.log`
	- `/var/log/vmware/vsan-health/vmware-vsan-health-service.log`

#### ESX Logs
- For the ESX host process:
	- `/var/run/log/vmkernel.log`
	- `/var/run/log/syslog.log`
	- `/var/run/log/settingsd.log`
	- `/var/run/log/lifecycle.log`
- For VM-related issues:
	- `/var/run/log/hostd.log`
	- `/vmfs/volumes/<datastore>/<vm>/vmware.log`
