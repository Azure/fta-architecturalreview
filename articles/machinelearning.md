# FastTrack for Azure Architectural Discussion Framework - Machine Learning Solutions

Machine Learning archtitectures are designed to process data and output data to give additional insights to a user or entire organization. These insights can be stored, reported immediately, or used within an application to enhance the user experience. While the mathematics to create such a solution can be complicated, the architecture itself should adhere to the same ar cloud architectures.

Machine Learning is usually a service of an architecture. For instance, when looking at building an architecture for preventitive maintenance of machinery, machine learning is a processing service in a [Lambda Architecture](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/#lambda-architecture) or [Batch Processing Architecture](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/batch-processing).

- [FastTrack for Azure Architectural Discussion Framework - Machine Learning Solutions](#fasttrack-for-azure-architectural-discussion-framework---machine-learning-solutions)
    - [Architecture Patterns that utilize Machine Learning](#architecture-patterns)
    - [Scalability & Availability](#scalability--availability)
    - [Resiliency](#resiliency)
    - [Management & DevOps](#management--devops)
    - [Security](#security)
    - [Technology Choices](#technology-choices)

## Architecture Patterns

The following architecture patterns either have a direct reference to Machine Learning or utilize Machine Learning in them. There is a good chance that the ultimate goal for a specific architecture, may align with one of these architectures.

Other architecture patterns can utilize the Cognitive Services within them that are not listed below. If the customer is looking to utilize pre-built algorithms for text, video, or image recognition or understanding, the cognitive services should be considered. Other machine learning services.

   - [Machine Learning at Scale](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/machine-learning-at-scale)
   - [Real Time Processing](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/real-time-processing)
   - [Lambda Architecture](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/#lambda-architecture)
   - [Batch Processing](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/batch-processing)
   - [Big Data Architecture Style](https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/)

## Scalabilty & Availability

This section will consist of scalability and availability design patterns that can directly relate to projects that use machine learning. This list is not a complete list of all design patterns in this area.

   - [Availability Patterns](https://docs.microsoft.com/en-us/azure/architecture/patterns/category/availability)
       - [Health Endpoint Monitoring](https://docs.microsoft.com/en-us/azure/architecture/patterns/health-endpoint-monitoring)
       - [Queue-Based Load Leveling](https://docs.microsoft.com/en-us/azure/architecture/patterns/queue-based-load-leveling)
       - [Throttling](https://docs.microsoft.com/en-us/azure/architecture/patterns/throttling)
    - [Performance and Scalability Patterns](https://docs.microsoft.com/en-us/azure/architecture/patterns/category/performance-scalability)
        - [Index Table](https://docs.microsoft.com/en-us/azure/architecture/patterns/index-table)
        - [Materialized View](https://docs.microsoft.com/en-us/azure/architecture/patterns/materialized-view)
        - [Sharding](https://docs.microsoft.com/en-us/azure/architecture/patterns/sharding)

## Resiliency

This section will consist of resiliency design patterns that can directly relate to projects that use machine learning. This list is not a complete list of all design patterns in this area. 

   - [Resiliency Patterns](https://docs.microsoft.com/en-us/azure/architecture/patterns/category/resiliency)
       - [Bulkhead](https://docs.microsoft.com/en-us/azure/architecture/patterns/bulkhead)
       - [Queue-Based Load Leveling](https://docs.microsoft.com/en-us/azure/architecture/patterns/queue-based-load-leveling)
       - [Scheduler Agent Supervisor](https://docs.microsoft.com/en-us/azure/architecture/patterns/scheduler-agent-supervisor)

## Management & DevOps

This section will consist of Management and DevOps design patterns that can directly relate to projects that use machine learning. This list is not a complete list of all design patterns in this area.

   - [Management and Monitoring Patterns](https://docs.microsoft.com/en-us/azure/architecture/patterns/category/management-monitoring)
       - [External Configuration Store](https://docs.microsoft.com/en-us/azure/architecture/patterns/external-configuration-store)
       - [Sidecar](https://docs.microsoft.com/en-us/azure/architecture/patterns/sidecar)

## Security

This section will consist of security design patterns that can directly relate to projects that use machine learning. This list is not a complete list of all design patterns in this area.

   - [Security Patterns](https://docs.microsoft.com/en-us/azure/architecture/patterns/category/security)
       - [Federated Identity](https://docs.microsoft.com/en-us/azure/architecture/patterns/federated-identity)
       - [Gatekeeper](https://docs.microsoft.com/en-us/azure/architecture/patterns/gatekeeper)
       - [Valet Key](https://docs.microsoft.com/en-us/azure/architecture/patterns/valet-key)

## Technology Choices

These are the technologies that you would use to deploy machine learning within your architecture. There are PaaS services and IaaS deployments as well. Azure Machine Learning Studio should be highly considered for those  that do not have a data science team. It gives customers pre-built algorithms to use with their data. Most data scientists will not appreciate this type of tool as they aren't using their own algorithms and have to relinquish some control. Please keep that in mind when considering the different tools. All links go to the Azure Docs for that service.

   - Azure Machine Learning PaaS Services
       - [R Server for Azure HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/r-server/r-server-overview)
       - [Azure Databricks](https://docs.microsoft.com/en-us/azure/azure-databricks/)
       - [Azure Machine Learning Studio](https://docs.microsoft.com/en-us/azure/machine-learning/studio)
       - [Cognitive Services](https://docs.microsoft.com/en-us/azure/cognitive-services/)
       - [Azure Batch AI](https://docs.microsoft.com/en-us/azure/batch-ai/)
   - Azure Machine Learning IaaS Deployments
       - [Microsoft Machine Learning Server](https://docs.microsoft.com/en-us/machine-learning-server/)
       - [Microsoft SQL Server](https://docs.microsoft.com/sql/)