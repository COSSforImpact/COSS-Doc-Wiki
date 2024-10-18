---
icon: elementor
---

# Design: Addition information on certificate QR scan

### Introduction <a href="#design-additioninformationoncertificateqrscan-introduction" id="design-additioninformationoncertificateqrscan-introduction"></a>

Currently, upon scanning the QR code on the certificate only the user name, course completed by the users plus the completion date is shown to the user. This needs to be enhanced to show the users' profile information so that it can help administrators uniquely identify and validate user credentials.

The design approach, focuses on below points.

1. Enable or disable of additional fields
2. Easy addition or deletion of additional fields for new certificates
3. Backward compatibility of existing certificates
4. Handling PII information.

### Problem Statement <a href="#design-additioninformationoncertificateqrscan-problemstatement" id="design-additioninformationoncertificateqrscan-problemstatement"></a>

Add below additional fields to certificate json and make it available on QR scan.

User info:

* users' state name
* users' district name
* users' block name
* users' cluster name
* users' school name

Enrolment and Assess meta data:

* Course name
* Course completion date
* Users' assessment score (best attempt score) for all course assessments in the course

#### Assumptions <a href="#design-additioninformationoncertificateqrscan-assumptions" id="design-additioninformationoncertificateqrscan-assumptions"></a>

* For all additional fields, values at the time of certificate generation are to be considered.
* As QR scan is public all PII related info are masked.
* The additional fields are available upon QR scan only for new certificates or re-Issued certificates.

### Design <a href="#design-additioninformationoncertificateqrscan-design" id="design-additioninformationoncertificateqrscan-design"></a>

* To enable addition fields in certificates, specify `additionalProps` as a new field in certificate template as below

```
{
  "additionalProps" : { <Map<String, List<String>>> // Optional, On empty, the  property is ignored
		"location": [], <List<String> like "state" "district", "block", "cluster", "school" // Optional. Details are from userLocations in user read API
		"user": [] <List<String> like "phone" // Optional. Details are from user read API
		"enrolment": [], <List<String> like "completedOn" // Optional. Details are from user_enrolments table
		"assessment": [] <List<String>> like "score" // Optional. Details are from user_activity_agg table
		"course": [] <List<String>> like "name" // Optional. Details are from content read API
	}
}
```

* Based on the fields specified for user and enrolments the values at the time of generation of certificate are fetched
* This allows addition or deletion of fields with just an update to certificate template.
* Upon certificate generation, the specified additional fields are made available in `related` column of `cert_registry` as below

```
Below is the schema in related Coulmn with additional fields
{
  "location": { // Optional
    "state": <String>, //Optional
    "district": <String>, //Optional
    "block": <String>, //Optional
    "cluster": <String>, //Optional
    "school": <String>, //Optional
  },
  "user" :{ //Optional
    "phone": <String>, //masked phone
  }
  "enrolment": { // Optional
    "completedOn": <TimeStamp>, //Optional
  },
  "assessment": { // Optional
    "score": <Map<String, double>> //Optional
  },
  "course": { // Optional
    "name": <String>, //Optional
  }
}
```

#### Flink Job changes <a href="#design-additioninformationoncertificateqrscan-flinkjobchanges" id="design-additioninformationoncertificateqrscan-flinkjobchanges"></a>

* In `certificate-pre-processor` flink job, add a new configuration as below.

```
pii_fields = ["userName"]
```

* If `additionalProps` present in certificate template then,
  * Fetch user details from user read API response
  * Fetch masked values for PII fields
  * Fetch enrolment related data from user\_enrolments
  * Fetch score data from user\_activity\_agg table `aggregates` column.
* Prepare the `related` column data and insert into `cert-registry`

### Conclusion: <a href="#design-additioninformationoncertificateqrscan-conclusion" id="design-additioninformationoncertificateqrscan-conclusion"></a>

\<TODO>
