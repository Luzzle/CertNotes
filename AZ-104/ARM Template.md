#PrequisitesForAzureAdministrators

*Azure Resource Manager* templates.
### Overview
ARM templates are JSON files that define the infrastructure and configuration for a deployment. They allow you to declare what you intend to deploy without having to write the sequence of programming commands to create it.

You specify resources and define properties of those resources.

### File Structure

| Element               | Description                                                                                 |
| --------------------- | ------------------------------------------------------------------------------------------- |
| schema                | Defines the location of the JSON schema file that describes the structure of the data.      |
| contentVersion        | Defines the version of your template.                                                       |
| apiProfile (optional) | Defines a collection of API versions for resource types.                                    |
| parameters (optional) | Define values that are provided during deployment.                                          |
| variables (optional)  | Define values that are used to simply template langauge expressions                         |
| functions (optional)  | Define user-defined functions that can be used in the template.                             |
| resources             | Defines the actual items you want to deploy or update in a resource group or a subscription |
| output (optional)     | Specify which values are returned at the end of the deployment                              |
### Deployment
```Azure CLI
az group create --name {name of RG} --location '{location}' -> create resource group
az deployment group create \
	--name {name} \
	--resource-group {name of RG}
	--template-file {path to template file}
```

