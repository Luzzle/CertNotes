#vcf9 

### Host is unresponsive
This occurs wehen the ESX host stops responding and displays a purple diagnostic screen. This can be caused by the following:

- CPU exception
- Driver or module panic message
- Machine check exception
- Hardware fault
- Software defect

To recover from this state:
- Record the state of the system.
- Restart the host
	- If vSphere HA cannot restart the VMs due to existing logs, the VM must registered to a different host.
- Contact VMware technical support

To verify that a host is not responding, you can perform the following:
- Ping the management interface
- Determien if the client responds to queries.
- Monitor network traffic from the host and its VMs.

If any of these tasks are successful, your ESX host should be at least minimally operational. If so, use the esxtop utility to check CPU and memory utilization for the ESX host.

An operating ESX host running virtual machines can appear of `Not Responding` in vCenter. This can occur if:
- vpxa agent not running.
- ESX host not sending heartbeats to vCenter.
- SSL handshake failure between ESX host and vCenter.
- Network failure between ESX and vCenter.

### TLS Profile Troubleshooting
The state of TLS profiles is maintained using three main configuration files on disk:
- Definitions: `/etc/applmgmt/appliance/tls_settings.yaml`
- Active profile: `/var/lib/applmgmt/tls_settings.yaml`
- Global settings: `/var/lib/tls_settings/global_{service}.json`

Inconsistent TLS configuration per service can cause an SSL handshake failure and prevent communication between services.

