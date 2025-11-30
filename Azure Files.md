#AzureStorage 

### Definition
Azure Files allow for configuration of network file shares, which can be accessed using SMB and Network File System (NFS) protocols. 

Soft delete can be enabled on the storage account which allows you to recover deleted files during a configured retention period.

#### Access

|Authentication method|Description|
|---|---|
|Identity-based authentication over SMB|Provides the same seamless single sign-on (SSO) experience when accessing Azure file shares as accessing on-premises file shares.|
|Access key|An access key is an older and less flexible option. An Azure storage account has two access keys that can be used when making a request to the storage account, including to Azure Files. Access keys are static and provide full control access to Azure Files. Access keys should be secured and not shared with users, because they bypass all access control restrictions. A best practice is to avoid sharing storage account keys and use identity-based authentication whenever possible.|
|A Shared Access Signature (SAS) token|SAS is a dynamically generated Uniform Resource Identifier (URI) that's based on the storage access key. SAS provides restricted access rights to an Azure storage account. Restrictions include allowed permissions, start and expiry time, allowed IP addresses from where requests can be sent, and allowed protocols. With Azure Files, a SAS token is only used to provide REST API access from code.|

#### Snapshots
Azure allows you to create read only snapshots of file shares.

- The Azure Files share snapshot capability is provided at the file share level.
- Share snapshots are incremental in nature. Only data changed since the most recent share snapshot is saved.
- Incremental snapshots minimize the time required to create share snapshots and saves on storage costs.
- Even though share snapshots are saved incrementally, you only need to retain the most recent share snapshot to restore the share.
- You can retrieve a share snapshot for an individual file. This level of support helps with restoring individual files rather than having to restore to the entire file share.
- If you delete a file share that has share snapshots, all of its snapshots are deleted along with the share.

#### Azure File Sync
Azure File Sync allows you to cache several Azure file shares to an on premises Windows server or VM. 
You can use any protocol that's available on Windows Server to access your data locally with Azure File Sync, including SMB, NFS, and FTPS.

Cloud tiering is an optional feature of Azure File Sync. Frequently accessed files are cached locally on the server while all other files are tiered to Azure Files based on policy settings.

- When a file is tiered, Azure File Sync replaces the file locally with a pointer. A pointer is commonly referred to as a _reparse point_. The parse point represents a URL to the file in Azure Files.
- When a user opens a tiered file, Azure File Sync seamlessly recalls the file data from Azure Files without the user needing to know that the file is stored in Azure.
- Cloud tiering files have greyed icons with an offline `O` file attribute to let the user know when the file is only in Azure.
