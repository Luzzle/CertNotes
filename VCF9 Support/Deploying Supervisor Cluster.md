#vcf9 

### Self-Service IaaS
Self-Service IaaS is a VCF Automation feature that enables users to create resources such as VMs, Kubernetes guest clusters and storage volumes using a self-service consumption model.

Enabling Self-Service IaaS in VCF Automation has the following requirements:
- vSphere Supervisor must be enabled during the workload domain creation.
- vSphere Supervisor requires the Centralized connectivity mode to be configured after the workload domain creation.

vSphere Supervisor can be enabled on the **General Information** tab of the workload domain deployment.

To log into the VCF Automation Provider Management console, you must enter **system** as the name for the organisation and provide credentials for the admin user that you specified during the VCF Automation deployment.

#### Discovering the Workload Domain
VCF Automation does not automatically discover the creation of the workload domain with Supervisor enabled.

To ensure that VCF Automation discovers and registers the workload domain for IaaS use, you must navigate to **Administration > VCF Instances**. Click the vertical ellpises icon next to the name of the SDDC Manager in the management domain and select **Refresh**.

### vSphere Supervisor Configuration
On the vSphere Supervisor Configuration tab in the workload domain deployment wizard, you specify the following:
- Supervisor Name
- Service CIDR
- Control plane IP range (this must be 5 available IP addresses)
- Private (Transit Gateway) CIDR
- Private CIDR
- Workload DNS
- Workload NTP

The Service CIDR and Control Plane IP range must NOT be in the same range.

### Supervisor Deployment Workflow
Deploying a workload domain with vSphere Supervisor:

1. vCenter deploys a single control plane supervisor virtual machine.
2. The control plane supervisor VM is connected to the management network.
3. vCenter configures a new virtual private network or reuses an existing one.
4. The Supervisor cluster goes on a WAITING state if no NSX Edge cluster is found.
5. If not found, a new NSX Edge cluster must be manually deployed from vCenter.
6. After the NSX Edge clusters are deployed, the Supervisor cluster state changes to ready.

The NSX Edge cluster is configured as part of the network connectivity for the workload domain. To deploy an NSX Edge cluster you must select the **Centralized Connectivity** option.

You specify the NSX Edge cluster details using the Configure Network Connectivity wizard.

IaaS requires the deployment of large NSX Edge nodes.

#### Supervisor Cluster Control VM
The control plane VM is configured with 2 NICs: one for connection to the management network and the second for conenction to the private subnet of the new kube-system VPC.

#### VPC Configuration
You can verify the VPC configuration from the workload domain vSphere Client by navigation to **Networks** and expanding the **VPC** icon.

Two VPCs with the prefixes *kube-system* and *vmware-system-supervisor-services-vpc* are created during the workload domain deployment with IaaS enabled.

You can visualize the VPC configuration from the NSX UI by navigating to **VPCs > Topology**

#### Namespace Creation
In the context of VKS or a workload domain with IaaS enabled, a namespace, similar to a resource pool in vSphere, is a construct used to divide cluster resources.

During the deployment of a workload domain with IaaS enabled, the following two namespaces are created by default with the following prefixes:

- **svc-tkg-domain**: Runs vSphere pods dedicated to manage and monitor the Supervisor cluster.
- **svc-velero-domain**: Runs vSphere pods dedicated to back up, restore and performs disaster recovery.

### Edge-Cases Exam BS
When enavling vSphere Supervisor with NSX Classic (not NSX VPC mode as described above), the vSphere Workload Management wizard filters the list of available NSX Edge Clusters to ensure they are explicitly designed for use with Kubernetes workloads.

The **WCPReady** tag is the primary mechanism vCenter uses to identify a valid, compatible edge cluster for workload management and is assigned to the NSX Edge Cluster object.

#### Account Lockouts
When an NSX Admin account becomes locked in NSX Manager, this occurs due to failed login attempts exceeding the lockout threshold for either: CLI access, API access, or UI login, which is tied to API authentication.

Once locked, the only supported method to recover the NSX admin account is to log in to the NSX Manager console as the root user and manually clear the lockout counters. This is documented in NSX Manager password-recovery procedures and is the standard administrative recovery action. 