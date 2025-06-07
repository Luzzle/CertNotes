#AutomationAndProgrammability #ccna-day62

### Overview
SDN is an approach to networking that centralized the control plane into an application called a controller.

The controller interacts with network devices using APIs.

The **SBI** is used for communications between the controller and the network devices it controls.
The **NBI** is what allows us to interact with the controller with scripts and applications.

### Layers
![[Pasted image 20250530163604.png]]

### SD Access
Cisco SD-Access is Cisco's SDN solution for automation campus LANs.
Cisco DNA Center is the controller at the center of SD-Access.

The **underlay** is the underlying physical network of devices and connections which provide IP connectivity.
- E.g. multilayer extensions and their connections.

The **overlay** is the virtual network built on top of the physical underlay network.
- SD access uses VXLAN (Virtual Extensible LAN) to build tunnels.

The **fabric** is the combination of the overlay and the underlay.

### Benefits of DNA Center
![[Pasted image 20250530164125.png]]

