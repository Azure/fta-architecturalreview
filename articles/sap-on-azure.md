# FastTrack for Azure Architectural Discussion Framework - SAP on Azure Solution

- [FastTrack for Azure Architectural Discussion Framework - Sap on Azure Solution](#fasttrack-for-azure-architectural-discussion-framework---sap-on-azure-solution)
  - [SAP Landscape Design](#sap-landscape-design)
  - [SAP Systems Sizing](#sap-systems-sizing)
  - [High Availability and Business Continuity / Disaster Recovery](#high-availability-and-business-continuity--disaster-recovery)
  - [Performance and Scalability](#performance--scalability)
  - [Backup and Archiving](#backup--archiving)
  - [Migration Methodologies](#migration-methodologies)
  - [Security Design](#security-design)
  - [Monitoring and System Management](#monitoring-and-system-management)
  - [Stories](#stories)

## SAP Landscape Design
   In this step, we need understand the current landscape design and then we need to optimize it in Azure to meet the future roadmap of the organization.

- **What is your current SAP Landscape and systems in scope for the move to Azure?**

    Please provide a landscape diagram, Operating system details and database details of the SAP environment.
    - [SAP systems which are certified to run on Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/sap-certifications)

- **What are the driving factors for moving to Azure?**

   Determine the customer experience in current envionment and expectations in Azure.

- **What is your future environment roadmap and plans for move to S/4 Hana?**

    Projects which are planned in future along with moving to Azure. We can look at overall trransformation strategy for SAP Landscape.

- **Where are you hosting your systems?  In which region you are planning to host in Azure?**

    - [Worldwide Azure regions](https://azure.microsoft.com/en-us/global-infrastructure/regions/)

## SAP Systems Sizing
Sizing means determining the infrastructure requirements of an SAP application, such as the network bandwidth, memory, CPU processing power, and I/O capacity. The size of the servers and database is influenced by both business aspects and technological aspects. This means that the number of users using the various application components and the data load they put on the server must be taken into account. 

- **Can you provide the current sizing and exiting hardware specifications?**

    SAPS value for the current hardware and SAP quicksizer report will be helpful to determine the target system configuration.

    - [Learn about SAP Sizing and FAQ](https://www.sap.com/about/benchmark/sizing/decision-tree.html)  

- **Can you provide the SAP Early Watch Reports and any other performance data (Compute, Storage, Network & Application) ?**

    SAP Early Watch Report provides system usage and performace statistics to eastimate the SAP system design on Azure.

- **What is the current database size of each of the systems and average monthly growth?**

    Database size will be helpful in determining infrastructure requirement like Storage and VMs for the target design.

## High Availability and Business Continuity / Disaster Recovery

   SAP systems runs mission critical business application and any outage causes disruption in business flow and processes which in turn is loss in business value and its capabilities. Successful HA prevents downtime and data loss to eliminate single point of failure.
   Disaster Recovery is not just IT requirement, but it is also Business requirement. Production environment msut be available in case of any disaster  with minimum data loss and completely recoverable at different location. Failover should be completed as soon as possible with minimum impact to end users and sub systems. 


- **What are the availability SLAs. Can you explain the current High Availability design?**

    Refer to the High Availability & disaster recovery concepts for SAP on Azure.
    - [High Availability Architecture for SAP on Azure ](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/sap-certifications)
    - [Reference architecture design for SAP Netweaver for AnyDB on Azure](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/sap/sap-netweaver)

- **Can you expalin the present disaster recovery setup. What will be recovery time objective (RTO) and Recovery Point Objective (RPO)?**

    Azure Site recovery will be recommended approach to setup DR for SAP application layer. For the Database layer, DB specific setup will be required (like HSR for SAP HANA DB and SQL AlwaysOn for SQL server DB)
    - [Reference design for Azure Site Recovery(ASR) for SAP Netweaver on Azure](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-sap)

- **Can you explain the process for the Failover in case of a Disaster and what is the frequency of disaster recovery testing?**

   Process to test the disaster recovery, test plans and team involved to perform the activities. 

## Performance & Scalability

- **What are the performance related SLAs?**

    SAP application servers carry on constant communications with the database servers. For performance-critical applications running on any database platforms, including SAP HANA, consider enabling Write Accelerator to improve log write latency. To optimize inter-server communications, use Accelerated Networking. Note that these accelerators are available only for certain VM series.
  
    - [Guidelines for Accelarated Network](https://azure.microsoft.com/blog/linux-and-windows-networking-performance-enhancements-accelerated-networking/)
    - [Write Accelarator for M Series VMs](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/how-to-enable-write-accelerator)
  - [Best Practices for Storage performance optimization](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/premium-storage-performance)

 - **Are there Scalability requirements?**

    SAP application servers and the Central Services clusters can scale up/down or scale out by adding more instances.
    The database VMs can scale up/down with limitations on maximum size(4TB) of the VM. If your workload exceeds the maximum VM size, Microsoft also offers Azure Large Instances for SAP HANA. 
     
    - [Details about Azure Large Instances](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/hana-overview-architecture)

    - [Configuring Azure Infrastructure for SAP HANA Scale-out](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/hana-vm-operations#configuring-azure-infrastructure-for-sap-hana-scale-out)


## Backup & Archiving
   As part of data management and availiability, we need to regularly back up our operating system and database to restore the SAP system, if required. To use an appropriate back up and restore method is one of the most important tasks of the system and database administrator.
   Data archiving is used by companies with two main goals in mind: reducing data volumes in the system and complying with legal data retention requirements. Both goals are obtained using the same processes, which together make up this variant: Monitoring, Analyzing and Categorizing, Archiving and Post Processing.

- **What is the Current Backup Strategy?**

    Determine the type and frequency of backup in current SAP environment. It is strongly recommended to schedule regular data backups from the data area of your SAP HANA database to a secure location. SAP system on Azure Backup guide provides detailed information. 

    - [Backup guide for SAP workload on Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)

- **What is the Data Archiving Strategy?**

    Determine if data archiving is done on a regular basis and how archived data is selected and stored. What is the tool used for data archiving. 
    
    - [Data Archiving concepts and architectire](https://help.sap.com/SAPhelp_nw70/helpdata/en/8d/3e4c11462a11d189000000e8323d3a/frameset.htm)

    - [Benifits of Data Archiving](https://help.sap.com/saphelp_nw70/helpdata/EN/8f/f3b142304cc511e10000000a1550b0/frameset.htm)

## Migration Methodologies

- **Are you planning to change the operating system and database of the systems during migration to Azure?**

    Homogeneous migration can be performed if database and operating systems remains same in new platform, alternatively heterogenous migration needs to be performed if there are changes in the operating systems OR database. 

    - [Please refer to SAP Note 1928533(SAP login required) for the VM/OS/DB compatibility information.](https://launchpad.support.sap.com/#/notes/1928533)

    - [SAP System Heterogenous Migration (SAP Note 82478)](https://launchpad.support.sap.com/#/notes/82478)

- **Have you started planning for system migration and is the partner for the project delivery identified?**
   
   Organizations need a consistent and reliable methodology that enables them to plan,design, migrate and validate the migration. Solid migration planning can help identify potential problems and how to avoid them or, if problems are unavoidable, help IT define mitigation strategies.  While the amount of planning depends on the size and scope of the migration, the planning process generally should involve determining the requirements of the migration, identifying the current and future environment, and creating and documenting the migration plan. The importance of clear and complete documentation coupled with ongoing communications to the technical team as well as the business team can not be over emphasized.

## Security Design
 - **What is the current Governance model? How do you control access to the different infrastructure resources? What is the process for segregation of duties?**

    Azure policy and RBAC provides granular level access control for resources.
    - [Best practices for Azure Policy.](https://docs.microsoft.com/en-us/azure/azure-policy/azure-policy-introduction)
    - [Role Based Access control in Azure.](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview)

 - **What are the proactive steps taken in ensuring the security of the environment?**

    For infrastructure security, data is encrypted in transit and at rest. The "Security considerations” section of the SAP NetWeaver on Azure Virtual Machines (VMs) – Planning and Implementation Guide begins to address network security. The guide also specifies the network ports you must open on the firewalls to allow application communication.
    - [Security considerations of the SAP NetWeaver on Azure Virtual Machines (VMs)](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/planning-guide)

    - [FAQ : SAP HANA Security (SAP Note 2159014)](https://launchpad.support.sap.com/#/notes/2159014)

## Monitoring and System Management
   Monitoring SAP is a daily routine activity in which your IT SAP team is checking all processes, databases, servers, instance performance, system-wide performance, logs, users, batch jobs, dumps and many other elements, to see what is running, waiting, stopped working or just behaving weird.
   The smallest of things, say a long-running system backup, can cause performance issues, leading to delayed run times and eventually a system overload or failure. Early detection of a failure can prevent major incidents in the systems.

- **How do you monitor different layers of the systems?**
    System monitoring processes at application, database and infrastructure layers.
    - [SAP Solution Manager Monitoring guide](https://wiki.scn.sap.com/wiki/display/TechOps)

- **How do you determine if there is an outage and the alerts that have been setup?**

    Azure provides several functions for monitoring and diagnostics of the overall infrastructure. Also, enhanced monitoring of Azure virtual machines (Linux or Windows) is handled by Azure Operations Management Suite (OMS).
    - [Best practices for Monitoring and Diagnostics in Azure.](https://docs.microsoft.com/en-us/azure/architecture/best-practices/monitoring)

    To provide SAP-based monitoring of resources and service performance of the SAP infrastructure, the Azure SAP Enhanced Monitoring extension is used. This extension feeds Azure monitoring statistics into the SAP application for operating system monitoring and DBA Cockpit functions. SAP enhanced monitoring is a mandatory prerequisite to run SAP on Azure. 
    - [Azure SAP Enhanced Monitoring extension.](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/deployment-guide#d98edcd3-f2a1-49f7-b26a-07448ceb60ca)

- **What processes are automated for the overall management and operations?**
    - [Introduction to Azure Automation for system management.](https://docs.microsoft.com/en-us/azure/automation/automation-intro)

## Stories
 - [Top 10 considerations for deploying SAP workloads on SQL server in Azure.](https://blogs.msdn.microsoft.com/saponsqlserver/2015/05/25/top-10-key-considerations-for-deploying-sap-applications-on-azure/)

 - [Architecture design for SAP Dev/Test environment with high level pricing estimates.](https://docs.microsoft.com/en-us/azure/architecture/example-scenario/apps/sap-dev-test)
