#AzureCompute 

### Definition
In Azure App Service, an application runs in an Azure App Service plan. 

An App Service plan defines a set of compute resources for a web application to run. The compute resources are analogous to a server farm in conventional web hosting. 

One or more applications can be configured to run on the same computing resources (or in the same App Service plan).

#### Pricing Tiers
- **Shared compute**:
    - Free and Shared, the two base tiers, run an app on the same Azure VM as other App Service apps, including apps of other customers.
    - These tiers allocate CPU quotas to each app that runs on the shared resources, and the resources can't scale out.
    - These tiers are intended to be used only for development and testing purposes.
- **Dedicated compute**:
    - The Basic, Standard, Premium, PremiumV2, and PremiumV3 tiers run apps on dedicated Azure VMs.
    - Only apps in the same App Service plan have the same compute resources. The higher the tier, the more VM instances that are available to you for scale-out.
- **Isolated**:
    - The Isolated and IsolatedV2 tiers run dedicated Azure VMs on dedicated Azure virtual networks.
    - This tier provides network isolation on top of compute isolation to your apps.
    - This tier provides the maximum scale-out capabilities.

| Feature         | Free F1              | Basic B1             | Standard S1          | Premium P1V3                |
| --------------- | -------------------- | -------------------- | -------------------- | --------------------------- |
| Usage           | Development, Testing | Development, Testing | Production workloads | Enhanced scale, performance |
| **Staging slots**   | **N/A**                  | **N/A**                  | **5**                    | **20**                          |
| Auto scale      | N/A                  | Manual               | Rules                | Rules, Elastic              |
| Scale instances | N/A                  | 3                    | 10                   | 30                          |
| Daily backups   | N/A                  | N/A                  | 10                   | 50                          |
**NOTE - STUDY STAGING SLOTS**

##### Free and Shared
The Free and Shared service plans are base tiers that run on the same Azure virtual machines as other applications. Some applications might belong to other customers. 

Intended for testing purposes only.

##### Basic
The Basic service plan is designed for applications that have lower traffic requirements, and don't need advanced auto scale and traffic management features. 

Pricing is based on the size and number of instances you run. Built-in network load-balancing support automatically distributes traffic across instances.

##### Standard
The Standard service plan is designed for running production workloads. 

The Standard plan includes auto scale that can automatically adjust the number of virtual machine instances running to match your traffic needs.

##### Premium
The Premium service plan is designed to provide enhanced performance for production applications. 

The upgraded Premium plan, Premium v2, offers Dv2-series virtual machines with faster processors, SSD storage, and double memory-to-core ratio compared to the Standard tier. 

The new Premium plan also supports higher scale via increased instance count while still providing all the advanced capabilities of the Standard tier

##### Isolated
The Isolated service plan is designed to run mission critical workloads that are required to run in a virtual network. 

The Isolated plan allows customers to run their applications in a private, dedicated environment in an Azure datacenter. 

The plan offers Dv2-series virtual machines with faster processors, SSD storage, and a double memory-to-core ratio compared to the Standard tier. 

The private environment used with an Isolated plan is called the App Service Environment. 

The plan can scale to 100 instances with more available upon request.