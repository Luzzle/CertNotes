#ManagingVNETs 

### Definition
An NSG contains a list of security rules that allow or deny inbound or outbound network traffic. This can be associated with a subnet, or NIC and can be associated multiple times.

| Setting            | Value                                                                                                                                                                                                 |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Source             | Any, IP Addresses, My IP address, Service Tag, or Application security group                                                                                                                          |
| Source port ranges | Specify the ports on which the rule allows or denies traffic                                                                                                                                          |
| Destination        | Any, IP Addresses, Service Tag, or Application security group                                                                                                                                         |
| Protocol           | Restrict the rule to the Transmission Control Protocol (TCP), User Datagram Protocol (UDP), or Internet Control Message Protocol (ICMP). The default is for the rule to apply to all protocols (Any). |
| Action             | Allow or Deny                                                                                                                                                                                         |
| Priority           | A value between 100 and 4,096 that's unique for all security rules within the NSG                                                                                                                     |
### Rule Evaluation
- Inbound: Azure evaluates NSG rules for subnets before NICs.
- Outbound: Azure evaluates NSG rules for NICs before subnets.
