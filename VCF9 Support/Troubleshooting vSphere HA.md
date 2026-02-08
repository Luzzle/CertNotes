#vcf9 

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
