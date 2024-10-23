---
icon: elementor
---

# inQuiry v2 for QuML Compliance : Approach for Backward compatibiliy

**Context :** The QuML Spec (Q 1) will be upgraded to a new version (QuML version 2 - Q 2). The inQuiry implementation will be upgraded to support the spec changes and to attain full QuML Compliance. ie, the Editor, Player and API will be updated to Version 2.

**Backward Compatibility** : inQuiry V2 creates and supports data as per the the Q 2 spec. Existing adopters of inQuiry would already have created data as per the Q 1 spec.

* V2 Player should allow playing of questions created as per the Q1 spec
* V2 Editor should allow updating of questions created as per the Q1 spec. Upon Save, questions will be saved in Q2 spec (on-demand transformation).
* V2 Publish APIs WILL NOT ALLOW publishing of questions which are in the Q1 spec\
  \
  Hence any adopter upgrading to the V2 of inQuiry, should be able to use (update, play ..) the existing data (which is in Q1).

This support will be temporary. The v1 APIs will be deprecated eventually. The adopters will have to migrate any existing data in Q1 (which they would want to re-use) to Q2 format.

\
**How to handle backward compatibility?**

Approach 1 : InQuiry V2 APIs will support data which is created as per the the QuML version 2 (Q2) spec as well as QuML version 1 (Q1) spec. The support for Q1 will be temporary, till the adopters are able to upgrade / migrate to the new system (this timeframe can 6 months).

eg : The v2 `read` API will be able to read a question will is created as per the current Q1 spec and return it in the Q2 format. The v2 `update` will be able update question created as per the current Q1 spec and transform it to the new v2 structure upon saving.

_The v2 publish API will not allow publishing of question created in Q1_\


Approach 2 : One-time migration for all the data that is created as per the current implementation Q1 to Q2 has to be done. InQuiry V1 APIs will support data which is created as per the Q2 spec ( as well as Q1). We can give a timeline by when V1 APIs will be deprecated. InQuiry V1 APIs will support only Q2.

In this case

* One time (big bang) transformations is risky
* Adopters who are partly QuML compliant currently can have different type of questions and meta data, so a transformation job satisfying all the possibilities is a problem.
* Often production data can have data inconsistencies that can break the job mid way inspite of handling data edge cases and tested against non-production environment.
* If going with one time transformation then we need to alter the current stable V1 api to re-transform the V2 question to V1 format. This will need modification to questions and republishing them

**Backward compatibility for Backend vs** **Front-end**

* If the V2 APIs handle the transformation (of the old Q1 data to Q2), the inQuiry Editor V1 and Player V1 as well as any other custom Editor and Player implemented by the adopters - as per the Q1 will also work seamlessly.
  * Currently we do not have any adopters using the inQuiry Editor or Player individually without using the inquiry API services and hence handling backward compatibility in the Editor and Player is not mandatory as the APIs will be handling this.
  * Whereas, we have adopters using custom Editor / Player (ShikshaLokam, iGot).
* If the V2 APIs do not do the transformation (of the old Q1 data to Q2), the adopters who are using custom Editor / Player will have to accommodate the changes for the transformation in their respective Editor / Player when they are upgrading to the V2 APIs.
  * The transformation will have to be done in two places, the Editor and Player, as suppose to changing only on the API side.\
