---
icon: elementor
---

# Sunbird-ED: Post installation scripts for basic setup of creation & consumption

Sunbird-Ed: GCP setup

Bearer key should have access to all the API’s

## Lern: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-lern" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-lern"></a>

#### User creation: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-usercreation" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-usercreation"></a>

* Generate new get token as Admin

#### Org creation: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-orgcreation" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-orgcreation"></a>

* Required above user-token

#### System settings: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-systemsettings" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-systemsettings"></a>

* To create root\_org, custodian\_org & default\_channel

### Note: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-note" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-note"></a>

* ES index should be working properly. Because data only sync when the data is created. Once it is created, we can’t sync the data if missed.

### Postman Collection: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-postmancollection" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-postmancollection"></a>

[https://api.postman.com/collections/4925867-1a9b39be-b540-430f-aab9-5d23a753d347?access\_key=PMAT-01GQ6RM8D76P5PZ2JZX2PWQ7QK](https://api.postman.com/collections/4925867-1a9b39be-b540-430f-aab9-5d23a753d347?access\_key=PMAT-01GQ6RM8D76P5PZ2JZX2PWQ7QK)

## Knowledge: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-knowledge" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-knowledge"></a>

* Jenkins job: To create the schema’s in neo4J
* Schema’s should be uploaded to the blob by running the Jenkins job.
* Postman collection worked well
* Master category API’s are not onboarded to kong. Hence we can’t use postman
* Postman API’s collection should be automated by storing the response in postman variables & these variables should be used as input for the next API’s(if required).

### Note: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-note-.1" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-note-.1"></a>

GCP specific issue: schema files loading was filed(loading as text). So pointed to local schema’s. Search index Job was not deploying because of deployment script issues. Master category creation api’s are not on-boarding. Hence executed directly on the pod machine(learning-service ingress ip) using curl commands. GCP specific issue: Disabled checkpoints because jobs deployment was failing

### Postman Collection: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-postmancollection-.1" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-postmancollection-.1"></a>

[https://grey-firefly-8143.postman.co/workspace/Knowlg-BB\~eec448a5-0dd9-4b09-ab3c-b0fc5a1ff78e/collection/1419050-cdbeca03-58a4-4413-ac18-e711185783da?action=share\&creator=1419050](https://grey-firefly-8143.postman.co/workspace/Knowlg-BB\~eec448a5-0dd9-4b09-ab3c-b0fc5a1ff78e/collection/1419050-cdbeca03-58a4-4413-ac18-e711185783da?action=share\&creator=1419050)

### Creation workflows: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-creationworkflows" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-creationworkflows"></a>

## ED: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-ed" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-ed"></a>

* Both the tenants sunbird & ntp(this has to be removed from the code)
* Graylog should be present to debug the issue while setting up initial data.

### Note: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-note-.2" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-note-.2"></a>

Sunbird & NTP channels should be created. Telemetry service issue while running the portal. url: hostURL + "/api/org/v2/search", data: JSON.stringify({ request: { filters: { isTenant: true, slug: id || 'ntp' } } }),

### Postman Collection: <a href="#sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-postmancollection-.2" id="sunbird-ed-postinstallationscriptsforbasicsetupofcreation-and-consumption-postmancollection-.2"></a>
