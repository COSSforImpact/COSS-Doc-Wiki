---
icon: elementor
---

# Data migration problem and approach

### Problem Statement <a href="#datamigrationproblemandapproach-problemstatement" id="datamigrationproblemandapproach-problemstatement"></a>

With the introduction of breaking changes like multi lingual capability and QuML compliance, there was a need to support backward compatibility.

The approach that was taken was to do the following

* Reading to do on the fly (on-demand) transformation of question and questionSet in QuML 1.0 format to QuML 1.1 format
* Updating to do transformation of QuML 1.0 question and questionSet to QuML 1.1 and store the changes permanently.

With the pursued approach, there is a limitation encountered with the QuestionSets that contains questions which are of global visibility (i.e that can be added to any questionSets)

This is the case with crowd sourced questions which is created through CoKreat and brought into InQuiry (ED) using question import features.

Possibilities of QuestionSet is as below,

**Possibility 1**

```
QuestionSet
  - Q1 (Parent Visibility)
  - Q2 (Parent Visibility)
```

Visibility Parent means that the question can be used only within that QuestionSet and cannot be used outside

**Possibility 2**

```
QuestionSet
  - Q1 (Parent Visibility)
  - Q2 (Default Visibility)
```

Visibility Default means that the question can be used in any QuestionSet

#### On-demand migration and problem <a href="#datamigrationproblemandapproach-on-demandmigrationandproblem" id="datamigrationproblemandapproach-on-demandmigrationandproblem"></a>

When the creator edits a questionSet, we can do an auto migration to QuML 1.1.

This is straightforward when all the Questions in the QuestionSet is of visibility Parent (as explained in the Possibility 1)

When the QuestionSet contains Questions in mixed visibility (as explained in Possibility 2), we cannot auto migrate all the questions. As the visibility Default question could be in use in some other QuestionSet which is yet to be migrated.

## Solutions to overcome this <a href="#datamigrationproblemandapproach-solutionstoovercomethis" id="datamigrationproblemandapproach-solutionstoovercomethis"></a>

The below table looks at some of the possible solutions to over come this,

<\<Draft>>

Migrated Question will not be playable in the Old Player

Newly created Questions will not be playable in the Old Player

| **Solution Description**                            | **Pros**                                                                                                                                                                                                                                                                             | **Cons**                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| On demand migration - WITH end user intervention    | <ul><li><p>Only QuestionSet that is updated will be migrated</p><ul><li>Other QuestionSet will NOT be migrated and consumption from Old Player will not effected</li></ul></li></ul>                                                                                                 | <ul><li>End user is made aware of the migration and there will be a call to action (Migrate button)</li><li><p>We can’t do migration of the Questions that are public (Visibility Default)</p><ul><li>Questions that cannot be migrated will need to be removed (Visibility Default) from the QuestionSet. Again needs user action.</li></ul></li></ul>                                                                                              |
| On demand migration - WITHOUT end user intervention | <ul><li>End user is NOT aware of the migration and there will be NO call to action (Migrate button)</li><li>All the Questions (Visibility Default OR Parent) will be migrated</li></ul>                                                                                              | <ul><li>Need a deep copy of the Question that is Visibility Default and create it as Visibility Parent</li><li>If there was one Default Question now there will be multiple Questions each specific to a QuestionSet</li></ul><p><strong>Question</strong></p><ul><li>In the context of adopters using inQuiry what is the volume of questions that is Default Visibility and how many QuestionSets uses it? [Diksha / VDN / iGot / UPSMF]</li></ul> |
| Static Migration                                    | <ul><li>No need for on-demand / on the fly data transformation</li><li>Only one time of migrating the old Question / QuestionSet and any new will be created in QuML 1.1 format</li></ul>                                                                                            | <ul><li>Consumption of old LIVE question and QuestionSet will be stopped immediately after the migration</li></ul><p><strong>Question</strong></p><ul><li>What is the amount of Question / QuestionSet in production system of adopters that will be affected.</li><li>What is the impact to adopters?</li></ul>                                                                                                                                     |
| Static Migration - With data versioning             | <ul><li>No need for on-demand / on the fly data transformation</li><li>Only one time of migrating the old Question / QuestionSet and any new will be created in QuML 1.1 format</li><li>Migrated questions will be playable in old player as the Question is now versioned</li></ul> | <ul><li><p>A copy of the old version data needs to be stored in the cloud when the migration happens</p><ul><li>If an adopter uses 6.0.0 release without following the Static migration procedure, then the QuestionSet will not be playable</li><li>Needs extensive changes to the Old and New APIs to consider the version parameter for reading purpose</li></ul></li></ul>                                                                       |
| No Migration                                        | <ul><li>New Question / QuestionSet will be playable in New Player</li><li>Old Question / QuestionSet will be playable in Old and New Player</li></ul>                                                                                                                                | <ul><li>Old QuestionSets cannot be modified</li><li>Old QuestionSets cannot be updated and sent for review or publish</li><li>New Questions will work only with New QuestionSet</li><li>Migrated Question will not be playable in the Old Player</li></ul>                                                                                                                                                                                           |

Static Migration will need new jobs to be developed as reference for the adopters for extension.

## Solutions picked & conclusion <a href="#datamigrationproblemandapproach-solutionspicked-and-conclusion" id="datamigrationproblemandapproach-solutionspicked-and-conclusion"></a>

<\<TODO>>
