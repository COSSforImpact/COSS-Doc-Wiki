---
icon: folder-open
---

# Client integration with V2 API | Backward compatibility

#### **Background** <a href="#clientintegrationwithv2api-or-backwardcompatibility-background" id="clientintegrationwithv2api-or-backwardcompatibility-background"></a>

We are in the process of building V2 APIs for QuML Compliance and Multi lingual. This needs conclusion on how the existing questions will be handled by the client applications (QuML Editor and Player)

#### **Current Adopters of APIs (inQuiry Service)** <a href="#clientintegrationwithv2api-or-backwardcompatibility-currentadoptersofapis-inquiryservice" id="clientintegrationwithv2api-or-backwardcompatibility-currentadoptersofapis-inquiryservice"></a>

* Internal inQuiry Editor and inQuiry Player
* Samagra using inQuiry Editor and inQuiry Player
* SikshaLokam using inQuiry editor and custom Player
* iGot using inQuiry API Services (through their custom APIs) and custom Editor and custom Player
* UPSMF using inQuiry QuML player and inQuiry Editor

#### **For simplicity in explaining, naming the questions created as below,** <a href="#clientintegrationwithv2api-or-backwardcompatibility-forsimplicityinexplaining-namingthequestionscrea" id="clientintegrationwithv2api-or-backwardcompatibility-forsimplicityinexplaining-namingthequestionscrea"></a>

V1 API Creates V1 Questions (uses QuML v1.0)

V2 API Creates V2 Questions (uses QuML v1.1)

**Possible Usage Scenarios and outcomes**

* Old Player using V1 API to fetch V1 questions - Permitted
* Old Player using V1 API to fetch V2 questions - Not permitted
* New/Upgraded Player using V2 API to fetch V1 questions - Permitted
* New/Upgraded Player using V2 API to fetch V2 questions - Permitted

***

### Possible Layers that can assist in backward compatibility and their advantage and disadvantage <a href="#clientintegrationwithv2api-or-backwardcompatibility-possiblelayersthatcanassistinbackwardcompatibili" id="clientintegrationwithv2api-or-backwardcompatibility-possiblelayersthatcanassistinbackwardcompatibili"></a>

#### **If it has to be done in the Client (Player & Editor)** <a href="#clientintegrationwithv2api-or-backwardcompatibility-ifithastobedoneintheclient-player-and-editor" id="clientintegrationwithv2api-or-backwardcompatibility-ifithastobedoneintheclient-player-and-editor"></a>

This is one option where the backward compatibility is done at the client. The responsibility of inQuiry Service will then be to send back the questions AS-IS based on the identifier supplied. i.e; If inQuiry Player or inQuiry Editor ask for V1 Question, then V1 Question is given without any transformation. If the client ask for V2, then the V2 question is given back without any transformation. In this case, the Editor and Player need to know how to handle both the question formats.

**Advantage to API**

* API can simply return the question based on the V1 question identifier or V2 question identifier
* No data transformation is needed in the backend on the fly

**Disadvantage to Client**

* Changes to be done by the Adopters also (some of the adopters uses their custom player and they need to do the backward compatibility in their player also)
* Complexity in maintaining 2 versions of QuML and data transformations
* Changes / Fixes if any cannot be easily rolled out
* Changes are to be done in Editor and Player
* Client to continue data transformation for all the previous versions of QuML when new future versions comes up
* Transformations can result in performance issues in Player & Editor

**General Assumption**\
Client (Player & Editor) updates will always support latest QuML specification

***

#### **If it has to be done in the Backend (inQuiry Service)** <a href="#clientintegrationwithv2api-or-backwardcompatibility-ifithastobedoneinthebackend-inquiryservice" id="clientintegrationwithv2api-or-backwardcompatibility-ifithastobedoneinthebackend-inquiryservice"></a>

This is one option where the backward compatibility is done at the inQuiry Service layer. The responsibility of inQuiry Service will then be to send back the questions with transformation. i.e; If inQuiry Player or inQuiry Editor ask for V1 Question, then V1 Question is given with transformation to V2 (V2 API does this transformation). If the client ask for V2, then the V2 question is given back without any transformation. In this case, the Editor and Player need NOT know how to handle both the question formats as the V2 API is returning data in only one format i.e; V2 format.

**Advantage to Client**

* No changes to be done by the Adopters using V1 api (as they will be invoking only V1 api and V1 api always returns V1 format question. This will continue to work as long as V1 API is not decommissioned)
* No changes to be done by the Adopter who has migrated to V2 for their custom players as once V2 is incorporated it will always return V2 format content (For both V1 question identifier and V2 question identifier)
* Relatively less complexity in maintaining 2 versions of API calls and data transformations. The maintenance of both version of APIs needed only until all adopters migrate to V2 API and V1 is ready to be decommissioned)
* Changes / Fixes if any can be easily rolled out

**Disadvantage to API**

* API cannot simply return the question based on the V1 question identifier or V2 question identifier
* Data transformation is needed in the backend on the fly
* API to continue data transformation for all the previous versions of QuML when new future versions comes up (TBD the time line for decommissioning is to be determined in consent with the Adopters and we are not able to force a timeline from our end alone)

***

#### **Decision concluded** <a href="#clientintegrationwithv2api-or-backwardcompatibility-decisionconcluded" id="clientintegrationwithv2api-or-backwardcompatibility-decisionconcluded"></a>

* The V2 APIs will be backward compatible (this is not optional)
* Front end will not be doing backward compatibility as per the below reasons
  * Performance overhead if the player and editor needs to be aware of V1 format and V2 format and need to do the transformation at the client side.
  * This will not be useful for adopters who are using custom Editor / Player and they will need to accomodate backward compatibility their respective Editor and Player. This will lead to code maintenance issues
* One time (big bang) transformations is risky
  * Adopters who are partly QuML compliant currently can have different type of questions and meta data, so a transformation job satisfying all the possibilities is a problem.
  * Often production data can have data inconsistencies that can break the job mid way inspite of handling data edge cases and tested against non-production environment.
  * If going with one time transformation then we need to alter the current stable V1 api to re-transform the V2 question to V1 format. This will need modification to questions and republishing them
* Doing on-demand transformation (V1 question that gets edited through V2 API) can contain the failure if any to that specific question and is less risky compared to big bang. Preference is to go with on-demand transformation instead of One time transformation.
