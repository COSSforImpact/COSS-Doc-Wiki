---
icon: elementor
---

# Question Set Creation: Configurable Metadata

### Metadata derivation and dependency <a href="#metadata-derivation-and-dependency" id="metadata-derivation-and-dependency"></a>

Expected workflow - in case of Projects with Target Collections -

1. Target collection has required basic metadata - in case of SchoolEd it is B, M, C, S
2. Question set created for the target collection carries forward the basic metadata. It is viewable in question set details.
3. Questions created in the question set inherit / derive / carry forward basic metadata from parent question set.

**→** **What if metadata is not present in the target collection?**

For an object, for a primary category, when being created in a particular channel / tenant - if certain required metadata (as per the form definition of primary category in that channel) is empty - the system should prompt user to provide those details. For example,

If B,M,C,S is not available for the question being created - user should be able to and required to provide these values on question creation page.

**But..** what happens when

• creators updated the values of B,M,C,S in question set details - does it automatically push / overwrite children question’s metadata?

Here we should consider two design patterns - _Global or linked (or dependent)_ metadata and _Local or unlinked (or independent)_ metadata.

Linked metadata should only be editable in parent object, e.g. B,M,C,S can be edited only in question set and would reflect accordingly in all questions created under this (current) question set by the creator. Careful not to update questions added from library which were created for some other question set.

Unlinked metadata can be edited independently for each object. Additionally, to ease process of creation - it will be derived once at the time of creation but after that it is independent of question set.

In such a scenario, we may want to consider a mechanism through which users can update metadata of questions in bulk. For example, a table where I can edit B,M,C,S + marks (weightage) + other behaviour (mandatory, Show/hide hints, etc)

**Conclusion**:

* By definition of collection, since question set is also a collection of questions, we should go with unlinked metadata approach.
* We should not have _behavioural_ attributes that can be edited at both question and question set level - for example, show feedback should always be at question set level only
* Metadata for discovery should be independent yet derived at the time of creation if available in the parent. When creating a question, framework + audience + legal attributes are copied once - user can still edit these as per configuration.

See table below for details

|                                                                  | **Question Set** | **Question**                              |
| ---------------------------------------------------------------- | ---------------- | ----------------------------------------- |
| **Name**                                                         | Editable         | Not required                              |
| **Description**                                                  | Editable         | Not required                              |
| **Instruction**                                                  | Editable         | Not available                             |
| **Keywords**                                                     | Editable         | Not available                             |
| **Framework (B, M, C, S, Topics)**                               | Editable         | Derived once, Editable                    |
| **Learning Outcome**                                             | Not required     | Editable                                  |
| **Learning Level**                                               | Not required     | Editable                                  |
| **Shuffle, Show x/y**                                            | Editable         | Not available                             |
| **Show/hide Feedback, Solution, Hints**                          | Editable         | Not available                             |
| **Max Attempts, Submit required,**                               | Editable         | Not available                             |
| **Mandatory**                                                    | Not required     | Editable, in relation to the question set |
| **Visibility**                                                   | Editable         | Not required                              |
| **Scoring logic**                                                |                  | Editable                                  |
| **Evaluation Rubric**                                            | Editable         |                                           |
| **Legal & Ownership (Author, Attributions, Copyright, License)** | Editable         | Derived once, Editable                    |
| **Discovery (Audience, Target framework)**                       |                  |                                           |

\*Editable = If configured in primary category form definition.

\*Not required =

&#x20;

**Visibility**

1. Define Question Set primary category and Question primary category forms
   1. Question Set: Visibility = private
   2. Question: Visibility = parent
2. Define Question form for the Question set primary category
   1. Question in this Question set category: Visibility = private, view-only
   2. Sections in this Question set category:
      1. L1

&#x20;

**Framework**

Que Set: B,M,C,S = required on Submit

Que: B,M,C,S = required on Save

Que in Que Set: B,M,C,S = derived if available, else editable & required on Save
