#vcf9 

### Overview
In vSphere 7+ and VCF-managed clsuters, the vSphere CLuster Services (vCLS) VMs must remain powered on for DRS, cluster health and policy enforcement to function. If the vCLS VMs cannot power on, no workloads - including new VMs, can be deployed, because vSphere **considers the cluster as unhealthy**.

A common cause for this is insufficient resources (CPU / Memory), datastore issues or policy conflicts. Retreat mode can be used as a troubleshooting mechanism, which temporarily disabled vCLS, allowing the administrator to deplyo VMs and correct underlying issues.

### Logs
Each ESX host has its own HA log at `/var/log/fdm.log`. FDM is installed as a service named `vmware-fdm`.

### Activation Failures
If vSphere HA fails to activate, take the following actions:
- Re-attempt to activate.
- Check FDM log.
- Check the release notes for known issues with HA.

### Insufficient Resources
In vCenter, you can see the following error message `Insufficient resources to satisfy configured failover level for vSphere HA`.

The problem occurs when you try to power on a VM that is part of a HA cluster with insufficient failover resources.

**Possible causes**

| Component       | Cause                                                 |
| --------------- | ----------------------------------------------------- |
| vSphere HA      | Admission control policy is not configured correctly. |
| Virtual Machine | One of more VMs have excessive reservations.          |
| ESX Host        | The cluster has insufficient physical resources.      |
