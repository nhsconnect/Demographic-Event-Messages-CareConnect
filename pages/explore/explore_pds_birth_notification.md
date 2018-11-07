---
title: PDS Birth Notification
keywords:  messaging, bundles
tags: [fhir,messaging]
sidebar: foundations_sidebar
permalink: explore_pds_birth_notification.html
summary: "The FHIR profiles used for the PDS Birth Notification event message bundle"
---

## FHIR Profiles ##
The PDS Birth Notification event message bundle is expected to include a combination of the following resources to support the event header and data item requirements:

| PDS Birth Notification Event Message Bundle                           |
|-----------------------------------------------------------------------|
| [EMS-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-Bundle-1)                                                          |
| [EMS-MessageHeader-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-MessageHeader-1) |
| [CareConnect-Organization-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Organization-1)                                            |
| [EMS-HealthcareService-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-HealthcareService-1)                                                 |
| [EMS-Communication-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-Communication-1)                                                   |
| [CareConnect-EMS-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-Patient-1)                                          |
| [EMS-PDS-RelatedPerson-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-PDS-RelatedPerson-1)                                                 |
| [CareConnect-EMS-PDS-Baby-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-PDS-Baby-Patient-1)                                            |
| [CareConnect-EMS-PDS-BirthWeight-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-PDS-BirthWeight-Observation-1)                             |
| [CareConnect-EMS-PDS-GestationAge-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-PDS-GestationAge-Observation-1)                            |
| [CareConnect-EMS-PDS-NumberOfBirths-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-PDS-NumberOfBirths-Observation-1)                          |
| [CareConnect-EMS-PDS-StillbornIndicator-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-PDS-StillBornIndicator-Observation-1)                      |
| [CareConnect-EMS-PDS-SuspectedCongenitalAbnormalityIndicator-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-PDS-SuspectedCongenitalAbnormalityIndicator-Observation-1) |
| [CareConnect-EMS-PDS-DeliveryPlace-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-PDS-DeliveryPlace-Organization-1)                          |
| [CareConnect-EMS-PDS-RegisteringAuthority-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-PDS-RegisteringAuthority-Organization-1)                   |
| [CareConnect-Practitioner-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Practitioner-1)                                            |

<img src="images/explore/pds_birth_notification_bundle.png" >

The focus of the PDS Birth Notification event message is the `CareConnect-EMS-Patient-1` resource representing the mother, referenced from the event message Communication resource. The baby in this birth notification is linked to the mother through the `EMS-PDS-RelatedPerson-1` resource which shows the relationship of mother to baby. Additional information about the birth is included in the bundle as observation resources which are either linked to the mother or the baby


## PDS Birth Notification Event Message Life Cycle ##

The `PDS Birth Notification` event message is always a `new` event and there is no concept of `update` or `delete` for the event message.

The birth notification event will be triggered by a birth being registerd on the Spine.


## Resource population requirements and guidance ##

