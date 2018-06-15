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

* **What size data are your ingesting and is your data already hosting in Azure - such as Blob Storage, Azure Datalake Store or coming from an Azure resource?**

    Determine the amount of data that is expected to be stored in the DW and is Azure SQL DW the best resource to use.


## Data Architecutre

* **Is your database structured as a star schema or well definded Dimensions & Facts?**

    Determine the amount of effort required to design for a MPP warehouse solution and suitability of the Database to move to SQL DW


## Data Cleanliness

* **Do you master your data and do you pre-process your data to ensure conformity and accuracy of the data?**

    Determine is a process needs to be defined to clean the and process the data.  Is there data governance in place in the existing solution

## Query Patterns

* **How many concunnret users do you exct to be querying the data from the data warehouse?**

    Determine access patterns and define is a Mart or BSymantic Layer is required to facilite querying.  Limitations in concurrent access within SQL DW

## Performance & Scalability

* **Do you have any requirments, SLAs or boundaries that required queries to return within a specific period of time?**

    Determine sizing of the DW, influencing MPP schema and supporting infrastructure

## Security

* **What level of sensitivity is the data you are storing?**

    Determine what security requirments are required to handle the data

* **Is the data subject to GDPR compliance?**

    Do GDPR rules apply and do the relevent processes need to be in place to handle this

* **Do you need to implement persona based access controls, row level secuirty or cell level security**

    Determine the required implementaion technology to facilitate enhanced securty when accessig the data
