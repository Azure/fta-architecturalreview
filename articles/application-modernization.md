# FastTrack for Azure Architectural Discussion Framework - Application Modernization

- [Introduction](#introduction)

- [App Services](#app-services)
  * [App and Data Migration](#app-and-data-migration)
  * [Distributed Architecture](#distributed-architecture)
  * [High Availability, Business Continuity and Disaster Recovery](#high-availability,-business-continuity-and-disaster-recovery)
  * [Monitoring and Management](#monitoring-and-management)
  * [Performance and Scalability](#performance-and-scalability)
  * [Security](#security)
- [Service Fabric](#service-fabric)
  * [App Migration](#app-migration)  
  * [Distributed architecture](#distributed-architecture)
  * [High availability, business continuity and disaster recovery](#high-availability,-business-continuity-and-disaster-recovery)
  * [Monitor and diagnose](#monitor-and-diagnose)
  * [Performance and scalability](#performance-and-scalability)
  * [Security](#security)

- [Summary](#summary)

## Introduction
The Architectural discussion framework is a series of questions that guides discussion of application architecture for Azure. It stems from recommended patterns and practices and contain links to supporting technical documentation. This framework is adopted by various Azure teams including FastTrack for Azure while engaging with hundreds of customers across various industries. You can use these questions within your own organization, to help you plan and validate your architecture on Azure. The questions are deliberately open-ended, they are meant to facilitate discussion among the various stakeholders in your organization.

This architecture discussion can be run by anyone who is responsible for application architecture, this could be an Architect or Lead Developer. They should involve the necessary stakeholders as needed while discussing SLA (Service Level Agreements), availability requirements (including uptime), business continuity (RPO, RTO) etc. they need to involve business stakeholders and while discussing monitoring, alerting, etc. involve operations teams.


* **Have you investigated the full range of Azure compute (hosting) options and compared their features before making a decision?**

    Azure offers several compute options: Azure App Service, Azure Kubernetes Service, Azure Container Services, Azure Functions, Virtual Machines, Service Fabric (de-emphasized), Cloud Services (legacy). It is critical that you choose the right hosting model by comparing different options and select the right hosting model(s) based on your requirements. All the different services have different characteristics for maintenance, operations, resiliency, scalability, cost and performance envelope.   
    
    > [Criteria for choosing an Azure compute option](https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-comparison)
    >
    > [Azure App Service, Virtual Machines, Service Fabric, and Cloud Services comparison](https://docs.microsoft.com/en-us/azure/app-service/choose-web-site-cloud-service-vm)

# App Services

## App and data migration    

* **Are you migrating existing Web app or API Apps from Windows Server or Linux Server? Are you aware of the Azure App Service Migration Assistant tool?**

    The App Service Migration assistant tool creates a readiness report to identify any potential blocking issues which may prevent a successful migration from on-premises to Azure. If you do not feel comfortable using the tool to migrate (i.e. prefer a manual migration), then you can use the readiness report as a minimum to identify potential blocking issues.    
    
    > [Azure App Service Migration Assistant](https://appmigration.microsoft.com/)

* ****Existing App Migration**: What type of authentication is being used?**

    Web Apps support Anonymous Authentication by default and Forms Authentication where specified by an application. Windows Authentication is not supported within App Service; however Azure Active Directory can be used (optionally with ADFS) by implementing token-based Authentication (SAML- / Oauth-based), this approach can also provide a fully integrated Single Sign On Experience if required. All other forms of authentication - for example, Basic Authentication - are not currently supported.    
        
* ****Existing App Migration**: Does the application reference assemblies from the GAC (Global Assembly Cache)?**

    The GAC is not supported in Web Apps. If your application references assemblies which you usually deploy to the GAC, you will need to deploy to the application bin folder in Web Apps.    
    
* ****Existing App Migration**: Does the application make use of COM Components?**
    Web Apps do not allow the registration of COM Components on the platform. If your websites or applications make use of any COM Components, you must rewrite them and deploy them with the website or application.
    

* ****Existing App Migration**: What Port Bindings are being used?**

    Web Apps only support inbound connectivity on Port 80 for HTTP and Port 443 for HTTPS traffic, these ports are automatically exposed and load-balanced across multiple instances. The migration tool will ensure that any migrated applications are listening on these ports by default. 

* ****Existing App Migration**: Does your app call any User32/GDI32 functions directly, or registry accesses?**

    Web Apps do not support access to shared subsystems in Windows and do not support write access to any registry keys. 

* **Session State**: Does your application store session state in process on a server? 
 
    In an ideal case, you can make your application stateless in order to scale/switch at will. Where this is not feasible, use the  session state provider for Azure Redis Cache to persist your state across multiple services via a distributed cache mechanism.

## Distributed architecture    

* **Have you considered deploying your application to multiple regions?**

    Consider the rare scenario of a service outage in a region, or an entire Azure region going offline. Do you need to protect against this scenario? If so, it is necessary to deploy the application into two regions to achieve high availability with Traffic Manager at the front.

    Use Azure Traffic Manager to route your application's traffic to different regions, whilst using other services built-in features to geo-replicate storage, databases and other components.

    Consider if this level of HA is actually required, are you willing to pay for the extra expense for the extra potential uptime?

    > [Run a web application in multiple regions](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/app-service-web-app/multi-region)

* **Did you design the workload with resiliency in mind? Are you following one or more of the following common resiliency strategies?**
  * Retry Transient failures
  * Load balance across multiple instances
  * Replicate data
  * Degrade gracefully
  * Throttle high volume users
  * Use a circuit breaker
  * Use load leveling to smooth out spikes in traffic
  * Isolate critical resources
  * Apply compensating transactions
  * Testing for resiliency
  * Resilient deployment
  * Monitoring and Diagnostics

  When you design any application for a distributed environment such as public cloud services, it is important that you design for resiliency using well known strategies and design patterns.    
    
    > [Resiliency strategies](https://docs.microsoft.com/en-us/azure/architecture/resiliency/index#resiliency-strategies)

    > [Cloud Design Patterns](https://docs.microsoft.com/en-us/azure/architecture/patterns/)

## High availability, business continuity and disaster recovery

* **Do you have Availability Requirements defined for the workload? How much downtime is acceptable? (RTO) How much data loss is acceptable? (RPO)**

    It is critical that you have defined Resiliency (High Availability & Disaster Recovery) metrics like RPO/RTO/SLA. Without these metrics it will be hard to design an application and meet your end-customer expectations.    
    
    > [Defining your resiliency requirements](https://docs.microsoft.com/en-us/azure/architecture/framework/resiliency/overview#define-requirements)

* **Is there a defined SLA for the workload?**

    Microsoft provides an SLA for each of the Azure services. A customer should define their own target SLA for each workload. This makes it possible to evaluate whether the architecture meets the proposed business requirements. A customer should calculate the composite SLA (SLA of multiple Azure & other dependent services that makes up the workload) and see if that meets their business SLA requirements.    
    
    > [Understand service-level agreements (SLAs)](https://docs.microsoft.com/en-us/azure/architecture/framework/resiliency/business-metrics#understand-service-level-agreements)

* **Are there any third-party services used as part of your workload? If so, does the third-party provide an SLA?**

    If your application depends on a third-party service, but the third party provides no guarantee of availability in the form of an SLA, your application's availability also cannot be guaranteed. Your SLA is only as good as the least available component of your application.    

* **Have you performed Failure Mode Analysis (FMA)?**

    FMA is to identify possible points of failures and define how the applications will respond to those failures.    
    
    > [Failure mode analysis](https://docs.microsoft.com/en-us/azure/architecture/resiliency/failure-mode-analysis)

* **How do I know when we have a problem that will require either failover or intervention and how will I failover to a secondary implementation?**

    In the time it takes you to intervene to failover a service, your service is down – consider automatic failover, or rapid alerts to your operations team.

* **Are my backups / replicas stored in (or replicated to) a different region from my primary store?**
    In the event that you need to restore data to an alternative region, you need to ensure that your data is accessible in the event of an outage of the primary region. Consider geo Replication technologies, such as RA-GRS, Azure Backup, Azure SQL Database Active Geo-Replication / Geo Restore, or Azure CosmosDB.

* **Do I deploy a HA or DR copy of my service in an Active-Active vs. Active-Passive design?**
    Active-Active architectures reduce the amount of compute resource wasted and sitting idle when compared to Active-Passive, which are less complex to implement and create lower network egress charges.
    
    > [Disaster Recovery](https://docs.microsoft.com/en-us/azure/architecture/framework/resiliency/backup-and-recovery)

    > [High Availability](https://docs.microsoft.com/en-us/azure/architecture/resiliency/high-availability-azure-applications)


* **Have you implemented async operations whenever possible?**

  Though arguably simpler to implement, synchronous operations monopolize and hold open precious resources and block other operations while the caller waits for the process to complete. Design each part of your application to allow for asynchronous operations whenever possible to get the most out of your precious compute and connection resources.
    
  > [Asynchronous programming](https://docs.microsoft.com/en-us/dotnet/articles/csharp/async)

* **Use client classes and connection managers as intended**

  Complex classes such as connection managers and client classes are usually designed to reuse connections and ports effectively to minimize network roundtrips and possible SNAT exhaustion issues. Even in a fully managed environment there are limits to the number of open connections you can have at once! Reuse is always better than individual, atomic TCP connections for each request. Reuse results in more performant, very efficient TCP transactions. 
    
  > [App Service Sandbox Limitations](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)


## Monitoring and Management

* **Is there a strategy in place to monitor the application?**

    Performance issues in your cloud app can impact your business. With multiple interconnected components and frequent releases, degradations can happen at any time. And if you’re developing an app, your users usually discover issues that you didn’t find in testing. You should know about these issues immediately and have tools for diagnosing and fixing the problems. Azure has a range of tools for identifying these problems.
    
    * Azure Monitor
    * Application Insights
    * Log Analytics
    * Third Party Solution

    > [Monitoring Azure applications and resources](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview)

* **Are you aware of App Service's built in monitoring capabilities?**

    App Service provides built in monitoring functionality in the Azure Portal. This includes the ability to review quotas and metrics for an app as well as the App Service plan, setting up alerts and even scaling automatically based on these metrics    
    
    > [How to: Monitor Apps in Azure App Service](https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)

* **Have you configured and tested health probes for Load Balancers &amp; Traffic Manager?**

    Ensure that your health logic checks the critical parts of the system and responds appropriately to health probes.
    
    The health probes for  [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-overview/) and  [Azure Load Balancer](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview/) serve a specific function. For Traffic Manager, the health probe determines whether to fail over to another region. For a load balancer, it determines whether to remove a VM from rotation.
    
    For a Traffic Manager probe, your health endpoint should check any critical dependencies that are deployed within the same region, and whose failure should trigger a failover to another region.
    
    For a load balancer, the health endpoint should report the health of the VM. Don't include other tiers or external services. Otherwise, a failure that occurs outside the VM will cause the load balancer to remove the VM from rotation.
    
    > [Health Endpoint Monitoring Pattern](https://msdn.microsoft.com/library/dn589789.aspx)

* **Does the workload have any dependencies on third-party services? If so, is there a way to monitor and view diagnostics information of those services?**

    If your application has dependencies on third-party services, identify where and how these third-party services can fail and what effect those failures will have on your application. A third-party service may not include monitoring and diagnostics, so it's important to log your invocations of them and correlate them with your application's health and diagnostic logging using a unique identifier. For more information on proven practices for monitoring and diagnostics.
    
    > [Monitoring and Diagnostics guidance](https://docs.microsoft.com/en-us/azure/architecture/best-practices/monitoring)

* **Are you aware that you can setup various alerts based on App Service plan metrics and Application Insights metrics?**

    The benefits of alerts are that you can proactively get notified when certain conditions are met, for example a metric alert such as CPU or memory exceeding a certain limit. Activity Log alerts notify when a new Service Health incident occurs, or a user performs a given event.    
    
    > [Various alerts in Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-alerts)

* **Have you investigated various general best practices for monitoring and alerting in your application?**

    Without appropriate monitoring, diagnostics, and alerting, there is no way to detect failures in your application and alert an operator to fix the underlying issues.
    
    > [Monitoring and Diagnostics guidance](https://docs.microsoft.com/en-us/azure/architecture/best-practices/monitoring)

## Performance and scalability

* **Is your application architected to be scalable? Can individual components of the application, i.e. your web app, API and database be scaled independently?**

    A recommended practice is to enable the Web tier, App tier and DB tier to scale independently of each other using different App Service Plans. Refer to the associated link on how to accomplish this.
    
    > [Improve scalability in a web application](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/app-service-web-app/scalable-web-app)

* **Is your application configured to auto scale as the load increases?**

    If your application is not configured to scale out automatically as load increases, it is possible that your application's services will fail if they become saturated with user requests.
    
    > [Scalability checklist](https://docs.microsoft.com/en-us/azure/architecture/checklist/scalability)
    >
    > [Azure App Service: Scale instance count manually or automatically](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/insights-how-to-scale/)
    >
    > [Autoscale best practices](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/insights-autoscale-best-practices)

* **Have you performed or considered performing load test of your APP?**

    Your application is only as scalable as your weakest link. Your Application's SLA is as strong as the performance of the underlying code, this should be baselined and measured prior to deployment. 

    Additionally, consider regular load tests as part of your application development. At a minimum, consider this prior to pushing a new build into production to validate acceptable levels of performance.

    
    > [Run URL-based load tests with VSTS](https://docs.microsoft.com/en-us/vsts/load-test/get-started-simple-cloud-load-test?view=vsts)

## Security    

* **Have you looked into Azure App Service Security best practices?**

    Security in Azure App Service has two levels:
    
    * Infrastructure and platform security - You trust Azure to have the services you need to run things securely in the cloud.
    
    * Application security - You need to design the app itself securely. This includes how you integrate with Azure Active Directory, how you manage certificates, and how you make sure that you can securely talk to different services.

    
    While Azure is responsible for securing the underlying infrastructure and platform that your application runs on, it is your responsibility to secure your application yourself. In other words, you need to develop, deploy, and manage your application code and content in a secure way. Without this, your application code or content can still be vulnerable to threats such as:

    * SQL Injection
    * Session hijacking
    * Cross-site-scripting
    * Application-level MITM
    * Application-level DDoS
    
    > [Secure an app in Azure App Service](https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-security?toc=%2fazure%2fapp-service-mobile%2ftoc.json)

* **Have you performed penetration testing on your app?**

    One of the easiest ways to get started with testing for vulnerabilities on your App Service app is to use the [integration with Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) to perform one-click vulnerability scanning on your app. You can view the test results in an easy-to-understand report and learn how to fix each vulnerability with step-by-step instructions. Its recommended that you perform your own pen testing on your applications, because when you enhance the security of your applications, you help make the entire Azure ecosystem more secure. Microsoft no longer requires pre-approval to conduct a penetration tests against Azure resources
    
    > [Web Vulnerability Scanning for Azure App Service powered by Tinfoil Security](https://azure.microsoft.com/en-us/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)
    >
    > [Pen Testing on Azure](https://docs.microsoft.com/en-us/azure/security/azure-security-pen-testing)

* **In terms of Secure communications, are you aware that you can immediately use HTTPS with App Services?**

    If you use the **\*.azurewebsites.net** domain name created for your App Service app, you can immediately use HTTPS, as an SSL certificate is provided for all **\*.azurewebsites.net**  domain names. If your site uses a [custom domain name](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-tutorial-custom-domain), you can upload an SSL certificate to [enable HTTPS](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-tutorial-custom-ssl) for the custom domain. Enabling [HTTPS](https://en.wikipedia.org/wiki/HTTPS) can help protect against MITM attacks on the communication between your app and its users    
    
    > [Enable HTTPS for custom domain](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-tutorial-custom-ssl)
    >
    > [Enforce HTTPS](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-tutorial-custom-ssl#enforce-https)

* **Are you aware of App Service Authentication / Authorization feature that provides a way for your application to sign in users without changing code?**

    App Service Authentication / Authorization is a feature that provides a way for your application to sign in users so that you don't have to change code on the app backend. It provides an easy way to protect your application and work with per-user data. App Service uses federated identity, in which a third-party identity provider stores accounts and authenticates users. App Service supports five identity providers out of the box:<ul><li>Azure Active Directory</li><li>Facebook</li><li>Google</li><li>Microsoft Account</li><li>Twitter</li></ul>    
    
    > [Authentication and authorization in Azure App Service](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview)

* **Does the App Service need to authenticate with an on-premises Active Directory?**

    If your company policy prohibits AD data from being stored in Azure, you can leverage an on-premises secure token service (STS) like Active Directory Federation Service (AD FS) or pass through authentication. 

    Note: If you do this, ensure that your ADFS service is considered in your dependency graph and Failure Mode Analysis for your application, as then your on-premises AD infrastructure becomes a downstream application dependency.

    > [Integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnect)
    
    > [Failure mode analysis](https://docs.microsoft.com/en-us/azure/architecture/resiliency/failure-mode-analysis)


# Service Fabric  
 
## App Migration
* **Are you looking to migrate a solution built in Cloud Services Web and Worker Roles to Service Fabric?**

    For Application Migration, you can learn about the differences between Cloud Services and Service Fabric before migrating your applications. You also have the option to convert Web and Worker roles to Service Fabric stateless services. If you are still evaluating which platform to use, consider App Services as well.

    > [Guide to converting Web and Worker Roles to Service Fabric stateless services](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cloud-services-migration-worker-role-stateless-service)

    > [Learn about the differences between Cloud Services and Service Fabric before migrating applications](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cloud-services-migration-differences)

* **Are you considering containerizing your application?**
    One of the most common scenarios supported by Service Fabric is to containerize your existing applications and orchestrate the containerized applications on Service Fabric.  However, Azure also supports other container orchestrators.  There's a lot involved in the decision of what orchestrator to use; it's an important architectural decision.

    >[Service Fabric and containers](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-containers-overview)
    
    >[Azure Kubernetes Services](https://azure.microsoft.com/en-us/services/kubernetes-service/)
    
    >[Azure Red Hat OpenShift](https://azure.microsoft.com/en-us/services/openshift/)
    
    >[VMware Tanzu (formerly Pivotal Cloud Foundary)](https://azure.microsoft.com/en-us/overview/linux-on-azure/pivotal/)

## Distributed architecture
* **Are you aware of microservices architecture style and best practices?**

    A microservices architecture consists of a collection of small, autonomous services. Each service is self-contained and should implement a single business capability. Consider the amount of services that are implemented; do you need 1000 services, when in reality you could deploy only 5?

    > [Microservices architecture style](https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices)

## High availability and business continuity / disaster recovery
* **Have you considered mitigations and actions to take if a disaster happens?**

    There is guidance available for hardware and software faults and the availability of Service Fabric Clusters
    > [Disaster recovery in Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-disaster-recovery)

* **Are you thinking of the Service Fabric platform for microservices or a development platform in general?**

    You can use the platform if you want to host any exe and utilize the offered High Availability aspect. Service Fabric ensures that instances of an application are running. Be aware that Geo-Replication of the Service Fabric Cluster is not yet supported. You can back up any data on the compute to a BLOB and restore that in case of such a disaster. More information on Azure Storage and BLOB storage can be found here.
    
    > [Deploy a guest executable to Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-deploy-existing-app)


## Monitor and diagnose

* **Have you considered your monitoring and diagnostics strategy? What are you currently using for logging?**

    Monitoring and diagnostics are critical to developing, testing, and deploying applications and services in any environment. Service Fabric solutions work best when you plan and implement monitoring and diagnostics that help ensure applications and services are working as expected in a local development environment or in production. If you are already using OMS and Splunk, you may keep using those. From the application level, one can leverage Application Insights. 

    > [Service Fabric diagnostics overview](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-diagnostics-overview)

* **Are you familiar with the Service Fabric Health Model?**

    Azure Service Fabric introduces a health model that provides rich, flexible, and extensible health evaluation and reporting. The model allows near-real-time monitoring of the state of the cluster and the services running in it. You can easily obtain health information and correct potential issues before they cascade and cause massive outages. In the typical model, services send reports based on their local views, and that information is aggregated to provide an overall cluster-level view.

    > [Service Fabric health introduction](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction)
    
    > [Use system health reports to troubleshoot](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-understand-and-troubleshoot-with-system-health-reports)


* **Are you aware of Application Insights support for Microservices and Containers?**

    Azure Application Insights is an extensible platform for application monitoring and diagnostics. It includes a powerful analytics and querying tool, customizable dashboard and visualizations, and further options including automated alerting. It is the recommended platform for monitoring and diagnostics for Service Fabric applications and services. A single Application Insights resource can be used for all the components of your application. The health of the services and the relationships between them are displayed on a single Application Map. You can trace individual operations through multiple services with automatic HTTP correlation.

    > [Event analysis and visualization with Application Insights](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights)
    
    > [Application Insights support for Microservices and Containers](https://azure.microsoft.com/en-us/blog/app-insights-microservices/)

## Performance and scalability

* **Are you familiar with the Service Fabric application lifecycle?**

    As with other platforms, an application on Azure Service Fabric usually goes through the following phases: design, development, testing, deployment, upgrading, maintenance, and removal. Service Fabric provides first-class support for the full application lifecycle of cloud applications, from development through deployment, daily management, and maintenance to eventual decommissioning. During each lifecycle phase, the code and the config go through being compiled, published, deployed.

    > [Service Fabric application lifecycle](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-lifecycle)

    > [Model an application in Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-model)

* **Have you given thought to how you would scale stateful services and stateless services? Have you decided how you would partition data, and select partition scheme for stateful services?**

    Defining partition scheme and number of partitions for stateful services upfront is very important. Number of partitions defined cannot be changed later. In general, you must have a good reason to use stateful services. You want data to be persisted to an external store (Azure SQL DB, Cosmos DB, etc.). If you do use stateful services, then do not put data in the stateful service that you cannot afford to lose.

    > [Scaling in Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-concepts-scalability)

    > [Partition Service Fabric reliable services](https://azure.microsoft.com/en-us/documentation/articles/service-fabric-concepts-partitioning/)

* **Are you going to manually scale the cluster or use auto-scale?**

    Virtual machine scale sets are an Azure compute resource that you can use to deploy and manage a collection of virtual machines as a set. Every node type that is defined in a Service Fabric cluster is set up as a separate Virtual Machine scale set. With scaling you are trying to achieve the right balance with cost vs availability. Try to use calendar-based auto scale rather than reactive. Do not turn on auto-scale unless Monitoring is on. Generally, scale up aggressively and scale down conservatively.

    > [Scale a Service Fabric cluster in or out using auto-scale rules](https://azure.microsoft.com/en-us/documentation/articles/service-fabric-cluster-scale-up-down/)
    
    > [Overview of autoscale with Azure virtual machine scale sets](https://azure.microsoft.com/en-us/documentation/articles/virtual-machine-scale-sets-autoscale-overview/)

* **Have you created secure clusters to deploy your workloads?**

    When deploying workloads, it is recommended that you deploy them on secure Service Fabric Clusters. Please put all the certificates for the cluster in KeyVault. Please do NOT lose these keys.

    > [Create a Service Fabric cluster in Azure using the Azure portal](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal)

    > [Create a secure cluster in Azure by using PowerShell](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-tutorial-create-cluster-azure-ps)

    > [Connect to a secure cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-connect-to-secure-cluster)

* **Have you considered securing applications running under different user accounts?**

    By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts

    > [Configure security policies for your application](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-runas-security)

* **Have you evaluated Linux Clusters and Java Development?**
    
    Service Fabric is currently available as a public preview on Linux, enabling you to build, deploy, and manage highly available, highly scalable applications in that environment just as you would on Windows. In addition, the high-level Service Fabric frameworks (Reliable Services and Reliable Actors) can now be built in Java.

    > [Create Service Fabric clusters on Windows Server or Linux](https://azure.microsoft.com/en-us/documentation/articles/service-fabric-linux-overview/)

* **Have you had conversations as a team around cluster capacity planning?**

    Capacity planning for Clusters is important from finding the right balance needed between cluster resources needed to run your workload and the managing costs. There are tools and resources available to help you with this.

    > [Capacity planning for Service Fabric applications](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-capacity-planning)

* **Are you looking at the Service Fabric Platform for future implementations or are you already deployed on the platform with your applications? What programming models are you considering using to build your applications in Service Fabric?**

    Service Fabric offers multiple ways to write and manage your services. It is important to decide on which programming model your teams will be using. Be aware of guidelines on when to use Actors and when to use Reliable Services.

    > [Service Fabric programming model overview](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-choose-framework)

    > [Introduction to Service Fabric Reliable Actors](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-actors-introduction)

    > [When to use Reliable Services APIs](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-introduction#when-to-use-reliable-services-apis)

* **Have you considered Azure API Management as a frontend gateway to your Service Fabric Application?**

    Cloud applications typically need a front-end gateway to provide a single point of ingress for users, devices, or other applications. In Service Fabric, a gateway can be any stateless service such as an [ASP.NET Core application](https://docs.microsoft.com/en-us/aspnet/core/), or another service designed for traffic ingress, such as [Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-what-is-event-hubs), [IoT Hub ][6], or [Azure API Management ][7]. For Event Hubs, be aware of the limits on the number of events that can be ingested.  The key here is going to need a front door, this is one suggestion. The Key here is that you **Must have a Front Door: There are a few options here**  **Traffic Pattern**  **Technology Selection**    
    
    > [Service Fabric with Azure API Management overview](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-api-management-overview)

* **Are you aware of Service Fabric team blog and Service Fabric customer profiles?**

    The Service Fabric Team Blog is a good resource to keep up with latest Service Fabric announcements. There are also case studies published by customers on how they leveraged Azure and Service Fabric.
    
    > [Azure Service Fabric Team Blog](https://blogs.msdn.microsoft.com/azureservicefabric/)
    
    > [Azure Service Fabric Team Blog: Customer profile](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)


## Security    

* **Have you considered security aspects around microservices?**

    The same Application Security Rules can be applied to an application developed on Service Fabric Platform. You can apply standard SDL best practices.    
    
    > [Microservices security](https://www.mulesoft.com/resources/api/microservices-security)

* **Are you wondering about application security for applications running on Service Fabric?**

    This is no different than implementing security using AD for example, for any other regular application. The guidance on using AD is the same. Did you know that you can implement the same infrastructure level security to a Service Fabric Cluster as you would to any server farm?  
    
    > [Secure a standalone cluster on Windows by using Windows security](https://azure.microsoft.com/en-us/documentation/articles/service-fabric-windows-cluster-windows-security/)

* **Have you considered securing applications running under different user accounts?**

    By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts    
    
    > [Configure security policies for your application](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-runas-security)

## Summary 
When customers move to Azure, generally there is a misconception that Azure will automatically take care of  highly availability, disaster recovery, etc. The intent of the Architectural discussion framework is to guide you to build highly available, resilient, scalable & secure applications.
