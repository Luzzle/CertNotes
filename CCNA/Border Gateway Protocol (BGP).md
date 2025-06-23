#IPConnectivity

### Overview
BGP is a routing protocol that forms the backbone of the internet. It is used to determine how data packets travel across the internet.

BGP takes into consideration all different peering options a router has and chooses the closest one to where the router is.

Routes are exchanged and traffic is transmitted over the Internet using eBGP (external BGP). Routes can be shared inside internal networks using iBGP (internal BGP).

I.e. routing between the same Autonomous System -> iBGP. Routing between different different Autonomous Systems -> eBGP.

#### BGP Functions
BGP performs the following 3 main functions.

##### Route Discovery
BGP peers exchange routing information with neighbouring BGP peers through network-layer reachability information (NLRI) and path attributes.

Path attributes include information like latency, hop count and cost.

##### Route Storage
During the discovery process, every BGP router collects route advertisement information and stores it in the form of routing tables.

##### Path Selection
See below.

### Attributes and Path Selection
BGP assigns attributes to each path, used to find the most efficient path for network traffic.
Unlike [[IGP|IGPs]] which select a route based on lowest "metric", BGP selects a path based on a list of attributes.

Paths are chosen based on attribute priority.

##### 1. Weight
The router will always prefer the path with the **highest** weight. This value is local to the router and the default value for all routes not originated by the router.

##### 2. Local Preference
The local preference is used within an autonomous system and exchanged between iBGP routers. The router will prefer the path with the highest local preference. The default value is 100.

##### 3. Originate
The router will prefer the path that the local router originated. A BGP router will prefer routes that it installed into BGP itself, over a route installed by another router.

##### 4. AS Path Length
The router will prefer the route with the lowest AS path.

##### 5. Origin Code
The router will prefer the lowest origin code.
From lowest to highest: *IGP* -> *EGP* -> *INCOMPLETE*

##### 6. MED (Metric)
The router will prefer the lowest MED. This value is propagated across autonomous systems.

##### 7. eBGP over iBGP
The router will prefer eBGP over iBGP. 

##### 8. Shortest IGP path to BGP next hop
The router will prefer the path within the AS with the lowest [[IGP]] metric to the next BGP hop.

##### 9. Oldest Path
The router will prefer the path that is received first.

##### 10. Router ID
The router will prefer the path with the lowest BGP neighbour router ID.

##### 11. Neighbour IP Address
The router will prefer the path with the lowest neighbour IP address.

### BGP Messages
**Open** - used to establish a neighbour relationship
**Keepalive** - used to maintain a neighbour relationship and is sent periodically
**Update** - used to exchange path attributes
**Notification** - used to exchange error signals

### BGP Neighbours
BGP neighbours, also called peers, are manually configured and communicate through a [[TCP]] session on port 179.
Neighbours can be in any of the following states.

**Idle** - can be either administratively down or awaiting the next retry attempt.
**Connect** - waiting for the TCP connection to be established.
**Active** - TCP connection is complete but no BGP messages have been sent.
**Opensent** - BGP messages have been sent but no BGP open message has been received.
**Openconfirm** - Open messages have been sent and received but awaiting keepalive message
**Established** - Full adjacency has been established and exchanging update messages.

### Prefix Lists
Prefix lists can be used to control route advertisement **or** route acceptance, meaning they can be applied both outbound and inbound. 

**ge (greater than or equal)** and **le (less than or equal)** is used to match routes within a subnet with a certain prefix length.

Unsetting ge and le or setting them to the exact same value will result in only route matching the exact prefix.
##### Configuration
Configure the prefix list.
```fortios
config router prefix-list
	edit "PrefixListName"
		config rule
			edit 1
				set prefix 10.0.0.0 255.0.0.0
				set ge 24
				set le 24
			next
		end
	next
end
```

Configure a route map.
```fortios
config router route-map
	edit "RM-PrefixListName"
		config rule
			edit 1
				set match-ip-address "PrefixListName"
				set action permit
			next
		end
	next
end
```

Apply route map to BGP neighbour
```fortios
config router bgp
	set as ASN
	config neighbor
		edit "neighbourIP"
			set remote-as ASN
			set route-map-in "PrefixListIN"
			set route-map-out "PrefixListOUT"
		next
	end
end
```

You can then check the advertised routes through
```fortios
get router info bgp neighbors NEIGHBOR advertised-routes
```