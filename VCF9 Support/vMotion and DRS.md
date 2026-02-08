#vcf9 

### Overview
A vSphere vMotion migration occurs over a network that is configured for vMotion.
![[Pasted image 20260208142342.png|500]]

#### TCP / IP Stacks
Each host can be configured so that vMotion uses a seperate TCP/IP stack, which will track its own routing table, ARP table and a seperate memory heap.

`esxcli network ip netstack` - list  ESX host network stacks.
`esxcli network ip netstack get -N [name]` - list detailed information about network stack.

[[Troubleshooting vMotion and DRS]]