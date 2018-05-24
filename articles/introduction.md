# FastTrack for Azure Architectural Review and Discussion Framework

 - [Introduction](#introduction)
 - [Agenda](#agenda-and-stages)
  * [Confirm the Objectives of the Review](1-Aim-and-Confirm-objectives-of-the-Review)
  * [Confirm Scope and Service Levels to review against](#2-Plan-and-Confirm-Scope-and-Service-Levels-to-review-against)
  * [Do the Architectural Review](#3-Do-the-Architectural-Review)
  * [Discuss Identified Risks and Links to Azure Docs](4-Review-and-Discuss-Identified-Risks-and-Links-to-Azure-Docs)
  * [Additional Assistance Required and Next Steps](5-Aim-with-Additional-Assistance-Required-and-Next-Steps)
- [References](#references)

# Introduction
This guide supports discussion during Fast Track for Azure Architectural Guidance sessions. Questions stem from recommended patterns and practices, and link back to technical documentation on Azure.com.

The general structure of a formal review can be seen in ppt format in the Delivery Deck with rough timings for the sections.

* NOTE: This framework can be applied in a number of ways, all that needs to happen is that you can vary the technical depth of conversation by narrowing or widening the solution scope or reducing the amount of time allocated. 

If you have a short amount of time, spend less time on the scoping and requirements, and run a very deep solution area discussion - this would be typical of the style of review at the "Architecture Bars" at Ignite / TechSummit. 

If you have slightly more time, spend longer on the scoping and requirements to allow a broader, more holistic review of their architecture and patterns and practices - the higher you go the more you are likely to see, this is what we would refer to as an "Architectural Review". 

If the customer wants a "Solution Review" (i.e. of their implementation of a service), then limit the scope to one service area and go deep into it, but beware of being pulled into the weeds and doing a different type of review from the one you scope in Section 1.

Whatever type of review you execute, ensure that you know which one you are doing and why. 

# Agenda and Stages 

## 1 Aim and Confirm objectives of the Review

FastTrack's objectives are below, be honest and transparent about them - but the customer will likely have their own idea about why this is required - ensure that they are captured for context if they have not already been. i.e. Was there a prior outage, a migration project to onboard to Azure, is there a significant increase in scale planned, or maybe a production go-live is planned?

### Confidence
Ensure that you have confidence in the Azure platform to meet the needs of your solution based upon an the advice of an Azure Engineering Expert.

### Identify
Pick up on any common errors or common improvement points that can be made to your architecture and signpost you to the relevant documentation to resolve them.

### Onboarding
Quickly identify and define the scope of the knowledge transfer and MS assistance that you will require to help you to either rapidly move the application yourselves or with a partner / MS Services.

## 2 Plan and Confirm Scope and Service Levels to review against 	

Once we understand why we need a review, we can set the parameters for what we are reviewing and what we are reviewing against, we need to know this so we can ensure that the subject of the review (the scope and purposes) meets the success criteria for the relevant stakeholders.

Look for the following information at a minimum 

### Scope
What solution are we reviewing? What is it called?

### Purposes
What are the high level functional requirements, what does the solution do?

### Success Criteria
What does the solution need to do to achieve the purposes and how does it need to do it, including availability and non-functional requirements.
	
### Stakeholders
Are there other (internal or external) customers involved with an SLA too?
	
Here are some more sample questions to ask to help with item 2 in order to gain an understanding into the purpose of the solution

	* What is the purpose of the solution from a business perspective? What does it do? Why is it needed?
	* What is the origin of the solution? Is it a Lift and Shift, refactored for the cloud, or born in the cloud application?
	* What are the availability, uptime and business continuity requirements for the solution?
	* Why is an architectural review required? Has there been a recent outage, or is this proactive architectural planning?
	* How many users (total and concurrently active will use the solution? How are they geographically distributed?
	* How many operations/messages per second must the solution handle? Is there any seasonality to usage of the solution?
	* Who designed the solution originally? In-house design, third party?
	* Are there any internal policies, legal, or compliance considerations to note as part of your architectural design?

## 3 Do the Architectural Review	

Here we are performing the meat of the actual review, for a high level review we are simply reviewing architecture against the pillars of software quality, for a detailed solution review we would hit our detailed review guidance and use much more depth of engineer knowledge. The end game for this section is to review whether the solution would meet the requirements stated and if there are any common gotchas embedded in the architecture. 

### Review Areas

These are the pillars of software quality we are looking for and areas to look out for regardless of the review type.

	* Availability and Resilience 
	* Performance and Scalability
	* Security and Identity 
	* Manageability and Supportability 
	* Development, Testing and Deployment (DevOps)
   
### Discovery, if the customer has no documentation that follows the below pattern, then use a whiteboard to map out:

	* The major components of the solution architecture.
	* Note down dependencies for these major components (These can be subtle. For example, dependencies relating to security or identity such as Active Directory for Infrastructure as a Service (IaaS) solutions or third-party services such as a payment provider or e-mail messaging service.
	* Detemrmine how dependencies across components and third party services are tied together. For example, E.g. vNet Peering, Express Route, VPN Connections, API calls over public Internet, Loose Coupling.  You don't care so much about the configuration of those resources, e.g. SKU, cost, etc.
	
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
	* What is the strategy to OS level updates and application updates?

### Additionally engineers would leverage their own skills for the following 2 areas if they go deep into a solution area.
   
   	* Service Specific Aspects
   	* Other Observations

### For the Solution / Service  Specific components - ensure you review the appropriate sections for your solution:

	* [Application Modernisation](application-modernisation.md)
	* [Backup, Archive & Disaster Recovery](backup-archive-disaster-recovery.md)
	* [Database](database.md)
	* [DevTest](devtest.md)
	* [Lift and Shift](lift-and-shift.md)

## 4 Review and Discuss Identified Risks and Links to Azure Docs 

At this point you would read back to the customer identified risks and possible enhancements to their architecture with supporting links to patterns and practices or service documentation, these should be recorded in the Engagement system for later follow up. 

## 5 Aim with Additional Assistance Required and Next Steps 	

If the review identified a need for additional engagements or discovered additional workloads, then this should be fed back to the Lead Engineer and PM for scheduling and pickup.

At this point we are trying to leverage what we have learnt to accelerate the customer and help them to reach their objectives by using azure.

## References
* [Azure Architecture Center](https://docs.microsoft.com/en-us/azure/architecture/)
* [Azure Architecture Center - Design Review Checklist: Availability](https://docs.microsoft.com/en-gb/azure/architecture/checklist/availability)
* [Azure Architecture Center - Design Review Checklist: DevOps](https://docs.microsoft.com/en-gb/azure/architecture/checklist/dev-ops)
* [Azure Architecture Center - Design Review Checklist: Resiliency](https://docs.microsoft.com/en-gb/azure/architecture/checklist/resiliency)
* [Azure Architecture Center - Design Review Checklist: Scalability](https://docs.microsoft.com/en-gb/azure/architecture/checklist/scalability)
