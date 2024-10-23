---
icon: elementor
---

# Exam Question Paper (Prashnavali)

## Overview <a href="#examquestionpaper-prashnavali-overview" id="examquestionpaper-prashnavali-overview"></a>

Examinations are an integral part of the school education process. There are examinations that are conducted by the State at a fixed schedule of the year. Additionally, as part of the regular ongoing teaching and learning process teachers conduct multiple tests, quizzes etc.

Prashnavali is envisioned to create a digitized process pertaining to these two use cases.

### Existing Scenario <a href="#examquestionpaper-prashnavali-existingscenario" id="examquestionpaper-prashnavali-existingscenario"></a>

**Question Paper Creation:**

Schedule: 6 SAT cycles for all grades (bi-monthly)

Process:

1. Select few teachers come to SCERT and create a question bank only for the upcoming examination
2. SCERT lead, with the role of question paper creation, selects the questions from the pool created at previous step and creates a question paper, which remains confidential
3. Before examination, the question paper is emailed as PDF/Word Doc to the HM (school leaders) to take printout and conduct examinations

**Question Bank:**

No central repository of question bank, past year question paper exists at present.

**Actors/Users in Prashnavali:**

| **Actor**              | **Action**                                                            | **Portal**             |
| ---------------------- | --------------------------------------------------------------------- | ---------------------- |
| Admin                  | Project Setup and Management (including roles management)             | Diksha-web, Vidyadaan  |
| Contributor            | Add questions (teachers or 3rd party vendors)                         | Vidyadaan (contribute) |
| Question reviewer      | Review each question (Subject matter experts)                         | Vidyadaan (contribute) |
| Question paper creator | Create final question paper, choosing from approved list of questions | Vidyadaan (sourcing)   |
| Teachers               | Search Question bank, Select questions and create a paper             | Diksha App, Diksha     |

***

## Release 3.6 <a href="#examquestionpaper-prashnavali-release3.6" id="examquestionpaper-prashnavali-release3.6"></a>

