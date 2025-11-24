#ManagingVNETs 

### Linking and Auto-Registration

Once you create a private DNS zone in Azure, it is not immediately accessible from any virtual network. You must link it to a virtual network before a VM hosted in that network can access the private DNS zone.
When you create a link between a private DNS zone and a virtual network, you have an option to turn on auto-registration of DNS records for virtual machines. If you choose this option, the virtual network becomes a **registration virtual network** for the private DNS zone.
– A DNS record is automatically created for the virtual machines that you deploy in the network. DNS records are created for the virtual machines that you have already deployed in the virtual network.
– One private DNS zone can have multiple registration virtual networks, however, every virtual network can have exactly one registration zone associated with it.

When you create a virtual network link under a private DNS zone and choose not to enable DNS record auto-registration, the virtual network is treated as a **resolution only virtual network.**
– DNS records for virtual machines deployed in such networks will not be automatically created in the linked private DNS zone. However, the virtual machines deployed in such a network can successfully query the DNS records from the private DNS zone.
– These records may be manually created by you or may be populated from other virtual networks that have been linked as registration networks with the private DNS zone.
– One private DNS zone can have multiple resolution virtual networks and a virtual network can have multiple resolution zones associated to it.

**Take note that you can only link a virtual network and use the auto registration feature to a private DNS zone only.**