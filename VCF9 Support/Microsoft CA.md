#vcf9 

### Overview
SDDC Manager uses the Certification Authority Web Enrollment role in AD to obtain signed certificates.

To use this service:
1. Configure and issue a VMware Certificate template for Machine SSL and Solution User certificates on this CA server.
2. Configure the web server Internet Information Services (IIS) security setting to use basic authentication.
3. Ensure that the service acount that you configure on SDDC Manager has least priviledge access to the CA service.

#### Configuration
To add a Microsoft CA, navigate to **Fleet Management > Certificates**.