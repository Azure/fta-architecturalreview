# FastTrack for Azure Architectural Discussion Framework - High Performance Compute

- [FastTrack for Azure Architectural Discussion Framework - High Performance Compute Solutions](#fasttrack-for-azure-architectural-discussion-framework---highperformancecompute-solutions)
    - [Business and Workload Objectives](#business-and-workload-objectives)
    - [Choosing an HPC Solution](#choosing-an-hpc-solution)
    - [Performance and Scalability](#performance-and-scalability)
    - [Data](#data)


## Business and Workload Objectives

- **What are the key objectives, or non-functional requirements, to running your HPC workload in the cloud?**
    Determining the major objectives in a new workload will provide some focus on the solution you need, putting these in priority order will also ensure the right descisions are being made. These could be one or more of the following:

    -   Availability
    -   Performance
    -   Cost
    -   Management
    -   Scalability
    -   Security

- **What are the consequences to the business if the workloads don't complete?**
    
    An example of this is in the Financial sector where there are penalties that can be applied by regulatory bodies in the event reports are late or not being adhered to. HPC workloads will contribute to these reports and could be a blocker if they have failed to run. In these instances, thinking about the resiliancy and how the recovery of a failed run can be mitigated will be a key objective.

- **Are there any SLA's which need to be met for any of the workloads?**
    
    For some customers, there will be an imperative to complete certain workloads within a specific timeframe, this could be down to project deadlines or regulatory requirements. For example providing a set of figures on a daily basis before a certain time is a requirement in the banking sector and has major implications for a business if this fails to materialise. Providing a Proof of Concept which uses different machine SKU's could help choose which would be more suitable for cost and performance needs, while meeting the deadlines. 

    - [Banking Regulations][banking-regs]

## Choosing an HPC Solution

- **Do you already have a Scheduler currently in use which you'd like to continue using?**
    Already having a Scheduler in mind, which is familiar and being used currently, can dictate the solution for an HPC workload in Azure. For instance Azure CycleCloud is predominantly aimed at customers who already use a Scheduler and want a way to orchestrate a new infrastructure they can be familar with, like a lift and shift scenario. The Scheduler determines what jobs are run on which resources, of which there are numerous Schedulers available i.e. slurm, pbs, hpc pack to name but a few. CycleCloud can orchestrate these and more to minimise downtime and management, while also providing autoscale functionality out of the box. In addition to a Scheduler, CycleCloud can also orchestrate File Servers and Applications depending on the needs of the workload

    - [What is CycleCloud?](https://docs.microsoft.com/en-us/azure/cyclecloud/overview)
    - [Installing CycleCloud](https://docs.microsoft.com/en-us/azure/cyclecloud/quickstart-install-cyclecloud)
    - [Full List of Schedulers and Applications supported by CycleCloud](https://github.com/Azure?utf8=%E2%9C%93&q=cyclecloud&type=&language=)

- **What if you don't have a Scheduler in mind or you want to modernise a workload without requiring a specific Scheduler?**
    Managing an HPC infrastructure can incur overhead and complexity for those customers who just want to run a workload without the additional steps to create clusters and HPC solutions. Azure Batch provides a managed infrastructure which is solely focussed on a workloads' needs, where updating the application, on-demand scaled compute, and job/task submission are provided natively.

    - [What is Azure Batch?](https://docs.microsoft.com/en-us/azure/batch/batch-technical-overview)


## Performance and Scalability

- **What compute node size will be required for the applications?**

    Azure provides access to a large number of machines sizes, some of which are specific to HPC due to specialsed hardware (RDMA for MPI), whereas others can be used for general compute purposes:

    - High Performance Compute: The latest in high performance computing VMs aimed at handling HPC workloads - batch processing, analytics,         molecular modeling, and fluid dynamics with RDMA for MPI workloads
    - Compute Optimised: Up to 72 core VMs available with Fsv2 and Premium Storage, cost effective for general compute needs
    - GPU Optimised: VM sizes are specialized virtual machines available with single or multiple NVIDIA GPUs. RDMA options available
    - General Purpose: Broad range of machines with a balanced CPU to Memory ratio, ideal for testing and development
    - Memory Optimsed: Offering a set of high memory to CPU ratio machines, over 3TB of memory is available for the M series
    - Storage Optimised: Offering high disk throughput and IO, and are ideal for Big Data, SQL, and NoSQL databases
  
    Each of the above can be used across the HPC solutions that Azure provides: 

    - [Azure Cycle Cloud](https://docs.microsoft.com/en-us/azure/cyclecloud/overview)
    - [Azure Batch](https://docs.microsoft.com/en-us/azure/batch/)
    - [HPC Pack](https://docs.microsoft.com/en-us/powershell/high-performance-computing/overview?view=hpc16-ps)
    - [Virtual Machine Scale Sets](https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/overview)
    - 

    Baselining and testing performance across the different SKU sizes will be important to get an idea as to how applications will run and what the best cost effective approach is versus the speed at which workloads can complete

    - [High Performance Compute](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes-hpc) 
    - [Compute Optimised](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes-compute)
    - [GPU Optimised](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes-gpu)
    - [General Purpose](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes-general)
    - [Memory Optmised](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes-memory)
    - [Storage Optmised](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes-storage)

- **Is there any seasonality or general autoscaling that needs to be factored into the solution?**

    Scaling based on demand, whether it's from the business or a customer, requires a solution which can adapt and provide compute as and when is needed. The HPC solution you choose will have an effect on how this can be achieved, where an ideal situation is to have this fully automated but with a degree of control to ensure projected costs are not exceeded. 

    - [Azure CycleCloud Auto-Scale](https://docs.microsoft.com/en-us/azure/cyclecloud/autoscale)
    - [Azure Batch Autoscaling](https://docs.microsoft.com/en-us/azure/batch/batch-automatic-scaling) 
    - [Virtual Machine Scale Sets - Autoscaling](https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview)
    - [Automatically grow and shrink the HPC Pack cluster resources](https://docs.microsoft.com/en-us/powershell/high-performance-computing/hpcpack-auto-grow-shrink)
 

- **Can the application make use of Low Pirority VM's to reduce costs?**

    Low-Priority Virtual Machines are available in Azure to reduce the cost of workloads on Azure Batch and CycleCloud, depending on the type of workload being used. Low Proority offers as much as a 60% discount for Windows and 80% for Linux, with the caveat that there is no SLA for these VM types as this comprises surplus compute which can be reassigned at any time and therefore there is no guarantee these will available in the first place. 

    As a result, the workloads which would be suitable have to withstand the compute being recsinded at any time, please check the following link to determine if your workload meets the needs of Low Priority:

    - [Use cases for Low Priority VMs](https://docs.microsoft.com/en-us/azure/batch/batch-low-pri-vms#use-cases-for-low-priority-vms)

    - [Using Low Priority VMs with Azure Batch][batch-lowpri]
    - [VM Scale Sets and Low Priority VMs][vmss-lowpri]
    

- **Is the required hardware available in your region of choice?**

    While there may be a preferred SKU of choice for your workload, making sure this is also in the region where you want to deploy will be important. Check which regions support the compute you want in the link below.


    - [Virtual Machine products by region](https://azure.microsoft.com/en-us/global-infrastructure/services/?products=virtual-machines)

- **Capacity Requirements: How many cores do the workloads require?**

    Capacity planning is something Microsoft takes very seriously, as we want to ensure all our customers are able to run their workloads as expected and have access to the on-demand compute when its needed. For those customers that are looking to deploy thousands or hundreds of thousands of cores, making sure we can accomodate your current and future growth requests we ideally would like to know ahead of time. 

    Please let us know your core quota requests by using the Azure Portal to update your requirements

    - [Quota Increase Request](https://docs.microsoft.com/en-us/azure/azure-supportability/resource-manager-core-quotas-request)


## Data

- **Does the data for the workloads already reside in Azure? How will this be accessed?**

    If your data is already in Azure, making this available to your workloads running in Azure will be fairly straight forward, but for those where the data resides elsewhere some thought will be required as to how this will be accessed or staged in Azure. Several solutions are available depending on the I/O speed required for file access:

    Staging Data
    - [Data Factory Copy](https://docs.microsoft.com/en-us/azure/data-factory/copy-activity-overview)
    - [AZCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy)
    - [Azure Data Box Services](https://docs.microsoft.com/en-gb/azure/databox-family/)
    - [Data Transfer with CycleCloud](https://docs.microsoft.com/en-us/azure/cyclecloud/data-overview)
    - [Storage Migration FAQs](https://docs.microsoft.com/en-us/azure/storage/common/storage-migration-faq)

    Solutions for Accessing Data in Azure
    - [Mount blob storage on Linux](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-how-to-mount-container-linux)
    - [Avere vFXT for Azure](https://docs.microsoft.com/en-us/azure/avere-vfxt/avere-vfxt-overview)
    - [Azure NetApp Files](https://docs.microsoft.com/en-us/azure/azure-netapp-files/azure-netapp-files-introduction)
    - [Running Parallel File Systems in Azure](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
    


- **Does the data need to be transformed before or after the workload has run?**

    If the workload you're running is being exported from other systems or pipelines, there could be some data transformation that's required before the HPC application is able to use that data as intended. 

    - [Data Processing with Batch and Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/transform-data-using-dotnet-custom-activity?toc=%2fazure%2fbatch%2ftoc.json)


## High Availability

- **Do you need the HPC solution to be highly available?**
    Thnking about what would happen if the HPC infrastructure had a failure of some kind and wasn't able to ulfill the required workloads could potentially have a mojor impact if its part of a business critical system or solution. Ensuring you're able to get back up and running or switch across to a standby server would provide the piece of mind and ability to provide a highly available service. 

    - [Azure Batch and HA](https://docs.microsoft.com/en-us/azure/batch/high-availability-disaster-recovery) 

    - [Backup and Restore of CycleCloud](https://docs.microsoft.com/en-us/azure/cyclecloud/cyclecloud-references/backup-and-restore)



<!--- Links
--->
[batch-lowpri]:https://docs.microsoft.com/en-us/azure/batch/batch-low-pri-vms
[vmss-lowpri]:https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-use-low-priority
[banking-regs]:https://www.hpcwire.com/solution_content/ibm/financial/enabling-banks-to-meet-new-financial-risk-regulations-and-more/




