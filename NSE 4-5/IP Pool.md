#NSE4 

### Definition
IP Pools define a single IP address or range of IP addresses to be used as the source address for the duration of a session.

These IPs should be configured in the same range as the outgoing interface address.

There are 4 types of IP pools.
- Overload (PNAT)
- One-to-One
- Fixed Port Range
- Port block allocation

The latter 2 are useful for [CG-NAT](https://en.wikipedia.org/wiki/Carrier-grade_NAT).