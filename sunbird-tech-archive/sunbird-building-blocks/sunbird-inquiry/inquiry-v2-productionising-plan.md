---
icon: elementor
---

# inQuiry V2 Productionising Plan

### **Overview** <a href="#inquiryv2productionisingplan-overview" id="inquiryv2productionisingplan-overview"></a>

The inQuiry components have been enhanced to Version 2 (v2), aligning with the latest Quml spec v1.1. However, Ed is currently operating on the older version of inQuiry.

The proposal is for Ed to upgrade to the most recent inQuiry version within the 7.0.0 Release. Further details about the plan and its implications are provided below.

Current Usage of inQuiry components in ED,

* inQuiry Player (v5.7.0)
* inQuiry Microservice (v5.7.0)
* inQuiry Editor - Not Used (instead using Collection Editor)

Between the Collection Editor and inQuiry Editor, below are some of the significant changes as of v7.0.0

* Support MMCQ format questions
* Server side evaluation capabilities
* Capturing the review comments on the question sets

### **Microservice** <a href="#inquiryv2productionisingplan-microservice" id="inquiryv2productionisingplan-microservice"></a>

* inQuiry v2 Service deployment to production ie Sunbird Ed upgrading to the latest inQuiry version does not have any challenges since both v1 & v2 APIs exist in the system
* We are providing a script for migrating questions / question sets from v1 → v2.

### **Player** <a href="#inquiryv2productionisingplan-player" id="inquiryv2productionisingplan-player"></a>

* \[TO DO] Player to introduce backward compatibility. The latest version of the Player (v2) will be enhanced further to support v1 questions/question sets hence the consumption will not impacted when a adopter/user upgraded to v2 and will still be allowed to play content in v1 format.

![](<../../../.gitbook/assets/grey\_arrow\_down (2).png>)V1 / V2 Player Capability

| **Player** | **Search V1 Questions**                                | **Play V1 Questions Online**                           | **Search V2 Question**                                 | **Play V2 Questions Online**                           | **Play V1 Questions Offline**                                                                | **Play V2 Questions Offline**                          |
| ---------- | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | -------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| V1         | ![(blue star)](../../../.gitbook/assets/1f7e2.png) Yes | ![(blue star)](../../../.gitbook/assets/1f7e2.png) Yes | ![(blue star)](../../../.gitbook/assets/1f7e2.png) Yes | ![(blue star)](../../../.gitbook/assets/1f534.png) No  | ![(blue star)](../../../.gitbook/assets/1f7e2.png) Yes                                       | ![(blue star)](../../../.gitbook/assets/1f534.png) No  |
| V2         | ![(blue star)](../../../.gitbook/assets/1f7e2.png) Yes | ![(blue star)](../../../.gitbook/assets/1f7e2.png) Yes | ![(blue star)](../../../.gitbook/assets/1f7e2.png) Yes | ![(blue star)](../../../.gitbook/assets/1f7e2.png) Yes | ![(blue star)](../../../.gitbook/assets/1f7e0.png) Player should have backward compatibility | ![(blue star)](../../../.gitbook/assets/1f7e2.png) Yes |

### **Editor** <a href="#inquiryv2productionisingplan-editor" id="inquiryv2productionisingplan-editor"></a>

* Will **ONLY** support V2 question creation & updating (however reading of v1 is supported in the v2 Editor)
  * ![(blue star)](../../../.gitbook/assets/1f534.png) When a user tries to **update / save / send for review / publish** v1 question and question sets using the v2 Editor, an error will be displayed to the user.
  * \[TODO] When a user opens a V1 question or question set in the V2 editor, a warning will be displayed, indicating that it is for viewing only and cannot be saved.
* Solution for the above problem,
  * Selectively migrate DRAFT / REVIEW questions and questionSets.
    * InQuiry provides a standalone script and job that can help with migration of questions and questionSets.
    * This approach will enable question creators to edit the old question / questionSets (which are currently under creation / modification) using the V2 Editor
  * ![(blue star)](../../../.gitbook/assets/1f7e0.png) Migration of LIVE questions and question sets can be scheduled for a later agreed-upon time.
    * The advantage of this approach is that it ensures uninterrupted use of the existing LIVE questions and question sets.
    * The drawback is that LIVE questions or question sets cannot undergo any updates or modifications until the migration process is finished ie, v1 questions cannot be updated using v2 Editor
