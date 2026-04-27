#NSE5

### Overview
There are 2 types of Administrative profiles:

**System Admin**
System Admin profiles allow for a wider scope and granularity for configuring administrator permissions. You can allow them to view and configure as much or as little as possible.

**Restricted Admin**
This type allows you to delegate administrators the management of ***web filtering profiles, IPS sensors and application sensors*** associated with their ADOM. When a restricted administrator logs into the FortiManager, they enter the restricted admin mode.

Admin profiles can be configured under **System Settings** > **Administrators**.

#### Security
Administrators can be restricted by the following methods:

 - ADOMs: Administrators have access to only those ADOMs to which they are assigned.
 - Administrative Profiles: The level of access is determined by the administrative profile selected.
 - Trusted Hosts: This option restricts administrators to log in from only specific IP addresses or subnets. 

You can also configure an external server to validate your administrator log in's via LDAP, RADIUS, TACACS+ and public key infrastructure (PKI).

#### Monitoring
To track administrator sessions, including who is logged in and from what trusted host, navigate to **System Settings** > **Administrators**. Only the default admin account or users with the **super_user** profile can see the complete Administrators list.