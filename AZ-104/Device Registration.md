#IdentityAndGovernance 

### AD Registered Devices
Provide users with support for BYOD support. These devices are registered to Microsoft Entra ID without requiring an organizational account to sign in to the device.

Microsoft Entra ID registration can be accomplished when accessing a work application for the first time or manually using the Windows 10 Settings menu.

Administrators can secure and further control these devices using Mobile Device Management tools like Microsoft Intune, but will require AD Premium 2.

**MDM** - Controls the entire device and can wipe data from it.
**MAM** - Mobile Application Management. Can publish, push, configure, secure and monitor mobile apps.

### AD Joined Devices
Devices signed in to using an organizational Microsoft Entra account directly. This is aimed to be used for companies who operate in a hybrid or cloud-only environment.

The capabilities include SSO to both cloud and on-prem resources and conditional access. 

Administrators can secure and further control Microsoft Entra joined devices using MDM tools, or in co-management scenarios using Microsoft Endpoint Configuration Manager.

### Hybrid AD Joined Devices
Devices joined to on-premises AD and Microsoft Entra ID requiring an organizational account to sign into the device.

