#vcf9 

#### Architecture

| Attribute      | vSphere                          | VCF                                                                          |
| -------------- | -------------------------------- | ---------------------------------------------------------------------------- |
| **Management** | Managed using vCenter and tools. | One VCF Operations manages all VCF instances.                                |
| **Automation** | Customer-built scripts.          | Built in automation for deployment, configuration and life-cycle management. |
### vSphere Foundation

##### Limitations

- vSphere Foundation has no Workload Domain construct so all operations are converted.
- Customers with NSX or Aria automation must use VCF because vSphere does not support it.