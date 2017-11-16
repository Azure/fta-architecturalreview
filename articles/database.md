# FastTrack for Azure Architectural Discussion Framework - Database Solution

- [FastTrack for Azure Architectural Discussion Framework - Database Solution](#fasttrack-for-azure-architectural-discussion-framework---database-solution)
  * [App & Data Migration](#app---data-migration)
  * [Distributed Architecture](#distributed-architecture)
  * [High Availability and Business Continuity / Disaster Recovery](#high-availability-and-business-continuity---disaster-recovery)
  * [Monitoring &amp; Management](#monitoring--amp--management)
  * [Performance & Scalability](#performance---scalability)
  * [Security](#security)
  * [Stories](#stories)

## App & Data Migration    

* **Is your database already hosted in Azure? If not, then what are your plans to migrate your database to Azure? Do you have a requirement to migrate without downtime?**

    Determine the current migration strategy, and what requirements or limitations may exist.    
    
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-cloud-migrate](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-cloud-migrate)

* **Are you hosting your SQL databases on Azure using an Infrastructure as a Service approach? Are you planning to modernize onto Azure SQL DB?**

    Determine if there are plans to rearchitect the solution to use the Platform as a Service (PaaS) alternative, reducing the overall management overhead of the solution.    
    
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-cloud-migrate](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-cloud-migrate)

* **What size is your database and how many databases are you planning to migrate?**

    Determine the appropriate migration paths, given the size and volume of databases to be migrated.    
    
    > [https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service)
    >
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-pool](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-pool)

* **How much downtime can you afford during data and app migration?**

    Determine whether Backup and Restore can be used as a migration strategy, or whether replication is needed.    
    
    > [https://blogs.msdn.microsoft.com/sqlcat/2017/02/03/migration-from-sql-server-to-azure-sql-database-using-transactional-replication/](https://blogs.msdn.microsoft.com/sqlcat/2017/02/03/migration-from-sql-server-to-azure-sql-database-using-transactional-replication/)

* **Have you assessed the compatibility of your database with your target destination (I.e. Azure SQL DB or SQL Server on IaaS)?**

    Understand that there is tooling available to assess the feasibility of migrating databases onto Azure. Determine whether this has been evaluated as part of the overall migration strategy.    
    
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-migrate-your-sql-server-database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-migrate-your-sql-server-database)

## Distributed Architecture    

* **Do you have multiple databases that need to speak to each other (MSDTC or linked serversfor example).**

    Understand the inter-dependencies within the solution, and the ability to rearchitect the solution.    
    
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-transactions-overview](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-transactions-overview)
    >
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-query-getting-started-vertical](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-query-getting-started-vertical)

* **Have you scaled out your data layer (data partitioning)?**

    Identify those dependencies between servers. This will lead lead to PaaS vs IaaS architectures.    
    
    > [https://docs.microsoft.com/en-us/azure/architecture/best-practices/data-partitioning](https://docs.microsoft.com/en-us/azure/architecture/best-practices/data-partitioning)
    >
    > [https://docs.microsoft.com/en-us/azure/architecture/patterns/sharding](https://docs.microsoft.com/en-us/azure/architecture/patterns/sharding)

* **Do you use readable secondaries?<br> Have you considered how you might make use of them?**

    Determine whether this has been considered as part of the wider solution. This will lead the conversation to High Aailability, and also the load balancing of read activity at the database layer.    
    
    > [https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups)

## High Availability and Business Continuity / Disaster Recovery    

* **How much data can you afford to lose in your solution if you have to recover a database?**

    Determine whether any loss of data is allowed. If this is not allowed, approaches to High Availability will need to be considered.    

* **How much downtime can you afford to have?**

    Determine the allowed recovery time and if backups are the approach    

* **Are you running your SQL tier on Azure IaaS? What is your planned approach to High Availability or Disaster Recovery?**

    Determine the High Availability vs Disaster Recovery strategy. Common options include <br><br>**High Availability**<ul><li> Always on Availability Groups</li><li>Fail-Over Clustering</li></ul>**Disaster Recovery (Azure Only)**<ul><li>Availability Groups</li><li>Backup and Restore with Azure Blob</li><li>Transaction Log Shipping </li></ul>    
    
    > [https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)
    >
    > If the considered option is to use Failover Clustering -  [https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-create-failover-cluster](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-create-failover-cluster)
    >
    > If the considered option is to use Availability Groups - [https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial)

* **Are you aware of the built-in functionality of Azure SQL Database for Business Continuity and Disaster Recovery?**

    Has Infrastructure as a Service (IaaS) been chosen without considering all potions? Could mangaeability of the database solution be improved, by using Azure SQL DB?    
    
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-automated-backups](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-automated-backups)
    >
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-recovery-using-backups](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-recovery-using-backups)

* **Have you considered Active Geo-Replication in Azure SQL Database for High Availability?**

    Is High availability being assumed as a part of the solution because it is a Platform as a Service (PaaS) solution? Has there been any consideration to the steps needed to be taken during region failure or RPO?    
    
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview)

* **How does the application behave if the database fails over to a secondary site? &nbsp;**

    Does the application fail over too, or does the retry logic connect to the new remote primary?    

## Monitoring & Management    

* **How do you monitor your data layer?**

    Determine whether there is any enterprise monitoring of the data layer. How is it determined that the solution is working appropriately? If this is not being used, consider the associated documentation.    
    
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-single-database-monitor](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-single-database-monitor)

* **How would you know if you had an outage or failure?**

    Monitoring may be configured, but how much is it used? Determine if a live issue would first be reported by end-users, or whether monitoring systems would pick this up in advance. This also leads towards DevOps, and having a representative environment prior to production, which has representative tests in place.    
 
* **What alerts have been set-up?**

    Does the monitoring system require an individual to take the initiative and review the details, or will it send proactive notifications such as e-mails?    
    
* **Do you track the performance of queries from the application through to the DB layer?**

    Determine if proactive measures are being taken to manage database performance, and therefore proactive steps in managing the SLA and Performance of the application.    
    
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-automatic-tuning](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-automatic-tuning)
    >
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-operate-query-store](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-operate-query-store)

