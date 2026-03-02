#vcf9 
### Overview
The NSX management cluster is formed by a group of three NSX management nodes for HA and scalability.

The NSX Manager appliance has built-in policy, manager and controller roles.
- The management plane includes the policy and manager roles.
- The **central control plane** (CCP) includes the controller roles.

The desired state is replicated in the distributed persistent database, providing the same configuration view to all nodes in the cluster.

![[Pasted image 20260215154936.png|600]]

#### Monitoring of the NSX Management Cluster
To view the status of the NSX Management Cluster, open the NSX UI and navigate to **System > Configuration > Appliances** or run `get cluster status` from the CLI.

You can run `get cluster config` to determine configuration details about the cluster.

##### Status Definitions
**Overall**: AVAILABLE, DEGRADED
**Member Status**: UP, DOWN
**Group Status**:
	- STABLE - All members of the group are UP.
	- DEGRADED - One or 2 members of the group are DOWN.
	- UNAVAILABLE - All members of the group are down.


### Errors
**Remote Logging Not Configured** - Update the NSX Node profile to configure a remote logging server.