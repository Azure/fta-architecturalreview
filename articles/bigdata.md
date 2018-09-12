# FastTrack for Azure Architectural Discussion Framework - BigData Solutions

- [FastTrack for Azure Architectural Discussion Framework - BigData Solutions](#fasttrack-for-azure-architectural-discussion-framework---bigdata-solutions)
    - [Data Volumes & Ingestion](#data-volumes--ingestion)
    - [Data Usage](#data-usage)
    - [Security & Compliance](#security--compliance)

## Migration

- **Are you already using Big Data technologies on-premises?**

    Determining what technologies are in play is an important step. While Azure offers many technologies in this space, it makes no sense to take on a new technology and retrain the staff, when an existing technology and serve both the business need and minimize cost.

## Data Volumes & Ingestion

- **Where is the data sourced from?**
    
    Where the data is coming from and how it flows can change the tools that you use for collecting and even processing data. The architecture can change based on the format of the data and velocity.

    - [Real-time Messaging Ingestion](https://docs.microsoft.com/en-us/azure/architecture/data-guide/technology-choices/real-time-ingestion)
    - [Pipeline Orchestration](https://docs.microsoft.com/en-us/azure/architecture/data-guide/technology-choices/real-time-ingestion)
    - [Real-Time Processing](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/real-time-processing)

- **What size of data are you storing, how often will the data be arriving and is your data coming from within Azure, for example, Azure storage, Event Hubs?**

    Understanding the data volumes, speed of arrival and rate of change is important in deciding how to handle and store the data for processing.  Understanding if this is streaming data or batch ingest will determine of it has already been processed or might require transformation - which could also be achieved at runtime.

    - [Big Data Architecture Styles](https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/big-data)
    - [Big Data Architectures](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/)
    - [Azure Storage Scalability & Performance Targets](https://docs.microsoft.com/en-us/azure/storage/common/storage-scalability-targets)
    - [Introduction to Azure Data Lake Storage Gen 2](https://docs.microsoft.com/en-us/azure/storage/data-lake-storage/introduction)
    
- **How will the data be formatted when it leaves the source system and how do you plan on consuming that data once it is in Azure?**

    Understanding how the data will be used and what format it will arrive in is critical to defining what processing needs to take place, or what schema on read resources might need to be used to facilitate data access.

    - [Use HDInsight Spark cluster to read and write data to Azure SQL database](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-connect-to-sql-database)
    - [Serialize data in Hadoop with the Microsoft Avro Library](https://docs.microsoft.com/en-us/azure/hdinsight/hadoop/apache-hadoop-dotnet-avro-serialization)
    - [Polybase Guide](https://docs.microsoft.com/en-us/sql/relational-databases/polybase/polybase-guide?view=sql-server-2017)


## Data Structure and Usage

- **How will the data be consumed ?  Is the expectation that there will be some type of interactive query capability or will this be batch processed ?**

    Understanding how the data will be accessed is critical in the choice of BigData technology.  Interactive query leads to technologies such as HDInsight LLAP (Interactive Hive), Azure SQL Data Warehouse or even Spark/DataBricks.  Those can also work for batch but there are also Hive, MapReduce and similar technologies that can help with batch scenarios.

    - [Use Interactive Query with HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/interactive-query/apache-interactive-query-get-started)
    - [Azure DataBricks](https://azure.microsoft.com/en-us/services/databricks/)
    - [Azure HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/)
    - [Azure SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is)

- **What is the eventual use for the data being collected?**
    - [Batch Processing](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/batch-processing)
    - [Real Time Processing](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/real-time-processing)
    - [Machine Learning at Scale](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/machine-learning-at-scale)
    - [Advanced Analytics](https://docs.microsoft.com/en-us/azure/architecture/data-guide/scenarios/advanced-analytics)
    - [Time Series Solutions](https://docs.microsoft.com/en-us/azure/architecture/data-guide/scenarios/time-series)

- **Is your team familiar with Python, Scala, R, Java, or another programming language in the analytics space?**
    
    When determining a BigData technology, it's almost as important to know the existing skillset in this space as it is to understand the business problem itself. There are so many tooling choices for each type of solution, that it's important to not only match solutions to business problems, but also the skillset of the team that is adopting the technology. 
    
    - [Azure HDInsight with Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)
    - [Azure HDInsight with ML Services](https://docs.microsoft.com/en-us/azure/hdinsight/r-server/r-server-overview)

## Security & Compliance

- **How sensitive is the data being stored, what retention policies are you using, what access restrictions are needed with the data?**

    Understanding the security and compliance is critical when storing potentially sensitive customer data.  Does the company have permission to hold the data, is the data sensitive and therefore required audit or restricted access ?  Will the resulting output from the data process be accessible to everyone or not ?

    - [Enterprise Security Package for HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/domain-joined/apache-domain-joined-introduction)
    - [General Data Protection Rules (GDPR) Explained](https://ico.org.uk/for-organisations/guide-to-the-general-data-protection-regulation-gdpr/)
    - [Access Control for SQL Database and SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access)

## Management and Monitoring

- **How do you plan on monitoring your architecture for issues?**

    For alerting, scaling, and management, a set of reporting and monitoring needs to be setup so that we can understand how our architecture is doing and the quality of the performance of the application. 

    - [Using Azure Log Analytics to monitor HDInsight clusters](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-oms-log-analytics-tutorial)
    - [Monitor Cluster Performance(HDInsight)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-key-scenarios-to-monitor?toc=%2Fen-us%2Fazure%2Fhdinsight%2Fdomain-joined%2FTOC.json&bc=%2Fen-us%2Fazure%2Fbread%2Ftoc.json)
    - [Manage HDInsight Clusters by using the Ambari web UI](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-manage-ambari)
    - [Monitoring Databricks Jobs with Application Insights](https://msdn.microsoft.com/en-us/magazine/mt846727.aspx)
    - [Monitoring Azure applications and resources](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview)
    - [HDInsight Orchestration using Azure App Services](https://www.microsoft.com/developerblog/2016/08/28/hdinsight-orchestration-using-azure-app-services/)
    - [Cluster Size and Autoscaling](https://docs.azuredatabricks.net/user-guide/clusters/sizing.html)