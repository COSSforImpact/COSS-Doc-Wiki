
# Overview
Examinations are an integral part of the school education process. There are examinations that are conducted by the State at a fixed schedule of the year. Additionally, as part of the regular ongoing teaching and learning process teachers conduct multiple tests, quizzes etc.

Prashnavali is envisioned to create a digitized process pertaining to these two use cases.


## Existing Scenario
 **Question Paper Creation:** Schedule: 6 SAT cycles for all grades (bi-monthly)

Process:


1. Select few teachers come to SCERT and create a question bank only for the upcoming examination


1. SCERT lead, with the role of question paper creation, selects the questions from the pool created at previous step and creates a question paper, which remains confidential


1. Before examination, the question paper is emailed as PDF/Word Doc to the HM (school leaders) to take printout and conduct examinations



 **Question Bank:** No central repository of question bank, past year question paper exists at present.

 **Actors/Users in Prashnavali:** 



|  **Actor**  |  **Action**  |  **Portal**  | 
|  --- |  --- |  --- | 
| Admin | Project Setup and Management (including roles management) | Diksha-web, Vidyadaan | 
| Contributor | Add questions (teachers or 3rd party vendors) | Vidyadaan (contribute) | 
| Question reviewer | Review each question (Subject matter experts) | Vidyadaan (contribute) | 
| Question paper creator | Create final question paper, choosing from approved list of questions | Vidyadaan (sourcing) | 
| Teachers | Search Question bank, Select questions and create a paper | Diksha App, Diksha | 


# Release 3.6

