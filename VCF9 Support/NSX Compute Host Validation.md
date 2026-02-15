#vcf9 

### Overview
From ESX 9.0, the NSX vSphere Installation Bundles (VIBs) are included as part of the ESX host installation.

To verify the correct installation of the NSX VIBs, run the following on the ESX host.
`esxcli software vib list | grep "nsx\|vsip"`

#### Host Communications with NSX Manager
**Appliance Proxy Hub** acts as a communication channel between NSX Manager and the ESX transport node.

It offers the following functions:
- Runs as a service on the NSX Manager.
- Provides secure connectivity based on NSX-RPC.
- Uses port 1234 for communication between the management plane and transport node.
- Uses port 1235 for communications between the Central Control Plane (CCP) and transport node.

#### Troubleshooting Connectivity
You run the following commands to verify the status of agents and the controller-manager connectivity.
`/etc/init.d/nsx-proxy status`

For the manager: `esxcli network ip connection list | grep 1234`
For the controller: `esxcli network ip connection list | grep 1235`

We can also use the `nsxcli` utility.
- `get managers`
- `get controllers`

You can verify the VDS (Virtual Distributed Switch) configuration using `esxcfg-vswitch -l`.

#### Verify Overlay Tunnel Status
 To verify the overlay tunnel status, navigate to **System > Fabric > Hosts > Clusters** on the NSX UI home page, and Select **Tunnels** for a host.

#### Verify TEP Interfaces
On a host interfaces VMK10 and VMK11 are dedicated VMkernel interfaces which are used as TEP interfaces for Geneve or VXLAN overlay traffic.

You can verify these ports exist using `esxcli network ip interface ipv4 get`.

If these interfaces are assigned `169.254.x.x` IP's verify DHCP server configuration as it means they have failed to receive an IP address.

On a host you can run `vmkping ++netstack=vxlan [IP] -d (do not fragment) -s [SIZE] -I [vmk10/vmk11]` to verify that all TEPs can communicate successfully with **jumbo frames**.

**Geneve** is a more modern and extensible VXLAN protocol.

#### Log Files

| Log Use          | Log File                |
| ---------------- | ----------------------- |
| TEP Installation | `/var/log/vmkernel.log` |
| System Events    | `/var/log/syslog.log`   |
