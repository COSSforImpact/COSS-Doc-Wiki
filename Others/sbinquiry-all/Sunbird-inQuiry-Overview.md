 **What’s Sunbird inQuiry?** Sunbird inQuiry is a software building block that enables setting up of question banks for various use cases such as assessments, quizzes, practice worksheets, surveys, and many more. These are applicable in multiple domains related to education and human development. 

DescriptionThis building block consists of tools(editor and player) and services that enable  **creation**  ofquestion(s), organising the questions to question set(s),  **configuration** oftheir behaviour,  **curation**  and  **publishing** them for users to  **play**  on any device and  **emission**  of meaningful data.


## Overview of capabilities:

1.  **Creation:**  of question(s) and question set(s) as per an interoperable QuML spec either using the question set editor or by bulk upload  using APIs.


1.  **Configuration** : of the question set behaviour. For ex., randomize the questions from the question bank, limit the number of attempts, set timer etc.


1.  **Tagging** : of question(s) and question set(s) with meaningful metadata useful for discovery and analysis.


1.  **Publish:** Curation, publishing and packing for online and offline consumption of question(s) and question set(s).


1.  **Play** : The player for question set(s) is embeddable, configurable and extendable.


1.  **Data Emission** :



a) Emission of question response and result data using an interoperable specification (QuML)

b) Emission of question set result and summary data using an interoperable specification (QuML)

c) The editor and player emit useful telemetry to make meaning of the user's action, which can be used to generate reports and derive insights. 

Similar to various [Sunbird](https://sunbird.org) building blocks, this is also open sourced under MIT license and you are free to adopt for your purposes. We strongly encourage you to contribute back, participate in the community to help improve this project.

ComponentsQuestion and Question Set ServiceQuestion and Question set service is a micro-service which provides APIs to manage the lifecycle and workflows of creation and consumption of question & question set objects. Today it leverages question & question Set services (assessments APIs) from Sunbird Knowlg. 

link to the source code: [https://github.com/project-sunbird/knowledge-platform](https://github.com/project-sunbird/knowledge-platform)

Design:  [[Design: Question and QuestionSet - Lifecycle|Design--Question-and-QuestionSet---Lifecycle]]


### Question Set Player
Question set player is responsible for rendering questions & question sets created as per QuML spec. This player is embeddable, configurable and extendable.

link to the source code:[https://github.com/project-sunbird/sunbird-quml-player](https://github.com/project-sunbird/sunbird-quml-player)


### Question Set Editor
Question set editor is used to create a question set, configure its behaviour, and add/create questions in the question set. 

Today it leverages collection editor from Sunbird Knowlg for this purpose.

link to the source code:[https://github.com/Sunbird-Ed/sunbird-collection-editor](https://github.com/Sunbird-Ed/sunbird-collection-editor)

Dependencies
### Sunbird QuML 
Sunbird QuML (Question Markup Language) is a specification for creating, rendering and re-using questions and question sets objects. Using this specification reference schema properties are defined for questions and question sets. So it makes sure all questions, question sets and their results are in a standard/common format​.


### Sunbird Knowlg
This is used for the question set editor, question and question set services and the asset category service(taxonomy service) to define the primary category of question and question set objects.


### Sunbird Obsrv
Only the telemetry service and data pipeline of Sunbird Obsrv is used for generating session summaries and question response related data products.


### Sunbird Telemetry
Sunbird Telemetry is a specification to instrument all the key events. Using this specification reference question set editor, question set player and question set services will generate telemetry events.


# Adopters
Sunbird inQuiry is leveraged in DIKSHA - Digital Infrastructure for Knowledge Sharing, the national school education platform of India.  


# Contributors
Avanti Fellows, EkStep, Samagra & Shikshalokam







*****

[[category.storage-team]] 
[[category.confluence]] 