1. [https://project-sunbird.atlassian.net/browse/SB-22258](https://project-sunbird.atlassian.net/browse/SB-22258)
2. [https://project-sunbird.atlassian.net/browse/SB-22259](https://project-sunbird.atlassian.net/browse/SB-22259)

Creators can now contribute (non-interactive) Match the Following and Fill in The Blank through a sourcing project. It is important to note that this is a “non-interactive” question category primarily meant to be used in an exam question paper which are going to be printed. Refer to [the image](https://user-images.githubusercontent.com/19550456/103541631-bd81ff00-4ec1-11eb-8999-283efefce8db.png) for a quick glance at MTF

_Follow discussion thread here_: [https://github.com/project-sunbird/sunbird-community/discussions/57](https://github.com/project-sunbird/sunbird-community/discussions/57)

## Release 3.7 <a href="#examquestionpaper-prashnavali-release3.7" id="examquestionpaper-prashnavali-release3.7"></a>

**Configuration changes**

1. [Create a new Collection Category](https://project-sunbird.atlassian.net/browse/SB-22256) for ‘Exam Question Paper’
2. [Create a new content Category 'Exam Question'](https://project-sunbird.atlassian.net/browse/SB-23136)

**Functional enhancements**

1. Sourcing Admin can [Define Blueprint for a collection (question paper](https://project-sunbird.atlassian.net/browse/SB-22263))
2. Sourcing Admin can [View Progress against Blueprint](https://project-sunbird.atlassian.net/browse/SB-22264) to track completion of Question Paper
3. Contributors can [Tag a Question - Competency, chapter covered, Marks\*](https://project-sunbird.atlassian.net/browse/SB-23137)
4. [Remove “Add” button from question set editor for Collection category = Question Paper, Content Type = Exam Question](https://project-sunbird.atlassian.net/browse/SB-23138)
5. [Sourcing Portal Reviewer can filter contributions by Status - Add Status filter](https://project-sunbird.atlassian.net/browse/SB-23139) on Sourcing Portal Reviewer page
6. [Print Preview](https://project-sunbird.atlassian.net/browse/SB-22267) for Admin to check Question Paper before printing

_Follow discussion thread here_: [https://github.com/project-sunbird/sunbird-community/discussions/30#discussioncomment-364691](https://github.com/project-sunbird/sunbird-community/discussions/30#discussioncomment-364691)

**Prashnavali V1 ready to be rolled out**

## Release 3.8 <a href="#examquestionpaper-prashnavali-release3.8" id="examquestionpaper-prashnavali-release3.8"></a>

**Completed**

1. [Create new question - Comprehension (New)](https://project-sunbird.atlassian.net/browse/SB-22261): Non-interactive question category. Configuration change.
2. [Blueprint definition - Show error message if anything except numbers is entered in marks field (Bug)](https://project-sunbird.atlassian.net/browse/DP-1630)

**Descoped from 3.8**

1. [Print preview - Add support for images](https://project-sunbird.atlassian.net/browse/SB-23508)
2. [Upgrade CKEditor on Vidyadaan (New)](https://project-sunbird.atlassian.net/browse/SB-23506)
3. [Upgrade to the new Question set editor (Refactoring)](https://project-sunbird.atlassian.net/browse/SB-23507) → Design under discussion. Targeting 3.10 / 4.0
4. [Download report (Bug)](https://project-sunbird.atlassian.net/browse/DP-1632) → Backlogged

_Follow discussion thread here_: [https://github.com/project-sunbird/sunbird-community/discussions/175](https://github.com/project-sunbird/sunbird-community/discussions/175)

## Release 3.9 <a href="#examquestionpaper-prashnavali-release3.9" id="examquestionpaper-prashnavali-release3.9"></a>

1. [Support for comprehension in Print service](https://project-sunbird.atlassian.net/browse/SB-23979)
2. [Support for images in Print Service](https://project-sunbird.atlassian.net/browse/SB-23980)
3. [Upgrade CKEditor on Vidyadaan](https://project-sunbird.atlassian.net/browse/SB-23506) (Sourcing Solution)
   1. [Enable Math Symbols](https://project-sunbird.atlassian.net/browse/SB-23781) (Special Characters) when creating a question
   2. [Enable resize of images](https://project-sunbird.atlassian.net/browse/SB-23781) when creating a question
4. [Adding text and Image in same line](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2416705560/Inline+image+support+in+the+Question+editor) - available in latest CK Editor release scheduled on 21st April

***

## Release 4.0 <a href="#examquestionpaper-prashnavali-release4.0" id="examquestionpaper-prashnavali-release4.0"></a>

1. Restrict the Visibility of Questions and question papers to only authorized users. (API level restrictions as well as frontend restrictions)\
   Jira Ticket: [Frontend restriction](https://project-sunbird.atlassian.net/browse/SB-24209), API restriction (_To be created)_\
   Github Discussion: [#277](https://github.com/project-sunbird/sunbird-community/discussions/277)\
   Confluence document: (To be created)\
   Size: L
2. QuML Editor upgrade\
   Jira Ticket: (To be created)\
   Github Discussion: [#271](https://github.com/project-sunbird/sunbird-community/discussions/271)\
   Confluence document: [QuML Editor Upgrade](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2341208118/QuML+Editor+Upgrade)\
   Size: XL
3. Sharing question paper to other applications\
   Jira Ticket: (To be created)\
   Github Discussion: NA\
   Confluence document: [Sharing question paper to other application](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2497282066/Sharing+question+paper+to+other+application)\
   Size: Unknown
4. Question contribution - Adding inline images (Include CKEditor latest changes) Evaluation is needed, before confirming it for development for 4.0\
   Jira Ticket: (To be created)\
   Github Discussion: [#177](https://github.com/project-sunbird/sunbird-community/discussions/177)\
   Confluence document: [Inline image support in the Question editor](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2416705560/Inline+image+support+in+the+Question+editor)\
   Size: L
5. Template for question paper\
   Jira Ticket: (To be created)\
   Github Discussion: NA\
   Confluence document: [Provision of Templatizing Question Papers during Print  ](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2246246401/Provision+of+Templatizing+Question+Papers+during+Print)\
   Size: XL
6. Question content editing by reviewer\
   Jira Ticket: (To be created)\
   Github Discussion: [#242](https://github.com/project-sunbird/sunbird-community/discussions/242)\
   Confluence document: [Editing of Questions during review of question by Question Reviewer](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2245328958/Editing+of+Questions+during+review+of+question+by+Question+Reviewer)\
   Size: unknown

***

| **Category**                        | **Overview**                                                                                                                                                                                                      | **Priority**  | **Development Cycle** | **Task Size** | **Status**                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | --------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Print                               | [Support for comprehension](https://project-sunbird.atlassian.net/browse/SB-23979)                                                                                                                                | P1 (critical) | 3.9                   | S             | <p>PR MEREGED TESTING</p><p>Samagra to share tests report</p>                                                                                                                                                                                                                                                                                                                                                                                                      |
| Print                               | [Support for images](https://project-sunbird.atlassian.net/browse/SB-23980)                                                                                                                                       | P1 (Critical) | 3.9                   | L             | <p>PR MEREGED TESTING</p><p>Samagra to share tests report</p>                                                                                                                                                                                                                                                                                                                                                                                                      |
| Question Contribution               | [Enable Math Symbols](https://project-sunbird.atlassian.net/browse/SB-23781)                                                                                                                                      | P1            | 3.9                   | S             | <p>PR SUBMITTED</p><p>Samagra / EkStep TO will merge PR?</p>                                                                                                                                                                                                                                                                                                                                                                                                       |
| Question Contribution               | [Enable resize of images](https://project-sunbird.atlassian.net/browse/SB-23781)                                                                                                                                  | P1            | 3.9                   | S             | <p>PR SUBMITTED</p><p>Samagra / EkStep TO will merge PR?</p>                                                                                                                                                                                                                                                                                                                                                                                                       |
| Question Contribution               | [Adding text and Image in same line](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2416705560/Inline+image+support+in+the+Question+editor)                                                          | P1            | 3.9                   | L             | <p>ON HOLD</p><p>Dependent on external (CkEditor, open-source project) team to fix it. They have committed to a new release on 21st April</p>                                                                                                                                                                                                                                                                                                                      |
| Vulnerability                       | [Hide Public link for a Question](https://project-sunbird.atlassian.net/browse/SB-24209)                                                                                                                          | P1            | 3.9                   | M             | <p>REQUIREMENT FINALIZED PRODUCT DECISION PENDING ENGINEERING DISCUSSION PENDING<br><em><strong>Pending on decision from Ekstep team</strong></em></p>                                                                                                                                                                                                                                                                                                             |
| Vulnerability                       | [Make restrictions at the API level](https://github.com/project-sunbird/sunbird-community/discussions/277)                                                                                                        | P1            | 4.0                   | ?             | <p>REQUIREMENT PRODUC DECISION PENDING ENGINEERING APPROACH PENDING<br><em><strong>Pending on Inputs from Ekstep team</strong></em></p>                                                                                                                                                                                                                                                                                                                            |
| Refactor                            | [QuML Editor Upgrade](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2341208118/QuML+Editor+Upgrade)                                                                                                 | P1            | 4.0                   | XL            | <p>REQUIREMNTPRODUCT DECISION ENGINEERING DISCUSSION PENDING</p><p>Open items:<br>1) Adding sections in question set - <em><strong>Owner Ekstep</strong></em><br>2) Enginnering design for project creation - <em><strong>Owner Ekstep</strong></em><br>3) Task break down of Question Review flow - Contribution - <em><strong>Owner Samagra</strong></em><br>4) Task break down of Question Review flow - Sourcing - <em><strong>Owner Samagra</strong></em></p> |
| Sharing question paper across aspps | [Sharing question paper to other application](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2497282066/Sharing+question+paper+to+other+application)                                                 | P1            | 4.0                   | ?             | <p>REQUIREMENT UNDER DISCUSSION<br><em><strong>Pending on Inputs from Ekstep team</strong></em></p>                                                                                                                                                                                                                                                                                                                                                                |
| Question Contribution               | [Adding text and Image in same line](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2416705560/Inline+image+support+in+the+Question+editor)                                                          | P1            | 4.0                   | L             | <p>TO BE REVIEWED</p><p>Dependent on external (CkEditor, open-source project) team to fix it. They have committed to a new release on 21st April<br><em><strong>Pending on Samagra team</strong></em></p><p><a href="https://github.com/ckeditor/ckeditor5/issues/9394">https://github.com/ckeditor/ckeditor5/issues/9394</a></p>                                                                                                                                  |
| Print preview                       | [Template for question paper](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2246246401/Provision+of+Templatizing+Question+Papers+during+Print)                                                      | P1            | 4.0                   | L             | <p>REQUIREMENT TO FINALIZED ENGINEERING APPROACH NOT FINALIZED<br><em><strong>Pending on Inputs from Ekstep team</strong></em></p>                                                                                                                                                                                                                                                                                                                                 |
| Question content editing            | [Editing of Questions during review of question by Question Reviewer](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2245328958/Editing+of+Questions+during+review+of+question+by+Question+Reviewer) | P1            | 4.0                   | L             | <p>REQUIREMENT TO FINALIZED ENGINEERING APPROACH NOT FINALIZED<br><em><strong>Pending on Samagra Team</strong></em></p>                                                                                                                                                                                                                                                                                                                                            |