The following requirements and resource population guidance should be followed in addition to the requirements and guidance outlined in the [Events Management Service](https://developer.nhs.uk/apis/ems-beta/explore_event_header_information.html) specification.


### EMS-MessageHeader-1

The messageHeader resource included as part of the event message SHALL conform to the [EMS-MessageHeader-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-MessageHeader-1) constrained FHIR profile and the additional population guidance as per the table bellow:

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| extension(eventMessageType) | 1..1 | Fixed value: `new` |
| event | 1..1 | Fixed Value: PDS003 (PDS Birth Notification) |
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
| identifier | 1..1 | Patient NHS Number SHALL be included within the nhsNumber identifier slice |
| name (official) | 1..1 | Patients name as registered on PDS, included within the resource as the `official` name element slice |
| birthDate | 0..1 | The patient birth date shall be included in the patient resource |
| generalPractitioner | 0..1 | References to an organization representing the Mother's Primary Care provider, the reference organization should contain the organization ODS Code, name and relevant contact details. |



### CareConnect-EMS-PDS-Baby-Patient-1

The patient resource included in the event message SHALL conform to the [CareConnect-EMS-PDS-Baby-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-PDS-Baby-Patient-1) constrained FHIR profile and the additional population guidance as per the table below:

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| identifier | 1..1 | Patient NHS Number SHALL be included within the nhsNumber identifier slice |
| name (official) | 1..1 | The babys name as registered on PDS, included within the patient resource as the `official` name element slice |
| gender | 1..1 | The gender of the baby |
| birthDate | 1..1 | The birth date of the baby shall be included in the patient resource |
| extension(patient-birthTime) | 1..1 | The delivery time for the birth |
| deceased | 0..1 | Deceased dateTime of the baby has died |
| extension(deathNotificationStatus) | 0..1 | The death notification status if the baby has died |
| address.line | 1..* | The address for the baby. Note: the address lines SHALL appear in the the resource in order, i.e. Address line 1 first, line 2 second, etc. |
| address.postalcode | 0..1 | address post code |
| multipleBirthInteger | 1..1 | The multiple birth indicator will be an number indicating the position in the order of births, i.e. the first baby would be `1`, a second baby for example in twins would be `2` |
| extension(birthPlace) | 0..1 | The address of the place where the baby was born |
| extension(ethnicCategory) | 1..1 | The ethnicity of the baby |



### CareConnect-EMS-PDS-BirthWeight-Observation-1

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| valueQuantity | 1..1 | The birth weight of the baby |
| subject | 1..1 | The birth weight observation will reference the baby patient resource it relates. |


### CareConnect-EMS-PDS-GestationAge-Observation-1

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| valueQuantity | 1..1 | Gestation Age of the baby |
| subject | 1..1 | The gestation age observation will reference the baby patient resource it relates. |


### CareConnect-EMS-PDS-NumberOfBirths-Observation-1

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| valueQuantity | 1..1 | Number of Births in Confinement |
| subject | 1..1 | The number of births observation will reference the mother patient resource. |


### CareConnect-EMS-PDS-StillbornIndicator-Observation-1

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| valueQuantity | 1..1 | Will indicate if the baby was still born or not. |
| subject | 1..1 | The stillborn indicatior observation will reference the baby patient resource it relates. |


### CareConnect-EMS-PDS-SuspectedCongenitalAbnormalityIndicator-Observation-1

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| valueQuantity | 1..1 | Suspected Congenital Abnormality Indicator, 'code' element uses SNOMED CT code '1097291000000101 - Suspected congenital abnormality (situation)' |
| subject | 1..1 | This observation will reference the baby patient resource it relates. |


### CareConnect-EMS-PDS-DeliveryPlace-Organization-1

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| type | 0..1 | Delivery Place Type |
| identifier | 0..1 | Delivery Place Code, using the ODS identifier slice |
| name | 0..1 | Delivery Place Name |


### CareConnect-EMS-PDS-RegisteringAuthority-Organization-1

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| type | 1..1 | Registering Authority Type |
| identifier | 1..1 | Organisation identifier using the ODS identifier slice |


### CareConnect-Practitioner-1

| Element | Cardinality | Additional Guidance |
| --- | --- | --- |
| name.given | 1..* | Practitioner given name(s) |
| name.family | 1..1 | Practitioner family name |




### Other resource data item requirements are expected to be fulfilled as below:

| PDS Birth Notification data item name | FHIR Resource | FHIR element | Mandatory/Optional/Required | Note |
|---|---|---|---|---|
| Business Effective From Date | CareConnect-EMS-Patient-1.registrationDetails | registrationPeriod.period.start | Required | |
| Business Effective To Date | CareConnect-EMS-Patient-1.registrationDetails | registrationPeriod.period.end | Required | |
| Partner Child Health Organisation Code | CareConnect-Organization-1 | identifier | Mandatory | |
| Responsible Child Health Organisation Code | CareConnect-Organization-1 | identifier | Mandatory | |

