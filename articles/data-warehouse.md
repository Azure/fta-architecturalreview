# FastTrack for Azure Architectural Discussion Framework - Data Warehouse Solution

- [FastTrack for Azure Architectural Discussion Framework - Data Warehouse Solution](#fasttrack-for-azure-architectural-discussion-framework---data-warehouse-solution)
  - [Data Volumes & Ingestion](#data-volumes--ingestion)
  - [Data Architecture](#data-architecture)
  - [Data Cleanliness](#data-cleanliness)
  - [Query Patterns](#query-patterns)
  - [Performance & Scalability](#performance--scalability)
  - [Security](#security)

## Data Volumes & Ingestion

- **What size of data are you ingesting and is your data already hosted in Azure, for example, Blob Storage, Azure Data lake Store or coming from an Azure resource?**

    Understanding how much data is being stored is a deciding factor when selecting the RDBMS to store the data in.  If the data volume is less that 4TB in total, Azure SQL Database can prove to be easier to implement and more cost effective.  Leveraging ColumnStore indexes in SQL DB will provide the warehouse level of performances across aggregate queries.

  - [Azure SQL DB Pricing Page with storage limits](https://azure.microsoft.com/en-us/pricing/details/sql-database/single/)
  - [ColumnStore support in Standard tier Azure SQL Databases](https://azure.microsoft.com/en-us/blog/columnstore-support-in-standard-tier-azure-sql-databases/)

    Understanding the ingestion of data is critical to the technology choice. If we're talking data lake, could the amount of data exceed Azure Storage ([Detailed here](https://docs.microsoft.com/en-us/azure/azure-subscription-service-limits#storage-limits)).

    What approach do we need to take to ingestion if we're moving 10TB a day. For instance, overnight jobs may not be considered due to time taken for processing.

  - [Migrating data to Azure SQL Data Warehouse in practice](https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/)
  - [Polybase Guide](https://docs.microsoft.com/en-us/sql/relational-databases/polybase/polybase-guide?view=sql-server-2017)

## Data Architecture

- **Is your database structured as a star schema, Data Vault or well defined Dimensions & Facts?**

    Determine the amount of effort required to design for a MPP warehouse solution and suitability of the Database to move to SQL Data Warehouse.

    Is this a traditional data warehouse, or a modern data warehouse? Has someone designed a Data Warehouse, and is created for a business need, and to solve a specified business output? Or are they taking a modern data warehouse approach - storing all data - using compute to solve a problem as it is defined / when someone asks.

    Are we batch processing overnight, or are we streaming? This will help in determining the amount of time available for the processing of this data.

    These questions drives technology choices - You have to structure the data if you are using SQL Data Warehouse, whereas HD insight and Azure Data Lake take a schema on read approach.

  - [Guidance for designing distributed tables in Azure SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-tables-distribute)
  - [Design guidance for using replicated tables in Azure SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/design-guidance-for-replicated-tables)
  - [Stream big data into a data warehouse](https://docs.microsoft.com/en-us/azure/event-grid/event-grid-event-hubs-integration)
  - [Designing Extract, Load, and Transform (ELT) for Azure SQL Data Warehouse](https://docs.microsoft.com/en-gb/azure/sql-data-warehouse/design-elt-data-loading)

## Data Cleanliness

- **Do you master your data and do you pre-process your data to ensure conformity and accuracy of the data?**

    Determine if a process needs to be defined to clean the and process the data. Is there data governance in place in the existing solution?

## Query Patterns

- **How many concurrent users do you expect to be querying the data from the data warehouse?**

    Determine access patterns and define if a Mart or Symantic Layer is required to facilitate querying. Limitations in concurrent access within SQL DW.

  - [Hub and spoke series integration with SQL Database](https://azure.microsoft.com/en-gb/blog/azuresqldw-hub-and-spoke-series-integration-with-sql-database/)
  - [SQL Data Warehouse capacity limits](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits)

## Performance & Scalability

- **Do you have any requirements, Service Level Agreements (SLAs) or boundaries that required queries to return within a specific period of time?**

    This information will influence the sizing of the Data Warehouse, in addition to an MPP schema and appropriate supporting infrastructure.

  - [SQL Data Warehouse capacity limits](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits)

## Security

- **What level of sensitivity is the data you are storing?**

    This helps determine whether there is any Personally Identifiable Information in the data being held, or whether there are specific security requirements for the data being stored. These may drive technology decisions, and configuration decisions of those technologies.

  - [Authenticate to Azure SQL Database](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-authentication)
  - [Service to Service Authenticate within Azure](https://docs.microsoft.com/en-gb/azure/data-lake-store/data-lake-store-service-to-service-authenticate-using-active-directory)

- **Is the data subject to GDPR compliance?**

  Do GDPR rules apply and do the relevant processes need to be in place to handle this

  - [Azure Security and Compliance Blueprint: Data Warehouse for GDPR](https://docs.microsoft.com/en-us/azure/security/blueprints/gdpr-datawarehouse-overview)