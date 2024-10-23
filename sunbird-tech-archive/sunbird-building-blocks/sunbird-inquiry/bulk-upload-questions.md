---
icon: elementor
---

# Bulk Upload Questions

## Bulk Upload Questions <a href="#bulkuploadquestions-bulkuploadquestions" id="bulkuploadquestions-bulkuploadquestions"></a>

[https://project-sunbird.atlassian.net/browse/SB-22801](https://project-sunbird.atlassian.net/browse/SB-22801)

Teachers have a large pool of questions they would have already created for conducting tests, quizzes, and exams. We want to leverage all these assets available in abundance in the community of educators through ecosystem participation. We have seen following scenarios where the need of bulk upload of questions has come up:

1. An organisation already have questions in an existing system. Hence creating them manually through UI is a lot of effort
2. An organisation is creating new questions, but wants to import questions in multiple systems, not just Sunbird (e.g. DIKSHA). Hence they would like to keep the questions in a common spreadsheet format and bulk uploaded into multiple systems
3. An organization is creating new questions and also simultaneously getting the questions translated into multiple languages. Hence having the questions in a spreadsheet is easy to share them with multiple translators and get the translations done.

Sunbird enables creation of question sets through various workflows enabled in Sourcing solution. We plan to complement those workflows by enabling bulk upload of questions in following workflows (in order of priority)

1. Bulk upload questions within a question set such that questions are linked at the right place in the question set. Here the question set might be created in a target collection driven sourcing project or in a taxonomy driven sourcing project.
2. Bulk upload questions within a question set such that questions are linked at the right place in the question set. Here the question set is the target object in a sourcing project.
3. (Future) Bulk upload questions in a framework driven sourcing project.

To enable 1 & 2 above, capabilities fundamentally requires

1. Ability to bulk upload questions
2. Link them at the right place in a question set

We will be enabling bulk upload of questions and linking them to a question set considering CSV (comma separated values) input. Users are likely to use tools such as Google Sheets, Microsoft Office Excel, and other spreadsheet editing tools. Detailing out the key milestones below

The goal is to upload questions with its associate media (images)

1. Support Multiple Choice Question (MCQ) with validations such as
   1. Minimum 2 options, maximum 4 options
   2. At least and only one correct option
2. Question and Options can have images - provided as Google Drive public link. Google Drive path for image is provided by user which is extracted by system (bulk upload tool).
   1. Images will be placed at the beginning of the text with left align and small size (25%).
3. Question and Options can have either Images only or text only or both.
4. User can download sample bulk upload format. User provides CSV in the prescribed format filled with required details.
5. Mandatory columns (configurable) are coloured in **red**.
6. Basic validations such as
   1. Text contains only unicode characters
   2. Any cell does not contain any images
   3. All mandatory columns are filled for a particular row in CSV

### Explanation of Bulk Upload Question format <a href="#bulkuploadquestions-explanationofbulkuploadquestionformat" id="bulkuploadquestions-explanationofbulkuploadquestionformat"></a>

[https://docs.google.com/spreadsheets/d/1ndzapGGV6q8698x-NQzK\_ufln4YX1HQ09jsFsC7kA60/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1ndzapGGV6q8698x-NQzK\_ufln4YX1HQ09jsFsC7kA60/edit?usp=sharing)

#### Details to be provided by contributor using CSV format <a href="#bulkuploadquestions-detailstobeprovidedbycontributorusingcsvformat" id="bulkuploadquestions-detailstobeprovidedbycontributorusingcsvformat"></a>

1. **Name** is set to default as _Multiple Choice Question_ for this version.
   1. Mandatory: No
   2. Default: Multiple Choice Question
   3. Validations: - Upto 120 characters - No special characters
   4. Tip: Please provide name for the question
2. **Question Text** will support text as per the _Text validations_ listed below. Maximum character limit for Question Text is 1000 (configurable). _Question Text_ and _Question Image_ are merged to compose the _Question Body_. Question Body is required to create a question in the platform.
   1. Mandatory: Conditional - any one of text or image should be provided.
   2. Default: None
   3. Validation: Length not more than 1000 characters.
   4. Tip: Provide text in Unicode.
3. **Question Image** will support Google Drive path (publicly accessible) for images. Images will be placed at the beginning of the _Question Text_ with left align and small size (25%) styling.
   1. Mandatory: Conditional - any one of text or image should be provided.
   2. Default: None
   3. Validation: Only JPG format. Google Drive Link - Publicly accessible.
   4. Tip: Only JPG format. Google Drive Link - Publicly accessible.
4. **Option Layout** will support three possible values: Horizontal, Vertical, Grid OR 1, 2, 3. Default value = Vertical.
   1. Mandatory: Yes
   2. Default: None
   3. Validation: Only 1, 2, or 3
   4. Tip: Layout number = Needs involved decision making, depending on question length and answer/option length.\
      1 = vertical (most flexible)\
      2 = horizontal (suitable for one-two words or images)\
      3 = grid (suitable for a few words or images)
5. **OptionX** will support text as per the _Text validations_ listed below. Maximum character limit for Option Text is 500 (configurable). _Option Text_ and _Option Image_ are merged to compose the _Option Body_. Option Body is required to create a question in the platform.\
   (Same as Question Text)
   1. Mandatory: Conditional - any one of text or image should be provided.
   2. Default: None
   3. Validation: Length not more than 1000 characters. Minimum 2 options, maximum 4 options.
   4. Tip: Provide text in Unicode.
6. **OptionXImage** will support Google Drive path (publicly accessible) for images. Images will be placed at the beginning of the _Option Text_ with left align and small size (25%) styling.\
   (Same as Question Image)
   1. Mandatory: Conditional - any one of text or image should be provided.
   2. Default: None
   3. Validation: Only JPG format. Google Drive Link - Publicly accessible.
   4. Tip: Only JPG format. Google Drive Link - Publicly accessible.
7. **Answer No** will be a number between 1 to 4.
   1. Mandatory: Yes
   2. Default: None
   3. Validation: At least and only one correct option. Only 1, 2, 3, or 4. If user has provided only 2 options and provided “3” as correct answer, system should throw an error.
   4. Tip: Enter Correct answer option value between 1 to 4
8. **Level 1 Question Set Section** will be Level 1 Section’s (unit) Name so that question can be linked to that folder.
   1. Mandatory: No
   2. Default: None
   3. Validation: Should match with the names provided in the question set hierarchy. Not case-sensitive / Case insensitive.
   4. Tip: Provide name of the folder where you want to upload a question
9. **Keywords**
   1. Mandatory: No
   2. Default: None
   3. Validation: Comma separated values. No special characters.
   4. Tip: Keywords
10. **Audience**
    1. Mandatory: No
    2. Default: Audience category of the Question Set (derived value).
    3. Validation: Supported values in the platform
    4. Tip: Audience of the question. Should be same as audience of the question set.
11. **Author**
    1. Mandatory: No
    2. Default: None
    3. Validation: No special characters. Max 300 characters.
    4. Tip: The person or organization who has authored the content
12. **Copyright**
    1. Mandatory: No
    2. Default: Name of the tenant.
    3. Validation: No special characters. Max 300 characters.
    4. Tip: Person or Organization who owns the copyright. Default name is DIKSHA tenant.
13. **Attributions**
    1. Mandatory: No
    2. Default: None
    3. Validation: No special characters. Max 300 characters.
    4. Tip: List of persons or organizations who have contributed to this content.

#### Details to be pre-filled / derived by system <a href="#bulkuploadquestions-detailstobepre-filled-derivedbysystem" id="bulkuploadquestions-detailstobepre-filled-derivedbysystem"></a>

1. **Question Category** will be _Multiple Choice Question_ for this version_._
   1. Mandatory: Yes
   2. Default: MCQ
   3. Validation: If anything other than MCQ, reject the question
   4. Tip: Always fill "MCQ"
2. **Additional Category** is derived from the question set
   1. Mandatory: No
   2. Default: Primary category of the Question Set (derived value).
   3. Validation:
   4. Tip: Purpose of the question. Should be same as content type of question set.
3. **Target Question Set ID** to be auto-derived when user is uploading questions within a question set. This will _not be shown in the CSV_ upload format to the contributor.
   1. Mandatory: Yes
   2. Default: Question Set ID where Question Upload file was provided
   3. Validation: Should exist in the platform
   4. Tip: Identifier of the Question Set where questions are to be linked
4. **Taxonomy Framework Categories**: These will derived from the Question set when questions are being uploaded within a question set. Questions can be uploaded in a question created for any framework - all available categories should be derived and tagged to questions. Below are sample categories for K-12 framework:
   1. **Org\_FW\_Board**
   2. **Org\_FW\_Medium**
   3. **Org\_FW\_Class**
   4. **Org\_FW\_Subject**
   5. **Org\_FW\_Topic**
   6. **Org\_FW\_LearningOutcome** is not supported in bulk upload sheet. User can edit from UI.
   7. **Org\_FW\_Skill** is not supported in bulk upload sheet. User can edit from UI.
5. **License**
   1. Mandatory: No
   2. Default: License of the tenant (derived).
   3. Validation: No special characters. Max 300 characters.
   4. Tip: One of the supported licenses in DIKSHA. If this is empty, default to the default license configured for the tenant.

Editing questions and details: After uploading questions, contributor can edit details as configured in the primary category of the question set. Math Formulae, Additional text formatting, and other rich text features can be used in the editor.

#### User flow - Contributor <a href="#bulkuploadquestions-userflow-contributor" id="bulkuploadquestions-userflow-contributor"></a>

**Flow 1**: Contributors will be able to upload questions within a question set

As a **contributor** I should be able to bulk upload questions for a question set in a sourcing project. Following is the flow to enable this:

1. When a contributor logs into contribution portal and opens a target collection page of a project to which she can contribute (i.e. her nomination is accepted), currently against each target collection there is a “Create New” action using which user can create a question set.
2. Given user has access to a sourcing project where she can contribute, When she creates a question set within the sourcing project, Then she can upload questions to the question set
3. User will see an option to “Bulk Upload Question” in the question set similar to “QR codes” in the collection/question set editor.
4. Clicking “Bulk Upload Question” option, Bulk Upload Question screen should open up. The screen should have following options
   1. Option to select a Bulk Upload Question (metadata) file from local folder (of user’s system)\
      _Assumption: the metadata file will have publicly accessible URLs to the question related files_
   2. There is a link to sample metadata file: “Sample Bulk Upload Question metadata file”
   3. User selects metadata file, user clicks “Upload”. System provides a message “Validating file”
   4. The system should first validate metadata file against the selected files. Following are the validations:
      1. All the columns are available
      2. All the mandatory columns have values filled in
5. In case there are errors in the metadata file validation, display relevant error message on the Upload dialog
   1. Some columns are not available:\
      “Metadata file validation failed. Following columns are not found in the file. Please check and upload again: \<list the missing column names>”
   2. Some mandatory columns have values missing:\
      “Metadata file validation failed. Following rows have missing values. Please check and upload again: \<list the row numbers (starting from 1) with missing values>“
6. In case of metadata file validation errors, “Upload” button is disabled unless user re-selects a metadata file again.
7. In case metadata file doesn’t have any validation errors, the dialog shows\
   “Bulk Upload is in progress.\
   Number of questions uploaded successfully: \<no.>\
   Number of questions failed: \<no.>\
   Number of questions pending: \<no.>”
8. After the bulk upload is complete. There is an option to download status report as a [csv](https://docs.google.com/spreadsheets/d/1DIQf1UqM47Nf0EihMwVbHyjVtMga1gUDiOhB-MKms9s/edit?usp=sharing). The status report should include identifier of the question (as generated by the system i.e. API response) and status (Success, Failure, Error, Invalid, etc)
9. User can close it dialog box while a bulk upload is in progress.
10. In the Question Set page, whenever user clicks “Bulk Upload Questions”, in case a bulk upload is in progress, it shows the status dialog as described in point 8. (_This will be in future since we do not have support for background / minimised upload in the first version_)
11. User can edit any question after it is uploaded and saved as draft in the question set. Using this user can Learning Outcome or any other detail of the question.

Limits on number of question, size:

* Number of question per question set for one bulk upload job: 300. Maximum 300 questions per CSV
* Maximum size of each content is same as max size supported by system.

***

### Reference material <a href="#bulkuploadquestions-referencematerial" id="bulkuploadquestions-referencematerial"></a>

1. Bulk Upload Question Guidelines (current manual script driven process) [https://docs.google.com/document/d/1PW5b-Mdie6--wsFhGzC-fxVcPbvax4cA-hJyajr8Xew/edit#heading=h.we2s93hce9f4](https://docs.google.com/document/d/1PW5b-Mdie6--wsFhGzC-fxVcPbvax4cA-hJyajr8Xew/edit#heading=h.we2s93hce9f4)
2. Bulk Upload Content related [Bulk Content Upload on VDN](https://project-sunbird.atlassian.net/wiki/spaces/DO/pages/1581350917/Bulk+Content+Upload+on+VDN)
   1. [https://project-sunbird.atlassian.net/browse/DP-18](https://project-sunbird.atlassian.net/browse/DP-18)
   2. [https://project-sunbird.atlassian.net/browse/DP-947](https://project-sunbird.atlassian.net/browse/DP-947)
   3. [https://project-sunbird.atlassian.net/browse/DP-967](https://project-sunbird.atlassian.net/browse/DP-967)
   4. [https://project-sunbird.atlassian.net/browse/DP-1480](https://project-sunbird.atlassian.net/browse/DP-1480)

#### Implementation details <a href="#bulkuploadquestions-implementationdetails" id="bulkuploadquestions-implementationdetails"></a>

1. Create a generate QuML API for various interaction types such that it takes required parameters as input and generate a QuML output. For example, Multiple Choice Question fundamentally contains Question, Options, and Correct Answer. The API takes these 3 as inputs in HTML or JSON format and generates a QuML spec. This also allows QuML to evolve rapidly as just by updating this ‘Generate QuML’ API with latest QuML spec, we can upgrade various places where Questions & Question sets are getting created such as Question Set Editor, Bulk Upload Questions & Question sets.
   1. This logic exists today ingrained in the Question creation component. It needs to be extracted out and made available as API / something.
2. [Kartheek Palla](https://project-sunbird.atlassian.net/wiki/people/557058:9f800fda-c0d5-42bd-896d-d7b80b367795?ref=confluence) What will be the technology stack? Please list out specific tech stack
   1. Angular (version 9) and Java (with Scala)
3. Images: Extracting files from Google Drive is already available as a component in context of ‘Bulk Upload Content’. Read more [here](https://project-sunbird.atlassian.net/browse/DP-1480).
4. Images also exist independently as Media Asset in the system - so first they need to be uploaded and then the system generated identifier need to be referred in the _Question Body_.

#### Question Set APIs: <a href="#bulkuploadquestions-questionsetapis" id="bulkuploadquestions-questionsetapis"></a>

[http://docs.sunbird.org/latest/apis/questionapi//#tag/QuestionSet-APIs](http://docs.sunbird.org/latest/apis/questionapi/#tag/QuestionSet-APIs)

#### Question APIs: <a href="#bulkuploadquestions-questionapis" id="bulkuploadquestions-questionapis"></a>

[http://docs.sunbird.org/latest/apis/questionapi//#tag/Question-APIs](http://docs.sunbird.org/latest/apis/questionapi/#tag/Question-APIs)
