#ManagingVNETs

### Attributes
- **SKU** - Basic or Standard. This value must match the SKU of the [[Azure Load Balancer]] with which the IP is used.
- **Address Assignment**:
	- Dynamic addresses are assigned when a machine powers on, and can change when deallocated. They remain the same if restarted by the OS.
	- Static addresses are assigned when the IP is created and are not released until the resource is deleted.

#### SKU
|Feature|Basic SKU|Standard SKU|
|---|---|---|
|IP assignment|Static or Dynamic|Static|
|Security|Open by default|Secure by default, closed to inbound traffic|
|Resources|Network interfaces, VPN gateways, Application gateways, and internet-facing load balancers|Network interfaces or public standard load balancers|
|Redundancy|Not zone redundant|Zone redundant by default|
