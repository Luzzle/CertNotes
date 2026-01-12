#NSE4 

### Definition
A security profile inspects each packet in the traffic flow, where the session has been accepted by a firewall policy.

Security profiles configured in firewall policies protect your network by:
- Blocking threats
- Controlling access to certain applications
- Preventing specific data from leaving your network.

![[Pasted image 20251224185137.png]]


If a security profile detects a violation, Fortigate will record the attack log. To improve performance and reduce the number of logs, you can configure the Fortigate to log the denied session into the session table, and block all packets for that session automatically.

```
config system setting
	set ses-denied-traffic [disable | enable]
end
config system global
	set block-session-timer [1-300]
end
```

[[AntiVirus]]
[[Web Filter]]
[[Intrusion Protection]]
[[Application Control]]