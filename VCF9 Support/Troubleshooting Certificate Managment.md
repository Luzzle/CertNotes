#vcf9 

### Overview
You use VCF Operations console to view and manage the certificates for VCF.

You can perform the following:
	- View certificates and certificate alerts.
	- Enable automatic renewal of certificates.
	- Configure a certificate authority (CA).
	- Generate certificate signing requests (CSRs).
	- Replace certificates.

VCF Operations provides manual and automated digital certificate management.
- Fully automated by VCF - **[[Microsoft CA]]**.
- Partially automated: **Third-party CA**.

To view certificates in VCF Operations:
- Navigate to **Fleet Management > Certificates**.
- Click the VCF Instance.
- Select the Management or Workload Domain.

#### Certificate Status
Certificates can have a status of **Active**, **Expiring** or **Expired**. You are notified when certificates are approaching the end of the validity period.

To add an OpenSSL CA in VCF Operations, navigate to **Fleet Management > Certificates**.

### Replacing Certificates
Replacing certificates is an important task. You would replace a certificate for the following reasons:
- A certificate expired or is close to expiry.
- A certificate was revoked.
- You do not want to use the default VMware Certificate Authority certificate.
- (Optional) You create a workload domain.

After you configure a CA in VCF Operations, you can generate a certificate using a CSR, and then replace an existing certificate for a VCF component.

1. Generate a CSR.
2. Enter the information and click Save.
3. Select **Replace With Configured CA Certificate**.
4. Select your CA and click **Replace**.

##### Replacing using an External CA-Signed Certificate

1. Select a component, click on the ellipsis icon and click **Generate CSR**.
2. Enter the information for the CSR and click Save.
3. Click the ellipsis and select **Download CSR**.
4. When the download completes, request a signed certificate from your external CA.
5. Click the ellipsis icon and select **Import Certificate**.
6. Selct a source and enter the required information.
7. When the signed certificate is validated successfully and saved, select **Replace with Imported Certificate**.
8. Select the imported certificate and click Replace.

These tasks can be viewed in the `vcops-bridge.log` file.

### Verifying CA Configuration
To verify that the CA configuration was applied successfully, or troubleshoot an issue adding a CA, you can reviewing the `vcops-bridge.log` file on the VCF Operations appliance.