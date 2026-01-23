#NSE4 

### Overview

IPsec is a suite of separate protocols:

| Protocol                                 | Description                                                                                                                        |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **[[Internet Key Exchange (IKE)]]**      | Used to authenticate peers, exchange keys and negotiate the encryption and checksums that are used. This is the *control channel*. |
| **Authentication Header (AH)**           | Checksums that verify the integrity of the data. This is not used by FortiGate                                                     |
| **Encapsulating Security Payload (ESP)** | The encapsulated security payload. The data channel.                                                                               |
You have 3 options when configuring the remote gateway type of the VPN:
1. Dialup user
2. Static IP
3. Dynamic DNS - FQDN

There are 2 types of IPsec VPN. Route and Policy Based.

Policy based is legacy and only exists for backwards compatibility and should never be used.

##### Route Based
The FortiGate automatically adds a virtual interface with the VPN name that allows you to configure routing and firewall polciies for the IPsec traffic in the same way you do for normal traffic.

You must configure at least one firewall policy that accepts traffic on your IPsec tunnel, otherwise the tunnel will not come up.


##### Ports
**[[Internet Key Exchange (IKE)|IKE]]** - UDP 500
**[[Internet Key Exchange (IKE)|IKE]] NAT-T** - UDP 4500

### Modes
**Transport Mode** - Directly encapsulates and protects the 4th layer and above. It does not protect the original IP header and does nto add an additional IP header.

**Tunnel Mode** - It encapsulates the entire IP packet and adds a new IP header at the beginning.

### Security Associations (SA)

In order to create an IPsec tunnel, both devices must establish their SAs and secret keys.

An SA is the bundle of algorithms and parameters being used to encrypt and authenticate data travelling through the tunnel. In normal two-way traffic, this exchange is secured by a pair of SAs, one for each traffic direction.

IKE uses two distinct phases: [[IPSec Phase 1|phase 1]] and [[IPSec Phase 2|phase 2]]. Each phase negotiates different SA types. The SA negotiated during [[IPSec Phase 1|phase 1]] is called IKE SA, and the SA negotiated during [[IPSec Phase 2|phase 2]] is called IPsec SA.

FortiGate uses **IKE SAs** for setting up a secure channel to **negotiate IPsec SAs**. 

FortiGate uses **IPsec SAs** for **encrypting and decrypting the data sent and received, respectively, through the tunnel**.

### IPSec Topologies

#### Remote Access (Dialup)
The remote user connects to a VPN server located on the corporate premises, such as FortiGate, to establish a secure tunnel. After the user is authenticated, FortiGate provides access to network resources, based on the permissions granted to that user.

FortiGate does not know the IP address of the remote user, only the remote user can initiate a VPN connection request.

#### Site-to-site
Site-to-site VPN is also known as LAN-to-LAN VPN. A simple site-to-site deployment involves two peers communicating directly to connect two networks located at different office.

When you need to connect more than two locations, you can use a hub-and-spoke topology. 

If every site connects to every site this is a partial or full mesh. A major upside to this topology is fault resistance.

### NAT Traversal
**ESP** cant support NAT because it has no port numbers.

If NAT Traversal is set to enable, it detects whether NAT devices exist on the path.
	If yes, both ESP and IKE will use UDP port 4500.

If NAT Traversal is set to forced, ESP and IKE will always use UDP port 4500.

### Dead Peer Detection (DPD)
After a Phase 2 tunnel is considered up, the peers can be configured to send DPD probes to detect a failed (or dead) tunnel and bring it down before its IPSec SA's expire.

There are 3 modes:
1. On Demand - DPD probes are sent when there is no inbound traffic.
2. On Idle - DPD probes are sent when there is no traffic.
3. Disabled - Only reply to DPD probes - dont send probes.