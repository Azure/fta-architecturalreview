# FastTrack for Azure Architectural Discussion Framework - Lift and Shift

- [FastTrack for Azure Architectural Discussion Framework - Lift and Shift Solution](#fasttrack-for-azure-architectural-discussion-framework---lift-and-shift-solution)
  * [App &amp; Data Migration](#app--data-migration)
  * [Azure Design Principles with Lift and Shift](#azure-design-principles-with-lift-and-shift)
  * [Linux Lift and Shift into Azure](#linux-lift-and-shift-into-azure)
  * [Distributed Architecture](#distributed-architecture)
  * [High Availability and Business Continuity / Disaster Recovery](#high-availability-and-business-continuity---disaster-recovery)
  * [Monitoring &amp; Management](#monitoring--management)
  * [Performance &amp; Scalability](#performance--scalability)
  * [Security](#security)

## App &amp; Data Migration  

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Are you aware of the Microsoft Azure Virtual Machine Readiness Assessment tool?| This assessment will automatically inspect your on-premises environment, whether it is bare metal or already virtualized. After that, the tool will provide you with tailored guidance and recommendations for migrating your environment to Microsoft Azure. If you’re running Active Directory, SQL, or SharePoint this tool will make it easy for you to get started.| [https://azure.microsoft.com/en-us/downloads/vm-readiness-assessment/ ][1]  |  

## Azure Design Principles with Lift and Shift   

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Have you considered your approach to governance and taxonomy in an Azure environment?|The goal is to determine the approach to governance in the Azure environment, facilitating business discussion to plan where the workloads will go and also separate Production from DevTest. This will also lead to a naming convention and planning for subscription placement. It also allows for a set of defined TAGS and implementation of policies once the solution has been moved.| Azure Taxonomy<br>[https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-governance][2]<br>[https://blogs.msdn.microsoft.com/cclayton/2011/06/07/standard-cloud-taxonomies-and-windows-azure/][3]<br><br>Manage Azure Resources with TAGS<br>[https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags][4]<br>[https://azure.microsoft.com/en-us/updates/organize-your-azure-resources-with-tags/][5]<br><br>Divide subscription based on Prod, Dev, Test or regions<br>[https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/][6]<br><br>Enabling EA DevTest Subscriptions<br>[https://channel9.msdn.com/blogs/EA.Azure.com/Enabling-and-Creating-EA-DevTest-Subscriptions-through-the-EA-Portal?term=ea%20portal%20taxonomy][7]<br><br>Azure Subscription Limits<br>[https://docs.microsoft.com/en-us/azure/azure-subscription-service-limits][8]  |  
|How does the application communicate? Are there legacy applications that need to be taken into account that cannot be migrated?|Determine data flows, as well as dependencies within the application.|Design Principles for Applications hosted in Azure :<br>[https://docs.microsoft.com/en-us/azure/architecture/resiliency/][9]  |  
| Have you considered the load and runtime requirements of your solution?| It is important to plan the vm size and storage appropriately, ensuring that performance is not compromised once the solution has been migrated to Azure. Plan on your storage. Will it be Standard or Premium storage? Understand the vm sizes and how they will support memory, processing, and the throttling of storage.|VM Sizing:<br> [https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes][10]<br/><br/>Capacity Planning VMware Environments: https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-deployment-planner<br/><br/>Capacity Planning Hyper-V environments: https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-capacity-planner   |  
| Have you defined your networking requirements? What is needed to transfer your data from on-premises into Azure? Additionally, have you thought about how you will segregate your workloads across subnets or Virtual Networks?| The goal to understand the network capacity to transfer data and also to secure the application across tiers.|Azure Architecture Center<br>[https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/][11]<br>[https://docs.microsoft.com/en-us/azure/architecture/][12]<br><br>VNET Peering:<br> [https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-peering-overview][13]<br/><br/>Bandwidth Planning for replicating workloads to Azure:<br/>https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-deployment-planner<br/>https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-capacity-planning-for-hyper-v-replication<br/><br/>Drive shipping workloads for low bandwidth:<br/>https://docs.microsoft.com/en-us/azure/storage/common/storage-import-export-service |

## App & Data Migration 

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| What are the current set of dependencies that your current and legacy applications have?  Do you plan to extend your current authorization and authentication for applications or do you plan to create a hosting domain to insulate your internal Active Directory? &nbsp; &nbsp;| The goal is to understand whether there is an on-premises environment and considerations made for the moving of the application to a new environment.  Which Azure services are used within the solution?  Are there any third party services used within the solution?  Does the solution talk to any on-premises components? Are the applications currently virtualized in VMWare and moving to Azure? Understanding of the planning that must occur if Azure Site Recovery will be used.| [Reference - Minimize and understand service dependencies][15]<br>[https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-azure-to-azure-prereq][16]<br>[https://azure.microsoft.com/en-us/resources/videos/asrhowto-video2-migrate-virtual-machines-to-azure/][17]<br>[https://blogs.technet.microsoft.com/hybridcloud/2016/03/03/move-vmware-aws-hyper-v-and-physical-servers-to-azure-with-azure-site-recovery/][18]<br>[https://docs.microsoft.com/en-us/azure/site-recovery/vmware-walkthrough-overview][19]<br>[https://blogs.msdn.microsoft.com/zxue/2016/07/30/tips-and-tricks-on-doing-lift-and-shift-on-prem-systems-to-azure/][20]  |  
|Have you considered the feasibility of your internet connection, in line with the volume of data to be uploaded?| Establish if there is a sufficiently fast connection to the internet and if there is an opportunity to move unstructured data into Azure| [https://docs.microsoft.com/en-us/azure/storage/common/storage-import-export-service][21]<br>[https://docs.microsoft.com/en-us/azure/storage/common/storage-import-export-using-the-rest-api ][22] |  
| Are you aware of the options available to migrate your data to Azure?|Establish which options in moving the data to Azure will align best with your scenario and solution.|[https://docs.microsoft.com/en-us/azure/storage/common/storage-moving-data][23]  |  | The data that you want to move into Azure how much of it is data that is intended to be archived or actual live data you plan to use on a daily basis?| Determine whether the data needs to be moved for daily use or if the data is intended for archive| [https://docs.microsoft.com/en-us/azure/backup/backup-introduction-to-azure-backup][24]  |  

## Linux Lift and Shift into Azure   

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Do you have any Open Source workloads deployed on Linux that you plan to migrate to Azure and which distributions do you currently run in production| Understand what OSS workloads that are currently running and the file systems that are currently running.| [https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-support-matrix-to-azure][25]  |  

## Distributed Architecture  

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Is your application located in one central datacenter or is it spread across a multisite topology? Does this include multiple cloud providers? &nbsp;| Is part of the application on-premises, or an alternate cloud provider, or third party? Ensure that you are aware of the risk of upstream or downstream dependency failures.| [https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-migrate-aws-to-azure][26]<br>[Reference - Host applications in multiple datacenters ][15]<br>[Reference - Azure Paired Regions ][27]<br>[Reference - Multiple datacenter regions / Azure Traffic Manager][28]<br>[Reference - Recovery from a region-wide service disruption ][29]  |  

## High Availability and Business Continuity / Disaster Recovery  

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Do you have Availability Requirements defined for the workload? How much downtime is acceptable? Have you defined a Recovery Time OBjective (RTO) and Recovery Point Objective (RPO)?| It is critical that there are defind Resiliency (High Availability &amp; Disaster Recovery) metrics like RPO/RTO/SLA. Without these metrics it will be hard to design an application to hit business needs.| Designing resilient applications for Azure <br>[https://docs.microsoft.com/en-us/azure/architecture/resiliency/index#defining-your-resiliency-requirements ][30]  |  
| Is there a defined SLA for the workload?| It is important to understand how this impacts the SLA that you provide your end-users. You should define a target SLA for each workload. An SLA makes it possible to evaluate whether the architecture meets the business requirements.  Ensure that you calculate Composite SLA (SLA of multiple Azure and other dependent services that makes up the workload) and see if that meets the business SLA requirements.  You can then cross compare your SLAs with Microsoft Azure's to determine the neccessary requirements needed.| Defining Resiliency Requirements<br/>[https://docs.microsoft.com/en-us/azure/architecture/resiliency/index#defining-your-resiliency-requirements ][30]<br/><br/>Azure SLAs:<br/>https://azure.microsoft.com/en-us/support/legal/sla/  |  
| Have you performed Failure Mode Analysis (FMA)?| FMA is to identify possible points of failures and define how the applications will respond to those failures.| Failure Mode Analysis<br>[https://docs.microsoft.com/en-us/azure/architecture/resiliency/failure-mode-analysis ][31]   |  
| Do you require a level of high availability for your Open Source Application systems when they are migrated to Azure? Do you require your Linux system to be a failover cluster?| Understand if the Open Source System requires high availability as part of the application design.| TBC  |  
| Does your MySQL database have any high availability requirements?|Be aware of the associated guidance for MySQL on Azure.| [http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf][33]   |  

## Monitoring &amp; Management

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| How is the health and performance of the application measured and monitored? What KPIs are reviewed by the operations team? &nbsp;| When developing a monitoring strategy and implementation for a system, the first step is determining the Key Performance Indicators used to measure the health, behavior and performance of the system. Without having clear and quantified targets in mind, making informed engineering decisions is effectively impossible, and leads to circular, anecdotal discussions of &quot;the system feels slow&quot; &nbsp;| [Reference - Monitoring and diagnostics guidance ][34] &nbsp; [https://docs.microsoft.com/en-us/azure/backup/backup-azure-configure-reports][35]  &nbsp; [https://blogs.technet.microsoft.com/msoms/2016/07/27/introducing-oms-network-performance-monitor/][36] &nbsp;  |  
| If you are offering an SLA, do you have any methods of monitoring the SLA that you are providing?| Many commercial systems that support paying customers make guarantees about the performance of the system in the form of SLAs. Essentially, SLAs state that the system can handle a defined volume of work within an agreed time frame and without losing critical information. SLA monitoring is concerned with ensuring that the system can meet measurable SLAs. &nbsp;| [Reference - SLA Monitoring ][37]  |  
| What is the resource utilization across deployed resources? How much headroom (capacity) is there across the deployed resources? &nbsp;| Usage monitoring can help to determine which features may benefit from functional partitioning or re-architecture. Additionally, it may help to serve which components should be retired from the solution. &nbsp; It could also be used to Detect (possibly indirectly) user satisfaction with the performance or functionality of the system. For example, if a large number of customers in an e-commerce system regularly abandon their shopping carts, this might be due to a problem with the checkout functionality. &nbsp;| [Reference - Usage Monitoring ][38]  |  
| How many operations are executed across various tiers? Per second/hour/day? Peak load? Are you monitoring the performance of your application as it scales and is placed under more and more stress/load? &nbsp;| As the system is placed under more and more stress (by increasing the volume of users), the size of the datasets that these users access grows and the possibility of failure of one or more components becomes more likely. Frequently, component failure is preceded by a decrease in performance. If you&#39;re able detect such a decrease, you can take proactive steps to remedy the situation. &nbsp;| [Reference - Performance Monitoring ][39]  |  
| How many errors (user-visible) are produced in the system? Per second/hour/day? If needed, can a root-cause be defined? Do you actively check if the system is functioning as expected? Are you currently performing health monitoring? &nbsp;| An operator should be alerted quickly (within a matter of seconds) if any part of the system is deemed to be unhealthy. The operator should be able to ascertain which parts of the system are functioning normally, and which parts are experiencing problems. &nbsp;| [Reference - Health Monitoring ][40] [Reference - Overview of Azure Monitor ][41]  |  
| How many active, unique users does your application support (mobile, web, etc.)? &nbsp;| Understand the personas that are using the application and when peak usage occurs| &nbsp;  |  
| Are you aware of managed disks, and how they can provide High Availability compared with user managed disks?| Explain the benefit of Managed Disks as well as how they are supported in ASR during lift and shift.| [https://azure.microsoft.com/en-us/blog/managed-disks-with-azure-site-recovery/][42]  |  

## Performance &amp; Scalability  

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| How many users does your application need to support? (total and concurrently active; how are they geographically distributed) Have you designed for scaling within your solution? (e.g. Stateless where appropriate, auto-detection of new instances) &nbsp;| Determine whether the solution is being tested beyond the predicted peak load. Additionally, this will determine whether their solution has been configured for scaling or not, and whether it is architected to avoid platform limits.| [Reference - Scalability checklist ][43]  |  
| What are the per-operation latency targets, and acceptable latency range? How many operations/messages per second?| Reduce chatty interactions between components and services. Avoid designing interactions in which an application is required to make multiple calls to a service (each of which returns a small amount of data), rather than a single call that can return all of the data. Where possible, combine several related operations into a single request when the call is to a service or component that has noticeable latency. This makes it easier to monitor performance and optimize complex operations. For example, use stored procedures in databases to encapsulate complex logic, and reduce the number of round trips and resource locking.| [Reference - Scalability checklist - Reduce chatty interactions ][43]  |  
| What, if any, seasonality is there to the solution? &nbsp;| Azure Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments. It analyzes your resource configuration and usage telemetry and recommends solutions that can help you improve the cost effectiveness, performance, high availability and security of your Azure resources.| [Reference - Introduction to Azure Advisor ][44]  |  
| What are the operational constraints and requirements for the system? Are there compliance, location (required geography), regulatory (HIPAA, FEDRAMP, etc.) or sovereignty requirements?| Microsoft Trust Center provides you with a wealth of information about how Microsoft Cloud Services are secured, how Microsoft ensures privacy of your data, as well as information about Compliance and more.| [Reference - Microsoft Trust Center ][45]  |  

## Security  

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Do you have any requirements for encryption?| Understand if the current workload has or will require encryption.| [https://docs.microsoft.com/en-us/azure/storage/common/storage-service-encryption-customer-managed-keys][46]<br> [https://azure.microsoft.com/en-us/documentation/articles/security-get-started-overview/ ][47] &nbsp;  |  
| Who currently requires access to the application during and after the migration?| Define the security requirements and if there are new security requirements once the solution has moved onto Azure.| [https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-lock-resources ][48]<br> [https://docs.microsoft.com/en-us/azure/backup/backup-rbac-rs-vault ][49]  |  

[1]: https://azure.microsoft.com/en-us/downloads/vm-readiness-assessment/
[2]: https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-governance
[3]: https://blogs.msdn.microsoft.com/cclayton/2011/06/07/standard-cloud-taxonomies-and-windows-azure/
[4]: https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags
[5]: https://azure.microsoft.com/en-us/updates/organize-your-azure-resources-with-tags/
[6]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/
[7]: https://channel9.msdn.com/blogs/EA.Azure.com/Enabling-and-Creating-EA-DevTest-Subscriptions-through-the-EA-Portal?term=ea%20portal%20taxonomy
[8]: https://docs.microsoft.com/en-us/azure/azure-subscription-service-limits
[9]: https://docs.microsoft.com/en-us/azure/architecture/resiliency/
[10]: https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes
[11]: https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/
[12]: https://docs.microsoft.com/en-us/azure/architecture/
[13]: https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-peering-overview
[14]: https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/virtual-machines-windows/n-tier
[15]: https://docs.microsoft.com/en-gb/azure/best-practices-availability-checklist
[16]: https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-azure-to-azure-prereq
[17]: https://azure.microsoft.com/en-us/resources/videos/asrhowto-video2-migrate-virtual-machines-to-azure/
[18]: https://blogs.technet.microsoft.com/hybridcloud/2016/03/03/move-vmware-aws-hyper-v-and-physical-servers-to-azure-with-azure-site-recovery/
[19]: https://docs.microsoft.com/en-us/azure/site-recovery/vmware-walkthrough-overview
[20]: https://blogs.msdn.microsoft.com/zxue/2016/07/30/tips-and-tricks-on-doing-lift-and-shift-on-prem-systems-to-azure/
[21]: https://docs.microsoft.com/en-us/azure/storage/common/storage-import-export-service
[22]: https://docs.microsoft.com/en-us/azure/storage/common/storage-import-export-using-the-rest-api
[23]: https://docs.microsoft.com/en-us/azure/storage/common/storage-moving-data
[24]: https://docs.microsoft.com/en-us/azure/backup/backup-introduction-to-azure-backup
[25]: https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-support-matrix-to-azure
[26]: https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-migrate-aws-to-azure
[27]: https://docs.microsoft.com/en-gb/azure/best-practices-availability-paired-regions
[28]: https://docs.microsoft.com/en-gb/azure/resiliency/resiliency-disaster-recovery-azure-applications
[29]: https://docs.microsoft.com/en-gb/azure/resiliency/resiliency-technical-guidance-recovery-loss-azure-region
[30]: https://docs.microsoft.com/en-us/azure/architecture/resiliency/index#defining-your-resiliency-requirements
[31]: https://docs.microsoft.com/en-us/azure/architecture/resiliency/failure-mode-analysis
[33]: http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf
[34]: https://docs.microsoft.com/en-gb/azure/best-practices-monitoring
[35]: https://docs.microsoft.com/en-us/azure/backup/backup-azure-configure-reports
[36]: https://blogs.technet.microsoft.com/msoms/2016/07/27/introducing-oms-network-performance-monitor/
[37]: https://docs.microsoft.com/en-gb/azure/best-practices-monitoring#sla-monitoring
[38]: https://docs.microsoft.com/en-gb/azure/best-practices-monitoring#usage-monitoring
[39]: https://docs.microsoft.com/en-gb/azure/best-practices-monitoring#performance-monitoring
[40]: https://docs.microsoft.com/en-gb/azure/best-practices-monitoring#health-monitoring
[41]: https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview
[42]: https://azure.microsoft.com/en-us/blog/managed-disks-with-azure-site-recovery/
[43]: https://docs.microsoft.com/en-us/azure/best-practices-scalability-checklist
[44]: https://docs.microsoft.com/en-us/azure/advisor/advisor-overview
[45]: https://docs.microsoft.com/en-us/azure/security/security-microsoft-trust-center
[46]: https://docs.microsoft.com/en-us/azure/storage/common/storage-service-encryption-customer-managed-keys
[47]: https://azure.microsoft.com/en-us/documentation/articles/security-get-started-overview/
[48]: https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-lock-resources
[49]: https://docs.microsoft.com/en-us/azure/backup/backup-rbac-rs-vault
