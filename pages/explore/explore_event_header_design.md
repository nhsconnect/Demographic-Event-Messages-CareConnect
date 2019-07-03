---
title: PDS Event Header Design
keywords:  messaging, bundles
tags: [fhir,messaging]
sidebar: foundations_sidebar
permalink: explore_event_header_design.html
summary: "The standard event header information applicable to Patient Demographics Service (PDS) event messages"
---

## Event header information ##
Each event message will carry a standard set of event header information to help identify the patient, publisher, actual event, etc.

The following FHIR profiles are used to form the Event Header within the Event Message Bundle:

- [Event-MessageHeader-1](https://fhir.nhs.uk/STU3/StructureDefinition/Event-MessageHeader-1)
- [CareConnect-Communication-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Communication-1)
- [CareConnect-Patient-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Patient-1)
- [CareConnect-Organization-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Organization-1)
- [CareConnect-HealthcareService-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-HealthcareService-1)

## Header Structure

Specifies mandatory referencing within the Event Message Bundle.

<div style="text-align:center; margin-bottom:20px" >
	<a href="images/explore/pds_header.png" target="_blank"><img src="images/explore/pds_header.png"></a><br/>
	PDS Event Header <a href="images/explore/pds_header.png" target="_blank">(open in new TAB)</a>
</div>

## Data Item to FHIR mapping ##

The Event Header must be populated with the following **mandatory** data items, mapped to the relevant FHIR resource and element:

| Event Header item requirement          | FHIR resource                     | FHIR element                       | Additional Guidance                     |
|----------------------------------------|-----------------------------------|------------------------------------|-----------------------------------------|
| **Patient identification data:**       |
| NHS Number                             | CareConnect-Patient-1             | identifier                         | using NHS Number slice                 |
| Date of Birth                          | CareConnect-Patient-1             | birthDate                          |                                        |
| Name                                   | CareConnect-Patient-1             | name                               |                                        |
| **Event metadata:**                    |
| Event type                             | Event-MessageHeader-1             | event                              |                                        |
| type of service originating the event  | CareConnect--HealthcareService-1  | type                               |                                        |
| service provider originating the event | CareConnect-Communication-1       | sender                             |                                        |
| IT system holding the event data       | Event-MessageHeader-1             | source                             |                                        |
| event publisher                        | Event-MessageHeader-1             | responsible                        |                                        |
| event published date                   | Event-MessageHeader-1             | timestamp                          |                                        |
| publication reference number           | Event-MessageHeader-1             | id                                 | resource identifier for the MessageHeader, which SHALL use a UUID format |

The remaining resources in the message bundle depend on the Patient Demographics Service Event listed under the [Messages](explore.html) section.


An **optional** event-sequence element may be sent which, if included, **must** contain at least one of:

| DCH Event Header item requirement      | FHIR resource            | FHIR element                                                     |
|----------------------------------------|--------------------------|------------------------------------------------------------------|
| change timestamp         				 | Event-MessageHeader-1    | The resource meta.lastUpdated for the MessageHeader 				   |
| sequence number         | Event-MessageHeader-1    | The resource meta.versionId for the MessageHeader 				   |



The remaining resources in the bundle depend on the Event listed under the [Messages](explore.html) section.

## Example Message Header ##

<script src="https://gist.github.com/IOPS-DEV/a1d4a7f89b0658f3b9a0ace6dda09df9.js"></script>







