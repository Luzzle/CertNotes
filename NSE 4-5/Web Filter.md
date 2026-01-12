#NSE4 

### Overview
When the server [[Certificates|certificate]] SNI check configuration is set to **enable** FortiGate uses the CN field instead of the domain in the SNI Field. If the SNI field does not match any of the domains in the CN or SAN field, the connection is closed.

If it is set to Disable, FortiGate always rates URLs based on the FQDN.

### Inspection Modes

| Flow-based                                                                 | Proxy-based                                                           |
| -------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| Faster response time                                                       | FortiGate buffers traffic and examines it as a whole                  |
| Less change of a time-out error caused by the server                       | Examines more points of data                                          |
| FortiOS 7.4.4 and later - supports safe search and restrictions on YouTube | Proxy analyzes the headers and may change, such as HTTP host and URL. |
| Requires fewer processing resources                                        |                                                                       |

The **log all search keywords** feature is only available in proxy-based mode.

### Category Filter
This allows a FortiGate to block or allow websites based on website categorisation.

The following actions are available per category.
- Allow
- Monitor
- Block
- Warning
- Authenticate

#### Web Rating Override
This allows you to manually set the category if you believe it has been incorrectly categorised.

### URL Filter
This allows the FortiGate to perform one of the below actions based on the visited URL.

- Exempt: allows the traffic to bypass the security inspections.
- Block: denies the traffic and the user receives a replacement message.
- Allow: permits traffic and it is passed to the remaining operations.
- Monitor: allows the traffic while creating log entries. The traffic is still subject to all the other security profile inspections.

### HTTPS Inspection Order
**!! This is important !!**

URL -> Static URL filter -> Category Filter -> Advanced Filter -> Display Page
