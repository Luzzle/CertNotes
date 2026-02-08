#vcf9 

### Overview
When troubleshooting vMotion, you can review the following log files.

| Location                  | Files                                                                                                                                                                                                                                                                                                                   |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| vCenter                   | *vpxd.log* - Operation ID for vMotion Process                                                                                                                                                                                                                                                                           |
| Source / Destination Host | *vmware.log* - Information about the migration process. Search for **migrate**<br>*vpxa.log* <br>*hostd.log* - State transitioning information for vMotion. Search for VM .vmx filename and **State Transition**<br>*vmkernel.log* - Storage and network errors as well as timeouts. Search for **migrate and vMotion** |
#### DRS
If all VMs can access the required CPU and memory and no resource contention exists, no or a few migrations should occur.

Otherwise:
	- Ensure the DRS automation level is not set to manual or partially automated.
	- Verify that standard vMotion is working properly.
	- Check configuration table below.

**Valid Reasons:**

| DRS never migrates                                             | DRS seldom migrates                                                  | DRS frequently migrates                                 |
| -------------------------------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------- |
| Automation level is set to manual                              | VM loads are consistent                                              | VM loads are erratic                                    |
| Migration threshold is set to apply priority 1 recommendations | Migration threshold is set to apply priority 2 and 3 recommendations | Migration threshold is set to apply all recommendations |

**Configuration issues**

| DRS never migrates                                                             | DRS seldom migrates                                                | DRS frequently migrates                                                         |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------------------- |
| vMotion network is not configured or functioning properly                      | Some VMs cannot be migrated as they are using local host resources | VM loads are erratic, causing DRS to do more work to load balance across hosts. |
| Migration threshold is **incorrectly** set to apply priority 1 recommendations | Too many restrictive affinity or anti-affinity rules               |                                                                                 |

