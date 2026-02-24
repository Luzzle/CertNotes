#vcf9 

### Validation using NSX UI
You verify the BGP connectivity status for each neighbor from the NSX UI by navigating to **Networking > Connectivity > Tier-0 Gateways**.

### Validation using Edge Node CLI
On an NSX Edge node, you run the `get gateways` command to display information about all gateways, including their NRF instances.

On NSX edge node, you run the `vrf` command to change between VRF instances. This can be changed based on gateway UUID, VRF ID or gateway name.

On an NSX Edge node, you run the `get bgp` command to display all IPv4/6 BGP routes in an VRF instance. This displays learnt, advertised and next hop information.

	 ISR -> Intra-Site routing between one edge node to another

You can also run `get route bgp` to display a BGP routing table in a VRF instance. 

You can run `get bgp neighbor <ip> advertised-routes` to display routes advertised to a BGP neighbor in a VRF instance.

NSX manager will create a next hop `169.254.x.x` IP for routes that lead to the transit gateway, to get access to internal networks.

On an NSX Edge node, you run the `get bgp neighbor summary` command to display the BGP neighbor information in the VRF instance. This includes BGP peering status.

From the NSX Edge Node, you run the `get vpcs` command to display information about the VPCs in the system.

To view the transit gateways configured in the system, you can run `get tgws`.

##### Logging
On an NSX Edge node, you run the `get log-file routing follow` command to display routing-related events.

### Other CLI's
If you are looking at any of the Service Routers (SRs), Virtual Private Clouds (VPC) or transit gateway, you run the `get forwarding` command to display the forwarding table in a VRF instance. These devices do not have routing tables, but instead have forwarding tables.