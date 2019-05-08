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