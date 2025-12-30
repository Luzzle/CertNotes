#NSE4 

### Overview
DC Agent Mode is the recommended mode for FSSO.

DC Agent Mode requires the following:
- One DC agent installed on each Windows DC.
- A collector agent installed on a windows server that is a member of the domain you are trying to monitor. It consolidates events received from the DC agents, then forwards them to the FortiGate.

When a user logs on, the DC agent intercepts the login even ton the domain controller and sends the clients NetBIOS or DNS name to the collector agent. The collector agent then sends a request to the DNS server to resolve the name and verify whether the users IP address has changed.

![[Pasted image 20251227125811.png]]

The collector agent uses the NetBIOS naming convention (Domain\groups) to access the Windows AD in standard access mode.