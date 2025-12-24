#NSE4 

### Definition

#### Source NAT (SNAT)
SNAT translates the source IP and port which can be enabled on a firewall policy.

There are 2 ways to SNAT traffic.
1. Packets matching the firewall policy are translated into the outgoing interfaces IP address.
2. Packets are mapped to a public IP address within a dynamic **[[IP Pool]]**.

#### Destination NAT (DNAT)
DNAT translates the destination IP and port which requires a VIP object on the firewall policy.

A VIP is a DNAT object that typically maps a public IP address to an internal address. This also enables port forwarding, which allows us to reuse the external IP for multiple internal addresses.

The default VIP type is **Static NAT** which performs a 1 to 1 mapping. However, you can also configure the VIP type as **FQDN** which allows you to configure an FQDN address object as the external IP address. This enables the FortiGate to automatically update the external address if the FQDN's resolved address changes.

The `match-vip` setting on a firewall policy instructs the firewall to not check VIPs during policy evaluation. This setting is only available when the firewall policy action is set to **deny**.

When you configure a VIP or IP pool, ARP reply is enabled by default which allows the FortiGate to reply to incoming ARP requests for the external address.