# FastTrack for Azure Architectural Discussion Framework

- [FastTrack for Azure Architectural Discussion Framework](#fasttrack-for-azure-architectural-discussion-framework)
  * [Introduction](#introduction)
  * [Rules of Engagement](#rules-of-engagement)
    + [Focus on](#focus-on)
    + [Avoid](#avoid)
    + [Steps](#steps)
    + [Engagement Output](#engagement-output)
  * [Review the appropriate sections for your solution](#review-the-appropriate-sections-for-your-solution-)
  * [References](#references)

## Introduction
This guide supports discussion during FastTrack for Azure Architectural Guidance/Review sessions. Questions stem from recommended patterns and practices, and link back to technical documentation on Azure.com.

## Rules of Engagement
### Keep in mind the FastTrack charter
* We need customers to be knowledgeable, and feel confident and supported in building (and betting) their businesses on Azure
* Generic cloud concerns - it is up to the IT Directors and/or Dev/Ops leaders to come up with the game plan to move from on-premises to the cloud. Concerns around security, integration, reliability, compliance and other areas, need to be addressed before any broad scale deployments take shape
* Take a solution centric approach

### Focus on
* Business requirements, Goals, and Objectives
  * Non Functional Requirements
    * SLAs / RTO / RPO / Cost of down time
    * Availability, uptime, business continuity, geographic (single vs. multi-region)
  * Purpose of the solution, what does it do? Why is it needed?
  * Why is an architectural review required? Has there been a recent outage, or is this proactive architectural planning?
  * Total number of users (total and concurrently active) and geographical distributed
  * Internal policies, legal, or compliance considerations
* High level technical design
  * What are the major components
    * Internal to the solution and 3rd party
  * Dependency map
    * Across components and 3rd party services
* Strategic dicussion
* Publicly documented recommended practices and design principles
* Work top down - start high level and make your way down to the technical details

### Avoid
* Low level technical requirements (don’t go into the weeds)
* Tactical discussion
  * Stay high level, and do not get distracted by deep amounts of detail. Remain focused on the priorities which the customer has defined. (be aware of tips and tricks, e.g. parking lot)
  * Red Flag: If there are customer-initiated questions that go into detailed design questions, is there an engagement that could help them?
* Deep design or specific configuration points
* Ambiguity - make no assumptions. If the customer answers in a vague way, ask them to confirm what they mean

### Steps
* Step 1 - Define Goals & Objectives
What is the vision for the end state
  * Focus is on creating clear definitions of the problem/goals and understanding the high level approach to solving the problem
  * Ensure a common vision and reach consensus among the team members

* Step 2 - Identify Business Goals (Non-Functional Requirements)
Vision for the end state driven by:
  * High level requirements, business goals
    * Reduce TCO (hardware, reliability, etc)
    * Maximize ROI
  * Design goals
    * High availability and reliability (improve SLA), robust security, high performance and scalability, consolidation of servers, single points of failure/transient faults, health, etc
  * Scope
  ** A common way of gathering and analyzing information is through developing use-cases and building usage scenarios to document the business processes and user requirements. While use cases describe the high level interactions between an individual and the system, usage scenarios provide additional information about the activities and task sequences that constitute a process

* Step 3 - High-Level Techical Design (dependency map)
  * Solution concept
    * Outlines the high level approach the team will take for all components of the system (includes a high level solution design strategy)
    * Includes assessment of technologies (the solution concept focuses on the concepts and not the details)
    * Factors to consider – business needs, technical feasibility, time/budget

* Step 4 - Solution Specific Questions
Assess architecture proposed by customer
  * Application (migration (lift/shift), modernization, etc)
    * Does the app interoperate with other apps/systems - where are they located
  * Database (migration)
    * What specialized features are used
    * Shared by multiple apps
  * Infrastructure
    * Compute, storage, network and connectivity, identity
    * What are the 'abilities' needed? Availability, scalability, manageability, security
  * Users - who are they and how will they consume the service

### Engagement Output
Stay high level, and do not get distracted by deep amounts of detail. Remain focused on the priorities which the customer has defined
* Refer the customer to public available documentation, and guide the customer as appropriate. Do not provide customised reports, or deeps amount of detail relating to specific configurations of their solution
* Advise the customer on matters relating to the deployment / migration. For example, has the customer load tested? If so, is this in relation to their current level of expected load? If yes, does this also take into account the business’ future plans for growth?

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
