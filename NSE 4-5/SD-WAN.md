#NSE4 

### Overview

[[SD-WAN Components]]

According to Gartner, software-defined WAN (SD-WAN) provides dynamic, policy-based, application path
selection across multiple WAN connections, and supports service chaining for additional services, such as
WAN optimization and firewalls. The Fortinet implementation of SD-WAN is called secure SD-WAN because it
also provides security by leveraging the built-in security features available on FortiOS.

Secure SD-WAN relies on well-known FortiOS features, such as IPsec, link monitoring, advanced routing,
internet services database (ISDB), traffic shaping, UTM inspection, and load balancing.

Note that SD-WAN controls egress traffic, not ingress traffic.

In an SD-WAN environment, the terms underlay and overlay are commonly used to describe the link type of
an SD-WAN member.

**Underlays** refer to the physical links that you can rent or buy from an ISP, such as cable, DSL, fiber, MPLS,
3G/4G/5G/LTE, and ATM links. These links are part of the ISP physical infrastructure that is responsible for
delivering packets across networks. 

**Overlays** are virtual links that you build on top of underlays. A common example of an overlay is an IPsec tunnel. Because original packets are often encapsulated in ESP packets, the networks that communicate through the IPsec tunnel are no longer restricted to the routing policies of the ISP. In addition, the privacy and authentication features provided by IPsec protect your traffic from unauthorized access.

When the FortiGate matches a SD-WAN policy it performs the following:

1. Performs a [[FortiGate Routing|Forwarding Information Base (FIB)]] lookup for the packet destination IP. If the resolved interface for the *fib-best-match* isnt an SD-WAN member, then FortiGate moves onto the next rule. **SD-WAN rules are skipped if the best route is to the destination isnt an SD-WAN member**.
2. If the resolved interface is an SD-WAN member, then the FortiGate looks for one or more acceptable members in the *outgoing-interface* list, starting wiht the first member in the list.  An acceptable member is an alive member that has a route to the destination. **SD-WAN rules are skipped if none of the configured members in the rule have a valid route to the destination.**

Steered traffic must be allowed by a firewall policy and reference an SD-WAN zone instead of an outgoing or incoming interface.

### Use Cases
#### Direct Internet Access (DIA)
DIA, also known as local breakout is the most common use case for SD-WAN. A site has multiple internet (underlay) links. The links are connected to FortiGate using different types of physical interfaces: port, VLAN, link aggregations, etc...

A use case is to send sensitive traffic over the best-performing links, whilst distributing non-criticial traffic over one or more links using a best effort approach.

#### Site-To-Site Traffic
You can use SD-WAN to steer corporate site-to-site traffic. Usually, companies follow a hub-and-spoke
topology, and use VPN tunnels—typically dynamic IPsec tunnels—to transport the traffic between the sites.

The tunnels (also known as overlay links) are established over internet or MPLS links (also known as
underlay links). Tunnels can also carry internet traffic from a spoke to a hub where it then exits to the internet.

#### Remote Internet Access (RIA)
Remote Internet Access (RIA), also known as remote breakout, is another use case for SD-WAN. Internet traffic from the spokes is backhauled through the WAN using overlay links. When the traffic arrives at the hub, it breaks out to the internet.

The most common reason to use RIA is to centralize security inspection and internet access on the hub. For example, you can have a central high-end FortiGate device that inspects all the internet traffic that leaves the organization and conforms with the company policy, instead of having each low-end spoke FortiGate device to inspect traffic, thus reducing costs and administrative overhead.

Another reason to use RIA is for DIA backup. For example, you could configure FortiGate to steer internet traffic through an MPLS link if the performance measured for internet applications on internet links is worse than on MPLS links, or simply if the internet links become unavailable.

### Policy Routes
When you configure an SD-WAN rule, FortiGate essentially applies a policy route on FortiOS. They provide more granular matching than static routes by allowing you to match based on:

- Protocol
- Source Address
- Source Ports
- Destination Ports
- ToS marking
- Destination internet service.

**They have precendence over any other routes.**

The actions that can be taken are:
**Stop Policy Routing** - Skips all policy routes and uses the FIB.
**Forward Traffic** - Forward traffic using the set outgoing interface and gateway. The FIB must have a matching route; otherwise the policy route is considered invalid.

When you configure a static route, you can reference one or more zones as the outgoing interface. As a result, FortiOS installs a static route in the routing table for every member configured in the zone. Because the static routes share the same distance, they become ECMP routes. FortiOS uses the gateway defined for each zone member.

To list policy routes: **diagnose firewall proute list**. The *vwl_service* and *vwl_mbr* which indicate the SD-WAN rule that allowed the route creation and the SD-WAN member used to steer the traffic.