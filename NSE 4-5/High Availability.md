#NSE4 

### Overview
Fortigate HA uses FGCP to discover members, elect the primary FortiGate, synchonise data between members and monitor the health of members.

A FortiGate Cluster includes one device that acts as the primary FortiGate. The primary sends its complete config to other members that join the cluster, overwriting their configuration. It also synchonizes session information, FIB entries, FortiGuard definitions and other info.

The cluster shares one or more heartbeat interfaces among all members. The secondary devices are all responsible for monitoring the health of the primary.

##### Requirements
To form a HA cluster you must ensure all members have the same:

- Model
- Firmware
- Licensing
- Hard Drive Configuration.
- Operating mode (NAT vs Transparent mode)

If licensing is not the same, the clsuter defautls to the lowest licensing level among all members.

From a configuration setup POV, all HA settings on each member must have the same group ID, name, password and heartbeat interface settings.

The following settings are not synchronised over HA:
- System interface settings of the HA interface and HA default route.
- In-band HA management interface.
- HA override.
- HA device priority.
- Virtual cluster priority.
- FortiGate host name.
- Cache.
- All licenses except FortiToken licenses.
- GUI dashboard widgets.

On the primary, each inteface is assigned a virtual MAC address. Upon failover, the newly elected primary adopts the same virtual MAC addresses as the former primary. Gratuitous ARP informs the network that the virtual MAC address is now reachable through a different FortiGate.

### HA Modes
##### Active-Passive
In active-passive mode, the primary FortiGate is the only FortiGate that actively processes traffic. Secondary FortiGate devices remain in passive mode, monitoring the status of the primary device.

In either of the two HA operation modes, the operation information (sessions, FIB entries, and so on) of the primary FortiGate is synchronized with secondary devices. If a problem is detected on the primary FortiGate, one of the secondary devices takes over the primary role.

##### Active-Active
In Active-Active mode all cluster members can process traffic.

That is, based on the HA settings and traffic type, the primary FortiGate can distribute supported sessions to the secondary devices. If one of the secondary devices fails, the primary also reassigns sessions to a different secondary FortiGate.

### Failovers
To force a failover run: `diagnose sys ha reset-uptime`.

##### Election Process
1. Member with the most available monitored intefaces becomes the primary.
2. The member with the highest HA uptime, by at least 5 minutes, becomes the primary.
3. Member with the highest priority becomes the primary.
4. Member with the highest serial number becomes the primary.

If the HA override setting is enabled, the priority is considered before the HA uptime.
```
config system ha
	set override enable
end
```

If override is enabled, to trigger a failover you can change the HA priorities.

#### Failover Types
- **Device Failover**: Secondary devices stop receiving hello packets from the primary.
- **Link Failover**: The link of one or more monitored interfaces goes down.
- **Remote Link Failover**: One or more interfaces are monitored using the link health monitor. If primary fails the accumulated penalty of all failed intefaces reaches the configured threshold, a remote link failover occurs.
- **Memory-based failover**: Memory utilization on the primary exceeds the configured threshold and monitoring period.
- **SSD Failover**: FortiOS detects EXT-FS errors on the SSD.