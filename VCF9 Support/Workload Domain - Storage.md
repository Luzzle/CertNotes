#vcf9 

### Overview
VCF uses the workload domains principal storage to deploy and run virtual machines.

You can select the following storage types as principal storage for your workload domain:
- vSAN
- NFS
- VMFS over Fibre Channel
- vSphere Virtual Volumes

### Monitoring vSAN from VCF Operations
VCF Operations provides a view of the entire VCF Storage Infrastructure, regardless of storage type. It allows for the following monitoring:
	- Storage operations dashboard.
	- vSAN insights.
	- Global deduplication and data protection.
	- Federated Metrics Views.

**vSAN Cluster Diagnostics** - accessed from the vSAN Cluster Performance panel.
**Skyline Health** - a tool used to view alerts and monitor vSAN data stores and networks.

### vSAN Objects
vSAN objects include components which contain data that resides on disks.
In the vSAN datastore:
 - Storage policies are applied to objects.
 - Components are created according to the specified storage policy.
 - Components are stored on physical storage devices on vSAN hosts.

Components can be in the following states:

| Component State   | Object State                              | Description                                                                                                                  |
| ----------------- | ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Active            | Healthy.                                  | Compliant with defined storage policy, all components are in an available state.                                             |
| Absent            | Reduced availability with no rebuild.     | Non-compliant due to vSAN is waiting for the object repair time to elapse before starting a resync.                          |
| Absent / Degraded | Reduced availability with active rebuild. | Non-compliant due to vSAN is rebuilding the missing components in the vSAN cluster.                                          |
| Absent / Degraded | Reduced availability with no rebuild.     | Non-compliant due to insufficient host/storage devices to rebuild the absent/degraded components.                            |
| Absent / Degraded | Inaccessible                              | Non-compliant due to the object encountering more failures that it was configured to tolerate and is currently inaccessible. |
The statuses of all objects can be viewed under the **Virtual Objects** view. The statuses of all components under **Physical disk placement** on the hosts monitoring page.

### ESXCLI Commands
You can use `esxcli storage` to display commands for viewing storage information.

| Command                                         | Description                                                                                                                                                            |
| ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `esxcli storage core adapter stats get`         | Check adapter statistics.                                                                                                                                              |
| `esxcli vsan health cluster list`               | Check vSAN cluster health.                                                                                                                                             |
| `esxcli vsan health cluster get -t [test_name]` | List reason for test result, you can use the full name in quotations or the shortname of the test.                                                                     |
| `esxcli vsan cluster get`                       | Check cluster information.                                                                                                                                             |
| `esxcli vsan storagepool list`                  | Check vSAN storage pool information.                                                                                                                                   |
| `esxcli vsan network`                           | Check information about vSAN network and other network-related information.                                                                                            |
| `esxcli vsan cluster unicastagent list`         | Check the vSAN unicast table. The unicast table has information about other hosts in the cluster used for network connections such as NodeUUID or IP address and port. |
| `esxcli vsan debug object health summary get`   | Determine vSAN object states.                                                                                                                                          |
| `esxcli vsan debug object list -u UUID`         | Check details of a single object.                                                                                                                                      |
| `esxcli vsan debug object overview`             | Display health information summary about all vSAN objects.                                                                                                             |
| `esxcli vsan debug disk overview`               | List all vSAN disks in cluster.                                                                                                                                        |
| `esxcli vsan debug vmdk list`                   | List all VMDKs and VM Home namespaces'                                                                                                                                 |
| `esxcli vsan faultdomain get`                   | List information about if a host is a member of a fault domain. (Preferred or secondary)                                                                               |
You can also use `vdq -q` to view a disks information related to vSAN. 
`vsantop` provides performance information.