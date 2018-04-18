# FastTrack for Azure Architectural Discussion Framework - Backup, Archive and Disaster Recovery Solution

- [FastTrack for Azure Architectural Discussion Framework - Backup, Archive and Disaster Recovery Solution](#fasttrack-for-azure-architectural-discussion-framework---backup--archive-and-disaster-recovery-solution)
  * [Business Objectives](#business-objectives)
  * [Workload Considerations](#workload-considerations)
  * [Hybrid Architecture](#hybrid-architecture)
  * [Monitoring &amp; Management](#monitoring--amp--management)
  * [Performance &amp; Scalability](#performance--amp--scalability)
  * [Security](#security)
  * [Understand the Portfolio of applications are supported for Disaster Recovery](#understand-the-portfolio-of-applications-are-supported-for-disaster-recovery)

## Business Objectives

* **What are your defined Recovery Point Objectives (RPOs), Recovery Time Objectives (RTOs) and Service Level Agreement (SLAs)?**

    Varying RPOs, RTOs and SLAs will have an impact upon your choice of Azure services, 3rd party services and software design choices. For example, a lower RTO will influence bandwidth requirements and technology choice. From a Disaster Recovery perspective, your RPO and RTO will determine whether you are aiming for a hot or warm Disaster Recovery solution. A strict availability SLA will determine your high availability requirements, and decision to deploy across data centers or Azure regions. 

    > [Disaster recovery for Azure applications](https://docs.microsoft.com/en-us/azure/architecture/resiliency/disaster-recovery-azure-applications)

* **Who makes the decision to commit to a failover?**

    When building any solution (on-premises or cloud), people and process is a key part of the overall solution’s success. In the unlikely event that a failover is required, who is responsible for making that decision? 

    If it is unclear who is responsible for the processes and procedures for Disaster Recovery, then this should be defined as a high priority to move forward with a successful Azure Site Recovery implementation. 

    Once the project is live, you should regularly review and test your Disaster Recovery Plan and update the list of stakeholders who are authorized to make the call to initiate a failover. 

* **Do you have a defined Disaster Recovery plan today?**

    Having a Disaster Recovery plan defined for your on-premises computing systems gives you a baseline in determining your Disaster Recovery needs in the cloud. However, some of these steps may be manual and prone to errors. Azure has built in capabilities to help you in automating such steps as part of your Disaster Recovery process. 

    Consider Recovery Plans in Azure, as this can help automate, orchestrate and document failover steps to ensure a successful Disaster Recovery solution without manual interaction post failover. 

    > [Create and customize recovery plans](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-create-recovery-plans)

* **Do you test and validate your Disaster Recovery plans today?**

    Having a Disaster Recovery plan defined is a good initial step, though you also need to have the confidence that the plan itself is valid and will provide you with the ongoing level of service that you are expecting. 

    Consider utilizing an environment to conduct regular effective testing within Azure without impacting production deployments, to help provide confidence that your steps should work in the event of a real scenario. 

    > [Test failover to Azure in Site Recovery](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-test-failover-to-azure)

* **Have you planned for capacity and scale of the infrastructure needed to support Disaster Recovery?**

    It is important to be sure there is sufficient network bandwidth, and the necessary on-premises and target environment infrastructure to support the protection of workloads. 

    > [Plan capacity and scaling for VMware replication with Azure Site Recovery](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-plan-capacity-vmware)

## Workload Considerations

* **What does your on-premises infrastructure look like? Hyper-V, VMware, Baremetal, etc?**

    The makeup of your on-premises estate, and specifically the virtualization technology (if any), will guide the migration options onto Azure.   
    
    > [What workloads can you protect with Azure Site Recovery?](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-workload)
    > 
    > [Hyper-V to Azure replication architecture](https://docs.microsoft.com/en-us/azure/site-recovery/hyper-v-azure-architecture)
    > 
    > [VMware to Azure replication architecture](https://docs.microsoft.com/en-us/azure/site-recovery/vmware-azure-architecture)
    > 
    > [Physical server to Azure replication architecture](https://docs.microsoft.com/en-us/azure/site-recovery/physical-azure-architecture)

* **What Operating System (OS) do you use?**

    OS specific dependencies will influence your available migration paths. For example, Azure Site Recovery supports specific guest OS versions    
    
    > [Support for replicated machine OS versions](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-support-matrix-to-azure#support-for-replicated-machine-os-versions)

* **What workloads will you protect?**

    Document existing workloads and their dependencies, both inter-workload and on-premises. Some workloads have been tested and documented as supported by Microsoft.    
    
    > [Site recovery workload summary](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-workload#workload-summary)

## Hybrid Architecture   

* **Are you looking at Disaster Recovery between on-premises to Azure or Azure to Azure?**

    Azure can be used as your primary site, DR site, or even both.    
    
    > [What can you replicate with Site Recovery](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-overview#what-can-i-replicate)

* **Do you need to protect workloads to a physically separate location?**

    Azure Site Recovery can replicate workloads across regions, and Azure Backup can store data in Geo-Redundant Storage    
    
    > [Set storage replication](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-first-look-arm#create-a-recovery-services-vault-for-a-vm#set-storage-replication)
    > 
    > [Replicate an Azure VM to another Azure region](https://docs.microsoft.com/en-us/azure/site-recovery/azure-to-azure-quickstart)

* **Is failback required from Azure to on-premises?**

    If your primary site comes back online after a DR situation, you may require additional infrastructure to handle the failback process. 

    > [Failback from Azure to an on-premises site (VMWare/Physical)](https://docs.microsoft.com/en-us/azure/site-recovery/vmware-azure-failback) 
    > 
    > [Failback from Azure to an on-premises site (Hyper-V)](https://docs.microsoft.com/en-us/azure/site-recovery/hyper-v-azure-failback)

* **For backups, are you protecting workloads in Azure or only on-premises?**

    Azure Backup Server may be required to protect workloads on-premises 

    > [Which Azure backup components should I use?](https://docs.microsoft.com/en-us/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use)

## Monitoring & Management   

* **What metrics do you gather today around  replication?**
* **What metrics do you gather today around   backups?**

    Determine those metrics and monitoring information that you require to evaluate the operational health of your Disaster Recovery and backup strategy, assess this against the capabilities of the service that you are planning to adopt. 

    For example, your requirements may determine that configuring reports for Azure Backup is sufficient, or utilizing advanced reporting in Azure Backup to augment your existing monitoring solution     
    > [Monitoring and troubleshooting Azure Site Recovery](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-monitor-and-troubleshoot)
    > [Configure Azure Backup reports](https://docs.microsoft.com/en-us/azure/backup/backup-azure-configure-reports)

## Performance & Scalability   

* **Have you run the capacity planning tools?**

    If you are targeting a hybrid architecture, then you should consider the capacity requirements between your live and DR sites. Are you comfortable that you have sufficient bandwidth to adhere to your DR strategy? 
    
    Consider running these tools as the first step in right-sizing Azure Site Recovery for an environment both on-premises and in Azure.     
    
    > [Azure Site Recovery Deployment Planner for VMware to Azure](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-deployment-planner)
    > 
    > [Azure Site Recovery Deployment Planner for Hyper-V to Azure](https://docs.microsoft.com/en-us/azure/site-recovery/hyper-v-deployment-planner-overview)

* **How do you handle backup of data today?**

    Consider again whether you are comfortable that you have sufficient bandwidth to adhere to your backup strategy, without compromising the bandwidth of other on-premises services. 

    Additionally, offline backups to Azure via Import/Export service may need to be considered based upon the volume of data.
    
    > [Offline-backup workflow in Azure Backup](https://docs.microsoft.com/en-us/azure/backup/backup-azure-backup-import-export)

## Security   

* **What are your requirements for encryption? Is there a requirement for customer-managed keys vs. Microsoft-managed keys?**

    A common requirement is for disks to be encrypted. You should consider the level of encryption that is needed (bring your own keys vs. Microsoft-managed keys). 
    
    You should determine at an overall solution level whether the extra management overhead and complexity is required for bringing your own keys, or whether Microsoft-managed keys would be suitable.     
    
    > [Back up and restore encrypted virtual machines with Azure Backup](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption)
    > 
    > [Restore Key Vault key and secret for encrypted VMs using Azure Backup](https://docs.microsoft.com/en-us/azure/backup/backup-azure-restore-key-secret)
    > 
    > [Storage Service Encryption using customer-managed keys in Azure Key Vault](https://docs.microsoft.com/en-gb/azure/storage/common/storage-service-encryption-customer-managed-keys)

* **Who has access to backups today?**

    Regularly review those RBAC rules that are needed to the backups and associated resource locks. This will help protect a backup solution being removed accidentally or maliciously.     
    
    > [Azure enterprise scaffold - prescriptive subscription governance](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-governance#role-based-access-control)
    > 
    > [Use Role-Based Access Control to manage Azure Backup recovery points](https://docs.microsoft.com/en-us/azure/backup/backup-rbac-rs-vault)
    > [Lock resources to prevent unexpected changes](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-lock-resources)

* **Do you leverage Multi Factor Authentication (MFA) today?**

    Consider this as part of your wider solution requirements. What is the risk of a compromised account with access to your Azure Resources? 

    You should consider leveraging Multi Factor Authentication to add an extra layer of protection against malicious activity on Azure subscriptions.   
    
    > [Azure identity management security overview](https://docs.microsoft.com/en-us/azure/security/security-identity-management-overview)

## Understand the Portfolio of applications are supported for Disaster Recovery  

* **What workloads do you plan to protect?**

    Gain an understanding of what needs to be secured. Use the associated documentation to determine those which are supported.    
    
    > [https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-workload#workload-summary](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-workload#workload-summary)
