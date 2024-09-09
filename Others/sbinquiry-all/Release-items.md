
# Changes in 4.1 
Changes required in 4.1 to complete roll-out of V1 Question Set editor & player

Offline support in mobile app and desktop app **Context** : In order to support offline consumption, complete question set needs to be downloaded. It would be useful to have complete archive of question set containing all questions for consumption clients. The metadata & body of complete question set should not exceed 2 MB to deliver optimal & smooth performance. 

 **Challenge** : In order to keep the metadata & body of complete question set should under 2 MB we need to limit the number of questions in a question set. 

Current data suggests that each question metadata is about 10 KB. So maximum of 150 or 180 questions can be supported given the current limits. If the total size exceeds 2 MB, multiple archives of 2 MB should be made available which can be downloaded and stitched together to make the complete question set available for offline consumption. 

Packaging each question as an archive will increase the number of download calls made by consumption clients. So that approach is not advisable. 

1incompleteAnalyse ‘Live’ content on production to understand number of questions used in a content2incompleteCreate few ‘realistic’ sample questions on pre-prod to validate actual size of a question metadata (10 KB is a guess based on dev data)

 **Solution approach 1** : Support upto 150 questions in a question set

This would require following changes (in 4.1):


1. On publish, generate complete question set archive (Knowledge management)


1. Ensure creators cannot create more than a certain maximum number of questions (Editor)


1. Support offline consumption of question set (Player & Consumption clients)





 **Solution approach 2** : Support upto 1000 (or more) questions in a question set

This would require following changes:


1. Breakdown question set into multiple archives by ensuring each archive is less than maximum size (2 MB)


1. Ensure creators have a smooth experience even with large number of questions


1. Support offline consumption of large question sets by downloading multiple part archives






## Multiple Choice Question (MCQ) layouts and image handling
Question body (stem) and/or options will support rich text with images. Creator can resize and align  images to create variety of layouts.

3incompleteEditor to support text alignment along with other functionality already enabled for rich text4incompletePlayer to support MCQ Option layout (horizontal, vertical, grid)5incompletePlayer to support image size and alignment


## Rich text Instructions for question set and its sections
[https://project-sunbird.atlassian.net/browse/SB-23246](https://project-sunbird.atlassian.net/browse/SB-23246)

In release-3.9 we have enabled feature  **Add Rich text (paragraph) Instruction for the Question set** for this we have used CkEditor library in SB-forms common repo. We came to know this is breaking change in mobile app because Both mobile & web are using the same package & the build size is increasing by around 9MB because of CkEditor library. 

For now we decided to remove CKEditor library from SB-forms. So,  **Instruction**  will be a plain textarea like description field in release-3.9 & 4.0. We will do proper design & we will enable  **Rich text ** for  **Instructions ** in upcoming releases. 


## Support Contributions from Avanti & Samagra
Unit test cases so that we know that contributed code is not breaking any existing functionalities. 


# Changes in 3.8
Changes in 3.8 to support roll-out of Exam Question Paper creation use-case

Category Definitions


1. API to support visibility


1. Delete Question Paper and Exam Question from ALL tenant (System)


1. Create Question Paper & Exam Question for One tenant - latest definition from Git (Bharat)



Collection forms


1. All tenant - collection form for save & review will not have B,M,C,S


1. One tenant - B,M,C,S





|  |  **Change**  |  **What to check?**  |  **Where to change?**  |  **Status**  |  **Links**  | 
|  --- |  --- |  --- |  --- |  --- |  --- | 
| 1 |  **Category definitions**  | 
| 2 | API to support visibility = private, protected[https://project-sunbird.atlassian.net/browse/SC-2268](https://project-sunbird.atlassian.net/browse/SC-2268) | Search APIs will take Visibility = Default if not specified explicitly in the search request.Sourcing workflow should work  | VDN & DIKSHA | Pre Prod: DoneGreenProd: autoBlue as part of build deployment |  | 
| 3 | Delete Existing Question Paper & Exam Question category from ALL tenant (System level) |  | VDN & DIKSHA | Pre Prod: To DOYellowprod: To DOYellow | Kartheek to provide over confidential | 
| 4 | Create Question Paper & Exam Question category for One tenant (Haryana) - take latest definition including visibility |  | VDN & DIKSHA | Pre Prod: To DoYellowprod: To DOYellow | [Exam Question content](https://github.com/Sunbird-Ed/creation-portal/blob/release-3.9.0/reference-sample-configuration/exam-question_content.json)  [Question Paper collection](https://github.com/Sunbird-Ed/creation-portal/blob/release-3.9.0/reference-sample-configuration/question-paper_collection.json) | 
| 5 |  **Collection Forms**  | 
| 6 | All tenant - collection form for save & review will not have B,M,C,S |  | DIKSHA | Pre Prod: DoneGreenprod: To DOYellow | Srivathsa has details | 
| 7 | For One (Haryana) tenant - Collection save & review form will have B,M,C,S as mandatory |  | DIKSHA | Pre Prod: DoneGreenprod: To DOYellow | Srivathsa has details | 



*****

[[category.storage-team]] 
[[category.confluence]] 
