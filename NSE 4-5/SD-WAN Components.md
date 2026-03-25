#NSE4 

#### Overview
##### Members
Members are logical or physical interfaces used to steer the traffic.

##### Zones
Zones are groups of members used to optimise the configuration. Usually this is used to group members that require a similar set of firewall policies. 

FortiGate creates the **virtual-wan-link** zone by default which cannot be deleted. It contains any SD-WAN member not explicitly assigned to a user-defined zone.

 By dividing SD-WAN members into zones, you can apply the same set of firewall policies to a zone instead of having to apply them to their individual members, thus reducing the administrative overhead and building a cleaner configuration.

##### Performance SLA
This allows you to define how you want to monitor the status of members and the performance criteria that you want to monitor. It can be packet loss, jitter, latency or a weighted mix of a few criteria.

You can set a detection mode which defines how the FortiGate will monitor the link quality:
	- **Active**: FortiGate sends active probes to the configured server to monitor the link health.
	- **Passive**: FortiGate uses traffic through the link to evaluate the link health.
	- **Prefer Passive**: FortiGate uses passive monitoring, and only if there is no traffic through the link, it will send probes.

##### SD-WAN Rules
These define where to steer the traffic matching a specific criteria. This also includes the strategy to apply and the performance metrics to determine the prefered members.

**Member Selection**
- Manual: Configuration order preference.
- Best quality: Best performing member based on quality criteria.
- Lowest Cost (SLA): Member that meets SLA target. Tiebreakers are cost and priority.