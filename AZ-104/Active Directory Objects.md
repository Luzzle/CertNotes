#IdentityAndGovernance 

#### Users
**Users** represent an identity for a person or employee in your domain. 
- Users can be assigned roles
- Users can be added to groups
- Users can have authentication methods like MFA
- Sign in's can be tracked, including onto devices
- MS Licenses can be assigned

##### Types of Users
**Users** - belongs to your organization.
**Guest Users** - belongs to another organization.

#### Groups
**Groups** assign a set of access permissions to all members of the group, instead of providing the rights one by one.

Groups contain:
**Owners** - permissions to add and remove members
**Members** - get assigned permissions


#### Roles
Azure AD roles are used to manage AD resources in a directory such as:
- creating or editing users
- assigning admin roles
- resetting user passwords
- managing licenses
- managing domains

*Built in roles*
- Global Administrator - Full access to all
- User Administrator - Full access to creating and managing users
- Billing Administrator - Ability to make purchases

Creating custom roles will require **AD Premium P1 or P2**

