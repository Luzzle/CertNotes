#vcf9

### vSphere Foundation Overview
vSphere Foundation is the workload engine that provides an enterprise class hyper-converged infrastructure solution. The solution combines compute (vSphere) and storage (vSAN) virtualisation with built in Kubernetes orchestration (VKS) and intelligent operations (VCF Operations).

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