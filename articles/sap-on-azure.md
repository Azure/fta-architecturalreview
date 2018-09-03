# FastTrack for Azure Architectural Discussion Framework - SAP on Azure Solution


- [FastTrack for Azure Architectural Discussion Framework - Sap on Azure Solution](#fasttrack-for-azure-architectural-discussion-framework---sap-on-azure-solution)
  - [SAP Landscape Design](#sap-landscape-design)
  - [SAP Landscape Sizing](#sap-landscape-sizing)
  - [High Availability and Business Continuity / Disaster Recovery](#high-availability-and-business-continuity--disaster-recovery)
  - [Performance and Scalability](#performance--scalability)
  - [Backup and Archival](#backup--archival)
  - [Migration Methodologies](#migration-methodologies)
  - [Security Design](#security-design)
  - [Monitoring and System Management](#monitoring-and-system-management)
  - [Stories](#stories)

## SAP Landscape Design

- **How is your current SAP Landscape and which systems are you planning to move to Azure?**

    Please provide landscape diagram, Operating system, database details of the SAP environment.
    - [SAP systems which are certified to run on Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/sap-certifications)

- **What are the driving factors for moving to Azure?**
   Determine the customer experience in current envionment and expectations in Azure.
   
- **What are your future roadmap to SAP environment and are there any plans to move to S/4 Hana?**
Projects which are planned in future along with moving to Azure. We can look at overall trransformation strategy for SAP Landscape.

- **Are you hosting it on-premises or partner data centre.  In which region you are planning to host in Azure?**

    - [Worldwide Azure regions](https://azure.microsoft.com/en-us/global-infrastructure/regions/)

## SAP Landscape Sizing

- **Could you provide SAP sizing and exiting hardware specifications?**

SAPS value for the current hardware and SAP quicksizer report will be helpful to determine the target system configuration.  

- **Could you provide SAP Early Watch Report for production systems in the landscape?**

SAP solution manager Early Watch Report provides system usage and performace statistics to eastimate the SAP system design on Azure.

- **What is the current database size of each of the SAP systems and average monthly DB growth?**

Database size will be helpful in determining infrastructure requirement like Storage and VMs for the target design.


## High Availability and Business Continuity / Disaster Recovery

- **What is the availability SLA for SAP production environment. Do you have clustered environment for SAP application & database layer for production systems?**

    Refer to the High Availability & disaster recovery concepts for SAP on Azure.
    - [High Availability Architecture for SAP on Azure ](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/sap-certifications)
    - [Reference architecture design for SAP Netweaver for AnyDB on Azure](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/sap/sap-netweaver)

- **What is the plans for disaster recovery setup. What will be recovery time objective (RTO) and Recovery Point Objective (RPO)?**

    Azure Site recovery will be recommended approach to setup DR for SAP application layer. For Database layer, DB specific setup will be required (like HSR for SAP HANA DB and SQL AlwaysOn for SQL server DB)
    - [Reference design for Azure Site Recovery(ASR) for SAP Netweaver on Azure](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-sap)

## Performance & Scalability

- **What are the performance related SLAs and response time in current production environment?**

    SAP application servers carry on constant communications with the database servers. For performance-critical applications running on any database platforms, including SAP HANA, consider enabling Write Accelerator to improve log write latency. To optimize inter-server communications, use the Accelerated Network. Note that these accelerators are available only for certain VM series.
  
  - [Guidelines for Accelarated Network](https://azure.microsoft.com/blog/linux-and-windows-networking-performance-enhancements-accelerated-networking/)
  - [Write Accelarator for M Series VMs](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/how-to-enable-write-accelerator)
  - [Best Practices for Storage performance optimization](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/premium-storage-performance)

 - **What are the Scalability requirements for SAP workloads?**

    SAP application servers and the Central Services clusters can scale up/down or scale out by adding more instances.
    The database VMs can scale up/down with limitations on maximum size(4TB) of the VM. If your workload exceeds the maximum VM size, Microsoft also offers Azure Large Instances for SAP HANA. 
     
     - [Details about Azure Large Instances](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/hana-overview-architecture)


## Backup & Archival

- **What is the Current Backup Strategy?**

    Determine the type and frequency of backup in current SAP environment. It is strongly recommended to schedule regular data backups from the data area of your SAP HANA database to a secure location. SAP system on Azure Backup guide provides detailed information. 

  - [Backup guide for SAP workload on Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)

- **What are the Data Archiving Strategy?**

    Determine if data archiving in done on a regular basis and how archived data is selected and stored. What is tool used for data archiving. 

## Migration Methodologies

- **Are you planning to change operating system and database of SAP Landscape during migration to Azure?**

    Homogeneous migration can be performed if database and operating systems remains same in new platform.
    Heterogenous migration needs to be performed if there are changes in operating systems OR database. 

- **Determine the high level plan for migration is available and if there are any specific requirement for migration?**

## Security Design
 - **How to control access the different infrastructure resources and segregation of duties?**

    Azure policy and RBAC provides granular level access control for resources.
    - [Best practices for Azure Policy.](https://docs.microsoft.com/en-us/azure/azure-policy/azure-policy-introduction)
    - [Role Based Access control in Azure.](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview)

 - **Determine the proactive steps being taken in maintaining the security of the SAP Landscape?**

    For infrastructure security, data is encrypted in transit and at rest. The "Security considerations” section of the SAP NetWeaver on Azure Virtual Machines (VMs) – Planning and Implementation Guide begins to address network security. The guide also specifies the network ports you must open on the firewalls to allow application communication.
    - [Security considerations of the SAP NetWeaver on Azure Virtual Machines (VMs)](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/planning-guide)

## Monitoring and System Management

- **How do you monitor SAP, database & Infrastructure layers?**
- **How do you determine if there is an outage and what are the alerts which have been setup?**


  Azure provides several functions for monitoring and diagnostics of the overall infrastructure. Also, enhanced monitoring of Azure virtual machines (Linux or Windows) is handled by Azure Operations Management Suite (OMS).
  - [Best practices for Monitoring and Diagnostics in Azure.](https://docs.microsoft.com/en-us/azure/architecture/best-practices/monitoring)

  To provide SAP-based monitoring of resources and service performance of the SAP infrastructure, the Azure SAP Enhanced Monitoring extension is used. This extension feeds Azure monitoring statistics into the SAP application for operating system monitoring and DBA Cockpit functions. SAP enhanced monitoring is a mandatory prerequisite to run SAP on Azure. 
  - [Azure SAP Enhanced Monitoring extension.](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/deployment-guide#d98edcd3-f2a1-49f7-b26a-07448ceb60ca)

- **What is the level of automation in system management and operations?**
  - [Introduction to Azure Automation for system management.](https://docs.microsoft.com/en-us/azure/automation/automation-intro)

## Stories
 - [Top 10 considerations for deploying SAP workloads on SQL server in Azure.](https://blogs.msdn.microsoft.com/saponsqlserver/2015/05/25/top-10-key-considerations-for-deploying-sap-applications-on-azure/)