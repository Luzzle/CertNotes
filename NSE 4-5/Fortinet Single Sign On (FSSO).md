#NSE4 

### Definition
FSSO is a software agent that enables FortiGate to identify network users for security policies or VPN access, without asking for their username and password.
When a user logs onto a directory service, the FSSO agent sends the FortiGate the username, ip address and list of groups, which the FortiGate uses to maintain a local database.

Authentication is performed by the domain controller, not the FortiGate.

### FSSO for Windows AD
FSSO for Windows AD uses a collector agent. There are 2 modes that monitor user sign on activities. 

- [[FSSO DC Agent Mode|DC Agent Mode]]
- [[FSSO Polling Mode|Polling Mode]]

[[FSSO Agentless Polling Mode|FortiGate also offers a polling mode that does not require an agent]], this is intended for small networks with minimal users.

For Citrix and Terminal Services environments, Fortigate offers the Terminal Server (TS) agent. This also requires the Windows AD collector agent.
This gathers logins for Citrix and Terminal servers where multiple users must share the same IP.

### Troubleshooting

General troubleshooting can be done using System Events (Log & Report > System Events > User Events).

``` fortios
	diagnose debug authd fsso [TAB]
```

#### Currently Logged-In Users

```fortios
	diagnose debug authd fsso list
```

#### Connection to FortiGate

```fortios
	diagnose debug authd fsso server-status
```

#### Polling Mode

```fortios
	diagnose debug fsso-polling detail
	diagnose debug fsso-polling refresh-user
	diagnose debug application fssod -1
```
