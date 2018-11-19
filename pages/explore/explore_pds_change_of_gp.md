---
title: PDS Change of GP 
keywords:  messaging, bundles
tags: [fhir,messaging]
sidebar: foundations_sidebar
permalink: explore_pds_change_of_gp.html
summary: "The FHIR profiles used for the PDS Change of GP event message bundle"
---

## FHIR Profiles ##

The PDS Change of GP event message bundle is expected to include a combination of the following resources to support the event header and data item requirements:

| PDS Change of GP Event Message Bundle |
|---------------------------------------|
| [EMS-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-Bundle-1)                              |
| [EMS-MessageHeader-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-MessageHeader-1) |
| [CareConnect-Organization-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Organization-1)                |
| [EMS-HealthcareService-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-HealthcareService-1)                   |
| [CareConnect-EMS-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-Patient-1)                     |
| [EMS-Communication-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-Communication-1)                       |
| [EMS-PDS-GPRegistration-EpisodeOfCare-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-PDS-GPRegistration-EpisodeOfCare-1) |


<div style="text-align:center; margin-bottom:20px" >
	<a href="images/explore/change_of_gp_bundle.png" target="_blank"><img src="images/explore/change_of_gp_bundle.png"></a>
	PDS Change of GP Bundle <a href="images/explore/change_of_gp_bundle.png" target="_blank">(open in new TAB)</a>
</div>

The `CareConnect-EMS-Patient-1` resource `generalPractitioner` element references the organization resource representing the patients current GP practice.

The `EMS-PDS-GPRegistration-EpisodeOfCare-1` resource `managingOrganization` element references the organization resource which was the patients previous GP practice.


## PDS Change of GP Message Life Cycle ##

The `PDS Change of GP` event message is always a `new` event and there is no concept of `update` or `delete` for the event message.

If a subscriber receive multiple `PDS Change of GP` event messages for the same patient, the latest event message as indicated by the `timestamp` element within the MessageHeader resource should be considered the source of truth for the patients GP details.

## Resource population requirements and guidance ##

The following requirements and resource population guidance should be followed in addition to the requiremnts and guidance outlined in the [Events Management Service](https://developer.nhs.uk/apis/ems-beta/explore_event_header_information.html) specification.

### EMS-MessageHeader-1

The messageHeader resource included as part of the event message SHALL conform to the [EMS-MessageHeader-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-MessageHeader-1) constrained FHIR profile and the additional population guidance as per the table bellow:

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| extension(eventMessageType) | 1..1 | Fixed value: `new` |
| event | 1..1 | Fixed Value: PDS001 (PDS Change of GP) |
| focus | 1..1 | This will reference the "EMS-Communication-1" resource which contains information relating to the event message. |


### EMS-Communication-1

The Communication resource included in the event message SHALL conform to the [EMS-Communication-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-Communication-1) constrained FHIR profile and the additional population guidance as per the table below:

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| status | 1..1 | Fixed value: `completed` |
| payload | 1..1 | This will reference the patient resource representing the patient who is the focus of this event. |


### CareConnect-EMS-Patient-1

The patient resource included in the event message SHALL conform to the [CareConnect-EMS-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-Patient-1) constrained FHIR profile and the additional population guidance as per the table below:

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| meta.versionId | 1..1 | This element will contain the serial change number (SCN) of the patient record within Spine at the time this event was published. |
| identifier | 1..1 | Patient NHS Number SHALL be included within the nhsNumber identifier slice |
| generalPractitioner | 1..1 | References to an organization representing the new GP Practice which is the current primary care provider for the patient. |



### CareConnect-Organization-1

Within the bundle there will be multiple organization resources, including one for the patients current GP Practice and one for the patients previous GP Practice. Other Organization resource may be included where referenced from with resources. The Organization resources included in the bundle SHALL conform to the [CareConnect-Organization-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Organization-1) constrained FHIR profile and the additional population guidance as per the table below:

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| identifier | 1..1 | The organization ODS code SHALL be included within the odsOrganizationCode identifier slice |
| name | 1..1 | A human readable name for the organization SHALL be included in the organization resource |
| partOf | 1..1 | Reference to the commissioning organization |


### EMS-PDS-GPRegistration-EpisodeOfCare-1

The EpisodeOfCare resource included in the event message SHALL conform to the [EMS-PDS-GPRegistration-EpisodeOfCare-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-PDS-GPRegistration-EpisodeOfCare-1) constrained FHIR profile and the additional population guidance as per the table below:

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| status | 1..1 | Fixed value: finished |
| extension(systemEffectivePeriod).valuePeriod.start | 1..1 | The PDS system date on which the old GP Practice registration was added to PDS. |
| extension(systemEffectivePeriod).valuePeriod.end | 1..1 | The PDS system date on which the old GP Practice registration was ended on the PDS. |
| period.start | 1..1 | Date on which the **old** GP practice assumed responsibility for the patient. |
| period.end | 1..1 | Date on which the **old** GP Practice stopped being responsible for the patient, usually when the new GP Practice takes responsibility for the patient. |

