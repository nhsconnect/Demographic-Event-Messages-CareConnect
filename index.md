---
title: Introduction to Demographics Update Event Messages (Care Connect)
keywords: homepage
tags: [overview]
sidebar: overview_sidebar
permalink: index.html
toc: false
---

## Introduction ##

This implementation guide outlines the structure and content of the following PDS Demographics Update event messages:

- [PDS Birth Notification](explore_pds_birth_notification.html)
- [PDS Change of Address](explore_pds_change_of_address.html)
- [PDS Change of GP](explore_pds_change_of_gp.html)
- [PDS Death Notification](explore_pds_death_notification.html)

These event messages are constructed and published by the Spine when updates are made to the patient demographic information held by the Personal Demographics Service (PDS). The event messages will be published to the [NEMS](https://developer.nhs.uk/apis/ems-beta/) for the purpose of sharing updates with interested subscribers.


## [INTEROPen](http://www.interopen.org) ##

FHIR components specified within this site have been developed by NHS Digital and use CareConnect profiles created in collaboration with the INTEROPen community. 

The INTEROPen vision is to create a library of nationally defined HL7® FHIR® resources and interaction patterns that implementers can adopt to simplify integration and interoperability within UK health and social care.

See [CareConnect FHIR Profiles](support_careconnect.html) for further clarification on the use of CareConnect FHIR profiles within this Implementation Guide.

Find out more on the [INTEROPen website](http://interopen.org).

{% include important.html content="This site is under active development by NHS Digital and is intended to provide the FHIR messaging components for Demographics Update Event Messages, and remains subject to review. This project is being developed using an agile methodology so iterative updates to content will be added on a regular basis. Changes to this Implementation Guide following the initial beta release will be documented in the [Release Notes](overview_release_notes.html) section." %}