### Overview
FortiGate maintains two tables containing routing information in two tables. The RIB (Routing Information Base) and FIB (Forwarding Information Base).

![[Pasted image 20251225135320.png]]

The **Routing Monitor** widget can be used to view active (best) routes. This can be accessed in the GUI through `Dashboard > Network > Static & Dynamic Routing`

To view the routing table in the CLI run `get router info routing-table all`

[[Equal Cost Multipath (ECMP)]]

#### RIB (Routing Information Base)
Standard routing table containing active (or best) connected, static and dynamic routes.

#### FIB (Forwarding Information Base)
This can be best described as the routing table from the kernels point of view, which contains the same entries as the RIB, plus some system-specific entries.

This can be viewed from the CLI with command `get router info kernel`

### Administration Distances

| Connected | Static (SD-WAN) | Static (DHCP) | Static (Manual) | Static (IKE) | EBGP | OSPF | IS-IS | RIP | IBGP |
| --------- | --------------- | ------------- | --------------- | ------------ | ---- | ---- | ----- | --- | ---- |
| 1         | 1               | 5             | 10              | 15           | 20   | 110  | 115   | 120 | 200  |
### Reverse Path Forwarding Check
RPF check is a mechanism that protects your FortiGate from IP spoofing attacks. This check is performed on the first packet in a session, not on a reply.

The premise of an RPF check is as follows. When the Fortigate receives the packet on an interface, the firewall checks to ensure a route back to the source of the packet exists, and the outgoing interface for that route is the interface in which the incoming packet was received.

There are 2 modes: Feasible (Loose) and Strict.

##### Strict
The FortiGate verifies the matched route is the **best** route, otherwise the RPF fails. If there is a better route for the source address through another interface, it will not be accepted.

##### Feasible Path
The FortiGate checks to ensure that the route simply exists, it does not need to be the best route.