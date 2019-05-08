# FastTrack for Azure Architectural Discussion Framework - Analytics Solutions

- [FastTrack for Azure Architectural Discussion Framework - NoSQL Solutions](#fasttrack-for-azure-architectural-discussion-framework---NoSQL-solutions)
    - [Is it App or Data Modernization?](#Is-it-App-or-Data-Modernization?)
    - [Is it NoSQL Data Solution?](#Is-it-NoSQL-Data-Solution?)
    - [Distributed Architecture/Resiliency of Database/High Availability across regions](#Distributed-Architecture/-Resiliency-of-Database/-High-Availability-across-regions)
    - [Performance & Scalability](#Performance--Scalability)
    - [High Availability](#High-Availability)
    - [Monitoring & Management](#Monitoring--Management)
    - [Security & Compliance](#Security--Compliance)


## Is it App or Data Modernization?

 * Is this a sole Data Modernization or Data and Application Modernization play ?

## Is it NoSQL Data Solution?
 * For the data migration, what workloads, projects, services are they targeting?
    * Cloud scenarios include: 
        * Greenfield Application implementation on CosmosDB	
            * SQL Server migration to Azure SQL Database Managed Instance
            * OSS DB migration to Azure Database for MySQL and PostgreSQL
            * NoSQL migration to Azure Cosmos DB. 
        * Use cases we are targeting to use CosmosDB for.
        * Example: Source of Truth (SOT) for multiple down level applications, real time data store (IoT), order processing.
 
 * If application is involved, Is it a Green Field Application or existing application
    * Cloud Born or On premises?
    * Is your database already hosted in Azure?
 
 * Do you know the Data Model?
    * Is it Relational Data or NoSQL Data (unstructured Semi Structured)
    * If NoSQL, is it Key-Value, Columnar, Graph or Document Data Model?
 * What size is your database and how many databases are you planning to migrate?

## Distributed Architecture/Resiliency of Database/High Availability across regions

* Is the need to have a global application (supporting multiple regions apps)?
* Do need to support multi region writes or single write regions and multiple read regions?
* Horizonal Partitioning is done automatically in Azure Cosmos DB. Are you aware?



## Performance & Scalability

 * Do you need to build highly responsive apps? 
    Your application can be easily designed to perform near real-time reads and writes. It can use single-digit millisecond latencies against all the regions you chose for your database. Azure Cosmos DB internally handles the data replication between regions. As a result, the consistency level selected for the Azure Cosmos DB account is guaranteed.
 
    Many applications benefit from the performance enhancements that come with the ability to perform multi-region (local) writes. Some applications that require strong consistency prefer to funnel all writes to a single region. For these applications, Azure Cosmos DB supports single region and multi-region configurations.
 
 * What is the scalability need?
    With the multi-master feature, you can elastically scale read and write throughput all around the world. The multi-master feature guarantees the throughput that your application configures on an Azure Cosmos DB database or a container is delivered across all regions. The throughput also is protected by financially backed SLAs.
 
 * What type of Consistency you are looking for?
    The Azure Cosmos DB replication protocol offers five well-defined, practical, and intuitive consistency models. Each model has a tradeoff between consistency and performance. Use these consistency models to build globally distributed applications with ease.

 * Data access pattern and partitioning strategy?
    What is the balance between writes and reads in your service? How do you intend to modify the default index strategy, if at all? What are you going to use as your Partition Key, and what is driving that decision?


## High Availability

 * How much data can you afford to lose in your solution if you have to recover a database?
    Determine whether any loss of data is allowed. If this is not allowed, approaches to High Availability will need to be considered.
 * How does the application behave if the database fails over to a secondary site?  
 * How much downtime can you afford during data and app modernization?
    RTO/RPO Considerations.
    Determine the allowed recovery time and if backups are the approach. 


## Monitoring & Management

 * How do you monitor your data layer?
    RU Usage, 429 errors
 * How would you know if you had an outage or failure?
 * What alerts have been set-up?
    Does the monitoring system require an individual to take the initiative and review the details, or will it send proactive notifications such as e-mails?
 * Do you track the performance of queries from the application through to the DB layer?


## Security & Compliance

 * Are you aware of the Azure Cosmos DB Security best practices? Have you implemented these in your solution?
 * Is the data stored in your database sensitive? Do you require special data handling?
    Identify the encryption and protection requirements of the solution. Leverage the associated documentation in providing a solution to this problem.
 * Azure Cosmos DB—Database account auditing? Is there a level of detail needed, perhaps for compliance or some form of internal business policy?
 * Who has admin access to the system?
    This builds upon the previous question. Limiting admin access is a recommended practice. Admins can bypass security measures and potentially see protected data.
 * Do you encrypt your backups?
    Protecting data at rest may be important. Is there a guarantee that backed-up data cannot be restored to another server that is not under your control?
 * Can you define the business impact for a data breach?
    Determine whether there is an understanding into the follow-on effects of a data breach. Has the wider business impact been considered, rather than just focusing on the technology challenge and impact?
