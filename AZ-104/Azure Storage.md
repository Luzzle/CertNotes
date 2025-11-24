#AzureStorage

### Definition
**Azure Storage** is Microsoft's cloud storage solution for modern data storage scenarios. Azure Storage offers a massively scalable object store for data objects. It is an AI-ready service that you can use to store files, messages, tables, and other types of information. You use Azure Storage for applications like file shares.

#### Categories of Data

| Category                 | Description                                                                                                                                                                                            | Storage examples                                                                                                                                                                                                                                                                   |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Virtual machine data** | Virtual machine data storage includes disks and files. Disks are persistent block storage for Azure IaaS virtual machines. Files are fully managed file shares in the cloud.                           | Storage for virtual machine data is provided through Azure managed disks. Data disks are used by virtual machines to store data like database files, website static content, or custom application code. The number of data disks you can add depends on the virtual machine size. |
| **Unstructured data**    | Unstructured data is the least organized. The format of unstructured data is referred to as _nonrelational_.                                                                                           | Unstructured data can be stored by using Azure Blob Storage and Azure Data Lake Storage. Blob Storage is a highly scalable, REST-based cloud object store. Azure Data Lake Storage is the Hadoop Distributed File System (HDFS) as a service.                                      |
| **Structured data**      | Structured data is stored in a relational format that has a shared schema. Structured data is often contained in a database table with rows, columns, and keys. Tables are an autoscaling NoSQL store. | Structured data can be stored by using Azure Table Storage, Azure Cosmos DB, and Azure SQL Database. Azure Cosmos DB is a globally distributed database service. Azure SQL Database is a fully managed database-as-a-service built on SQL.                                         |
[[Azure Storage Types|Types of Storage]]


### Storage Accounts
**Standard** storage accounts use standard hard disk drives (HDD). They are slower but provide the lowest code per GB.
**Premium** storage accounts use solid state drives (SSD), and offer low latency performance. 

| Storage account             | Supported services                                                                        | Recommended usage                                                                                                                                                                                                                                                                   |
| --------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Standard General-Purpose v2** | Blob Storage (including Data Lake Storage), Queue Storage, Table Storage, and Azure Files | Standard storage account for most scenarios, including blobs, file shares, queues, tables, and disks (page blobs).                                                                                                                                                                  |
| **Premium block blobs**         | Blob Storage (including Data Lake Storage)                                                | Premium storage account for block blobs and append blobs. Recommended for applications with high transaction rates. Use Premium block blobs if you work with smaller objects or require consistently low storage latency. This storage is designed to scale with your applications. |
| **Premium file shares**         | Azure Files                                                                               | Premium storage account for file shares only. Recommended for enterprise or high-performance scale applications. Use Premium file shares if you require support for both Server Message Block (SMB) and NFS file shares.                                                            |
| **Premium page blobs**          | Page blobs only                                                                           | Premium high-performance storage account for page blobs only. Page blobs are ideal for storing index-based and sparse data structures, such as operating systems, data disks for virtual machines, and databases.                                                                   |

### Replication Configurations
#### Locally Redundant Storage (LRS)
LRS is the lowest cost replication option. Your storage is replicated twice across a single datacenter. LRS can be appropriate in several scenarios:

- Your application stores data that can be easily reconstructed if data loss occurs.
- Your data is constantly changing like in a live feed, and storing the data isn't essential.
- Your application is restricted to replicating data only within a location due to data governance requirements.

#### Zone Redundant Storage (ZRS)
Zone redundant storage synchronously replicates your data across three storage clusters in a single region. Each storage cluster is physically separated from the others and resides in its own availability zone. ZRS provides excellent performance and low latency.

#### Geo Redundant Storage (GRS)
Geo-redundant storage replicates your data to a secondary region. This provides redundancy, even during a regional outage.
If you implement GRS, you have two related options to choose from:

- **GRS** replicates your data to another data centre in a secondary region. The data is available to be read only if Microsoft initiates a failover from the primary to secondary region.
- **Read-access geo-redundant storage** (RA-GRS) is based on GRS. RA-GRS replicates your data to another data center in a secondary region, and also provides you with the option to read from the secondary region. With RA-GRS, you can read from the secondary region regardless of whether Microsoft initiates a failover from the primary to the secondary.

#### Geo-Zone Redundant Storage (GZRS)\
Geo-zone-redundant storage combines the high availability of zone-redundant storage with protection from regional outages as provided by geo-redundant storage. Data in a GZRS storage account is replicated across three Azure availability zones in the primary region, and also replicated to a secondary geographic region for protection from regional disasters.

### Storage Access
| Service           | Default endpoint                                    |
| ----------------- | --------------------------------------------------- |
| **Blob service**  | `//`**`mystorageaccount`**`.blob.core.windows.net`  |
| **Table service** | `//`**`mystorageaccount`**`.table.core.windows.net` |
| **Queue service** | `//`**`mystorageaccount`**`.queue.core.windows.net` |
| **File service**  | `//`**`mystorageaccount`**`.file.core.windows.net`  |
You can configure a custom domain to access blob data in your Azure storage account. **Direct mapping** lets you enable a custom domain for a subdomain to an Azure storage account. For this approach, you create a `CNAME` record that points from the subdomain to the Azure storage account.

Access can be restricted from public / private networks in the Networking tab.
![[Pasted image 20251124141921.png]]


This will allow access from the internet, restrict to only private networks (such as express routes) or none at all (forcing the use of a private endpoint for example)