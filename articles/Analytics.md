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

- **What size of data are you storing, how often will the data be arriving and is your data coming from within Azure, for example, Azure storage, Event Hubs?**

    Understanding the data volumes, speed of arrival and rate of change is important in deciding how to handle and store the data for processing.  Understanding if this is streaming data or batch ingest will determine of it has already been processed or might require transformation - which could also be achieved at runtime.

    - [Big Data Architecture Styles](https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/big-data)
    - [Azure Storage Scalability & Performance Targets](https://docs.microsoft.com/en-us/azure/storage/common/storage-scalability-targets)
    - [Introduction to Azure Data Lake Storage Gen 2](https://docs.microsoft.com/en-us/azure/storage/data-lake-storage/introduction)

    
- **How will the data be formatted when it leaves the source system and how do you plan on consuming that data once it is in Azure?**

    Understanding how the data will be used and what format it will arrive in is critical to defining what processing needs to take place, or what schema on read resources might need to be used to facilitate data access.

    - [Use HDInsight Spark cluster to read and write data to Azure SQL database](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-connect-to-sql-database)
    - [Serialize data in Hadoop with the Microsoft Avro Library](https://docs.microsoft.com/en-us/azure/hdinsight/hadoop/apache-hadoop-dotnet-avro-serialization)
    - [Polybase Guide](https://docs.microsoft.com/en-us/sql/relational-databases/polybase/polybase-guide?view=sql-server-2017)


## Big Data cluster & processing information

- **How will the data be consumed ?  Is the expectation that there will be some type of interactive query capability or will this be batch processed ?**

    Understanding how the data will be accessed is critical in the choice of BigData technology.  Interactive query leads to technologies such as HDInsight LLAP (Interactive Hive), Azure SQL Data Warehouse or even Spark/DataBricks.  Those can also work for batch but there are also Hive, MapReduce and similar technologies that can help with batch scenarios.

    - [Use Interactive Query with HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/interactive-query/apache-interactive-query-get-started)
    - [Azure DataBricks](https://azure.microsoft.com/en-us/services/databricks/)
    - [Azure HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/)
    - [Azure SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is)


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