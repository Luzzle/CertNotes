#IdentityAndGovernance

### Overview
Entra ID is a PaaS (Platform as a Service) used for providing secure access for cloud based resources for organisations and individuals. It provides developers with centralised authentication and authorisation for applications in Azure.

[[Device Registration]]

#### Features
- Configuring access to applications
- SSO for cloud-based SaaS applications
- Managing users and groups
- Provisioning users
- Enabling federation between organisations
- Providing an identity management solution
- Identifying irregular sign in activity
- MFA
- Extending on prem AD solutions to the cloud
- Conditional Access

###### Conditional Access
Conditional access allows for configuration of access control for users based on device, Entra-ID group or location.

###### Entra Connect Health
Used to gain operational insights into Entra ID. It contains alerts, performance counters, usage pattern data and configuration settings.

###### PIM (Privileged Identity Management)
PIM allows you to configure additional security levels of privileged users, such as administrators. You can define permanent or temporary roles.

### Tenant
Entra ID is multi-tenant by design. In this context a tenant is a organisation or individual who signed up for an Azure Subscription. 

A subscription can only have one Entra ID tenant, however multiple subscriptions can be associated to the same tenant.

### Users
**Cloud Identities**
- Users that exist only in Entra ID like Administrators and other users that are managed.
- **Source**: Microsoft Entra ID, External Microsoft Entra Directory

**Directory Synchronised Identities**
- Users that are synchronised over from an on prem [[Active Directory]] through Microsoft Entra Connect.
- **Source**: Windows Server AD

**Guest Users**
- Users that exist outside of Azure from another cloud provider.
- **Source**: Invited User

### Groups
**Security Groups**
- Used to manage member and computer access to shared resources for a group of users.
- E.g. creating a group for a specific security policy.

**Microsoft 365 Groups**
- Used to promote collaboration, giving users access to shared resources like mailboxes, files,  Sharepoint sites etc...

### Custom Domains
A custom domain that you own can be added to an Entra ID tenant. To validate you own the domain you must also add a TXT or MX record to the domain through the registrar using info provided by Azure.

This allows you to create users and other services using your custom domain, instead of using MS's domain.

### Administrative Units
An Administrative Unit separates administrative permissions to groups of administrators. Can be thought of as different "departments".
