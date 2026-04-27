#NSE5 

### Overview
FortiManager provides automation-driven, centralized management of your Fortinet devices from a single console. Centralized management through FortiManager can help you to more easily manage many deployment types with many devices and reduce cost of operation.

What can FortiManager do?
- Provision firewall policies across your network.
- Act as a central repository for configuration revision control and security audits.
- Deploy and manage complex mesh-and-star IPsec VPNs.
- Act as a private FortiGuard Distribution Network (FDN) server for your managed devices.
- Automate device provisioning and keep track of policy changes.

#### Features
- Centralized Management
- [[ADOMs|ADOM]]
- Revision control
- Fortiguard provisioning
- Firmware management
- Manager Panes
- Logging and Reporting
- MEAs - allows you to run licensed apps as docker containers on FortiManager.

#### Ports

| Functionality                                                        | Port                           |
| -------------------------------------------------------------------- | ------------------------------ |
| **INCOMING**                                                         |                                |
| Web Filter queries, anti virus, IPS updates                          | UDP 53, UDP/TCP 8888, TCP 80   |
| Antispam                                                             | UDP/TCP 8889                   |
| Registration for license validation and UTM updates (antivirus, IPS) | TCP 8890, TCP 443              |
| FortiGuard and FortiClient web filter and email filter               | TCP 8900, TCP 443              |
| **OUTGOING**                                                         |                                |
| Antivirus and IPS push updates                                       | UDP 9443                       |
| **INCOMING AND OUTGOING PORTS**                                      |                                |
| FGFM Management                                                      | TCP 541 (IPv4), TCP 542 (IPv6) |
By default the standard management ports are HTTP, HTTPS and SSH.

### FortiAnalyzer Mode
If you enable logging features, FMG can act as a FortiAnalyzer device. There are certain limitations to this however.
- Log rate and daily quota limitations are in place.
	- FortiManager supports up to 150 logs per second only.
	- FortiAnalyzer related licensing is not stackable.
- If FAZ features are enabled, you cannot add FortiAnalyzer to FortiManager and you cannot enable FortiManager HA.
