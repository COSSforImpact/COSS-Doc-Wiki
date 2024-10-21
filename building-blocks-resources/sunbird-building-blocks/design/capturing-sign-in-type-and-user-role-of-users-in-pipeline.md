---
icon: elementor
---

# Capturing Sign-in Type and User Role of users in Pipeline

### **Overview :** <a href="#capturingsign-intypeanduserroleofusersinpipeline-overview" id="capturingsign-intypeanduserroleofusersinpipeline-overview"></a>

Need to add the fields in telemetry User role and Sign In type for further breakdown of "No of Unique Users Count by district"

### **Problem Statement:** <a href="#capturingsign-intypeanduserroleofusersinpipeline-problemstatement" id="capturingsign-intypeanduserroleofusersinpipeline-problemstatement"></a>

* Stamp user role in telemetry
* Stamp Sign In type in telemetry

### **Design:** <a href="#capturingsign-intypeanduserroleofusersinpipeline-design" id="capturingsign-intypeanduserroleofusersinpipeline-design"></a>

#### **Stamping User Role -** <a href="#capturingsign-intypeanduserroleofusersinpipeline-stampinguserrole" id="capturingsign-intypeanduserroleofusersinpipeline-stampinguserrole"></a>

&#x20;**Approach-1**

* Portal/App will generating the AUDIT event with userrole(TEACHER,STUDENT) in cdata

&#x20;            Example:- cdata {

&#x20;                               userrole: TEACHER/STUDENT

&#x20;                           }

* New Samza job will be introduced to capture the AUDIT event
  * Will be  the immediate next job to  extractor so that the other  telemetry events associated with userid will not be skipped from stamping user role
  * Will be capturing audit events and retreive the user role from event and store in redis db

**Approach-2**

* Portal/App will generating the AUDIT event with userrole(TEACHER,STUDENT) in cdata

&#x20;            Example:- cdata {

&#x20;                               userrole: TEACHER/STUDENT

&#x20;                           }

* In Current Extractor Job , we can check for  eid with "AUDIT"  &&  cdata contains "userrole"  key  and add the  "userrole" value to redis with actor.id  (if the audit event is not directly kept in raw topic)

#### **Stamping Sign In Type:**  <a href="#capturingsign-intypeanduserroleofusersinpipeline-stampingsignintype" id="capturingsign-intypeanduserroleofusersinpipeline-stampingsignintype"></a>

* In the Denormalisation Job, for the user denorm , we will be caputring the SignIn Type from cassandra user related tables  with below conditions
  * If the user has rootorgid associated with state, then "Validated" user
  * If the user has rootorgid but not state associated, then "Self-Signed" User
  * If the above both conditions fail, then "Anonymous" user
* Once the SiginType is retreived, the same details will be updated in redis cache and stamped in "userdata" field in telemetry both userrole and Signin type

\


\
