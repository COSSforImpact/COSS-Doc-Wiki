Question and Question Set GeneralisationContext: Currently we have two formats for questions and question set - ECML & QuML. 

ECML was designed / conceptualised primarily for practice use-case. It is a custom XML format that limits interoperability and also provides limited functionality. 

QuML 


### Feature parity

1. Support question types such as Fill in The Blank, Match The Following, Sequencing, and Reordering Words


    1. [Match The Following question creation](https://project-sunbird.atlassian.net/browse/SB-23842) ([EPIC](https://project-sunbird.atlassian.net/browse/SB-22953)) and Player


    1. [Fill in The Blank question creation](https://project-sunbird.atlassian.net/browse/SB-23396) ([EPIC](https://project-sunbird.atlassian.net/browse/SB-22953)) and Player



    
1. Ability to search and reuse questions and add it to a question set - Reuse of questions ([EPIC](https://project-sunbird.atlassian.net/browse/SB-22717))


1. Copy a question from Question set creation and Question reuse flow


1. Ability to create  _Sections_  in a question set


1. [Add Instructions (rich text, paragraph) for question set](https://project-sunbird.atlassian.net/browse/SB-23926) sections


1. Attaching audio to question, options (in MCQ), or pairs (in MTF)


1. [Support for Indian languages (incl Urdu) in question creation](https://project-sunbird.atlassian.net/browse/SB-25496)


1. Improve ease of tagging learning outcome to a question


1. Question Set creation (editor) UI improvements


    1. [Timer input user experience](https://project-sunbird.atlassian.net/browse/SB-23817)


    1. [Editors in Sourcing Solution should have minimal required header](https://project-sunbird.atlassian.net/browse/SB-25319)



    


### Deprecating and Backward compatibility of current QuML Questions

1. [Migrate QuML 0.5 Assessment items to QuML 1.0 Questions](https://project-sunbird.atlassian.net/browse/SB-25495) so that they can be reused to create Question Sets ([EPIC](https://project-sunbird.atlassian.net/browse/SB-23436))


1. Support editing of ECML Content containing QuML 0.5 Assessment Items




### Deprecate ECML Question Creation
This involves making a choice whether to allow creation of questions inside Interactive Content (ECML) or not. I believe question creation inside Interactive Content (ECML) will not be required if we do following


1. Enable Interactive Videos allowing user to intermix video with questions and additional information


1. Enable adding an information block (paragraph / page) at any point in a question set allowing user to intermix questions with any additional information




### New features (backlog)

1. [MCQ with multi-select](https://project-sunbird.atlassian.net/browse/SB-23363) ([EPIC](https://project-sunbird.atlassian.net/browse/SB-22953))


1. Add Information section (similar to a slide) anywhere in the question set





*****

[[category.storage-team]] 
[[category.confluence]] 
