# FastTrack for Azure Architectural Discussion Framework - Analytics Solutions

- [FastTrack for Azure Architectural Discussion Framework - Analytics Solutions](#fasttrack-for-azure-architectural-discussion-framework---Analytics-solutions)
    - [Is it a Big Data Processing Solution?](#Is-it-a-Big-Data-Processing-Solution?)
    - [Big Data cluster & processing information](#Big-Data-cluster--processing-information )
    - [Distributed Architecture/Resiliency of Database/High Availability across regions](#Distributed-Architecture/-Resiliency-of-Database/-High-Availability-across-regions)
    - [Performance & Scalability](#Performance--Scalability)
    - [Disaster Recovery](#Disaster-Recovery)
    - [Monitoring & Management](#Monitoring--Management)
    - [Security & Compliance](#Security--Compliance)


## Is it a Big Data processing solution?

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

 * Do we have a need for a global big data pipeline (supporting multiple regions)?
 * What happens when ingestion layer stops ingesting, because the primary layer, where ingestion component is deployed, goes down? How resilient is the ingestion layer deployment? For HDInsight, consider HA and DR 
 * What happens when the processing layer component is down, because the primary layer, where the big data processing component is deployed, is unavailable? How resilient is the processing layer deployment? 
 * If the serving layer is the source for batch processing, what happens when the serving layer component is down, because the primary region, where the serving layer component is deployed, is unavailable? How resilient is the serving layer deployment? 
    Please review [Availability and reliability of Apache Hadoop clusters in HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-high-availability-linux) for further information. 
    Another resource for HA consider is [Big data streaming - Microsoft Azure](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=2ahUKEwjYnMjixoziAhXWrZ4KHbRIA3kQFjABegQIAxAC&url=https%3A%2F%2Fazure.microsoft.com%2Fmediahandler%2Ffiles%2Fresourcefiles%2Fbig-data-streaming-choices-for-high-availability-and-disaster-recovery-on-microsoft-azure%2FBig_Data_streaming-Choices_for_HA_and_DR.pdf&usg=AOvVaw07rRAqZWLX_C5ExXZ8LT8w) 
    [￼High Availability and Disaster Recovery for HDInsight Kafka - Considerations](https://github.com/anagha-microsoft/hdi-kafka-dr) also goes over multiple aspects of HDInsight Cluster High Availability. 


## Performance & Scalability

 * For batch processing, how long does the processing job takes from the moment it takes the data from the store, processes the data and send stores it to serving layer? 
 * For real time analytics, what is the end to end latency to process data? (from the moment data is reached to the ingestion layer until the data is stored in the serving layer) 
    * Realtime processing
        * How many messages processed per sec?
            * Example: 500 messages per sec?
        * What is the end to end latency as messages are being stored into the serving layer store?
            * Example: 2 minutes 
    * Batch processing
        * Do we have a representative query that needs to be executed in x amount of time?
        * How much data are we talking about processing per x amount of time? 
 * What is the scalability need?
    * Realtime
        * How many messages are processing now?
            * Example: 200k message per day now
        * How many messages will be processed in the pick time (may on the full load) 
        * I millions message per day during full load
    * Batch
        * How many queries we need to process now?
        * How many queries we need to serve in the full load?

## Disaster Recovery

 * Even for a single region deployment, depending on the cluster configuration, when happens when worker nodes are going down? In HDInsight, for example, headnodes are HA. What happens if both head nodes are down (unlikely scenario, however we do need to consider) 
    * More worker nodes are consider for performance reason, for Hadoop/Spark jobs, but nodes being down, affects the resiliency of the cluster.
 * How much data can you afford to lose in your solution if you have to recover a database? 
    Determine whether any loss of data is allowed. If this is not allowed, approaches to High Availability will need to be considered.  
    This may apply to storage for ingestion layer or Server Layer storage or even in-flight messages, for real time analytics. For example, when a message is sent to Kafka, before Kafka can acknowledge the message (the elect leader got the message, but dies before the message is sent to other nodes in the quorum, so message is not really committed and added to the queue), the message is lost. What is the plan to handle this situation? Replay the message in the up stream? 
 * How much downtime can you afford, before the data/message, reaches to ingestion layer, processing layer or serving layer (message is durably stored in ingestion layer, so this is crucial)?
    Ingestion layer can hold messages for some time (default is 7 days for Kafka) 
    Messages/data can be reprocessed from raw data, if the serving layer doesn’t have the data. How much we can lose? How long can we wait for the fresh data? 
    RTO/RPO Considerations. 
    Determine the allowed recovery time. 
    Please review [Availability and reliability of Apache Hadoop clusters in HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-high-availability-linux) for further information. 
    Another resource for HA consider is [Big data streaming - Microsoft Azure](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=2ahUKEwjYnMjixoziAhXWrZ4KHbRIA3kQFjABegQIAxAC&url=https%3A%2F%2Fazure.microsoft.com%2Fmediahandler%2Ffiles%2Fresourcefiles%2Fbig-data-streaming-choices-for-high-availability-and-disaster-recovery-on-microsoft-azure%2FBig_Data_streaming-Choices_for_HA_and_DR.pdf&usg=AOvVaw07rRAqZWLX_C5ExXZ8LT8w) 
    [￼High Availability and Disaster Recovery for HDInsight Kafka - Considerations](https://github.com/anagha-microsoft/hdi-kafka-dr) also goes over multiple aspects of HDInsight Cluster High Availability.


## Monitoring & Management

 * How do you monitor ingestion layer, processing layer or serving layer? 
    If the data is coming from app, we need to consider app (i.e. Azure App Services) monitoring. 
    If Kafka is used for ingestion, for real time analytics scenario, then how you monitor HDInsight Kafka? What are the metrices to consider? 
 * How would you know if you had an outage or failure?
 * What alerts have been set-up? 
    Does the monitoring system require an individual to take the initiative and review the details, or will it send proactive notifications such as e-mails? 
    [Use Azure Monitor logs to monitor HDInsight clusters](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-oms-log-analytics-tutorial) can help understanding how we can monitor big data clusters in Azure. 
    The blog post, [Monitoring on Azure HDInsight Part 1: An Overview](https://azure.microsoft.com/en-us/blog/monitoring-on-hdinsight-part-1-an-overview/) also provides guidance on monitoring HDInsight Cluster, if used in the solution. 

## Security & Compliance

 * Are you aware of the Apache Hadoop security with Enterprise Security Package? 
    [An introduction to Apache Hadoop security with Enterprise Security Package](https://docs.microsoft.com/en-us/azure/hdinsight/domain-joined/apache-domain-joined-introduction)
    If Azure Databricks is in the consideration, we can use the following link for guidance. 
    [Get enterprise security for big data apps with Azure Databricks](https://databricks.com/get-enterprise-security-for-big-data-apps-with-azure-databricks)
 * Azure Blob Storage or Azure Data Lake store is the HDFS implementation for Azure HDInsight. The [Secure transfer required](https://docs.microsoft.com/en-us/azure/storage/common/storage-require-secure-transfer) feature enhances the security of your Azure Storage account by enforcing all requests to your account through a secure connection 
