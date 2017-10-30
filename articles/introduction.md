# FastTrack for Azure Architectural Discussion Framework

- [FastTrack for Azure Architectural Discussion Framework](#fasttrack-for-azure-architectural-discussion-framework)
  * [Introduction](#introduction)
  * [Gain an understanding into the purpose of the solution](#gain-an-understanding-into-the-purpose-of-the-solution)
  * [Decompose the overall architecture](#decompose-the-overall-architecture)
    + [Whiteboarding Section](#use-a-whiteboard-to-map-out-)
    + [Determine solution specific architectural questions](#once-you-have-a-clear-view-of-your-architecture--determine-the-answer-to-the-following-questions-)
  * [Review the appropriate sections for your solution](#review-the-appropriate-sections-for-your-solution-)
  * [References](#references)

## Introduction
This guide supports discussion duringFast Track for Azure Architectural Guidance sessions. Questions stem from recommended patterns and practices, and link back to technical documentation on Azure.com.

## Gain an understanding into the purpose of the solution

* What is the purpose of the solution from a business perspective? What does it do? Why is it needed?
* What is the origin of the solution? Is it a Lift and Shift, refactored for the cloud, or born in the cloud application?
* What are the availability, uptime and business continuity requirements for the solution?
* Why is an architectural review required? Has there been a recent outage, or is this proactive architectural planning?
* How many users (total and concurrently active will use the solution? How are they geographically distributed?
* How many operations/messages per second must the solution handle? Is there any seasonality to usage of the solution?
* Who designed the solution originally? In-house design, third party?
* Are there any internal policies, legal, or compliance considerations to note as part of your architectural design?

## Decompose the overall architecture

### Use a whiteboard to map out:

* The major components of the solution architecture.
* Note down dependencies for these major components (These can be subtle. For example, dependencies relating to security or identity such as Active Directory for Infrastructure as a Service (IaaS) solutions or third-party services such as a payment provider or e-mail messaging service.
* Detemrine how  dependencies across components and third party services are tied together. For example, E.g. vNet Peering, Express Route, VPN Connections, API calls over public Internet, Loose Coupling.  You don't care so much about the configuration of those resources, e.g. SKU, cost, etc.
* Annotate all components with
	* SLA requirements
	* Geographical locations (Single region / multi-region)
	* Recovery Time Objective (RTO)
	* Recovery Point Objective (RPO)
* Annotate resource and define whether there is some kind of health metric associated. Also determine how this is monitored, for example Application level monitoring, Infrastructure level Monitoring or monitoring of the business processes.

### Once you have a clear view of your architecture, determine the answer to the following questions:

* Is there a single point of failure in any of the components?
* How does the solution scale? How is extra capacity added, and in which situations would this be required? 
* How do transient faults in each component affect the health of the overall solution (including internal or 3rd party dependencies)?
* How do you determine the health of a tier / set of resources?
* Are there any upstream/downstream dependencies of this solution to other customer or 3rd party solutions?
* Additionally, are there workloads within the solution with different RPO/RTO targets?
	* RPO (recovery point objective â€“ how much data can be lost during a failure)
	* RTO (recovery time objective how long can the system take to recover from a failure) targets?
* How big are the largest databases of the solution? Have you considered the annual growth rate?
* What is the  strategy to OS level updates and application updates?

## Review the appropriate sections for your solution:

* [Application Modernisation](application-modernisation.md)
* [Backup, Archive & Disaster Recovery](backup-archive-disaster-recovery.md)
* [Database](database.md)
* [DevTest](devtest.md)
* [Lift and Shift](lift-and-shift.md)

## References
* [Azure Architecture Center](https://docs.microsoft.com/en-us/azure/architecture/)
* [Azure Architecture Center - Design Review Checklist: Availability](https://docs.microsoft.com/en-gb/azure/architecture/checklist/availability)
* [Azure Architecture Center - Design Review Checklist: DevOps](https://docs.microsoft.com/en-gb/azure/architecture/checklist/dev-ops)
* [Azure Architecture Center - Design Review Checklist: Resiliency](https://docs.microsoft.com/en-gb/azure/architecture/checklist/resiliency)
* [Azure Architecture Center - Design Review Checklist: Scalability](https://docs.microsoft.com/en-gb/azure/architecture/checklist/scalability)
