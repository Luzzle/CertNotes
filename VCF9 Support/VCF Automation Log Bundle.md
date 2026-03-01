#vcf9 

### Overview
You generate and downlaod a VCF Automation log bundle from the VCF Operations console.  When generating a log bundle, you specify the number of days for which you want to collect the logs. After the log bundle generation is complete, it is downloaded in a *tar.gz* format.

VCF Automation logs are automatically forwarded to VCF Operations for Logs if the appliance has been deployed in the environment. These can be viewed from **Infrastructure Operations > Analyze > Logs**

### Structure
The top-level support bundle structure includes the following files and directories.

- **antrea, apiserver-audit, audit, system-logs** - Logs for system services.
- **clusterdump** - Snapshots of cluster configuration and state.
- **cluster-info-dump.log** - Fetching log events and cluster information collection.
- **environment** - Summary file for VCF Automation backward compatibility.
- **metrics** - Snapshots of cluster metrics.
- **service-logs** - Logs for VMSP and component services.

##### Service-Logs
The services-logs folder of VCF Automation log bundle presents a hierarchical structure that allows you to review log information at the container level.

##### Cluster Dump
The clusterdump directory in the VCF Automation support log bundle includes multiple snapshots of the cluster configuration and state.

| Directory / Log | Description                                              |
| --------------- | -------------------------------------------------------- |
| crds            | Dumps of custom resource definitions                     |
| events.txt      | Events table                                             |
| failed-pod-logs | Snapshots of logs for currently failed pods              |
| live.txt        | Live call results                                        |
| nodes.txt       | Nodes table                                              |
| overview.txt    | Summary file containing commonly useful data             |
| ready.txt       | Ready call results                                       |
| top-nodes.txt   | Top output for nodes                                     |
| top-pods.txt    | Top output for pods                                      |
| table           | table data for Kuberenetes objects by type and namespace |
| yaml            | YAML output for Kubernetes objects by type and namespace |
