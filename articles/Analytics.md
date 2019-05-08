# FastTrack for Azure Architectural Discussion Framework - Analytics Solutions

- [FastTrack for Azure Architectural Discussion Framework - Analytics Solutions](#fasttrack-for-azure-architectural-discussion-framework---Analytics-solutions)
    - [Is it a Big Data Processing Solution?](#Is-it-a-Big-Data-Processing-Solution?)
    - [Big Data cluster & processing information](#Big-Data-cluster--processing-information )
    - [Distributed Architecture/Resiliency of Database/High Availability across regions](#Distributed-Architecture/-Resiliency-of-Database/-High-Availability-across-regions)
    - [Performance & Scalability](#Performance--Scalability)
    - [Disaster Recovery](#Disaster-Recovery)
    - [Monitoring & Management](#Monitoring--Management)
    - [Security & Compliance](#Security--Compliance)


## Is it a Big Data Processing Solution?

 * How do we know that the solution is a Big Data Processing pipeline? 
    * Volume – How much data are we ingesting? High throughput processing is a requirement? 
    * Velocity – How fast the data will be flowing into the pipeline? Do we need low latency processing? 
    * Variety – What type of data is flowing into the pipeline? Structured? Unstructured? Semi-structured? What is the data model? 


## Big Data cluster & processing information

 * What type of workload (s), project (s), services are they targeting? 
    * Scenarios
        * Real time big data workload processing.
        * Big data batch processing
        * Both (Lambda Architecture) 
    * Use cases
        * Real time analytics 
        * Real time order processing etc. 
        * Batch analytics on large amount of data  
        * Data Integration Hub 
    * Example: Real time data ingestion, store (IoT), and analytical processing pipeline to gather insights from the device data and provide services based on the analysis (i.e. vehicle maintenance notification)  
 * How is the data being ingested? Where the data is being ingested to? 
    * Is the data coming from applications? 
        * Example: API App (through API management) or web app? 
        * If this is coming through an app, please refer to [Application Modernization](https://github.com/Azure/fta-architecturalreview/blob/master/articles/application-modernization.md) for further considerations. 
    * Is it streaming data?
        * Event Hub
        * IoT Hub
        * Kafka
        * On demand ADF job 
    * Is it a batch data (coming from stored data sources – csv, tsv, relational in a batch)
        * Azure SQL DB
        * Blob
        * ADLS 
        * ADF Flow 
 * How the data is being processed?
    * For batch processing, [Choosing a batch processing technology in Azure](https://github.com/Azure/fta-architecturalreview/blob/master/articles/application-modernization.md), will help getting further guidance.
    * [Data warehousing and analytics](https://docs.microsoft.com/en-us/azure/architecture/example-scenario/data/data-warehouse) is an architecture pattern for batch analytics 
    * For real time analytics and processing, the following articles may help
        * [IoT for construction](https://docs.microsoft.com/en-us/azure/architecture/example-scenario/data/big-data-with-iot)
        * [Automotive IoT data](https://docs.microsoft.com/en-us/azure/architecture/example-scenario/data/realtime-analytics-vehicle-iot) 
        * [Real-time fraud detection](https://docs.microsoft.com/en-us/azure/architecture/example-scenario/data/realtime-analytics-vehicle-iot)
 * Do we have a serving layer consideration?
    * Store processed data for downstream modelling and reporting purposes
    * Modelling data (for Azure Analysis Service)
    * Reporting data (Power BI)
    * Serving data to other applications (store it in CosmosDB, Azure Blob Storage or Redis Cache etc.!!!) 
 * Are we planning to migrate and existing big data workload?
    * From on prem Or from other cloud deployment? 
    * For a migration scenario we try to collect the following scenario (considering)
        * Hadoop Distribution (Cloudera/Hortonworks)
        * Cluster workload type (Spark/Hadoop/MapReduce)
        * How many worker nodes or head nodes for the cluster?
            * How many CPU/Cores are in the Head Nodes (Name Nodes) and  Worker Nodes?
        * How much memory is in each of the Name Nodes or Data Node?
        * Do we have any specific component of Hadoop requiring specific memory confirmation?
            * HiveSever2 have allocated memory of 32 GB of RAM per node.
        * What is the size of HDFS, Hive (internal tables)?  
        * Where is HDFS mounted?
        * Hive tables are built on HDFS (typical)?
        * How much time does it take to get data uploaded to HDFS (data ingestion into Hadoop)?
        * How are we ingesting the data?
    * How much time does it take end to end (ingestion/processing)? What is the goal when we go to Azure.
    * Which component are used to ingest Data (i.e Sqoop)?
    * Which component are providing/sending data to serving layer (i.e. Data Warehouse)
    * How often we ingest/process the data (daily, hourly)?
    * Additional data sources for Hadoop?


## Distributed Architecture/Resiliency of Database/High Availability across regions

- **How sensitive is the data being stored, what retention policies are you using, what access restrictions are needed with the data?**

    Understanding the security and compliance is critical when storing potentially sensitive customer data.  Does the company have permission to hold the data, is the data sensitive and therefore required audit or restricted access ?  Will the resulting output from the data process be accessible to everyone or not ?

    - [Enterprise Security Package for HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/domain-joined/apache-domain-joined-introduction)
    - [General Data Protection Rules (GDPR) Explained](https://ico.org.uk/for-organisations/guide-to-the-general-data-protection-regulation-gdpr/)
    - [Access Control for SQL Database and SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access)


## Performance & Scalability

- **How sensitive is the data being stored, what retention policies are you using, what access restrictions are needed with the data?**

    Understanding the security and compliance is critical when storing potentially sensitive customer data.  Does the company have permission to hold the data, is the data sensitive and therefore required audit or restricted access ?  Will the resulting output from the data process be accessible to everyone or not ?

    - [Enterprise Security Package for HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/domain-joined/apache-domain-joined-introduction)
    - [General Data Protection Rules (GDPR) Explained](https://ico.org.uk/for-organisations/guide-to-the-general-data-protection-regulation-gdpr/)
    - [Access Control for SQL Database and SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access)

## Disaster Recovery

- **How sensitive is the data being stored, what retention policies are you using, what access restrictions are needed with the data?**

    Understanding the security and compliance is critical when storing potentially sensitive customer data.  Does the company have permission to hold the data, is the data sensitive and therefore required audit or restricted access ?  Will the resulting output from the data process be accessible to everyone or not ?

    - [Enterprise Security Package for HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/domain-joined/apache-domain-joined-introduction)
    - [General Data Protection Rules (GDPR) Explained](https://ico.org.uk/for-organisations/guide-to-the-general-data-protection-regulation-gdpr/)
    - [Access Control for SQL Database and SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access)


## Monitoring & Management

- **How sensitive is the data being stored, what retention policies are you using, what access restrictions are needed with the data?**

    Understanding the security and compliance is critical when storing potentially sensitive customer data.  Does the company have permission to hold the data, is the data sensitive and therefore required audit or restricted access ?  Will the resulting output from the data process be accessible to everyone or not ?

    - [Enterprise Security Package for HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/domain-joined/apache-domain-joined-introduction)
    - [General Data Protection Rules (GDPR) Explained](https://ico.org.uk/for-organisations/guide-to-the-general-data-protection-regulation-gdpr/)
    - [Access Control for SQL Database and SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access)

## Security & Compliance

- **How sensitive is the data being stored, what retention policies are you using, what access restrictions are needed with the data?**

    Understanding the security and compliance is critical when storing potentially sensitive customer data.  Does the company have permission to hold the data, is the data sensitive and therefore required audit or restricted access ?  Will the resulting output from the data process be accessible to everyone or not ?

    - [Enterprise Security Package for HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/domain-joined/apache-domain-joined-introduction)
    - [General Data Protection Rules (GDPR) Explained](https://ico.org.uk/for-organisations/guide-to-the-general-data-protection-regulation-gdpr/)
    - [Access Control for SQL Database and SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access)