* **What solutions do your DBAs use to manage the data estate?**

    Determine whether there is a reliance on a DBA using RDP onto the servers.<br><br>Determine if there is a more appropriate approach to managing the fleet driving the data layer.    

* **How do you determine the current patch level across the estate?**

    Determine whether there is any automation in place. Unpatched machines presents a risk in the environment, and this is undesirable, especially at the data layer which is generally core to an application.    
    
    > [https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)

* **Do you use any IDS/IPS software for threat detection?**

    Determine the proactive steps being taken in maintaining the security of the data estate.    
    
## Performance & Scalability    

* **Is your database performance and usage predictable?**

    Determine whether elastic pools or individual databases should be considered within the solution.    
    
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-pool](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-pool)

* **Azure SQL Server on IaaS - Have you placed your virtual machines into an availability set?**

    To provide redundancy to your application, it is recommended that you group two or more virtual machines of the same tier in an availability set. This configuration within a datacenter ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the 99.95% Azure SLA.    
    
    > [https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability(https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability)](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability(https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability))

* **Azure SQL Server on IaaS – Do you know about the difference between unmanaged and managed disks? Have you leveraged Azure Managed disks?**

    Determine whether level of IOPS / throughput have been safeguarded to  VM disks.<br><br>If using unmanaged disks, the placement of disks across storage accounts must be considered to maintain performance and resilience.    
    
    > [https://docs.microsoft.com/en-gb/azure/storage/storage-managed-disks-overview](https://docs.microsoft.com/en-gb/azure/storage/storage-managed-disks-overview)

* **Azure SQL Server on IaaS - Have you configured your implementation to the recommendations in the associated documentation?**

    The associate documentation provides recommended practices in configuring IaaS solutoions, and ensuring suitable performance.    
    
    > [https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

* **Azure SQLDB – Are you aware that Azure SQL DB can learn and adapt to help you tune your database? Have you used database advisor for Database tuning?**
 
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-advisor](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-advisor)

* **Azure SQLDB - Are you aware of the steps that you can take to manually tune your SQLDB, if the built-in recommendations do not provide any benefit?**
    
    > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-performance-guidance](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-performance-guidance)

## Security    

* **Are you aware of the Azure SQL DB best practices? Have you implemented these in your solution?**   
    
    > [https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices)

* **Is the data stored in your database sensitive? Do you require special data handling?**

    Identify the encryption and protection requirements of the solution. Leverage the associated documentation in providing a solution to this problem.    
    
    > [https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine)
  	>
    > [https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde)
    >
    > [https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption)

* **Do you use a multi-tenant database structure?**

    Establish risks of cross user contamination of data.    
    
    > [https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption)

* **Do you audit access to the servers and the DDL queries that are run?**

    Determine whether there is an understanding into which users are performing which tasks / queries / functoins? Is this level of detail needed, perhaps for compliance or some form of internal business policy?    
    
    > [https://powerbi.microsoft.com/en-us/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/](https://powerbi.microsoft.com/en-us/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/)

* **Who has admin access to the system?**

    This builds upon the previous question. Limiting admin access is a recommended practice. Admins can bypass security measures and potentially see protected data.    

* **Do you encrypt your backups?**

    Protecting data at rest may be important. Is there a guarantee that backed-up data cannot be restored to another server that is not under your control?    
    
    > [https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde)

* **Can you define the business impact for a data breach?**

    Determine whether there is an understanding into the follow-on effects of a data breach. Has the wider business impact been considered, rather than just focusing on the technology challenge and impact?    

## Stories 

  > [https://docs.microsoft.com/en-us/azure/sql-database/sql-database-customer-implementations](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-customer-implementations)