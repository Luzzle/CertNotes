#AzureStorage 

### Definition
Blob storage is optimized for storing large amounts of unstructured or non-relational data. Blob storage is ideal for:
- Serving images or documents directly to a browser.
- Storing files for distributed access.
- Streaming video and audio.
- Storing data for backup and restore, disaster recovery, and archiving.
- Storing data for analysis by an on-premises or Azure-hosted service.

#### Blob Storage Components
Blob storage uses three resources to store and manage your data:
- Azure storage account
- Containers
- Blobs inside a container

##### Access Tiers
**Hot**
The Hot tier is optimized for frequent reads and writes of objects in the storage account. This has the highest storage costs, but the lowest access costs.

**Cool**
The Cool tier is optimized for storing large amounts of infrequently accessed data, that should remain for at least 30 days. This is data this shouldn't be read frequently, but needs to be immediately available.

**Cold**
The Cold tier is similar to the cool tier, except data should remain for at least 90 days.

**Archive**
The archive tier is an offline tier designed for systems that can tolerate several hours of retrieval latency. An archive tier doesn't allow you to read or modify the content of a blob directly. However, you do have access to its metadata, including index tags. To access the blob's content, you can assign it to the hot, cool, or cold tier to trigger the process referred to as rehydration. Data must remain for at minimum 180 days.

#### Blob Types
- **Block blobs**. A block blob consists of blocks of data that are assembled to make a blob. Most Blob Storage scenarios use block blobs. Block blobs are ideal for storing text and binary data in the cloud, like files, images, and videos. The block blob type is the default type for a new blob. When you're creating a new blob, if you don't choose a specific type, the new blob is created as a block blob.

- **Append blobs**. An append blob is similar to a block blob because the append blob also consists of blocks of data. The blocks of data in an append blob are optimized for _append_ operations. Append blobs are useful for logging scenarios, where the amount of data can increase as the logging operation continues

- **Page blobs**. A page blob can be up to 8 TB in size. Page blobs are more efficient for frequent read/write operations. Azure Virtual Machines uses page blobs for operating system disks and data disks.

#### Blob Lifecycle Management
You can use Azure Blob Storage lifecycle management policy rules to accomplish several tasks.

- Transition blobs to a cooler storage tier (Hot to Cool, Hot to Archive, Cool to Archive) to optimize for performance and cost.
- Delete current versions of a blob, previous versions of a blob, or blob snapshots at the end of their lifecycles.
- Apply rules to an entire storage account, to select containers, or to a subset of blobs using name prefixes or blob index tags as filters.

#### Blob Replication
There are several considerations to keep in mind when planning your configuration for blob object replication.

- Object replication requires that blob versioning is enabled on both the source and destination accounts. When blob versioning is enabled, you can access earlier versions of a blob. This access lets you recover your modified or deleted data.
- Object replication doesn't support blob snapshots. Any snapshots on a blob in the source account aren't replicated to the destination account.
- Object replication is supported when the source and destination accounts are in the Hot, Cool, or Cold tier. The source and destination accounts can be in different tiers.
- When you configure object replication, you create a replication policy that specifies the source Azure storage account and the destination storage account.
- A replication policy includes one or more rules that specify a source container and a destination container. The policy identifies the blobs in the source container to replicate.