1. [https://project-sunbird.atlassian.net/browse/SB-22258](https://project-sunbird.atlassian.net/browse/SB-22258)


1. [https://project-sunbird.atlassian.net/browse/SB-22259](https://project-sunbird.atlassian.net/browse/SB-22259)



Creators can now contribute (non-interactive) Match the Following and Fill in The Blank through a sourcing project. It is important to note that this is a “non-interactive” question category primarily meant to be used in an exam question paper which are going to be printed. Refer to [the image](https://user-images.githubusercontent.com/19550456/103541631-bd81ff00-4ec1-11eb-8999-283efefce8db.png) for a quick glance at MTF

 _Follow discussion thread here_ : [https://github.com/project-sunbird/sunbird-community/discussions/57](https://github.com/project-sunbird/sunbird-community/discussions/57)


# Release 3.7
 **Configuration changes** 


1. [Create a new Collection Category](https://project-sunbird.atlassian.net/browse/SB-22256) for ‘Exam Question Paper’


1. [Create a new content Category 'Exam Question'](https://project-sunbird.atlassian.net/browse/SB-23136)



 **Functional enhancements** 


1. Sourcing Admin can [Define Blueprint for a collection (question paper](https://project-sunbird.atlassian.net/browse/SB-22263))


1. Sourcing Admin can [View Progress against Blueprint](https://project-sunbird.atlassian.net/browse/SB-22264) to track completion of Question Paper


1. Contributors can [Tag a Question - Competency, chapter covered, Marks\*](https://project-sunbird.atlassian.net/browse/SB-23137)


1. [Remove “Add” button from question set editor for Collection category = Question Paper, Content Type = Exam Question](https://project-sunbird.atlassian.net/browse/SB-23138)


1. [Sourcing Portal Reviewer can filter contributions by Status - Add Status filter](https://project-sunbird.atlassian.net/browse/SB-23139) on Sourcing Portal Reviewer page


1. [Print Preview](https://project-sunbird.atlassian.net/browse/SB-22267) for Admin to check Question Paper before printing



 _Follow discussion thread here_ : [https://github.com/project-sunbird/sunbird-community/discussions/30#discussioncomment-364691](https://github.com/project-sunbird/sunbird-community/discussions/30#discussioncomment-364691)

 **Prashnavali V1 ready to be rolled out** 


# Release 3.8
 **Completed** 


1. [Create new question - Comprehension (New)](https://project-sunbird.atlassian.net/browse/SB-22261): Non-interactive question category. Configuration change.


1. [Blueprint definition - Show error message if anything except numbers is entered in marks field (Bug)](https://project-sunbird.atlassian.net/browse/DP-1630)



 **Descoped from 3.8** 


1. [Print preview - Add support for images](https://project-sunbird.atlassian.net/browse/SB-23508)


1. [Upgrade CKEditor on Vidyadaan (New)](https://project-sunbird.atlassian.net/browse/SB-23506)


1. [Upgrade to the new Question set editor (Refactoring)](https://project-sunbird.atlassian.net/browse/SB-23507) → Design under discussion. Targeting 3.10 / 4.0


1. [Download report (Bug)](https://project-sunbird.atlassian.net/browse/DP-1632) → Backlogged 



 _Follow discussion thread here_ : [https://github.com/project-sunbird/sunbird-community/discussions/175](https://github.com/project-sunbird/sunbird-community/discussions/175)


# Release 3.9

1. [Support for comprehension in Print service](https://project-sunbird.atlassian.net/browse/SB-23979)


1. [Support for images in Print Service](https://project-sunbird.atlassian.net/browse/SB-23980)


1. [Upgrade CKEditor on Vidyadaan](https://project-sunbird.atlassian.net/browse/SB-23506) (Sourcing Solution)


    1. [Enable Math Symbols](https://project-sunbird.atlassian.net/browse/SB-23781) (Special Characters) when creating a question


    1. [Enable resize of images](https://project-sunbird.atlassian.net/browse/SB-23781) when creating a question



    
1. [[Adding text and Image in same line|Inline-image-support-in-the-Question-editor]] - available in latest CK Editor release scheduled on 21st April




# Release 4.0

1. Restrict the Visibility of Questions and question papers to only authorized users. (API level restrictions as well as frontend restrictions)

    Jira Ticket: [Frontend restriction](https://project-sunbird.atlassian.net/browse/SB-24209), API restriction ( _To be created)_ 

    Github Discussion: [#277](https://github.com/project-sunbird/sunbird-community/discussions/277)

    Confluence document: (To be created)

    Size: L


1. QuML Editor upgrade

    Jira Ticket: (To be created)

    Github Discussion: [#271](https://github.com/project-sunbird/sunbird-community/discussions/271)

    Confluence document: [[QuML Editor Upgrade|QuML-Editor-Upgrade]]

    Size: XL


1. Sharing question paper to other applications

    Jira Ticket: (To be created)

    Github Discussion: NA

    Confluence document: [[Sharing question paper to other application|Sharing-question-paper-to-other-application]]

    Size: Unknown


1. Question contribution - Adding inline images (Include CKEditor latest changes) Evaluation is needed, before confirming it for development for 4.0

    Jira Ticket: (To be created)

    Github Discussion: [#177](https://github.com/project-sunbird/sunbird-community/discussions/177)

    Confluence document: [[Inline image support in the Question editor|Inline-image-support-in-the-Question-editor]]

    Size: L


1. Template for question paper 

    Jira Ticket: (To be created)

    Github Discussion: NA

    Confluence document: [[Provision of Templatizing Question Papers during Print  |Provision-of-Templatizing-Question-Papers-during-Print  ]]

    Size: XL


1. Question content editing by reviewer

    Jira Ticket: (To be created)

    Github Discussion: [#242](https://github.com/project-sunbird/sunbird-community/discussions/242)

    Confluence document: [[Editing of Questions during review of question by Question Reviewer|Editing-of-Questions-during-review-of-question-by-Question-Reviewer]]

    Size: unknown







|  **Category**  |  **Overview**  |  **Priority**  |  **Development Cycle**  |  **Task Size**  |  **Status**  | 
|  --- |  --- |  --- |  --- |  --- |  --- | 
| Print | [Support for comprehension](https://project-sunbird.atlassian.net/browse/SB-23979) | P1 (critical) | 3.9 | S | PR MeregedGreenTestingYellowSamagra to share tests report | 
| Print | [Support for images](https://project-sunbird.atlassian.net/browse/SB-23980) | P1 (Critical) | 3.9 | L | PR MeregedGreenTestingYellowSamagra to share tests report | 
| Question Contribution | [Enable Math Symbols](https://project-sunbird.atlassian.net/browse/SB-23781) | P1 | 3.9 | S | PR SubmittedYellowSamagra / EkStep TO will merge PR? | 
| Question Contribution | [Enable resize of images](https://project-sunbird.atlassian.net/browse/SB-23781) | P1 | 3.9 | S | PR SubmittedYellowSamagra / EkStep TO will merge PR? | 
| Question Contribution | [[Adding text and Image in same line|Inline-image-support-in-the-Question-editor]] | P1 | 3.9 | L | on holdRedDependent on external (CkEditor, open-source project) team to fix it. They have committed to a new release on 21st April | 
| Vulnerability  | [Hide Public link for a Question](https://project-sunbird.atlassian.net/browse/SB-24209) | P1 | 3.9 | M | Requirement FinalizedGreenProduct decision pendingRedEngineering discussion pendingRed  **_Pending on decision from Ekstep team_**  | 
| Vulnerability | [Make restrictions at the API level](https://github.com/project-sunbird/sunbird-community/discussions/277) | P1 | 4.0 | ? | RequirementGreenProduc decision pendingRedEngineering Approach pendingRed  **_Pending on Inputs from Ekstep team_**  | 
| Refactor | [[QuML Editor Upgrade|QuML-Editor-Upgrade]] | P1 | 4.0 | XL | RequiremntGreenProduct decisionGreenEngineering discussion pendingRedOpen items:  1) Adding sections in question set -  **_Owner Ekstep_**  2) Enginnering design for project creation -  **_Owner Ekstep_**  3) Task break down of Question Review flow - Contribution -  **_Owner Samagra_**  4) Task break down of Question Review flow - Sourcing -  **_Owner Samagra_**  | 
| Sharing question paper across aspps | [[Sharing question paper to other application|Sharing-question-paper-to-other-application]] | P1 | 4.0 | ? | Requirement under discussion  **_Pending on Inputs from Ekstep team_**  | 
| Question Contribution | [[Adding text and Image in same line|Inline-image-support-in-the-Question-editor]] | P1 | 4.0 | L | To be reviewedYellowDependent on external (CkEditor, open-source project) team to fix it. They have committed to a new release on 21st April  **_Pending on Samagra team_** [https://github.com/ckeditor/ckeditor5/issues/9394](https://github.com/ckeditor/ckeditor5/issues/9394) | 
| Print preview | [Template for question paper](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2246246401/Provision+of+Templatizing+Question+Papers+during+Print) | P1 | 4.0 | L | requirement to finalizedRedEngineering Approach not FinalizedRed  **_Pending on Inputs from Ekstep team_**  | 
| Question content editing | [[Editing of Questions during review of question by Question Reviewer|Editing-of-Questions-during-review-of-question-by-Question-Reviewer]] | P1 | 4.0 | L | requirement to finalizedRedEngineering Approach not FinalizedRed  **_Pending on Samagra Team_**  | 



*****

[[category.storage-team]] 
[[category.confluence]] 
