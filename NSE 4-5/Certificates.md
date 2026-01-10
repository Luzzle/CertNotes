#NSE4 

### Overview
A Digital Certificate is a file or password used to authenticate a device or server through cryptography and public key infrastructure (PKI).

It is a digital document produced and signed by a Certificate Authority (CA).

**Use cases:**
- Identification of an entity or device.
- Verification of website legitimacy (aka SSL certificate).

Certificates serve three primary purposes:
- Authentication: The **Common Name (CN)** field or **Subject Alternative Name (SAN)** field are both used to identify the device the certificate is representing.
- Encryption and Decryption: Private and public key pairs are used to decrypt and encrypt traffic.
- Integrity: Messages are hashed using a secret key known to both the sender and the receiver. The receiver uses the key to check the hash value and confirm the integrity of the message data.

FortiGate identifies the device or person by reading the CN value in the Subject field, which is expressed as a **Distinguished Name (DN)**.

FortiGate supports the X.509v3 certificate standard.


### SSL Inspection

#### SSL Certification Inspection
FortiGate extracts the FQDN of the URL from either the TLS Server Name Indication (SNI) and SSL certificate Subject or SAN fields. This is used for web filtering.

#### Full SSL Inspection
Fortigate acts as a man in the middle proxy which maintains 2 seperate SSL sessions, client to Fortigate and Fortigate to server.
The Fortigate encrypts and decrypts packets using its own keys and can inspect the traffic.
![[Pasted image 20260110140338.png]]

##### Fortigate Self-Signed CA Certificates
By default, FortiGate uses a self-signed encrypting SSL CA certificate called `Fortinet_CA_SSL`.

This is not listed with an approved CA and by default not trusted. To avoid this, install the CA certificate as a trusted CA on user devices or install a company CA on FortiGate for SSL full inspection.

