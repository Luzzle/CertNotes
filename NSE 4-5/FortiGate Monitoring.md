#NSE4 

### Logging Workflow
1. Traffic passes through FortiGate to your network
2. FortiGate scans the traffic and acts based on configured policies
3. FortiGate records the activity and stores information in a log message
4. FortiGate adds the log message to a log file (either remote on a FortiAnalyzer or on the local device)

### Log Types
#### Traffic
*Traffic* logs record traffic flow information. It contains 3 subtypes:

| Type    | Description                                                                                                         |
| ------- | ------------------------------------------------------------------------------------------------------------------- |
| Forward | Contains information about traffic that the firewall has either accepted or rejected according to a firewall policy |
| Local   | Contains information about traffic sent directly to and from Fortigate management IP addresses.                     |
| Sniffer | Contains information about traffic seen by the one-arm sniffer                                                      |

#### Event
*Event* logs record system and administrative events such as adding or modifying a setting, or daemon activities.

#### Security
*Security* logs record security events such as virus attacks or intrusion attempts. These are based on security profile type. 
