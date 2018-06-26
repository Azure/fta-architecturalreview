# FastTrack for Azure Architectural Discussion Framework - Data Warehouse Solution

## This Page is currently under construction

- [FastTrack for Azure Architectural Discussion Framework - Data Warehouse Solution](#fasttrack-for-azure-architectural-discussion-framework---data-warehouse-solution)
  * [Data Volumes & Ingestion](#data-volumes--amp--ingestion)
  * [Data Architecture](#data-architecture)
  * [Data Cleanliness](#data-cleanliness)
  * [Query Patterns](#query-patterns)
  * [Performance & Scalability](#performance---scalability)
  * [Security](#security)

## Data Volumes & Ingestion

* **What size of data are you ingesting and is your data already hosted in Azure, for example, Blob Storage, Azure Data lake Store or coming from an Azure resource?**

    How much data we're talking about drives the technology to a degree. IF someone says they have less than 2 TB worth of data, Azure SQL Database would be a valid option (why? - Data in SQL DW ColumnStore indexes, drives efficiencies, SQL DB supports column level indexes of 4TB - Cost of DB becomes prohibitive). If they have more than this, and have querieis which are complex, then SQL Data Warehouse would become the preferable option. (SQL IaaS?)

    * [Azure SQL DB Pricing Page with storage limits](https://azure.microsoft.com/en-us/pricing/details/sql-database/single/)
    * [Columnstore support in Standard tier Azure SQL Databases](https://azure.microsoft.com/en-us/blog/columnstore-support-in-standard-tier-azure-sql-databases/)

    Talking about ingesting of data is critical to understand the technology choice. If we're talking data lake, could the amount of data exceed Azure Storage (what is this?) What approach do we need to take to ingestion if we're moving 10TB a day. Can't look at overnight due to time taken for processing.
    
    * [Migrating data to Azure SQL Data Warehouse in practice](https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/)
    * [Polybase Guige](https://docs.microsoft.com/en-us/sql/relational-databases/polybase/polybase-guide?view=sql-server-2017)

## Data Architecture

* **Is your database structured as a star schema or well defined Dimensions & Facts?**

    Determine the amount of effort required to design for a MPP warehouse solution and suitability of the Database to move to SQL DW

    Is this a traditional data warehouse, or a modern data warehouse? Has someone actually designed a DW, and is created for a business need and for a specified business output, and have thought about those kind of bits, or are htey doing mdodern data warehouse - store all data - stick tin in front of it and compute when someone asks us.

    Are we batch processing overnight, or are we streaming?

    Question drives technology - You have to structure the data if you are using SQL DW, whereas HD insight / data lake - schema on read.

    * [Guidance for designing distributed tables in Azure SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-tables-distribute)
    * [Design guidance for using replicated tables in Azure SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/design-guidance-for-replicated-tables)
    * [Stream big data into a data warehouse](https://docs.microsoft.com/en-us/azure/event-grid/event-grid-event-hubs-integration)
    * [Designing Extract, Load, and Transform (ELT) for Azure SQL Data Warehouse](https://docs.microsoft.com/en-gb/azure/sql-data-warehouse/design-elt-data-loading)

## Data Cleanliness

* **Do you master your data and do you pre-process your data to ensure conformity and accuracy of the data?**

    Determine is a process needs to be defined to clean the and process the data.  Is there data governance in place in the existing solution

## Query Patterns

* **How many concurrent users do you expect to be querying the data from the data warehouse?**

    Determine access patterns and define is a Mart or Symantic Layer is required to facilite querying.  Limitations in concurrent access within SQL DW

    * [Hub and spoke series integration with SQL Database](https://azure.microsoft.com/en-gb/blog/azuresqldw-hub-and-spoke-series-integration-with-sql-database/)
    * [SQL Data Warehouse capacity limits](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits)

## Performance & Scalability

* **Do you have any requirments, SLAs or boundaries that required queries to return within a specific period of time?**

    Determine sizing of the DW, influencing MPP schema and supporting infrastructure

    * [SQL Data Warehouse capacity limits](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits)

## Security

* **What level of sensitivity is the data you are storing?**

    Determine what security requirments are required to handle the data

    * [Authenticate to Azure SQL Database](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-authentication)
    * [Service to Service Authenticate within Azure](https://docs.microsoft.com/en-gb/azure/data-lake-store/data-lake-store-service-to-service-authenticate-using-active-directory)

* **Is the data subject to GDPR compliance?**

    Do GDPR rules apply and do the relevent processes need to be in place to handle this

    * [Azure Security and Compliance Blueprint: Data Warehouse for GDPR](https://docs.microsoft.com/en-us/azure/security/blueprints/gdpr-datawarehouse-overview)

