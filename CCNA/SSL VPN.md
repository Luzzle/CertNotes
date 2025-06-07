#SecurityFundamentals #ccna-day53

*Cristian's Note - This is also known as a remote access VPN or TLS VPN, no-one in real life calls them that. For all intents and purposes this is an SSL VPN and most real configurations (e.g. FortiGate configuration) will refer to it as such.*
### Overview
SSL VPNs allow end devices to access the companies internal resources securely over the internet.
SSL VPNs typically use TLS (formerly named SSL) for security.

VPN clients are installed on end-devices, which then form tunnels to one of the companies routers/firewalls over the internet from anywhere, which allows secure access to internal resources.

The company router/firewall essentially acts as a TLS server and decrypts the packet before forwarding it to its intended destination.