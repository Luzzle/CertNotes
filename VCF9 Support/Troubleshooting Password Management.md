#vcf9 

### Overview
VCF manages the passwords for multiple components and solutions. You must ensure you have a reguarly scheduled rotation policy.

You can rotate and update passwords using the password management functionality using VCF Operations, including:
	- ESX root account
	- SSO admin account
	- Admin user account used by virtual appliances
	- Service accounts that are automatically generated during deployment

#### Best Practice
- Change passwords immediately after deployment.
- Monitor component password expiration details.
- Rotate passwords at least every 90 days.
- Secure copies of passwords to comply with enterprise policy.

#### Expiry Notifications
VCF Operations runs a scheduled job every day that retreives the account password state from each connected component and displays the following alerts:

- Any password that is expired
- Any password that expires in the next 14 days

#### Checking Password Health
##### SoS Utility
SSH into SDDC Manager and run the following `sudo /opt/vmware/sddc-support/sos --password-health`

### Updating Passwords for VCF Components
Changing these passwords periodically or when certain events occur, such as an administrator leaving your organization, reduces the likelihood of security vulnerabilities.

Validate the below requirements:
- No pending or active workflows are pending, running or scheduled.
- Ensure you have sufficient privileges.

#### Managing Passwords using VCF Operations
VCF Operations provides the following options:

##### Components Page
**UPDATE PASSWORD**: Updates the password for an account that is in sync with SDDC Manager.
**REMEDIATE PASSWORD**: Synchronises the components current password with the SDDC Manager database. Only a user with the ADMIN role can perform this task.

##### Password Management
**Rotate All Passwords**: Randomizes passwords for all accounts.
**Rotate Password**: Randomizes passwords for the selected accounts.
**Schedule Rotation**: You can set the password rotation interval (30 days, 60 days or 90 days).

### Scheduling Password Rotation
Password rotation schedules are only available for certain products and while using supported accounts.

| Product        | Supported User Accounts                             |
| -------------- | --------------------------------------------------- |
| vCenter        | root<br>SDDC service account<br>NSX service account |
| vCenter SSO    | administrator@vsphere.local                         |
| NSX Manager    | admin<br>root<br>audit<br>SDDC service account      |
| NSX Edge nodes | admin<br>root<br>audit                              |

##### Considerations
- Set the password rotation interval to a period shorter than the period in your password expiration policy.
- If your environment has more than one VCF instance joined to a single vCenter SSO domain, do not schedule password rotation for the administrator@vsphere.local account.
- Autorate is automatically enabled for the vCenter system. Considering the autorotate policy for a newly deployed vCenter might take up to 24 hours.

### Common Password Operation Failures
- Target components have expired passwords.
- The dependent resources have expired or invalid passwords.
- Passwords are manually changed outside SDDC Manager.
- vCenter SSO has expired service accounts.
- SDDC Manager is locked because of password update operation failures.
- Expired passwords can cause password rotation workflow to fail.
- API calls to dependent resources fail if passwords are expired or invalid.
- Mismatches occur between the SDDC Manager database and component password.

### Log Files

| Component    | Log File                                                                  |
| ------------ | ------------------------------------------------------------------------- |
| HTTP API Web | `/storage/log/vcops/log/http_api.log`<br>`/storage/log/vcops/log/web.log` |
| Platform-api | `/storage/log/vcops/log/api.log`                                          |
| VCOPS Bridge | `/storage/vcops/log/vcops-bridge.log`                                     |
| Collector    | `/storage/vcops/log/adapters/ManagementAdapter/ManagementAdapter_xx.log`  |
