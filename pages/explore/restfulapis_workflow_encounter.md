---
title: Workflow | Encounter
keywords: usecase, encounter
tags: [rest, fhir, workflow]
sidebar: foundations_sidebar
permalink: restfulapis_workflow_encounter.html
summary: An interaction between a patient and healthcare provider(s) for the purpose of providing healthcare service(s) or assessing the health status of a patient.
---
{% include custom/search.warnbanner.html %}

{% include custom/profile.html content="Encounter" page="CareConnect-Encounter-1" %}

{% include custom/fhir.resource.html content="[Encounter](https://www.hl7.org/fhir/DSTU2/encounter.html#search)" %}

## 1. Read ##

<div markdown="span" class="alert alert-success" role="alert">
GET /Encounter/[id]</div>

{% include custom/read.response.html resource="Encounter" content="" %}

## 2. Search ##

<div markdown="span" class="alert alert-success" role="alert">
GET /Encounter?[searchParameters]</div>

Fetches a bundle of all `Encounter` resources for the specified patient.

{% include custom/search.header.html resource="Encounter" %}

### 2.1. Search Parameters ###

{% include custom/moscow.html content="[Encounter](https://www.hl7.org/fhir/DSTU2/encounter.html#search)" %}

| Name | Type | Description | Conformance | Path |
|------|------|-------------|-------|------|
| `date` | `date` | A date within the period the Encounter lasted | MAY | Encounter.period |
| `patient` | `reference` | The identity of a patient to list encounters for | MAY | Encounter.patient <br>(Patient) |

{% include custom/search.date.html para="2.1.1." content="Encounter" %}

{% include custom/search.patient.html para="2.1.2." content="Encounter" %}

{% include custom/search.response.html resource="Encounter" %}

## 3. Example ##

### 3.1 Query ###
Return all Encounter resources for Patient with a NHS Number of 9876543210, the format of the response body will be xml. Replace 'baseUrl' with the actual base Url of the FHIR Server.

#### cURL ####

{% include custom/embedcurl.html title="Search Encounter" command="curl -X GET  'http://[baseUrl]/Encounter?patient.identifier=https://fhir.nhs.uk/Id/nhs-number|9876543210&_format=xml'" %}

{% include custom/search.response.headers.html resource="Encounter" %}

### 3.3 Response Body ###

```xml
<Bundle xmlns="http://hl7.org/fhir">
    <id value="b2866816-e8f1-480b-a10c-1655ee68497f"/>
    <meta>
        <lastUpdated value="2017-06-02T08:55:05.472+01:00"/>
    </meta>
    <type value="searchset"/>
    <total value="1"/>
    <link>
        <relation value="self"/>
        <url value="http://127.0.0.1:8181/Dstu2/Encounter?patient=https%3A%2F%2Fpds.proxy.nhs.uk%2FPatient%2F9876543210"/>
    </link>
    <entry>
        <fullUrl value="http://127.0.0.1:8181/Dstu2/Encounter/24957"/>
        <resource>
            <Encounter xmlns="http://hl7.org/fhir">
                <id value="24957"/>
                <meta>
                    <versionId value="1"/>
                    <lastUpdated value="2017-06-02T08:53:47.393+01:00"/>
                    <profile value="https://fhir.hl7.org.uk/StructureDefinition/CareConnect-Encounter-1"/>
                </meta>
                <status value="finished"/>
                <class value="outpatient"/>
                <type>
                    <coding>
                        <system value="http://snomed.info/sct"/>
                        <code value="766841000000106"/>
                        <display value="Consultation with patient encounter type (record artifact)"/>
                    </coding>
                </type>
                <patient>
                    <reference value="https://pds.proxy.nhs.uk/Patient/9876543210"/>
                </patient>
                <participant>
                    <individual>
                        <reference value="https://sds.proxy.nhs.uk/Practitioner/C5206458"/>
                        <display value="FF Nathani"/>
                    </individual>
                </participant>
                <period>
                    <start value="2017-05-24T11:34:00.453-00:00"/>
                    <end value="2017-05-24T11:49:00.453-00:00"/>
                </period>
                <reason>
                    <coding>
                        <system value="http://snomed.info/sct"/>
                        <code value="702706001"/>
                        <display value="Diabetes clinic"/>
                    </coding>
                </reason>
                <location>
                    <location>
                        <reference value="https://sds.proxy.nhs.uk/Organization/Location/RY8RK"/>
                        <display value="Long Eaton Health Clinic"/>
                    </location>
                </location>
                <serviceProvider>
                    <reference value="https://sds.proxy.nhs.uk/Organization/Organization/RY8"/>
                    <display value="Derbyshire Community Health Services NHS Foundation Trust"/>
                </serviceProvider>
            </Encounter>
        </resource>
        <search>
            <mode value="match"/>
        </search>
    </entry>
</Bundle>
```