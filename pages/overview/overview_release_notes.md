---
title: Release Notes
keywords: development, versioning
tags: [development]
sidebar: overview_sidebar
permalink: overview_release_notes.html
summary: Summary release notes of the versions released in Demographic Update Event Messages Implementation Guide
---

This site is under active development by NHS Digital and is intended to provide guidance and FHIR components for the Demographic Update Event Messages. This project is being developed using an agile methodology so iterative updates to content will be added on a regular basis, and remains subject to clinical review. Changes to this specification following the initial beta release will be documented here.

## Beta 1.1.0 ##

**About** - renamed to **Contact Us** - this page has been updated to share contact information. Guidance around FHIR profiles for event messages has been removed as it is not within the scope of this Implementation Guide. 

**Event Header Design** renamed to **Event Header Information** - this page has been updated to include references to FHIR profiles in use, and include further clarification.

**Overview** text edited to refer to Implementation Guides and not specifications. 

The EMS Event Message Bundle Structure page has been update to include clarification on the use of absolute URL references to Organization resources via the [FHIR ODS Lookup API](https://developer.nhs.uk/apis/ods).

**PDS Change of GP**

- Business Effective from date - change from Mandatory to Required 
- System Effective from date - change from Mandatory to Required

**Error Handling**

The specification has been updated to include guidance on [Error Handling](explore_errors.html).

Following stakeholder feedback and INTEROPen curation, this implementation guidance has been updated as follows:

- Following INTEROPen curation, the following Level 3 profiles have been removed and replaced with Level 2 CareConnect profiles:
	- CareConnect-EMS-Organisation-1
	- CareConnect-EMS-Practitioner-1
	- CareConnect-EMS-PractitionerRole-1

**Examples** 
- all relevant example instances updated to reflect all of the changes above.

Added page [Versioning](explore_event_versioning.html) to clarify versioning of event instances and event definitions.

## Beta 1.0.1 ##
This implementation guide has been updated to include a guidance page for accessing example messages.
 
## Beta 1.0.0 ##
This Beta release includes implementation guidance to support the development of the Demographic Update Event Messages.


