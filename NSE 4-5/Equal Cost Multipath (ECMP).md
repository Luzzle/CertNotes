#NSE4 

### Overview

An ECMP route is a route that contains the same destination, distance, metric and priority as another route in the routing table.
![[Pasted image 20251226100550.png]]

### Load Balancing Algorithms

| Algorithm             | Description                                                                                                                                  |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Source IP             | Sessions sourced from the same address use the same route                                                                                    |
| Source-Destination IP | Sessions with the same source and destination address pair use the same route                                                                |
| Weighted              | Sessions are distributed based on route or interface weights. The higher the weight, the more sessions are routed through the selected route |
| Usage (Spillover)     | One route is used until the bandwidth threshold is reached, then the next route is used.                                                     |

![[Pasted image 20251226102721.png]]

### Configuration
```fortios
config system settings
	set v4-ecmp-mode [MODE]
end

config system interface
	edit [interface]
		set weight <0-255>
		set spillover-threshold <0-16776000 kbps>
		set ingress-spillover-threshold <0-16776000 kbps>
	next
end

config router static
	edit [route ID]
		set weight <0-255>
	next
end
```