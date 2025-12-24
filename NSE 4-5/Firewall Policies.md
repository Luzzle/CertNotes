#NSE4 

### Definition
A firewall policy is a set of instructions to control traffic flow through a FortiGate. These instructions determine where the traffic goes, how its handled and whether or not its allowed through the FortiGate at all.

Policies are evaluated from top to bottom of the sequence list. If no policies are matched, the traffic is dropped.

By default each policy must have a name if configured from the GUI, but this can be disabled in `System > Feature Visbility > Allow Unnamed Policies`

[[Security Profiles]]

##### Identification
A **Policy ID** is assigned when a new rule is created. This is used to uniquely identify the policy and differs from the sequence number, which is used to determine the order in which policies are evaluated.

```fortios
config firewall policy
	edit 1 <-- POLICY ID
```


### Policy Types

| Policy Type     | Description                                                         |
| --------------- | ------------------------------------------------------------------- |
| Firewall Policy | Set of rules that govern traffic that flows *through* the firewall. |
| Multicast       | Allows multicast traffic to flow from one interface to another.     |
| Local-In Policy | Controls traffic that is destined directly for the firewall itself. |
| DoS Policy      | Checks for anomalous patterns within network traffic.               |


### Configuration

```fortios
config firewall policy
	edit 1
		set name "Name"
		set action [accept | deny]
		set srcaddr <name1>, <name2>, ...
		set dstaddr <name1>, <name2>, ...
		set srcintf <name1>, <name2>, ...
		set dstintf <name1>, <name2>, ...
	next
end
```


### Inspection Modes

#### Flow Based
Flow based inspection identifies and blocks threats in real time as FortiOS identifies them. This prioritises traffic throughput.

#### Proxy Based
Proxy based inspection involves buffering traffic and examining it as a whole, before determining an action. Having all the data to analyze allows for the examination of more data points than flow based.

Some security profiles are only available in proxy-based inspection.
- Most notably WAF.

Proxy based inspection is not available on low-end platforms with 2GB of RAM or less.

### Logging
By default, only allowed traffic that has security profiles applied, will generate logs. This can be changed to log All Sessions. 