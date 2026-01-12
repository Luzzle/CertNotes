#NSE4 

### Overview

IPS Signatures and filters are evaluated from top to bottom. Source and destination IP addresses can be added as exemptions to specific signatures.

The following actions can be taken:
1. Allow: Allows traffic to continue to its destination
2. Monitor: Logs the activity but it is allowed
3. Block: Silently drops the traffic without matching any of the signatures in the entry.
4. Reset: Generates a TCP RST packet whenever the signature is triggered.
5. Default: Use the default action of the signatures.

To get the maximum benefit from your IPS features, you should enable deep packet inspection.

### Components
An Intrusion Prevention System is comprised of the following components.

1. Signatures - IPS uses signature databases to detect known attacks and exploits.
2. Protocol Decoders - This is used to detect network errors and protocol anomalies. 
3. IP Engine - Response for the IPS and protocol decoders, application control, flow-based antivirus protection etc...

### IPS Fail Open
Fail open is triggered when the IPS socket buffer is full and new packets can't be added for inspection.

```FortiOS
config ips global
	set fail-open <enable | disable> 
end
```

Enable - Bypass the packet without inspection
Disable - Drop the new packet (default)