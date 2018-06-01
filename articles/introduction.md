# FastTrack for Azure Architectural Review and Discussion Framework

 - [Introduction](#introduction)
 - [Agenda](#agenda-and-stages)
 	 * [Confirm the Objectives of the Review](#aim-and-confirm-objectives-of-the-review)
  	 * [Confirm Scope and Service Levels to review against](#plan-and-confirm-scope-and-service-levels-to-review-against)
  	 * [Do the Architectural Review](#do-the-architectural-review)
  	 * [Discuss Identified Risks and Links to Azure Docs](#discuss-identified-risks-and-links-to-azure-docs)
  	 * [Additional Assistance Required and Next Steps](#additional-assistance-required-and-next-steps)
- [References](#references)

# Introduction
This guide is intended to support discussions during the Fast Track for Azure Architectural Guidance sessions. The questions being asked  stem from recommended patterns and practices and link back to technical documentation on Azure.com and docs.microsoft.com.

* NOTE: This framework can be applied in a number of ways, by varying the technical depth of conversation by narrowing or widening the solution scope or reducing the amount of time allocated. 

If you have a short amount of time, spend less time on the scoping and requirements, and run a very deep solution area discussion - this would be typical of the style of review at the "Architecture Bars" at Ignite / TechSummit. 

If you have slightly more time, spend longer on the scoping and requirements to allow a broader, more holistic review of the architecture and patterns and practices (the higher you go the more you are likely to see), this is what we would refer to as an "Architectural Review". 

If a "solution review" is required (i.e. of the implementation of a service), then limit the scope to one service area and go deep into it, but beware of going too deeply into one area and doing a different type of review from the one you scope in 'Aim and Confirm objectives of the Review'.

The difference between the two styles is that the "Architecture Review" is looking at the holistic service being deployed, whereas the "solution review" is looking at a much deeper dive into one specific aspect of the service (For example - Database Implementation, or Networking). But the same guidelines to establish the Rules of Engagement and Scoping / objectives can be applied.

Whatever type of review you execute, it is extremely important to ensure that you know which type of review you are doing and why before you begin the exercise. 

# Agenda and Stages 

## Aim and Confirm objectives of the Review

FastTrack for Azure's objectives are below, when reviewing the reviewer should be honest and transparent about them - but the organisation that is engaged for the review will likely have their own idea about why this is required and may have their own objectives and goals to strive to meet. The reviewer should ensure that those reasons are captured for context (if they have not already been captured during scoping).

Examples could be: a prior outage, a migration project to onboard to Azure, a significant increase in scale planned or maybe a production go-live.

### Confidence
Ensure that you have confidence in the Azure platform to meet the needs of your solution based upon an the advice of an Azure Engineering Expert.

### Identify
Pick up on any common errors or common improvement points that can be made to your architecture and direct you to the relevant documentation on patterns or to resolve them.

### Onboarding
Quickly identify and define the scope of the knowledge transfer and MS assistance that you will require to help you to either rapidly move the application yourselves or with a partner / MS Services.

## Plan and Confirm Scope and Service Levels to review against 	

Once there is a joint understanding of why a review is needed, parameters can be set for the review. This is needed, so that the subject of the review (the scope and purposes) meets the success criteria for the relevant stakeholders.

Look for the following information at a minimum: 

### Scope
What solution is being reviewed? What is it called? What are the high level components of the solution that are in-scope of the review?
* What is the purpose of the solution from a business perspective? What does it do? Why is it needed?
* What is the origin of the solution? Is it a Lift and Shift, refactored for the cloud, or born in the cloud application?

### Purposes
What are the high level functional requirements, what does the solution do?
* What are the availability, uptime and business continuity requirements for the solution?
* Why is an architectural review required? Has there been a recent outage, or is this proactive architectural planning?

### Success Criteria
What does the solution need to do to achieve the purposes and how does it need to do it, including availability and non-functional requirements.
* How many users (total and concurrently active will use the solution? How are they geographically distributed?
* How many operations/messages per second must the solution handle? Is there any seasonality to usage of the solution?
* Are there any internal policies, legal, or compliance considerations to note as part of your architectural design?
	
### Stakeholders
Are there other (internal or external) customers involved with an SLA too?
* Who designed the solution originally? In-house design, third party?

## Do the Architectural Review	

This is the main focus of the session. For a "high level" review it is a review of the architecture against the pillars of software quality and will use more of the soft skills that an architect would have. For a "detailed solution" review, the detailed review guidance linked to below may additionally be needed and the activity will use much more of the depth of an engineer's knowledge in a specific area. 

Regardless, of the type of review, the aim for this section is to consider whether the solution would meet the requirements stated and if there are any common pitfalls embedded in the architecture. 

### Review Areas

These are the pillars of software quality we are looking for and areas to look out for regardless of the review type.

* Availability and Resilience 
* Performance and Scalability
* Security and Identity 
* Manageability and Supportability 
* Development, Testing and Deployment (DevOps)
   
### Discovery, if the reviewee has no documentation that follows the below pattern, then ask the customer to use a whiteboard (a digital whiteboard if doing remote delivery, or a physical one if reviewing / assisting at an onsite event) to map out:

* The major services being used and arrangement of components in the architecture.
* Note down what the dependencies are for these major components (These can be subtle. For example, dependencies relating to security or identity such as Active Directory for Infrastructure as a Service (IaaS) solutions or third-party services such as a payment provider or e-mail messaging service, you are looking to discover un-documented dependencies in this stage.
* Determine how dependencies across components and third party services are tied together. For example, E.g. vNet Peering, Express Route, VPN Connections, API calls over public Internet, Loose Coupling.  You don't care so much about the configuration of those resources, e.g. SKU, cost, etc. What you do care about is how those dependencies you discovered in the last section are arranged and communicate with each other.

* Annotate all components with
	* SLA requirements
	* Geographical locations (Single region / multi-region)
	* Recovery Time Objective (RTO)
	* Recovery Point Objective (RPO)
	* Health metrics associated, monitoring processes (for example Application level monitoring, Infrastructure level Monitoring or monitoring of the business processes)

### Once you have a clear view of the architecture, determine the answer to the following questions:

* Is there a single point of failure in any of the components?
* How does the solution scale? How is extra capacity added, and in which situations would this be required? 
* How do transient faults in each component affect the health of the overall solution (including internal or 3rd party dependencies)?
* How do you determine the health of a tier / set of resources?
* Are there any upstream/downstream dependencies of this solution to other reviewee or 3rd party solutions?
* Additionally, are there workloads within the solution with different RPO/RTO targets?
	* RPO (recovery point objective â€“ how much data can be lost during a failure)
	* RTO (recovery time objective how long can the system take to recover from a failure) targets?
* How big is the data set of the solution and is the store architecturally appropriate? Have you considered the annual growth rate and archiving strategy?
* What is the strategy to manage releases, service updates, versioning and application updates, even if PaaS is being used here so there is no patch management concern, DevOps aspects should be briefly considered here.

### Additionally engineers would leverage their own skills for the following two areas if they go deep into a solution area.

* Service Specific Aspects
* Other Observations

### For the Solution / Service  Specific components - ensure you review the appropriate sections for the scenario or area:

* [Application Modernisation](application-modernisation.md)
* [Backup, Archive & Disaster Recovery](backup-archive-disaster-recovery.md)
* [Database](database.md)
* [DevTest](devtest.md)
* [Lift and Shift](lift-and-shift.md)

## Discuss Identified Risks and Links to Azure Docs 

At this point you would review the identified risks and possible enhancements to the architecture with supporting links to patterns and practices or service documentation, these should be recorded for later follow up. 

Consider that what you are really looking for here is a list of what has to be done, by whom, and by when. This is to be phrase as a list of risks and recommendations, backed by links to Azure Docs (for an architectural review - links to patterns, practices, reference architectures, or for the more detailed solution reviews - links to technical service-specific documentation) and QUALIFIED with appropriate SLA's and NFRs discovered earlier. This gives context to the suggestions given – which might be required later. Consider why the recommendations are being provided.

For Example - a solution that has been designed without autoscaling and / or Queuing that the NFR says must cope with high daily spikes in load could have the following links provided (this could be expressed in one of two ways):- 

Risk: Peaks in load could cause service to become overloaded if under-specified for peak performance, consider using autoscaling and / or queue based load leveling techniques in your architecture or use a throttling pattern to keep a minimum level of service with fixed resource. 
NFR = Peak throughput of 10,000 requests at 9am and normal throughput of 100 requests per hour for the rest of the day. 
https://docs.microsoft.com/en-us/azure/architecture/patterns/queue-based-load-leveling
https://docs.microsoft.com/en-us/azure/architecture/patterns/throttling
https://docs.microsoft.com/en-us/azure/architecture/best-practices/auto-scaling

	OR 
	
Risk: Over-specified service sizing could cause excessive cost,  consider using autoscaling and / or queue based load leveling techniques in your architecture or use a throttling pattern to keep a minimum level of service with fixed resource.
NFR = Peak throughput of 10,000 requests at 9am and normal throughput of 100 requests per hour for the rest of the day. 
https://docs.microsoft.com/en-us/azure/architecture/patterns/queue-based-load-leveling
https://docs.microsoft.com/en-us/azure/architecture/patterns/throttling
https://docs.microsoft.com/en-us/azure/architecture/best-practices/auto-scaling

Also consider indirect risks associated with testing (and or lack of it)
Risk: High peak load can stress indirect dependencies in ways that do not show until the service is in full operation under load. Ensure you have load tested the application under the stress of at least 10,000 users using load testing tools.
NFR = Peak throughput of 10,000 requests at 9am and normal throughput of 100 requests per hour for the rest of the day. 
https://docs.microsoft.com/en-gb/vsts/test/load-test/index?view=vsts
https://docs.microsoft.com/en-gb/azure/architecture/checklist/dev-ops#testing

## Additional Assistance Required and Next Steps 	

At this point we are trying to leverage what we have learnt to accelerate the organization's adoption of Azure safely and help them to reach their objectives by using Azure. But if it becomes clear that additional resources, skills and / or experience are needed to help the goals to be achieved, then three approaches make sense :- 

* Advise PaaS services over IaaS
* Self Guided Learning 
* FastTrack for Azure Fundamentals training offerings
* Partner or MS Services Engagements

If the review identified a need for additional engagements or discovered additional workloads, information on these should be fed back to the organization participating in the review.

## References
* [Azure Architecture Center](https://docs.microsoft.com/en-us/azure/architecture/)
* [Azure Architecture Center - Design Review Checklist: Availability](https://docs.microsoft.com/en-gb/azure/architecture/checklist/availability)
* [Azure Architecture Center - Design Review Checklist: DevOps](https://docs.microsoft.com/en-gb/azure/architecture/checklist/dev-ops)
* [Azure Architecture Center - Design Review Checklist: Resiliency](https://docs.microsoft.com/en-gb/azure/architecture/checklist/resiliency)
* [Azure Architecture Center - Design Review Checklist: Scalability](https://docs.microsoft.com/en-gb/azure/architecture/checklist/scalability)
