#ManagingVNETs 

### Definition
Azure Network Watcher provides a suite of tools to monitor, diagnose, view metrics, and enable or disable logs for Azure IaaS (Infrastructure-as-a-Service) resources. Network Watcher enables you to monitor and repair the network health of IaaS products like virtual machines (VMs), virtual networks (VNets), application gateways, load balancers, etc.

Network Watcher consists of three major sets of tools and capabilities:

- Monitoring
    - Topology
    - Connection monitor
- Network diagnostic
    - IP flow verify
    - NSG diagnostics
    - Next hop
    - Effective security rules
    - Connection troubleshoot
    - Packet capture
    - VPN troubleshoot
- Traffic
    - Flow logs
    - Traffic analytics

#### Topology Tool
The topology capability of Azure Network Watcher allows you to view all of the following resources in a virtual network. Including, the resources associated to resources in a virtual network and the relationships between the resources.
All resources returned in a topology have the following properties:

- **Name**: The name of the resource.
- **Id**: The URI of the resource.
- **Location**: The Azure region the resource is in.
- **Associations**: A list of associations to the referenced object. Each association has the following properties:
    - **AssociationType**: References the relationship between the child object and the parent. Valid values are `Contains`and `Associated`.
    - **Name**: The name of the referenced resource.
    - **ResourceId**: The URI of the resource referenced in the association.
    
#### Connection Monitor tool
- Connection Monitor provides unified, end-to-end connection monitoring in Azure Network Watcher.
- Connection Monitor can detect changes that affect connectivity, such as network configuration changes or modifications to NSG rules.