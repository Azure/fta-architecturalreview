# FastTrack for Azure Architectural Discussion Framework - Application Modernisation

- [FastTrack for Azure Architectural Discussion Framework - Application Modernisation](#fasttrack-for-azure-architectural-discussion-framework---application-modernisation)
- [App Services](#app-services)
  * [App &amp; Data Migration](#app--amp--data-migration)
  * [Distributed Architecture](#distributed-architecture)
  * [High Availability and Business Continuity / Disaster Recovery](#high-availability-and-business-continuity---disaster-recovery)
  * [Monitoring &amp; Management](#monitoring--amp--management)
  * [Performance &amp; Scalability](#performance--amp--scalability)
  * [Security](#security)
- [Service Fabric](#service-fabric)
  * [Build Applications and Services](#build-applications-and-services)
  * [ ](#-nbsp-)
  * [Manage Applications (Performance and Scalability)](#manage-applications--performance-and-scalability-)
  * [Create and manage Clusters](#create-and-manage-clusters)
  * [Monitor and Diagnose](#monitor-and-diagnose)
  * [App Migration](#app-migration)
  * [Distributed Architecture](#distributed-architecture-1)
  * [High Availability and Business Continuity / Disaster Recovery](#high-availability-and-business-continuity---disaster-recovery-1)
  * [Security](#security-1)


| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Have you looked into the range of Azure compute (hosting) options and compared their features before making a decision?| Azure offers several compute options: Azure App Service, Service Fabric, Azure Container Service, Azure Functions, Virtual Machine, Cloud Service (legacy). It is critical that you chooses right hosting model by comparing various options and select the right hosting model(s) based on your requirements.| [https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-comparison ][1]<br>[https://docs.microsoft.com/en-us/azure/app-service-web/choose-web-site-cloud-service-vm#onprem ][3]   |  

# App Services

## App &amp; Data Migration    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Are you migrating existing Web app or API Apps from Windows Server or Linux Server? Are you aware of Azure App Service Migration Assistant tool?| The App Service Migration assistant tool creates a readiness report to identify any potential blocking issues which may prevent a successful migration from on-premises to Azure. If you do not feel comfortable using the tool to migrate (i.e. prefer a manual migration), then you can use the readiness report as a minimum to identify potential blocking issues.| [https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-migration-from-iis-server ][6]  |  
| **Existing App Migration**: What type of authentication being used?| Web Apps supports Anonymous Authentication by default and Forms Authentication where specified by an application. Windows Authentication can be used by integrating with Azure Active Directory and ADFS only. All other forms of authentication - for example, Basic Authentication - are not currently supported.   | [https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-migration-from-iis-server][6]  |  
| **Existing App Migration**: Does the application references assemblies from the GAC (Global Assembly Cache)?| The GAC is not supported in Web Apps. If your application references assemblies which you usually deploy to the GAC, you will need to deploy to the application bin folder in Web Apps.   | [https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-migration-from-iis-server][6]  |  
| **Existing App Migration**: Does the application makes use of COM Components?| Web Apps does not allow the registration of COM Components on the platform. If your websites or applications make use of any COM Components, you must rewrite them in managed code and deploy them with the website or application.  | [https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-migration-from-iis-server][6]  |  
| **Existing App Migration**: What Port Bindings are being used?| Web Apps only supports Port 80 for HTTP and Port 443 for HTTPS traffic. Different port configurations will be ignored and traffic will be routed to 80 or 443.| [https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-migration-from-iis-server][6]  |  
## Distributed Architecture    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Have you considered deploying your application to multiple regions?| Consider the rare scenario a service outage in a region, or an entire Azure region going offline. Do you need to prevent against this scenario? If so, it is necessary to deploy the application to two regions to achieve high availability with Traffic Manager at the front.<br><br>Use Azure Traffic Manager to route your application's traffic to different regions, Replicate Storage, Database and other components   Does the business demand this?| Use the Reference Architecture best practices to  [Run a web application in multiple regions][7]      |  
| Did you design the workload with Resiliency in mind? Are you following one or more of the following common Resiliency Strategies?<ulk><li>Retry Transient failures</li><li>Load balance across multiple instances</li><li>Replicate data</li><li>Degrade gracefully</li><li>Throttle high volume users</li><li>Use a circuit breaker</li><li>Use load leveling to smooth out spikes in traffic</li><li>Isolate critical resources</li><li>Apply compensating transactions</li><li>Testing for resiliency</li><li>Resilient deployment</li><li>Monitoring and Diagnostics</li></ul>| When you designing their application for a distributed environment like cloud, It is important that you design for resiliency using well known resiliency strategies.| Resiliency strategies:  [https://docs.microsoft.com/en-us/azure/architecture/resiliency/index#resiliency-strategies][8]   |  
|  |  |    |  

## High Availability and Business Continuity / Disaster Recovery    

| **Question**| **Purpose**| **Relevant Documentation**    |  
|---|---|---|  
| Do you have Availability Requirements defined for the workload? How much downtime acceptable? (RTO)  How much data loss is acceptable?(RPO)| It is critical that we have defined Resiliency (High Availability &amp; Disaster Recovery) metrics like RPO/RTO/SLA. Without these metrics it will be hard to design an application and meet your end-customer expectations.| Designing resilient applications for Azure:<br>[https://docs.microsoft.com/en-us/azure/architecture/resiliency/index#defining-your-resiliency-requirements][9]   |  
| Is there a defined SLA for the workload?| Microsoft provides SLA for each of the Azure service. Customer should define their own target SLA for each workload. An SLA makes it possible to evaluate whether the architecture meets the business requirements.  Customer should calculate Composite SLA (SLA of multiple Azure &amp; other dependent services that makes up the workload) and see if that meets their business SLA requirements| Defining Resiliency Requirements: <ve>[https://docs.microsoft.com/en-us/azure/architecture/resiliency/index#defining-your-resiliency-requirements][9]   |  
| Is there any third-party services used part of your workload? If so does the third-party provide SLA?| If your application depends on a third-party service, but the third party provides no guarantee of availability in the form of an SLA, your application's availability also cannot be guaranteed. Your SLA is only as good as the least available component of your application.  |    |  
| Have you performed Failure Mode Analysis (FMA)?| FMA is to identify possible points of failures and define how the applications will respond to those failures.| Failure Mode Analysis [https://docs.microsoft.com/en-us/azure/architecture/resiliency/failure-mode-analysis][10]   |  
| Did you design the workload with Resiliency in mind? Are you following one or more of the following common Resiliency Strategies?<ul><li>Retry Transient failures</li><li>Load balance across multiple instances</li><li>Replicate data</li><li>Degrade gracefully</li><li>Throttle high volume users</li><li>Use a circuit breaker</li><li>Use load leveling to smooth out spikes in traffic</li><li>Isolate critical resources</li><li>Apply compensating transactions</li><li>Testing for resiliency</li><li>Resilient deployment</li><li>Monitoring and Diagnostics</li></ul>|The cloud is built for scale, which means you may encounter transient faults or failures across your underlying application infrastructure.<br><br>When you design your application for a distributed environment, it is  important to design for resiliency using well known resiliency strategies.| Resiliency strategies:  [https://docs.microsoft.com/en-us/azure/architecture/resiliency/index#resiliency-strategies][8]   |  
| Have you implemented Async operation whenever possible?| Synchronous operations can monopolize resources and block other operations while the caller waits for the process to complete. Design each part of your application to allow for asynchronous operations whenever possible| For more information on how to implement asynchronous programming in C#, see [Asynchronous Programming with async and await][11]  |  

## Monitoring &amp; Management    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Is there a strategy in place to Monitor the application?| Performance issues in your cloud app can impact your business. With multiple interconnected components and frequent releases, degradations can happen at any time. And if you’re developing an app, your users usually discover issues that you didn’t find in testing. You should know about these issues immediately, and have tools for diagnosing and fixing the problems. Azure has a range of tools for identifying these problems.<ul><li>Azure Monitor</li><li>Application Insights</li><li>Log Analytics</li><li>Third Party Solution</li></ul>| [Overview of Monitoring in Microsoft Azure][12] |  
| Are you aware of App Service built in monitoring capabilities?| App Service provides built in monitoring functionality in the Azure Portal. This includes the ability to review quotas and metrics for an app as well as the App Service plan, setting up alerts and even scaling automatically based on these metrics  | [How to: Monitor Apps in Azure App Service][13]  |  
| Have you configured and tested health probes for Load Balancers &amp; Traffic Manager?|Ensure that your health logic checks the critical parts of the system and responds appropriately to health probes.<ol><li>The health probes for  [Azure Traffic Manager][14] and  [Azure Load Balancer ][15] serve a specific function. For Traffic Manager, the health probe determines whether to fail over to another region. For a load balancer, it determines whetherto remove a VM from rotation.</li><li>For a Traffic Manager probe, your health endpoint should check any critical dependencies that are deployed within the same region, and whose failure should trigger a failover to another region.</li><li>For a load balancer, the health endpoint should report the health of the VM. Don't include other tiers or external services. Otherwise, a failure that occurs outside the VM will cause the load balancer to remove the VM from rotation.</li></ol>| For guidance on implementing health monitoring in your application, see  [Health Endpoint Monitoring Pattern][16]  |  
| Does the workload have any dependencies on third-party services? If so is there a way to monitor and view diagnostics information of those services?| If your application has dependencies on third-party services, identify where and how these third-party services can fail and what effect those failures will have on your application. A third-party service may not include monitoring and diagnostics, so it's important to log your invocations of them and correlate them with your application's health and diagnostic logging using a unique identifier. For more information on proven practices for monitoring and diagnostics  | [Monitoring and Diagnostics guidance ][17]    |  
| Are you aware that you can setup various alerts based on App Service plan metrics and Application Insights metrics?  | The benefits of alerts is that you can proactively get notified whewhenre certain conditions are met, for example a metric alerty such as CPU or Memory exceeding a certain limit. Activity Log alerts notifies when a new Service Health incident occurs or a user performs a given event.  | [Various alerts in Azure][18]  |     
 Have you looked into various general best practices for monitoring and alerting in your application?| Without appropriate monitoring, diagnostics, and alerting, there is no way to detect failures in your application and alert an operator to fix the underlying issues.| [Monitoring and Diagnostics guidance ][17]    |  

## Performance &amp; Scalability    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Is your application architected to be scalable? Can individual components of the application, i.e. your web app, API and database be scaled independently?| A recommended practice is to enable the Web tier, App tier and DB tier to scale independently of each other using different App Service Plans. Refer to the associated link on how to accomplish this.  | [Improve scalability in a web application ][19]    |  
| Is your application configured to auto scale as the load increases?| If your application is not configured to scale out automatically as load increases, it is possible that your application's services will fail if they become saturated with user requests|<ul><li>General:  [Scalability checklist ][20]</li><li>Azure App Service:  [Scale instance count manually or automatically ][21]</li><li>[Autoscale Best Practices ][22]</li></ul>|  
| Have you performed or considered performing load test of your APP?| Your application is only as scalable as your weakest link. Your Application's SLA is as strong as the performance of the underlying code.<br><br>Additionally, consider regular load tests as part of your application development. At a minimum, consider this prior to pushing a new build into production to validate acceptable levels of performance.| Add and Remove Capacity for Web/App, Data tier scaled independently<br>[https://docs.microsoft.com/en-us/vsts/load-test/get-started-simple-cloud-load-test](https://docs.microsoft.com/en-us/vsts/load-test/get-started-simple-cloud-load-test)  |  

## Security    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Have you looked in to Azure App Service Security Best practices?| Security in Azure App Service has two levels:<ul><li>Infrastructure and platform security - You trust Azure to have the services you need to actually run things securely in the cloud.</li><li>Application security - You need to design the app itself securely. This includes how you integrate with Azure Active Directory, how you manage certificates, and how you make sure that you can securely talk to different services</li></ul><br>While Azure is responsible for securing the underlying infrastructure and platform that your application runs on, it is your responsibility to secure your application itself. In other words, you need to develop, deploy, and manage your application code and content in a secure way. Without this, your application code or content can still be vulnerable to threats such as:<ol><li>SQL Injection</li><li>Session hijacking</li><li>Cross-site-scripting</li><li>Application-level MITM</li><li>Application-level DDoS</li></ol>| [Secure an app in Azure App Service][23]  |  
| Have you performed Penetration testing on your app?| One of the easiest ways to get started with testing for vulnerabilities on your App Service app is to use the [integration with Tinfoil Security][24] to perform one-click vulnerability scanning on your app. You can view the test results in an easy-to-understand report, and learn how to fix each vulnerability with step-by-step instructions.    If you prefer to perform your own penetration tests or want to use another scanner suite or provider, you must follow the [Azure penetration testing approval process][25] and obtain prior approval to perform the desired penetration tests       | [Web Vulnerability Scanning for Azure App Service powered by Tinfoil Security][26]<br>[Pen Testing on Azure](https://docs.microsoft.com/en-us/azure/security/azure-security-pen-testing)  |  
| In terms of Secure communications, are you aware that you can immediately use HTTPS with App Services?| If you use the ***.azurewebsites.net**  domain name created for your App Service app, you can immediately use HTTPS, as an SSL certificate is provided for all ***.azurewebsites.net**  domain names. If your site uses a [custom domain name][27], you can upload an SSL certificate to [enable HTTPS][28] for the custom domain.    Enabling [HTTPS][29] can help protect against MITM attacks on the communication between your app and its users       | [Enable HTTPS for custom domain][28]   [Enforce HTTPS][30]  |  
| Are you aware of App Service Authentication / Authorization feature that provides a way for your application to sign in users without changing code?| App Service Authentication / Authorization is a feature that provides a way for your application to sign in users so that you don't have to change code on the app backend. It provides an easy way to protect your application and work with per-user data. App Service uses federated identity, in which a third-party identity provider stores accounts and authenticates users. App Service supports five identity providers out of the box:<ul><li>Azure Active Directory</li><li>Facebook</li><li>Google</li><li>Microsoft Account</li><li>Twitter</li></ul>| [Authentication and authorization in Azure App Service][31]  |  
| Does the App Service need to authenticate with an on-premises Active Directory?| If your company policy prohibits AD data from being stored in Azure, you can leverage an on-premises secure token service (STS) like Active Directory Federation Service (AD FS)| [Authenticate with on-premises Active Directory in your Azure app][32]  | 

# Service Fabric  
 
## Build Applications and Services    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Are you looking at Service Fabric Platform from for future implementation or are you already deployed on the platform with your applications? What programming models are you considering to build your applications in Service Fabric?| Service Fabric offers multiple ways to write and manage your services. It is important to decide on which programming model your teams will be using.   Be aware of guidelines on when to use Actors and when to use Reliable Services.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-choose-framework ][1]<br>[https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-actors-introduction ][2]<br>[https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-introduction#when-to-use-reliable-services-apis ][3]  |  
| Have you considered Azure API Management as a front end gateway to your Service Fabric Application?| Cloud applications typically need a front-end gateway to provide a single point of ingress for users, devices, or other applications. In Service Fabric, a gateway can be any stateless service such as an [ASP.NET Core application](https://docs.microsoft.com/en-us/aspnet/core/), or another service designed for traffic ingress, such as [Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-what-is-event-hubs), [IoT Hub ][6], or [Azure API Management ][7]. For Event Hubs, be aware of the limits on the number of events that can be ingested.  The key here is going to need a front door, this is one suggestion. The Key here is that you **Must have a Front Door: There are a few options here**  **Traffic Pattern**  **Technology Selection**     | [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-api-management-overview ][8]  |  
| Are you aware of Service Fabric Team Blog and Service Fabric Customer Profiles?| The Service Fabric Team Blog is a good resource to keep up with latest Service Fabric announcements.   There are also case studies published by customers on how they leveraged Azure and Service Fabric.| [https://blogs.msdn.microsoft.com/azureservicefabric/][9]<br>[https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/][10]  |  

## Manage Applications (Performance and Scalability)    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Are you familiar with the Service Fabric application lifecycle?| As with other platforms, an application on Azure Service Fabric usually goes through the following phases: design, development, testing, deployment, upgrading, maintenance, and removal. Service Fabric provides first-class support for the full application lifecycle of cloud applications, from development through deployment, daily management, and maintenance to eventual decommissioning.   During each lifecycle phase, the code and the config go through being compiled, published, deployed.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-lifecycle ][11]<br> [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-model ][12]    |  
| Have you given thought to how you would scale Stateful Services and Stateless Services? Have you decided how you would partition data, and select partition scheme for Stateful services?| Defining partition scheme and number of partitions for Stateful services upfront is very important. Number of partitions defined cannot be changed later.   In general, you must have a good reason to use statfeul services. You want data to be persisted to an external store (Azure SQL DB, Document DB, etc.). If you do use stateful services, then do not put data in the stateful service that you cannot afford to lose.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-concepts-scalability ][13]<br>[https://azure.microsoft.com/en-us/documentation/articles/service-fabric-concepts-partitioning/][14]  |  
| Are you going to manually scale the cluster or use auto-scale?| Virtual machine scale sets are an Azure compute resource that you can use to deploy and manage a collection of virtual machines as a set. Every node type that is defined in a Service Fabric cluster is set up as a separate Virtual Machine scale set.   With scaling you are trying to achieve the right balance with cost vs availability.   Try to use calendar based auto scale rather than reactive. Do not turn on auto-scale unless Monitoring is on. Generally, scale up aggressively and scale down conservatively.| [https://azure.microsoft.com/en-us/documentation/articles/service-fabric-cluster-scale-up-down/][15]<br>[https://azure.microsoft.com/en-us/documentation/articles/virtual-machine-scale-sets-autoscale-overview/][16]  |  
   
## Create and manage Clusters    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Have you created secure clusters to deploy your workloads?| When deploying workloads, it is recommended that you deploy them on secure Service Fabric Clusters. Please put all the certificates for the cluster in KeyVault. Please do **NOT** lose these keys.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal ][17]<br>[https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-tutorial-create-cluster-azure-ps ][18]<br>[https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-connect-to-secure-cluster][19]  |  
| Have you considered securing applications running under different user accounts?| By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-runas-security][20]  |  
| Have you evaluated Linux Clusters and Java Development?| Service Fabric is currently available as a public preview on Linux, enabling you to build, deploy, and manage highly available, highly scalable applications in that environment just as you would on Windows. In addition, the high-level Service Fabric frameworks (Reliable Services and Reliable Actors) can now be built in Java.| [https://azure.microsoft.com/en-us/documentation/articles/service-fabric-linux-overview/][21]  |  
| Have you had conversations as a team around cluster capacity planning?| Capacity planning for Clusters is important from finding the right balance needed between cluster resources needed to run your workload and the managing costs. There are tools and resources available to help you with this.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-capacity-planning][22]  |

## Monitor and Diagnose    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Have you considered your monitoring and diagnostics strategy? What are you currently using for logging| Monitoring and diagnostics are critical to developing, testing, and deploying applications and services in any environment. Service Fabric solutions work best when you plan and implement monitoring and diagnostics that help ensure applications and services are working as expected in a local development environment or in production.   If you are already using OMS and Splunk, keep using those. LogAnalytics and New Relic are other options.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-diagnostics-overview][23]       |  
| Are you familiar with the Service Fabric Health Model?| Azure Service Fabric introduces a health model that provides rich, flexible, and extensible health evaluation and reporting. The model allows near-real-time monitoring of the state of the cluster and the services running in it. You can easily obtain health information and correct potential issues before they cascade and cause massive outages. In the typical model, services send reports based on their local views, and that information is aggregated to provide an overall cluster-level view.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction ][24]<br>[https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-understand-and-troubleshoot-with-system-health-reports][25]  |  
| Are you aware of Application Insights support for Microservices and Containers?| Azure Application Insights is an extensible platform for application monitoring and diagnostics. It includes a powerful analytics and querying tool, customizable dashboard and visualizations, and further options including automated alerting. It is the recommended platform for monitoring and diagnostics for Service Fabric applications and services.   A single Application Insights resource can be used for all the components of your application. The health of the services and the relationships between them are displayed on a single Application Map. You can trace individual operations through multiple services with automatic HTTP correlation.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights ][26]<br>[https://azure.microsoft.com/en-us/blog/app-insights-microservices/ ][27]  |

## App Migration    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Are you looking to migrate a solution built in Cloud Services Web and Worker Roles to Service Fabric    | Application Migration from solutions built in Classic Cloud Services to Microservices based architecture.   If you are still evaluating which platform to use, consider App Services as well.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cloud-services-migration-worker-role-stateless-service][28]<br>[https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cloud-services-migration-differences][29]  |  
| Are you considering containerizing your application?     | Now you can use Service Fabric and develop and deploy your containerized applications. Determine if the putting ASP.NET application in App Services is a valid option. You can use Web App and Web jobs as an option as well. If you have made the decision to host in Service Fabric, be aware that you can containerize their application and put it here.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-containers-overview][30]  |

## Distributed Architecture    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Microservices Architecture Experience in the team, here are some best practices| If you are considering moving to microservices architecture either for brownfield or greenfield development, one must invest in training in microservices architecture and design patterns.| [https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices][31]  |  
| Are you aware of microservices architecture style?  | A microservices architecture consists of a collection of small, autonomous services. Each service is self-contained and should implement a single business capability. Consider the amount of services that are implemented; do you need 1000 services, when in reality you could deploy only 5?|[https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices][31]  |

## High Availability and Business Continuity / Disaster Recovery    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Have you considered mitigations and actions to take if a disaster happened?| There is guidance available for Hardware and Software faults and availability of Service Fabric Cluster| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-disaster-recovery][32]  |  
| Are you thinking of Service Fabric platform for microservices or development platform in general? | You can use the platform if you want to host any exe on the platform and utilize the High Availability aspect that the platform offers. Service Fabric ensures that instances of an application are running. Be aware that Geo-Distribution of the Service Fabric Cluster is not yet supported. You can back up any data on the compute to a BLOB and restore that in case of such a disaster.| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-deploy-existing-app][68]  |

## Security    

| **Question**| **Purpose**| **Relevant Documentation**   |  
|---|---|---|  
| Have you considered security aspects around microservices? | The same Application Security Rules can be applied to an application developed on Service Fabric Platform. You can apply standard SDL best practices.    |[https://www.mulesoft.com/resources/api/microservices-security][69]        |  
| Are you wondering about application security for applications running on Service Fabric?| This is no different than implementing security using AD for example, for any other regular application. The guidance on using AD is the same.   Did you know that you can implement same infrastructure level security to Service Fabric Cluster as you would to any Server Farms.| [https://azure.microsoft.com/en-us/documentation/articles/service-fabric-windows-cluster-windows-security/][70]   |  
| Have you considered securing applications running under different user accounts?| By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts| [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-runas-security][20]  |  


[1]: https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-comparison
[2]: https://docs.microsoft.com/en-us/azure/app-service-web/choose-web-site-cloud-service-vm#onprem
[3]: https://docs.microsoft.com/en-us/azure/app-service-web/choose-web-site-cloud-service-vm#onprem 
[6]: https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-migration-from-iis-server
[7]: https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/managed-web-app/multi-region-web-app
[8]: https://docs.microsoft.com/en-us/azure/architecture/resiliency/index#resiliency-strategies
[9]: https://docs.microsoft.com/en-us/azure/architecture/resiliency/index#defining-your-resiliency-requirements
[10]: https://docs.microsoft.com/en-us/azure/architecture/resiliency/failure-mode-analysis
[11]: https://docs.microsoft.com/en-us/dotnet/articles/csharp/async
[12]: https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview
[13]: https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor
[14]: https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-overview/
[15]: https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview/
[16]: https://msdn.microsoft.com/library/dn589789.aspx
[17]: https://docs.microsoft.com/en-us/azure/architecture/best-practices/monitoring
[18]: https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-alerts
[19]: https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/managed-web-app/scalable-web-app
[20]: https://docs.microsoft.com/en-us/azure/architecture/checklist/scalability
[21]: https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/insights-how-to-scale/
[22]: https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/insights-autoscale-best-practices
[23]: https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-security?toc=%2fazure%2fapp-service-mobile%2ftoc.json
[24]: https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/
[25]: https://security-forms.azure.com/penetration-testing/terms
[26]: https://azure.microsoft.com/en-us/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/
[27]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-tutorial-custom-domain
[28]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-tutorial-custom-ssl
[29]: https://en.wikipedia.org/wiki/HTTPS
[30]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-tutorial-custom-ssl#enforce-https
[31]: https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview
[32]: https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-authentication-authorization?toc=%2fazure%2fapp-service-mobile%2ftoc.json 

[36]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-choose-framework
[37]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-actors-introduction
[38]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-introduction#when-to-use-reliable-services-apis
[39]: ASP.NET%20Core%20application
[40]: Event%20Hubs
[41]: IoT%20Hub
[42]: Azure%20API%20Management
[43]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-api-management-overview
[44]: https://blogs.msdn.microsoft.com/azureservicefabric/
[45]: https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/
[46]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-lifecycle
[47]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-model
[48]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-concepts-scalability
[49]: https://azure.microsoft.com/en-us/documentation/articles/service-fabric-concepts-partitioning/
[50]: https://azure.microsoft.com/en-us/documentation/articles/service-fabric-cluster-scale-up-down/
[51]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machine-scale-sets-autoscale-overview/
[52]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal
[53]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-tutorial-create-cluster-azure-ps
[54]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-connect-to-secure-cluster
[55]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-application-runas-security
[56]: https://azure.microsoft.com/en-us/documentation/articles/service-fabric-linux-overview/
[57]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-capacity-planning
[58]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-diagnostics-overview
[59]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction
[60]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-understand-and-troubleshoot-with-system-health-reports
[61]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights
[62]: https://azure.microsoft.com/en-us/blog/app-insights-microservices/
[63]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cloud-services-migration-worker-role-stateless-service
[64]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cloud-services-migration-differences
[65]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-containers-overview
[66]: https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices
[67]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-disaster-recovery
[68]: https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-deploy-existing-app
[69]: https://www.mulesoft.com/resources/api/microservices-security
[70]: https://azure.microsoft.com/en-us/documentation/articles/service-fabric-windows-cluster-windows-security/