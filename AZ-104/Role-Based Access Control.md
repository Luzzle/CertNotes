#IdentityAndGovernance 

### Overview
Azure has **3 types** of roles that serve the same purpose.

1) Classic Subscription Admin
2) Azure Roles a.k.a *Role-Based Access Controls* and is built ontop of Azure Resource Manager
3) Azure Active Directory roles used to manage Azure AD in a directory.

Azure RBAC helps you manage access to Azure Resources.

#### Role Assignments
Role Assignments are the way you control access to resources.

A role assignment consists of three elements:
1) *Security Principal* - the identities requesting access to an Azure resource.
2) *Role Definition* - collection of permissions.
	- Role definitions list the operations that can be performed, such as RWD.
3) *Scope* - the set of resources that access for the Role Assignment applies to.

#### Anatomy of an Azure Role
```json
{
	"Name": "VM Operator",
	"Id": "Role-ID",
	"IsCustom": true,
	"Description": "Can monitor and restart VMs",
	"Actions": [
		"Microsoft.Compute/*/read",
		"Microsoft.Compute.virtualMachines/start/action"
		...etc...
	],
	"NotActions": [],
	"DataActions": [],
	"NotDataActions": [],
	"AssignableScopes": [
		"/subscriptions/Sub1"
	]
}
```
