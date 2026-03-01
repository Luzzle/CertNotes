#vcf9 

### VCF Management Service Platform (VMSP)
VMSP is a Kubernetes hosting platform for containerized VCF services, including VCF Automation and VCF Identity Broker.

It contains the following management service components:
- Internal Load Balancer
- Gateway
- PostgreSQL
- Registry
- Object Storage
- Log Shipping
- Backup and Restore
- Packaging and Release

During the deployment of VCF Automation, cluster node appliances are configured as follows:

- The appliance FQDN is used to create a primary virtual IP.
- The primary virtual IP load-balances traffic across all nodes in the cluster.
- A spare IP address is used to deploy an additional node if one of the other nodes in the cluster fails.
- An internal network is created for communication between containers.

### VCF Automation Installation Workflow
VCF Operations fleet management is used to orchestrate the VCF Automation deplloyment on VMSP:
1. VCF Operations fleet mangament provisions the VMSP cluster and platform services.
2. VCF Operations fleet management deploys the VCF Automation components on the VMSP cluster.
3. Runs health checks and validations

##### Log File
You use the `/var/log/vrlcm/vmsp_bootstrap_<id>.log` file in the VCF Fleet Management appliance to troubleshoot the VMSP Cluster provisioning.

### Monitoring using KubeCTL
From the VCFA container, you use the  `kubectl get pods -A` to view the status of Kubernetes pods across all namespaces.

###### Namespaces
**istio** - handles messages and ingress traffic
**kube-system** - kubernetes system components and add-ons
**prelude** - all VCF automation components
**vmsp-platform** - VMSP components such as registry and object storage services

You use the `kubectl describe pod -n <namespace> <pod_name>` command to obtain detailed information, error details and events about any pod.

You can view the current pod logs by using the `kubectl logs -n <namespace> <pod_name>` command. If a pod has restart, ou view the previous logs by using the `kubectl logs -n <namespace> <pod_name> -p` command.

You use `kubectl get vspheremachines -A` to check the status of each vSphere machine in the cluster.

### Checking the CAPV Logs
Cluster API vSphere Provider (CAPV) is a Kubernetes-native tool that enables the automated, declarative management of the Kubernetes cluster on the vSphere infrastructure.

If the `kubectl get vspheremachinees -A` command does not return the expected number of VMs based on your VCF Automation cluster deployment of choise, or if the VMs are not in a ready state, you can review the CAPV logs by running `kubectl logs -n vmsp-platform -l app.kubernetes.io/instance=vmsp-operator` command.

### Checking Package Deployments
You use the `kubectl get packagedeployments -n vmsp-platform` command to verify the successful package deployment for VMSP platform components.

### Checking Cluster Events
You can run `kubectl get events --sort-by='.lastTimestamp' -A` to check the latest VCF Automation cluster platform events.