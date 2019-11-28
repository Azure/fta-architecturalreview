# FastTrack for Azure Architectural Discussion Framework - DevTest Solution

- [FastTrack for Azure Architectural Discussion Framework - DevTest Solution](#fasttrack-for-azure-architectural-discussion-framework---devtest-solution)
  * [DevOps Self-Assessment Tool](#devops-self-assessment-tool)
  * [App &amp; Data Migration](#app--amp--data-migration)
  * [Distributed Architecture](#distributed-architecture)
  * [High Availability and Business Continuity / Disaster Recovery](#high-availability-and-business-continuity---disaster-recovery)
  * [Monitoring &amp; Management](#monitoring--amp--management)
  * [Performance &amp; Scalability](#performance--amp--scalability)
  * [Security](#security)
  * [Customer Examples](#customer-examples)

## DevOps Self-Assessment Tool 
Are you aware of the DevOps Self-Assessment tool? If not, this may be a great place to start to baseline your DevOps practices! [DevOps Self-Assessment](https://www.devopsassessment.net/)

## App & Data Migration    

* **Are you using tooling to streamline and build repeatable builds/deployments to Azure? Or are you building your code manually, and manually pushing this to Azure?**

    Determine whether the solution is being manually deployed to Azure (which is error-prone, and time consuming). Or, whether some form of tooling (e.g. Jenkins, VSTS) is being used to deploy either in a Continuous Integration (CI), daily build or gated check-in approach.  Automate deploying the application to test, staging, and production environments. Automation enables faster and more reliable deployments and ensures consistent deployments to any supported environment. It removes the risk of human error caused by manual deployments. It also makes it easy to schedule releases for convenient times, to minimize any effects of potential downtime.    
    
    > [DevOps Checklist: Release](https://docs.microsoft.com/en-us/azure/architecture/checklist/dev-ops#release)

* **If you have designed a build pipeline - How have you configured your builds to trigger?**

    * Continuous Integration
    * Off a particular branch?
    * Daily / Nightly Build
    * Combination, depending upon scenario
    
    If this is performed on a trigger event, what is the trigger? (e.g. which particular branch)

    If a pipeline has been established, could this be triggering too many builds or triggering off a build of a branch that does not represent a &#39;shippable version of the solution? For CI - Consider adopting a trunk-based development model. In this model, developers commit to a single branch (the trunk). There is a requirement that commits never break the build. This model facilitates CI, because all feature work is done in the trunk, and any merge conflicts are resolved when the commit happens.    
    
    > [DevOps Checklist](https://docs.microsoft.com/en-us/azure/architecture/checklist/dev-ops)

* **Are you using Infrastructure as Code to automate the deployment of your Azure environment? Are you aware of Azure Resource Manager templates? Have you used them to deploy your DevTest solution?**

    Determine whether there is an approach to automating the deployment of their environment, so that multiple environments (Dev/Test/Prod) can be implemented easily.    
    
    > [What is Infrastructure as Code?](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/)
    >
    > [Resource Manager template deployment](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#template-deployment)
    >
    > [Create and deploy your first Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template)

* **Are you aware of the Azure Resource Manager template best practices? Have you designed your Azure Resource Manager templates with these in mind?**

    Determine whether the template has been parameterized, so that it can be easily deployed across multiple environments, or whether parameters have been limited and a t-shirt sizing approach has been used.
    
    There are a number of other practices that are recommended. These can be reviewed in those articles linked in the associated documentation.    
    
    > [Understand the structure and syntax of Resource Manager templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-template-best-practices)
    >
    > [Design patterns for Resource Manager templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/best-practices-resource-manager-design-templates)

* **In addition to defining the Azure resources required for your solution (e.g. Azure Resource Manager template), how are you configuring the system / components on the box? (e.g. Manual, DSC, Chef, Puppet)**

    Determine whether the configuration of the machines themselves have been considered. Is this type of configuration being completed manually, or is it scripted in some way? Effectively, you are looking to understand whether the environment can be provisioned end-to-end without any manual intervention.    

    > [Overview of Desired State Configuration](https://docs.microsoft.com/en-us/powershell/dsc/overview)
    >
    > [Chef on Azure](https://docs.microsoft.com/en-us/azure/chef/)
    >
    > [Puppet and Windows Automation](https://puppet.com/products/managed-technology/microsoft-windows-azure)

## Distributed Architecture

* **Are you using a separate environment for your development environment, and promoting application code between those environments?**

    If development and test environments don&#39;t match the production environment, it is hard to test and diagnose problems. Therefore, keep development and test environments as close to the production environment as possible. Make sure that test data is consistent with the data used in production, even if it's sample data and not real production data (for privacy or compliance reasons). Plan to generate and anonymize sample test data.    

* **Are your components tightly coupled? Or are you using message brokering to separate the components, to help the application gracefully degrade?**

    If components are tightly coupled, then this would mean that there is a risk of components being brought down by other components (up-stream or downstream dependencies).    
    
    > [Queue-Based Load Leveling Pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/queue-based-load-leveling)
    >
    > [Retry Pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/retry)

## High Availability and Business Continuity / Disaster Recovery    

* **Have you deployed any resources where there is only one instance of a particular resource?**

    Determine whether there are single points of failure in the solution. If there are, what is the potential risk for this component? How could this impact the wider solution? What steps can be taken to mitigate this risk?    

* **Have you thought about redundancy across your solution?**

    * VMs in a load balancer
    * Replicating databases
    * Geo-replication (e.g. via Traffic Manager)
    * Deploying to more than one region
    * Using automatic failover but manual failback
    * Redundancy for traffic manager

    Determine whether redundancy has been built into the solution. Are there single points of failures in the solution? Could the solution be impacted by a failure of an Azure region? If so, would the requirements warrant the need for a geo-distributed application?    
    
    > [Design principal: Make all things redundant](https://docs.microsoft.com/en-us/azure/architecture/guide/design-principles/redundancy)

* **Do you have any dependencies on resources that are external to your solution? (e.g. third-party, such as payment providers or e-mail messaging). How are you protected against that third-party service from failing?**

    Determine if there are dependencies on third parties that could cause a failure of the solution itself. (Be careful, as these could be upstream or downstream dependencies). If so, how can this be mitigated? Are there agreements or SLAs in place? What are the escalation paths?    

* **DevTest on IaaS - Have you placed your virtual machines into an availability set?**

    To provide redundancy to your application, it is recommended that you group two or more virtual machines in an availability set. This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the 99.95% Azure SLA.    
    
    > [Manage the availability of Windows virtual machines in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability)

* **DevTest on IaaS  – Do you know about the difference between unmanaged and managed disks? Have you leveraged Azure Managed disks?**

    Determine whether the level of IOPS / throughput have been safeguarded to  VM disks. If using unmanaged disks, the placement of disks across storage accounts must be considered to maintain performance and resilience.    
    
    > [Azure Managed Disks overview](https://docs.microsoft.com/en-gb/azure/storage/storage-managed-disks-overview)

* **Have you deployed your environment in a way that is fully representative of production?**

  * If you are opting for a Disaster Recovery scenario - What is your process? Have you been able to test it in dev?
  * If you are opting for high availability (e.g. Geographic redundancy), are you reproducing this in DevTest i.e. that this is working appropriately

  Determine whether a pre-production environment that is fully representative of production.  There should be a representative environment to run comparable tests ahead of a release, allowing a decision to be made on whether the quality of the build is good and meets requirements (For example, can serve the required volume of users)

* **Does your solution support zero-downtime deployments?**

    Determine whether an environment can support a small downtime maintenance window to roll out a new version or if it is required that applications must be deployed seamlessly to a new version. One approach to accomplish this is blue-green deployments where a new version is deployed, traffic is drained off of the existing version, and then the old instance is deprovisioned. The new environment gives a fully configured environment that can be used for validation tests before users are directed to it.

    > [Blue-Green deployments using Azure Traffic Manager](https://azure.microsoft.com/en-us/blog/blue-green-deployments-using-azure-traffic-manager/)
    >
    > [Blue/Green Deployments in Service Fabric](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/10/17/bluegreen-deployments-in-service-fabric/)


## Monitoring & Management    

* **Do you require an environment that allows you to empower your developers and testers, but also allows IT to control Governance and Cost? If so, are you using / planning to use DevTest labs?**

    Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost. A customer can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.    
    
    > [About Azure DevTest Labs](https://docs.microsoft.com/en-au/azure/devtest-lab/devtest-lab-overview)

* **Are you monitoring for cost within your DevTest environment?**

    Determine whether there has been any consideration to cost, ahead of a run state of a DevTest environment. Who is accountable for managing and maintaining this? At what point does that individual take action if this cost is too high? Is this clearly defined, so that developers and testers are aware of the parameters in which they should operate?    
    
    > [View the monthly estimated lab cost trend in Azure DevTest Labs](https://docs.microsoft.com/en-au/azure/devtest-lab/devtest-lab-configure-cost-management)
    > 
    > [New Power BI content pack for Azure Enterprise users](https://azure.microsoft.com/en-au/blog/new-power-bi-content-pack-for-azure-enterprise-users/)

* **Have you implemented a mechanism/policy to control cost, and turn off resources when they are not required?**

    Determine if auto-startup / auto-shutdown has been implemented to ensure resources are used only when required.
    
    DevTest labs provides native functionality to control this for Virtual Machines. If there is a need to manage  costs for PaaS resources, Azure Automation and Run books may need to be considered. (For example, changing the SKU of resource type to a lower level, when not required)    
    
    > [Manage all policies for a lab in Azure DevTest Labs](https://docs.microsoft.com/en-au/azure/devtest-lab/devtest-lab-set-lab-policy)
    > 
    > [Runbook and module galleries for Azure Automation](https://docs.microsoft.com/en-us/azure/automation/automation-runbook-gallery)

* **Do you have a single pane of glass view of the health of your application?**

    Understand whether there is a clear view into the application.  How soon would there be awareness of an issue after it occurs? Is infrastructure monitoring only being performed, meaning that application level events may not be discovered? Or, is there a single monitoring dashboard which covers both application and infrastructure monitoring?    
    
    > [What is Monitoring?](https://www.visualstudio.com/learn/what-is-monitoring/)

* **Have you considered how to make insight easier for your operations team?**

    * Make all actions observable, so you can trace through your system (e.g. correlation ID)
    * Instrument for monitoring
    * Instrument for root cause analysis
    * Use distributed tracing
    * Standardize logs and metrics
    * Automate management tasks

    Understand whether there is a clear view into the application.  Can the lines of offending code be identified when an issue occurs, and can this be remediated quickly? Or would a search through logs need to take place, potentially joining a number of pieces of application telemetry to understand the problem?    
    
    > [What is Application Insights?](https://docs.microsoft.com/en-gb/azure/application-insights/app-insights-overview)
    > 
    > [Overview of Application Insights for DevOps](https://docs.microsoft.com/en-gb/azure/application-insights/app-insights-detect-triage-diagnose)

* **Are you aware of the Health Endpoint Monitoring pattern? Have you implemented this in your solution?**

    Implement health monitoring by sending requests to an endpoint on the application. The application should perform the necessary checks and return an indication of its status. A health monitoring check typically combines two factors: 
    
    * The checks (if any) performed by the application or service in response to the request to the health verification endpoint.     
    * Analysis of the results by the tool or framework that performs the health verification check. 
    
    > [Health Endpoint Monitoring Pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/health-endpoint-monitoring)

* **Facilitate hypothesis-based development**

    Be confident in your deployment and rollback mechanisms, get meaningful data and telemetry that allows to track feature adoption, usage as you experiment and test assumptions    
    
    > * *Testing in Production*
    > * *Fault Injection*
    > * *Usage Monitoring/User Telemetry*

* **Consider A/B deployment scenarios**

    As you experiment with new features and roll out new features, test your application in multiple configurations with different user groups to see how they are received. One set of users may see a feature lit up a certain way on one page, and a different group would see the feature in a different way on maybe another page. Testing both simultaneously allows you to measure which has the greater impact on your users.

    > [Case Study: Implementing A/B testing for Catraca Livre using open-source technologies on Azure](https://microsoft.github.io/techcasestudies/devops/2017/02/20/catraca-livre.html)

## Performance & Scalability    

* **Are you testing the functionality of your software?  Are these tests manual, or automated?**

    Manually testing software is tedious and susceptible to error. Automate common testing tasks and integrate the tests into your build processes. Automated testing ensures consistent test coverage and reproducibility. Integrated UI tests should also be performed by an automated tool.    
    
    > [DevOps checklist](https://docs.microsoft.com/en-us/azure/architecture/checklist/dev-ops)

* **Which types of tests are you running? Unit? Integration? Do you know how much code coverage you have from your tests? How do you ensure that your level of coverage is appropriate?**

    Software testing is like insurance. Creating tests is buying coverage against risks. Redundant tests, flaky tests or running tests unnecessarily is paying too much in premiums for the coverage you get. But it is hard to keep track of what you spend on a large software project. Using historical data about executing tests, we can derive expected cost and benefit of each test execution and make decisions for whether the price is worth it. Even a simple cost model can be very effective and save us money and time in testing.    
    
    > [Guidelines for checking in quality code](https://msdn.microsoft.com/en-us/library/ms182021(v=vs.100).aspx)
    > 
    > [Software testing at scale to increase velocity](https://www.visualstudio.com/learn/software-testing-scale-increase-velocity/)
    > 
    > [Is 100% code coverage worth the cost?](https://www.visualstudio.com/learn/100-code-coverage-worth-cost/)
    > 
    > [Getting the noise out of test runs](https://www.visualstudio.com/learn/getting-noise-test-runs/)

* **How often are you load/performance testing your application? Are you at least performance testing before a major production release? Are these tests being ran at a level of scale that is on part with expected load in production, AND future growth?**

    The impact of a serious performance issue can be just as severe as a bug in the code. While automated functional tests can prevent application bugs, they might not detect performance problems. Define acceptable performance goals for metrics like latency, load times, and resource usage. Include automated performance tests in your release pipeline, to make sure the application meets those goals. An application might work fine under test conditions, and then have problems in production due to scale or resource limitations. Always define the maximum expected capacity and usage limits. Test to make sure the application can handle those limits, but also test what happens when those limits are exceeded. Capacity testing should be performed at regular intervals. After the initial release, you should run performance and capacity tests whenever updates are made to production code. Use historical data to fine tune tests and to determine what types of tests need to be performed.    
    
    > [DevOps checklist](https://docs.microsoft.com/en-us/azure/architecture/checklist/dev-ops)
    > 
    > [Load test your application by using Visual Studio Team Services](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-vso-load-test)
    > 
    > [Get started with performance testing](https://www.visualstudio.com/en-us/docs/test/performance-testing/getting-started/getting-started-with-performance-testing)
    > 
    > [Performance test your Azure web app under load](https://www.visualstudio.com/en-us/docs/test/performance-testing/app-service-web-app-performance-test)

* **Have you tested for the scenario where components in your solution may fail, and other components attempt to send requests? How have you mitigated this scenario? For example, the circuit breaker pattern.**

    In a distributed environment, calls to remote resources and services can fail due to transient faults, such as slow network connections, timeouts, or the resources being overcommitted or temporarily unavailable.  These faults can range in severity from a partial loss of connectivity to the complete failure of a service. In these situations, it might be pointless for an application to continually retry an operation that is unlikely to succeed, and instead the application should quickly accept that the operation has failed and handle this failure accordingly.    
    
    > [Availability checklist: Errors and failures](https://docs.microsoft.com/en-us/azure/architecture/checklist/availability#errors-and-failures)
    > 
    > [Circuit Breaker pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker)
    > 
    > [Retry pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/retry)

* **Walk through how your solution will scale. (i.e. How hard is it to scale the entire solution to the right level for each component)**

    Identify whether you understand how the solution itself will scale, and whether the solution is setup in such a way that components can scale up as needed. Also determine whether the scaling approach is overcomplicated for the solution at hand.   

* **Are you aware of the scalability checklist? Some thoughts include**

    * Have you considered a share-nothing architecture?
    * Have you evaluated the chattiness vs size of requests in your solution?
    * Have you offloaded CPU/IO tasks?
    * Are you using Async calls?

    Scalability is an important aspect in cloud. Understand whether you have considered scalability as part of the solution, or whether the expectation is that this is a feature of the cloud.    
    
    > [Scalability Checklist](https://docs.microsoft.com/en-us/azure/best-practices-scalability-checklist)
    > 
    > [Task-based Asynchronous Pattern (TAP)](https://msdn.microsoft.com/library/hh873175.aspx)
    > 
    > [Retry pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/retry)

* **Have you considered horizontal scaling, instead of vertical scaling?**

    In particular;
    * Avoiding stickiness of a particular instance (e.g. routing to a specific instance)
    * Identified bottlenecks (as you scale one tier, does another become a bottleneck)
    * Design for scale in (i.e. gracefully handling removal of instances)

    There are two main ways that an application can scale:   Vertical scaling, also called scaling up and down, means changing the capacity of a resource. For example, you could move an application to a larger VM size. Vertical scaling often requires making the system temporarily unavailable while it is being redeployed. Therefore, it is less common to automate vertical scaling. Horizontal scaling, also called scaling out and in, means adding or removing instances of a resource. The application continues running without interruption as new resources are provisioned. When the provisioning process is complete, the solution is deployed on these additional resources. If demand drops, the additional resources can be shut down cleanly and deallocated.   Many cloud-based systems, including Microsoft Azure, support automatic horizontal scaling. The rest of this article focuses on horizontal scaling.    
    
    > [Design to scale out](https://docs.microsoft.com/en-us/azure/architecture/guide/design-principles/scale-out)
    > 
    > [Autoscaling](https://docs.microsoft.com/en-us/azure/architecture/best-practices/auto-scaling)
    

* **Is there a large amount of static content on your website (e.g. images, videos)? Are you aware of the Static Content Hosting pattern, and have you implemented it in your solution?**

    In most cloud hosting environments, it&#39;s possible to minimize the need for compute instances (for example, use a smaller instance or fewer instances), by locating some of an application’s resources and static pages in a storage service. The cost for cloud-hosted storage is typically much less than for compute instances.    
    
    > [Static Content Hosting Pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/static-content-hosting)

## Security    

* **Are you using a dataset in DevTest that is representative of production, but does not contain customer-sensitive data?  Or is your dataset not representative of production data?**

    Is testing taking place in the production environment with real production data? If this is the case, be aware of the risk that developers or testers may have access to sensitive data, which could leak.
    
    Also determine whether tests are being performed against non-representative data. If this is the case, are there scenarios that could arise in production that had not been thoroughly tested due to the dummy data?   

* **Consider the development pipeline - Is code being reviewed to ensure that there is no malicious code?**

    Determine whether code is being used from a third-party, e.g. a vendor or third-party package.
    
    Has the code been reviewed prior to it being released onto production servers? Could there be any malicious content, e.g. capturing user data.
    
    While this question focuses on third parties, this could also be the case if there was a rogue developer inside the organisation.

    Also scan not just code being written by the developers but run binary scans on any packages being used. These scanners will look to see if there is a known vulnerability in a particular library being referenced and can call that out during the deployment pipeline to avoid code with a known vulnerability for being pushed to end users.

* **Consider the development pipeline - What steps are being taken to ensure that secrets are not being stored in source control?**

    Determine whether any passwords, connection strings or additional secrets are being stored in source control.
    
    If there are, developers or testers may have access to production values. If a developer goes rogue, or you get a disgruntled employee leaving the organisation, this could pose a risk. This would also be a risk if you open sourced code, or code leaked.

    Place restrictions on the code repository to ensure that passwords are not getting checked in to source code.

* **How are you securing your source control? Are there third-party users or vendors who may have access to the underlying code, and could potentially exploit this?**

    Determine whether access to source control is secure, as well as the overall delivery pipeline the leads to production. 
    
    If not, could a third-party, or even internal audience, be injecting some kind of malicious tasks into the delivery pipeline to production and could cause a compromise?   

* **Have you considered security when you were building your DevOps pipeline? What have you specifically built in to achieve a Secure DevOps workflow?**

    Determine whether access to source control is secure, as well as the overall delivery pipeline the leads to production. 
    
    If not, could a third-party, or even internal audience, be injecting some kind of malicious tasks into the delivery pipeline to production and could cause a compromise?    
    
    > [Building cloud apps using the Secure DevOps Kit for Azure](https://www.microsoft.com/itshowcase/Article/Content/919/Building-cloud-apps-using-the-Secure-DevOps-Kit-for-Azure)
    > 
    > [DevOps practices for cloud security](https://www.microsoft.com/itshowcase/Article/Content/769/DevOps-practices-for-cloud-security)

* **Within your solution, have you built your own identity provider? Or have you leveraged an existing identity provider, e.g. Azure AD and leveraged their authentication (e.g. Oauth)**

    Determine if passwords or secrets are being stored in a database (potentially with just a hash).
    
    A commonly noted bad practice is storing MD5 password hashes, which is not a safe mechanism. Identify whether there is an opportunity to use an identity provider (such as Azure Active Directory, or Azure Active Directory B2C), so that the risk of managing identity in-house is mitigated. 

* **Are you applying the same security practices or measures to your development and test environments as your production environments?**

    Reduce the attack surface by ensure all environments are secured. Ensure tests are carried out in a similar environment and that additional security measures in production will not break functionality.    
    
    > [How to set security in DevTest Labs](https://azure.microsoft.com/en-us/resources/videos/how-to-set-security-in-your-devtest-lab/)

* **Are you sure that your dev and production environments are segregated?**

    Determine whether there are any resources that may be shared across environments. For example, if there is a Load Balancer configured in a production environment that routes to resources in both development and production. This could potentially lead to undesirable scenarios, such as production data being stored in a development environment.    
* **Is there separation of concerns in your deployment solution?**

    Especially in industries that are heavily regulated, there is a requirement to keep developers and deployment teams fundamentally separated. Running different release pipelines can help with that separation where developers have read / write access to pipelines running in lower environments and read-only access to environments that hit production. This will help limit the exposure of sensitive accounts and passwords to a minimum.
  
## Customer Examples
* Visual Studio Team Services
  * [Visual Studio Team Services DevOps Journey](http://stories.visualstudio.com/devops/)
  * [Universal Store: Journey to Continuous Delivery and DevOps](https://www.visualstudio.com/learn/universal-store-journey-continuous-delivery-devops/)
  * [Moving Microsoft to Visual Studio Team Services under One Engineering System (1ES)](https://www.visualstudio.com/learn/devopsmsft-overview/)
* Microsoft IT
  * [DevOps practices for cloud security](https://www.microsoft.com/itshowcase/Article/Content/769/DevOps-practices-for-cloud-security)
  * [Building cloud apps using the Secure DevOps Kit for Azure](https://www.microsoft.com/itshowcase/Article/Content/919/Building-cloud-apps-using-the-Secure-DevOps-Kit-for-Azure)
* Customer Case Studies
  * [Microsoft Azure DevOps Solution](https://azure.microsoft.com/en-au/solutions/devops/)
  * [Visual Studio Team Services Customer Stories](https://www.visualstudio.com/team-services/case-studies/)
