---
title: PDS Person Death   
keywords:  messaging, bundles
tags: [fhir,messaging]
sidebar: foundations_sidebar
permalink: explore_pds_person_death.html
summary: "The FHIR profiles used for the PDS Person Death event message bundle"
---

## FHIR Profiles ##

The PDS Person Death event message bundle is expected to include a combination of the following resources to support the event header and data item requirements:

| PDS Person Death Event Message Bundle |
|---------------------------------------|
| [EMS-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-Bundle-1)                              |
| [EMS-MessageHeader-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-MessageHeader-1) - where the coding and display elements for the 'event' type are fixed to 'PDS004 - PDS Person Death'                       |
| [EMS-Communication-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-Communication-1)                       |
| [CareConnect-EMS-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-Patient-1)                     |

<img src="images/explore/pds_death_bundle.png" >

The `extension(deathNotificationStatus)` and `deceased` elements within the patient resource are the main indicators of the patients death status.


## PDS Death Event Message Life Cycle ##

<img src="images/explore/pds_death_life_cycle.png" style="margin-left:auto; margin-right:auto;" >

|  | PDS Person Death (Informal) | PDS Person Death (Formal) | PDS Person Death (Entered in error) |
| --- | --- | --- | --- |
| | A death notification reported by a secondary source, no formal death certificate recieved. | A formal death where death certificate has been recieved. | A revoke of a patient death event as the death was entered in error, the patient is NOT DEAD. |
| **EMS-MessageHeader-1 Resource** |
| `extension(eventMessageType)` | Fixed value: `new` | Fixed value: `new` | Fixed value: `new` |
| `event` | Fixed value: `PDS004 (PDS Person Death)` | Fixed value: `PDS004 (PDS Person Death)` | Fixed value: `PDS004 (PDS Person Death)` |
| **EMS-Communication-1 Resource** |
| `status` | Fixed value: `completed` | Fixed value: `completed` | Fixed value: `completed` |
| **CareConnect-EMS-Patient-1** |
| `extension (deathNotificationStatus)` | Fixed value: 1 (Informal) | Fixed value: 2 (Formal) | **extension not included in resource** |
| `deceased` | element populated with dateTime of death | element populated with dateTime of death | **element not included in resource** |


## Resource population requirements and guidance ##

The following requirements and resource population guidance should be followed in addition to the requiremnts and guidance outlined in the [Events Management Service](https://developer.nhs.uk/apis/ems-beta/explore_event_header_information.html) specification.

### EMS-MessageHeader-1

The messageHeader resource included as part of the event message SHALL conform to the [EMS-MessageHeader-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-MessageHeader-1) constrained FHIR profile and the additional population guidance as per the table bellow:

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| extension(eventMessageType) | 1..1 | Will be populated as per the event life cycle table above. |
| event | 1..1 | Fixed Value: PDS004 (PDS Person Death) |
| focus | 1..1 | This will reference the "EMS-Communication-1" resource which contains information relating to the event message. |


### EMS-Communication-1

The Communication resource included in the event message SHALL conform to the [EMS-Communication-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-Communication-1) constrained FHIR profile and the additional population guidance as per the table below:

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| status | 1..1 | Will be populated as per the event life cycle table above. |
| payload | 1..1 | This will reference the patient resource representing the patient who is the focus of this event. |


### CareConnect-EMS-Patient-1

The patient resource included in the event message SHALL conform to the [CareConnect-EMS-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-Patient-1) constrained FHIR profile and the additional population guidance as per the table below:

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| extension(deathNotificationStatus) | 0..1 | This will be populated as per the event life cycle table above. |
| deceased | 0..1 | This will be populated as per the event life cycle table above. |


### CareConnect-Organization-1

References to Organization resources within this event message will use absolute URL reference which can be retrieved as described in the [FHIR ODS Lookup API Implementation guide](https://developer.nhs.uk/apis/ods/restfulapis_identification_organization.html) rather than including the organization resource within the event message bundle.

