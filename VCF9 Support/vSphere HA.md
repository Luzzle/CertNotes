#vcf9 

### Overview
vSphere HA allows a VM on a host to restart in the event of a host failure. This is initiated by vCenter.

When HA is enabled on a cluster, a tool called the **Fault Domain Manager** (FDM) is installed on all hosts. The hosts will be configured with a primary and redundant heartbeat network. This is used in tandem with heartbeat datastores to determine for certainty when a host has failed.

The primary node communicates the state of the HA to the to the **vpxd** process in vCenter.
HA however, is host based. This means that if the vCenter VM shuts down, the HA will remain up.

[[Troubleshooting vSphere HA]]