#IdentityAndGovernance

### Overview
Active Directory is a cloud-based **identity and access** management service.
[[Active Directory Objects]]

| External Resources   | Internal Resources                           |
| -------------------- | -------------------------------------------- |
| Microsoft Office 365 | Applications within your internal networking |
| Azure Portal         | Access to workstations on prem.              |
| SaaS Applications    |                                              |
**Active Directory** - On Prem
**Azure AD** - Cloud

AD comes in 4 editions.

| Edition         | Feature Set                                                        |
| --------------- | ------------------------------------------------------------------ |
| Free            | MFA, SSO, Security and Usage reports, User Management              |
| Office 365 Apps | Company Branding, SLA, Two-Sync between on-prem and cloud          |
| Premium 1       | Hybrid Architecture, Advanced Group Access, **Conditional Access** |
| Premium 2       | Identity Protection, Identity Governance                           |

### Terminology
**Domain**: An area of a network organized by a single authentication database. 
**AD Domain**: Logical grouping of AD objects on a network.
**Domain Controller (DC)**: A server that authenticates user identities and authorizes their access to resources.
**AD Object**: Basic element of AD. Users, groups, devices etc...
**Group Policy Object (GPO)**: Collection of policy settings which control what AD objects have access to
**Organization Unit (OU)**: A sub-division within an Active Directory which you can place users, groups and devices as well as other OUs.
**Directory Service**: A directory service such as *AD DS* provides the methods for storing data, and making this data available to users and admins. A DS runs on a DC.

### Azure Services
#### Azure Active Directory Domain Services (AD DS)
Azure AD DS provides a managed domain service such as:
- Domain joins
- Group policies
- Lightweight Directory Access Protocol (LDAP)
- Kerberos / NTLM authentication

You can use these services without the need to deploy, manage and patch DC's in the cloud.

#### Azure AD Connect
Azure AD Connect is a hybrid service to connect your on-prem AD to your Azure account. This allows for seamless SSO from your on-premises workstation to Azure. 

AD Connect has the following features:

| Feature                       | Description                                                                                       |
| ----------------------------- | ------------------------------------------------------------------------------------------------- |
| Password Hash Synchronisation | Synchronizes the hash of a users on-prem AD password with Azure AD.                               |
| Pass-through Authentication   | Allows users to have the same password on prem as in the cloud.                                   |
| Federation Integration        | Hybrid environment using an on-prem AD FS infrastructure for certificate renewal                  |
| Synchronization               | Responsible for creating users, groups and other objects, ensuring on-prem and cloud data matches |
| Health Monitoring             | Provides a central location for monitoring health statistics                                      |

### AD Access Right Assignment
**Direct Assignment** - the resource owner directly assigns the user to the resource.
**Group Assignment** - the resource owner assigns an AD group to the resource, which gives all group members access to the resource.
**Rule-based Assignment** - the resource owner creates a group and uses a rule to define which users are assigned to a specific resource.
**External Authority Assignment** - access comes from an external source, such as an on-prem AD or SaaS app.