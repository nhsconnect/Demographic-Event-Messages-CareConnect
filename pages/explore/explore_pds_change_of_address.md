---
title: PDS Change of Address 
keywords:  messaging, bundles
tags: [fhir,messaging]
sidebar: foundations_sidebar
permalink: explore_pds_change_of_address.html
summary: "The FHIR profiles used for the PDS Change of Address event message bundle"
---

## FHIR Profiles ##

The PDS Change of Address Bundle is expected to include a combination of the following resources to support the event header and data item requirements:

| PDS Change of Address Event Message Bundle |
|--------------------------------------------|
| [EMS-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-Bundle-1)                              |
| [EMS-MessageHeader-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-MessageHeader-1)  where the coding and display elements for the 'event' type are fixed to 'PDS002 - PDS Change of Address'                      |
| [CareConnect-Organization-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Organization-1)                |
| [EMS-HealthcareService-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-HealthcareService-1)                   |
| [CareConnect-EMS-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-EMS-Patient-1)                     |
| [EMS-Communication-1](https://fhir.nhs.uk/STU3/StructureDefinition/EMS-Communication-1)                       |

## Data item requirements  ##

The data item requirements are expected to be fulfilled as below:

| PDS Change of Address data item name | FHIR Resource             | FHIR element         | Mandatory/Optional/Required | Note         |
|--------------------------------------|---------------------------|----------------------|-----------------------------|--------------|
| Current Address Type                 | CareConnect-EMS-Patient-1 | address.use          | Required                    | value = home |
| Address Line 1 or 2                  | CareConnect-EMS-Patient-1 | address.line         | Required                    |              |
| Address Line 3                       | CareConnect-EMS-Patient-1 | address.line         | Optional                    |              |
| Address Line 4                       | CareConnect-EMS-Patient-1 | address.line         | Required                    |              |
| Address Line 5                       | CareConnect-EMS-Patient-1 | address.line         | Optional                    |              |
| Postcode                             | CareConnect-EMS-Patient-1 | address.postalcode   | Required                    |              |
| PAF Key                              | to be confirmed           | to be confirmed      | Optional                    |              |
| Address Description                  | to be confirmed           | to be confirmed      | Required                    |              |
| Address Effective From Date          | CareConnect-EMS-Patient-1 | address.period.start | Required                    |              |
| Address Effective To Date            | CareConnect-EMS-Patient-1 | address.period.end   | Optional                    |              |
| Previous Address Type                | CareConnect-EMS-Patient-1 | address.use          | Required                    | value = old  |
| Previous Address                     | CareConnect-EMS-Patient-1 | address.line         | Required                    |              |
| Previous Postcode                    | CareConnect-EMS-Patient-1 | address.postalCode   | Required                    |              |
| Previous Address Description         | to be confirmed           | to be confirmed      | Required                    |              |
| Previous Address Effective From Date | CareConnect-EMS-Patient-1 | address.period.start | Required                    |              |
| Previous Address Effective To Date   | CareConnect-EMS-Patient-1 | address.period.end   | Optional                    |              |








