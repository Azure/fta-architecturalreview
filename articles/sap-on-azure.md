# FastTrack for Azure Architectural Discussion Framework - SAP on Azure Solution

- [FastTrack for Azure Architectural Discussion Framework - Sap on Azure Solution](#fasttrack-for-azure-architectural-discussion-framework---sap-on-azure-solution)
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
    - [Worldwide Azure regions](https://azure.microsoft.com/en-us/global-infrastructure/regions/)

## SAP Landscape Sizing

- **Could you provide SAP sizing and exiting hardware specifications?**
- **Could you provide SAP Early Watch Report for production systems in the landscape?**
- **What is the current database size of each of the SAP systems and average monthly DB growth?**
- **When was current hardware was last procured/refreshed?**

## High Availability and Business Continuity / Disaster Recovery

- **What is the availability SLA for SAP production environment. Do you have clustered environment for SAP application & database layer for production systems?**

    Refer to the High Availability & disaster recovery concepts for SAP on Azure.
    - [High Availability Architecture for SAP on Azure ](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/sap-certifications)
    - [Reference architecture design for SAP Netweaver for AnyDB on Azure](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/sap/sap-netweaver)
- **What is the plans for disaster recovery setup. What will be recovery time objective (RTO) and Recovery Point Objective (RPO)?**

## Performance & Scalability

- **How many concurrent users do you expect to be querying the data from the data warehouse?**

    Determine access patterns and define if a Mart or Symantic Layer is required to facilitate querying. Limitations in concurrent access within SQL DW.

  - [Hub and spoke series integration with SQL Database](https://azure.microsoft.com/en-gb/blog/azuresqldw-hub-and-spoke-series-integration-with-sql-database/)
  - [SQL Data Warehouse capacity limits](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits)

## Backup & Archival

- **Do you have any requirements, Service Level Agreements (SLAs) or boundaries that required queries to return within a specific period of time?**

    This information will influence the sizing of the Data Warehouse, in addition to an MPP schema and appropriate supporting infrastructure.

  - [SQL Data Warehouse capacity limits](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits)

## Migration Methodologies

- **What level of sensitivity is the data you are storing?**

    This helps determine whether there is any Personally Identifiable Information in the data being held, or whether there are specific security requirements for the data being stored. These may drive technology decisions, and configuration decisions of those technologies.

  - [Authenticate to Azure SQL Database](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-authentication)
  - [Service to Service Authenticate within Azure](https://docs.microsoft.com/en-gb/azure/data-lake-store/data-lake-store-service-to-service-authenticate-using-active-directory)

- **Is the data subject to GDPR compliance?**

  Do GDPR rules apply and do the relevant processes need to be in place to handle this

  - [Azure Security and Compliance Blueprint: Data Warehouse for GDPR](https://docs.microsoft.com/en-us/azure/security/blueprints/gdpr-datawarehouse-overview)

## Security Design


## Monitoring and System Management
- **How do you monitor SAP, database & Infrastructure layers?**
- **How do you determine if there is an outage and what are the alerts which have been setup?**
- **What is the level of automation in system management and operations?**

## Stories
 - [Top 10 considerations for deploying SAP workloads on SQL server in Azure.](https://blogs.msdn.microsoft.com/saponsqlserver/2015/05/25/top-10-key-considerations-for-deploying-sap-applications-on-azure/)