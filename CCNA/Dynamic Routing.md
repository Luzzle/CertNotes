#IPConnectivity #ccna-day24

### Overview
Routers can use dynamic routing protocols to advertise information about the routes they know to other routers.

They form adjacencies / neighbor relationships with adjacent routers to exchange this information

If multiple routes are learned, the router determines which route is superior and adds it to the routing table It uses the metric of the route to decide which is superior (lower is preferred).

### Categories
**[[IGP]] (Interior Gateway Protocol)** - used to share routes within a single autonomous system, i.e. a single organization
**[[EGP]] (Exterior Gateway Protocol)** - used to share routes between different autonomous systems.

### Floating Static Routes
By changing the [[IGP#Administrative Distance|AD]] of a static route, you can make it less preferred than routes learned by a dynamic routing protocol. This is called a floating static route.

The route will be inactive unless the route learned by the dynamic routing protocol is removed.
