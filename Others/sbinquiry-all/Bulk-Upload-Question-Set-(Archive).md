Information below is outdated and retained here for archival purpose only.


# Bulk Upload Question Set
[https://project-sunbird.atlassian.net/browse/SB-22801](https://project-sunbird.atlassian.net/browse/SB-22801)

Many times organisations have a pool of questions available in some format - as Word docs on Hard disk, as Scan PDFs of exam papers, as questions in Excel sheet, and so on.

By enabling bulk upload of these questions or question sets would allows us to leverage what is already available in abundance and create maximum value out of it.

→ Bulk uploading of question sets can be done by providing data in the prescribed format. System will create questions, question sets and even link them to a collection (if details are provided).

→ Bulk upload  **format**  should support


1. Uploading of various question categories such as MCQ, Reference, FTB (in future), MTF (in future), and so on..


1. Providing Question set configuration and metadata



→ After bulk uploading, creator can review the uploaded question sets and  **bulk submit**  them for review.

→ System should have a configurable upper limit on number of questions in a question set that can be uploaded.

→ User flow should be similar to Bulk upload of content with an additional step of bulk submit for the contributor. (Check [Issue navigator - JIRA (atlassian.net)](https://project-sunbird.atlassian.net/issues/?jql=text%20~%20bulk%20AND%20project%20in%20(10016)%20AND%20issuetype%20in%20(story%2C%20epic%2C%20enhancement)%20ORDER%20BY%20issuetype%20DESC%2C%20status%20asc))


* User can download prescribed format


* Upload the data for bulk upload job


* (new) Preview question sets created as draft, edit, and submit


* (new) Bulk submit all question sets



→ Reviewer flow remain as-is similar to other bulk upload / approve projects.



Refer to current bulk upload process, template and guidelines here [https://docs.google.com/document/d/1PW5b-Mdie6--wsFhGzC-fxVcPbvax4cA-hJyajr8Xew/edit#](https://docs.google.com/document/d/1PW5b-Mdie6--wsFhGzC-fxVcPbvax4cA-hJyajr8Xew/edit#)



[https://project-sunbird.atlassian.net/browse/SB-23374](https://project-sunbird.atlassian.net/browse/SB-23374)

Bulk upload question set format should support 


1. creating multiple question types (V1 will support MCQ with layouts, Subjective reference questions)


1. creating multiple question sets at once with their details & configurations


1. linking of these question sets to (target) collections



Bulk upload question set workflow is detailed out here in this ticket



[https://project-sunbird.atlassian.net/browse/SB-23375](https://project-sunbird.atlassian.net/browse/SB-23375)

Contributors can access bulk upload question set functionality similar to how they would access bulk upload content functionality. Broadly, bulk upload can happen in context of project with target collection or in framework category driven projects.

As a contributor


1. I can download the prescribed format for uploading question set from the portal. Details of prescribed format are here


1. The question sets are uploaded as  **draft** 


1. Contributor can preview and edit any of the question sets, and the questions in them


1. Contributor can  **bulk submit**  question sets. Bulk Submit is can be performed for any asset in  _draft_  state. It will submit all the draft content for review.



As a reviewer, the workflow remains as-is - I can review assets individually or bulk approve.





|  **Columns / Information to be provided by Contributor**  |  **Description**  |  **In which version**  | 
|  **QUESTION DETAILS**  | 
| Human readable / relatable Name or Title or any identifying value for searching and retrieval later | V1 | 
| MCQ or Subjective? | V1 - MCQ  | 
| Derived from target collection or question set |  | 
| Should be able to create questions for any of the frameworks. If uploaded within a target collection, then relevant metadata (B,M,C,S) is derived from it. Additional metadata (Topics, LO) can be provided. | V1 - B,M,C,S | 
| Body or stem of the question | V1 | 
| Image to be used for the question body User provides Google Drive path. System will insert at the beginning of the text, small size, left aligned |  | 
| Should support min 2 & max 8 options | V1 - Only 4 | 
| Should support Google Drive link for the images. Insert images always at the beginning of the question text in small size & left alignment | V1 | 
| Support Horizontal, Vertical, and Grid layout. Default = vertical. | V1 | 
| Should be a number between 1 - 8 for MCQ. Can be text in case of Subjective questions | V1 | 
|  | V2 | 
|  | V2 | 
|  | V2 | 
| Provide if not same as user name of the creator ID on the platform |  | 
|  |  | 
| Default = Tenant name ? |  | 
| Default / Always = CC BY … ? |  | 
|  **QUESTION SET DETAILS 👇🏽**  | 
| Any unique ID to group the questions | V1 | 
|  |  | 
|  |  | 
| Derived from target collection |  | 
| On / Off |  | 
| Any number < 0 and < total number of questions in the set |  | 
| On / Off |  | 
| On / Off |  | 
| 0 < Attempts < 25 |  | 
| Provide if not same as user name of the creator ID on the platform |  | 
|  |  | 
| Default = Tenant name ? |  | 
| Default / Always = CC BY … ? |  | 
|  --- |  --- |  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
| Human readable / relatable Name or Title or any identifying value for searching and retrieval later | V1 | 
| MCQ or Subjective? | V1 - MCQ  | 
| Derived from target collection or question set |  | 
| Should be able to create questions for any of the frameworks. If uploaded within a target collection, then relevant metadata (B,M,C,S) is derived from it. Additional metadata (Topics, LO) can be provided. | V1 - B,M,C,S | 
| Body or stem of the question | V1 | 
| Image to be used for the question body User provides Google Drive path. System will insert at the beginning of the text, small size, left aligned |  | 
| Should support min 2 & max 8 options | V1 - Only 4 | 
| Should support Google Drive link for the images. Insert images always at the beginning of the question text in small size & left alignment | V1 | 
| Support Horizontal, Vertical, and Grid layout. Default = vertical. | V1 | 
| Should be a number between 1 - 8 for MCQ. Can be text in case of Subjective questions | V1 | 
|  | V2 | 
|  | V2 | 
|  | V2 | 
| Provide if not same as user name of the creator ID on the platform |  | 
|  |  | 
| Default = Tenant name ? |  | 
| Default / Always = CC BY … ? |  | 
| Any unique ID to group the questions | V1 | 
|  |  | 
|  |  | 
| Derived from target collection |  | 
| On / Off |  | 
| Any number < 0 and < total number of questions in the set |  | 
| On / Off |  | 
| On / Off |  | 
| 0 < Attempts < 25 |  | 
| Provide if not same as user name of the creator ID on the platform |  | 
|  |  | 
| Default = Tenant name ? |  | 
| Default / Always = CC BY … ? |  | 

At the time of uploading, the upload page has options such as


1. Upload as draft or Submit for review (on / off)


1. Question set category: (list of primary categories in the project) \[Should this be a column in the sheet?]






### Decision tree

1. Upload question sets in the project 


    1. Format for each question type


    1. Format for all question types



    
1. Upload questions in a question set


    1. Format for each question type


    1. Format for all question types



    


## Open questions

1. Should user upload Question set in a sourcing project or Upload questions in a Question set?


1. Should we have separate CSV formats for each question (interaction) type (primary category) or one single format supporting all types?


    1. Expectation is that each question is checked for validation before uploading



    
1. Should Images be supported? What are the limitations?


1. Questions and Question sets should be in separate sheets - Yes / No?


1. Benefits of using individual formats is that we can do client side validations such as.. Validations during upload (real-time) for Content upload


    1. Name of the columns


    1. Mandatory column cannot be blank


    1. Maximum 300 content per sheet



    
1. Other validations that happen async on server


    1. URL Validation while downloading from source (Google Drive)


    1. Framework values matching


    1. Primary category


    1. File Size limit


    1. ..



    



*****

[[category.storage-team]] 
[[category.confluence]] 
