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
```powershell
New-AzResourceGroupDeployment `
	-Name {name} `
	-TemplateFile {path to template file}
```

### Parameters
ARM template parameters allow you to customise the deployment by providing values that are tailored for a specific environment.

In the parameters section of the template, you specify which values you can input when you deploy the resources. 

#### Format
```json
"parameters": {
  "<parameter-name>": {
    "type": "<type-of-parameter-value>",
    "defaultValue": "<default-value-of-parameter>",
    "allowedValues": [
      "<array-of-allowed-values>"
    ],
    "minValue": <minimum-value-for-int>,
    "maxValue": <maximum-value-for-int>,
    "minLength": <minimum-length-for-string-or-array>,
    "maxLength": <maximum-length-for-string-or-array-parameters>,
    "metadata": {
      "description": "<description-of-the-parameter>"
    }
  }
}
```

#### Types
- String
- secureString
- Integer
- Boolean
- Object
- secureObject
- Array

The parameter can be used in a resource definition with the following syntax.
`[parameters('name')]`

You can also provide the value for a parameter when deploying from the CLI
```powershell
New-AzGroupDeployment `
	-paramName ParamValue
```

### Outputs
The outputs section allows you to specify which values are returned after a successful deployment.

#### Format
```json
"outputs": {
  "<output-name>": {
    "condition": "<boolean-value-whether-to-output-value>",
    "type": "<type-of-output-value>",
    "value": "<output-value-expression>",
    "copy": {
      "count": <number-of-iterations>,
      "input": <values-for-the-variable>
    }
  }
}
```
