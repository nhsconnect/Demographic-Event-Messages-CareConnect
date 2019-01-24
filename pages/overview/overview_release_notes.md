---
title: Release Notes
keywords: development, versioning
tags: [development]
sidebar: overview_sidebar
permalink: overview_release_notes.html
summary: Summary release notes of the versions released in Demographic Update Event Messages Implementation Guide
---

This site is under active development by NHS Digital and is intended to provide guidance and FHIR components for the Demographic Update Event Messages. This project is being developed using an agile methodology so iterative updates to content will be added on a regular basis, and remains subject to clinical review. Changes to this specification following the initial beta release will be documented here.

## 1.2.1-RC (23/01/2019) ##

[PDS Change of GP](explore_pds_change_of_gp.html)
- Updated the MESH WorkflowID


## 1.2.0-Beta (11/01/2019) ##

[PDS Birth Notification](explore_pds_birth_notification.html)
- Update of page format with additional detail on the resource population and message structure
- Added introductory paragraph about trigger for event message from Spine
- Added details related to MESH WorkflowID for this event message

[PDS Change of Address](explore_pds_change_of_address.html)
- Added introductory paragraph about trigger for event message from Spine
- Added details related to MESH WorkflowID for this event message

[PDS Change of GP](explore_pds_change_of_gp.html)
- Added introductory paragraph about trigger for event message from Spine
- Added details related to MESH WorkflowID for this event message

[PDS Death Notification](explore_pds_death_notification.html)
- Renamed from `PDS Person Death`
- Added introductory paragraph about trigger for event message from Spine
- Added details related to MESH WorkflowID for this event message


## 1.1.0-Beta ##

**About** - renamed to **Contact Us** - this page has been updated to share contact information. Guidance around FHIR profiles for event messages has been removed as it is not within the scope of this Implementation Guide. 

***Messaging Architecture** this section has been updated to refer to the central guidance in the [Events Management Service Implementation Guide](https://developer.nhs.uk/apis/ems-beta/).

**Overview** text edited to refer to Implementation Guides and not specifications. 

The EMS Event Message Bundle Structure page has been update to include clarification on the use of absolute URL references to Organization resources via the [FHIR ODS Lookup API](https://developer.nhs.uk/apis/ods).

**PDS Change of GP, PDS Change of Address, PDS Person Death**

These event pages have been updated to include elaboration of use cases that may apply and the FHIR representation to support them.

**PDS Birth Notification**
- Delivery Place Type - change from Mandatory to Required
- The patient focus for the event message has been changed to use [CareConnect-EMS-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-Patient-1) to represent the mother, to support birth notification subscriptions. Additionally, the [EMS-PDS-RelatedPerson-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-PDS-RelatedPerson-1) profile is in use to represent the relationship with the baby patient resource.


**Error Handling**

Following stakeholder feedback and INTEROPen curation, this implementation guidance has been updated as follows:

- Following INTEROPen curation, the following Level 3 profiles have been removed and replaced with Level 2 CareConnect profiles:
	- CareConnect-EMS-Organisation-1
	- CareConnect-EMS-Practitioner-1
	- CareConnect-EMS-PractitionerRole-1

**Examples** 
- all relevant example instances updated to reflect all of the changes above.

## 1.0.1-Beta ##
This implementation guide has been updated to include a guidance page for accessing example messages.
 
## 1.0.0-Beta ##
This Beta release includes implementation guidance to support the development of the Demographic Update Event Messages.


