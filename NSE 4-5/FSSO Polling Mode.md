#NSE4 

### Overview

No DC agent is required in this configuration. Instead, every few seconds the collector agent polls each DC for user login events. The collector agent uses:
- SMB (TCP 445) to request the event logs.
- TCP 135, 139 and UDP 137 as fallbacks.

There are 3 main methods:

| WMI                                                                                       | WinSecLog                                                                                                | NetAPI                                                                                                            |
| ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| DC returns all requested login events every 3 seconds.                                    | Polls all security events on DC every 10 seconds or more, depending on server count and network latency. | Polls the NetSessionEnum function on Windows every 9 seconds. This polls the authentication session table in RAM. |
| Improves WinSec bandwidth usage which reduces network load between collector agent and DC | This is slower but sees all login events.                                                                | Retrieves login sessions, includes DC login events.                                                               |


Event logging must be enabled on the DC's (except in NetAPI configurations.)