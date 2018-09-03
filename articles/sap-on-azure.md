# FastTrack for Azure Architectural Discussion Framework - SAP on Azure Solution

- [FastTrack for Azure Architectural Discussion Framework - Sap on Azure Solution](#fasttrack-for-azure-architectural-discussion-framework---data-warehouse-solution)
  - [SAP Landscape Design](#data-volumes--ingestion)
  - [SAP Landscape Sizing](#data-architecture)
  - [High Availability and Business Continuity / Disaster Recovery](#data-cleanliness)
  - [Performance & Scalability](#query-patterns)
  - [Backup and Archival](#performance--scalability)
  - [Migration Methodologies](#security)
  - [Security Design](#security)
  - [Monitoring & Management](#security)
  - [Stories](#security)

## SAP Landscape Design

- **How is your current SAP Landscape and which systems are you planning to move to Azure?**

    Please provide landscape diagram, Operating system, database details of the SAP environment.
    - [SAP systems which are certified to run on Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/sap-certifications)
- **What are your future roadmap to SAP environment and are there any plans to move to S/4 Hana?**
- **Are you hosting it on-premises or partner data centre.  In which region you are planning to host in Azure?**
 

## SAP Landscape Sizing

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