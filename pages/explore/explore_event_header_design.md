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

This event header information must consist of the following **mandatory** items and their corresponding FHIR profiles and elements:

| Event Header item requirement          | FHIR resource                     | FHIR element                                                                |
|----------------------------------------|-----------------------------------|-----------------------------------------------------------------------------|
| patient identification data:           | CareConnect-Patient-1             |                                                                             |
| NHS Number                             | CareConnect-Patient-1             | identifier using NHS Number slice                                           |
| Date of Birth                          | CareConnect-Patient-1             | birthDate                                                                   |
| name                                   | CareConnect-Patient-1             | name                                                                        |
| event type                             | Event-MessageHeader-1             | event                                                                       |
| type of service originating the event  | CareConnect--HealthcareService-1  | type                                                               |
| service provider originating the event | CareConnect-Communication-1       | sender                                                                  |
| IT system holding the event data       | Event-MessageHeader-1             | source                                                                      |
| event date time                        | CareConnect-Communication-1       | received                                                                |
| event publisher                        | Event-MessageHeader-1             | responsible                                                                 |
| event published date                   | Event-MessageHeader-1             | timestamp                                                                   |
| publication reference number           | Event-MessageHeader-1       | The resource identifier for the MessageHeader, which SHALL use a UUID format |

The remaining resources in the message bundle depend on the Patient Demographics Service Event listed under the [Messages](explore.html) section.









