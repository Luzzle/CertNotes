#vcf9 

### Overview

A workload domain is a logical grouping of compute, network and storage resources, designed to host virtual machines and containers.

![[Pasted image 20260131142834.png]]


VMware Cloud Foundation primarily uses the consolidated architecture or standard architecture model.

![[Pasted image 20260131142939.png|500]]

### Workload Domain Creation
![[Pasted image 20260131143145.png|700]]


You must make the following preparations before creating a workload domain:
- Verify that DNS records exist for vCenter instances and NSX Manager.
- Verify that enough unassigned hosts with the correct storage type are available.
- Verify that all hosts are associated with the same network pool.
- Add appropriate licenses with sufficient capacity in the VCF Operations UI.

##### Creating a Workload Domain
1. Navigate to Inventory
2. Expand VCF Instances and select the correct instance.
3. Click `ADD WORKLOAD DOMAIN`
4. Create New
