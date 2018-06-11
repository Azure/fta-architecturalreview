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

    Determine the current migration strategy, and what requirements or limitations may exist. For example, the requirement of migrating without downtime will then limit the options available to bring data onto the platform.    
    
    > [SQL Server database migration to SQL Database in the cloud](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-cloud-migrate)

* **Are you hosting your SQL databases on Azure using an Infrastructure as a Service approach? Are you planning to modernize onto Azure SQL Database?**

    Determine if there are plans to re-platform the solution to use the Platform as a Service (PaaS) alternative, reducing the overall management overhead of the solution. If so, it is important to consider potential compatibility issues of the PaaS approach. It is also worth understanding that there is tooling available to assess the feasibility of migrating databases onto Azure    
    
    > [SQL Server database migration to Azure SQL Database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-cloud-migrate)
    > 
    > [Migrate your SQL Server database to Azure SQL Database using DMS](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-migrate-your-sql-server-database)
    > 
    > [Database Migration Guide](https://datamigration.microsoft.com/)

* **What size is your database and how many databases are you planning to migrate?**

    The size of the database will affect the options available in transferring data to Azure. The number of databases (and interdependencies) will determine additional factors including timescales of data transfer, as well as management considerations such as Elastic Pools in Azure SQLDB.    
    
    > [Using the Import/Export service to transfer data to Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service)
    >
    > [Elastic pools help you manage and scale multiple Azure SQL databases](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-pool)

* **How much downtime can you afford during data and app migration?**

    Determine whether there is a clear strategy of Service Level Agreements (Recovery Time Objective and Recovery Point Objective). Consider whether a strategy has been created based upon this criterion, and the suitability of options. For example, whether Backup and Restore can be used as a migration strategy, or whether replication is needed.   
    
    > [Migration from SQL Server to Azure SQL Database using transactional replication](https://blogs.msdn.microsoft.com/sqlcat/2017/02/03/migration-from-sql-server-to-azure-sql-database-using-transactional-replication/)

## Distributed Architecture    

* **Do you have multiple databases that need to speak to each other (MSDTC or linked serversfor example).**

    Understand the inter-dependencies within the solution, and the ability to rearchitect the solution.    
    
    > [Distributed transactions across cloud databases](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-transactions-overview)
    >
    > [Get started with cross-database queries](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-query-getting-started-vertical)

* **Have you implemented any type of data partitioning?**

    If the database keeps on growing, could you potentially hit some technical limit of the platform? Additionally, consider data access as part of your sharing strategy and using different tiers of storage.    
    
    > [Data partitioning best practices](https://docs.microsoft.com/en-us/azure/architecture/best-practices/data-partitioning)
    > 
    > [Sharding pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/sharding)

* **Do you use readable secondaries? Have you considered how you might make use of them?**

    Identify whether High Availability at the database layer has been considered as part of the solution. Determine whether a secondary instance of the database in a read-only format could aid in the load balancing of database activity. You may want to consider the CQRS pattern in this scenario.     
    
    > [Readable secondary replicas (Always On availability groups)](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups)
    > 
    > [Command and Query Responsibility Segregation (CQRS) pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/cqrs)

## High Availability and Business Continuity / Disaster Recovery    

* **How much data can you afford to lose in your solution if you have to recover a database?**

    Determine whether any loss of data is allowed. If this is not allowed, approaches to High Availability will need to be considered.    

* **How much downtime can you afford to have?**

    Determine the allowed recovery time and if backups are the approach    

* **Are you running your SQL tier on Azure IaaS? What is your planned approach to High Availability or Disaster Recovery?**

    Determine the High Availability vs Disaster Recovery strategy. Common options include 
    * **High Availability**
      * Always on Availability Groups
      * Fail-Over Clustering
    * **Disaster Recovery (Azure Only)**
      * Availability Groups
      * Backup and Restore with Azure Blob
      * Transaction Log Shipping
    
    > [High availability and disaster recovery for SQL Server in Azure Virtual Machines](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)
    >
    > If the considered option is to use Failover Clustering -  [Configure SQL Server Failover Cluster Instance on Azure Virtual Machines](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-create-failover-cluster)
    >
    > If the considered option is to use Availability Groups - [Configure Always On Availability Group on Azure Virtual Machines](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial)

* **Are you aware of the built-in functionality of Azure SQL Database for Business Continuity and Disaster Recovery?**

    Identify whether Infrastructure as a Service (IaaS) been chosen without considering all options. Could manageability of the database solution be improved, by using Azure SQL Database?    
    
    > [Learn about automatic SQL Database backups](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-automated-backups)
    >
    > [Recover an Azure SQL database using automated database backups](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-recovery-using-backups)

* **Have you considered Active Geo-Replication in Azure SQL Database for High Availability?**

    Is High availability being assumed as a part of the solution because it is a Platform as a Service (PaaS) solution? Has there been any consideration to the steps needed to be taken during region failure or RPO?    
    
    > [Failover groups and active geo-replication](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview)

* **How does the application behave if the database fails over to a secondary site? &nbsp;**

    Determine whether automatic failover groups, or Always on Availability Groups being used to handle the failover. If they are not, identify how this is being achieved. Additionally, determine how the application handles rollback or failed transactions.   

     > [Compensating Transaction pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/compensating-transaction)

## Monitoring & Management    

* **How do you monitor your data layer?**

    Determine whether there is any enterprise monitoring of the data layer. How is it determined that the solution is working appropriately? If this is not being used, consider the associated documentation.    
    
    > [Monitoring database performance in Azure SQL Database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-single-database-monitor)

* **How would you know if you had an outage or failure?**

    Monitoring may be configured, but how much is it used? Determine if a live issue would first be reported by end-users, or whether monitoring systems would pick this up in advance. This also leads towards DevOps, and having a representative environment prior to production, which has representative tests in place.    
 
* **What alerts have been set-up?**

    Does the monitoring system require an individual to take the initiative and review the details, or will it send proactive notifications such as e-mails? 
    
* **Do you track the performance of queries from the application through to the DB layer?**

    Determine if proactive measures are being taken to manage database performance, and therefore proactive steps in managing the SLA and Performance of the application.    
    
    > [Automatic tuning in Azure SQL Database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-automatic-tuning)
    >
    > [Operating the Query Store in Azure SQL Database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-operate-query-store)

* **What solutions do your DBAs use to manage the data estate?**

    Determine whether an enterprise approach is being taken to managing the SQL estate, or whether each database is being maintained on a case-by-case basis. Identify whether there is an opportunity to manage the SQL estate as a fleet, rather than individual machines or databases.     

* **How do you determine the current patch level across the estate?**

    Determine whether there is any automation in place. Unpatched machines presents a risk in the environment, and this is undesirable, especially at the data layer which is generally core to an application.    
    
    > [Automated Patching for SQL Server in Azure Virtual Machines](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)

* **Do you use any IDS/IPS software for threat detection?**

    Determine the proactive steps being taken in maintaining the security of the data estate.  

    > [SQL Vulerability Assessment](https://docs.microsoft.com/en-us/azure/sql-database/sql-vulnerability-assessment)  
    
## Performance & Scalability    

* **Is your database performance and usage predictable?**

    Determine whether elastic pools or individual databases should be considered within the solution.    
    
    > [Elastic pools help you manage and scale multiple Azure SQL databases ](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-pool)

* **Are you using SQL Server on IaaS? Have you placed your virtual machines into an availability set?**

    To provide redundancy to your application, it is recommended that you group two or more virtual machines of the same tier in an availability set. This configuration within a datacenter ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the 99.95% Azure SLA. 
    
    > [Manage the availability of Windows virtual machines in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability)

* **Are you using SQL Server on IaaS? Do you know about the difference between unmanaged and managed disks? Have you leveraged Azure Managed disks?**

    Identify whether the throughput levels of your underlying disks and compute has been considered to safeguard the performance of your solution. Also be aware of managed disks, and the benefits that this could bring to the reliability of your solution.   
    > [Performance best practices for SQL Server in Azure Virtual Machines](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)
    > 
    > [Azure Managed Disks Overview](https://docs.microsoft.com/en-gb/azure/storage/storage-managed-disks-overview)

* **Are you using SQL Server on IaaS? Have you configured your implementation to the recommendations in the performance best practices documentation?**

    The associate documentation provides recommended practices in configuring IaaS solutoions, and ensuring suitable performance.    
    
    > [Performance best practices for SQL Server in Azure Virtual Machines](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

## Security    

* **Are you aware of the Azure SQL DB best practices? Have you implemented these in your solution?**   

    Security is a top concern when managing databases, and it has always been a priority for Azure SQL Database. Your databases can be tightly secured to help satisfy most regulatory or security requirements.
    
    > [Azure SQL Database security best practices](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices)
    > 
    > [Azure database security checklist](https://docs.microsoft.com/en-us/azure/security/azure-database-security-checklist)

* **Is the data stored in your database sensitive? Do you require special data handling?**

    Identify the encryption and protection requirements of the solution. Leverage the associated documentation in providing a solution to this problem.    
    
    > [Azure SQL Database Discovery and Classification](https://docs.microsoft.com/en-gb/azure/sql-database/sql-database-data-discovery-and-classification)
    > 
    > [Always Encrypted (Database Engine)](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine)
    > 
    > [Transparent Data Encryption (TDE)](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde)
    > 
    > [SQL Server Encryption](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption)

* **Do you audit access to the servers and the DDL queries that are run?**

    Determine whether there is an understanding into which users are performing which tasks / queries / functoins? Is this level of detail needed, perhaps for compliance or some form of internal business policy?    
    
    > [Monitor your Azure SQL DAtabase auditing with Power BI](https://powerbi.microsoft.com/en-us/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/)

* **Who has admin access to the system?**

    This builds upon the previous question. Limiting admin access is a recommended practice. Admins can bypass security measures and potentially see protected data.    

* **Do you encrypt your backups?**

    Protecting data at rest may be important. Is there a guarantee that backed-up data cannot be restored to another server that is not under your control?    
    

* **Can you define the business impact for a data breach?**

    Determine whether there is an understanding into the follow-on effects of a data breach. Has the wider business impact been considered, rather than just focusing on the technology challenge and impact?    

## Stories 

  > [Azure SQL Database customer implementation technical studies](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-customer-implementations)