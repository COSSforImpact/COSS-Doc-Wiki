<Back up>

The vision for [Project inQuiry](https://github.com/sunbird-specs/inQuiry) is to provide  _Question Bank Digital Infrastructure_  for various learning and administrative interactions for education & capability building. It strives to enable a variety of use-cases such as  _Practice_ ,  _Quiz_ ,  _Survey_ ,  _Assessment_  and many more for  **Learn** ,  **Help Learn** , and  **Manage Learn** . Question Bank Digital Infrastructure contains 


* Schema for Question and Question set objects to support configurable behaviour for various use-cases


* Specification for Question and Question set empowering various systems to interoperate - it is called QuML


* Microservices for managing Questions and Question sets.


* Reference Question set player and editor for any adopter to create and play question sets out of the box. These are configurable, embeddable, and pluggable.


    * The editor and player generates useful telemetry to make meaning of the user's action, generate reports, and derive insights.



    

We introduced [[Question|Question-Definition]] & [[Question Set|Question-Set-Definition]] objects along with [QuML specification](https://github.com/sunbird-specs/inQuiry/blob/master/README.md) as part of the [Question Bank Digital Infrastructure](https://www.youtube.com/watch?v=xgvZUfYrxmQ) in Sunbird.

Useful links
* A quick overview of diverse use-cases question bank can enable [https://www.youtube.com/watch?v=8B01FlIMGWk](https://www.youtube.com/watch?v=8B01FlIMGWk)


* Demystifying Question Bank Digital Infrastructure [https://www.youtube.com/watch?v=xgvZUfYrxmQ](https://www.youtube.com/watch?v=xgvZUfYrxmQ)  


* [QuML specification](https://github.com/sunbird-specs/inQuiry/blob/master/README.md)[https://github.com/sunbird-specs/inQuiry](https://github.com/sunbird-specs/inQuiry)  


* [[Question|Question-Definition]] & [[Question Set|Question-Set-Definition]] objects


* Reference sample implementation [[QuML Question Spec|QuML-Question-Spec]]


* Question set editor [https://github.com/Sunbird-Ed/sunbird-collection-editor](https://github.com/Sunbird-Ed/sunbird-collection-editor)  


* Question set player [https://github.com/project-sunbird/sunbird-quml-player](https://github.com/project-sunbird/sunbird-quml-player)  (Javascript player for consuming QuML questions & question sets)


* Telemetry specification [https://github.com/sunbird-specs/Telemetry](https://github.com/sunbird-specs/Telemetry)  


* [https://docs.google.com/presentation/d/1ZVj7HEideforroJJJt2JCgH77by0blVgrI1aYoEPC6A/edit#slide=id.ga7ecb044cd_0_414](https://docs.google.com/presentation/d/1ZVj7HEideforroJJJt2JCgH77by0blVgrI1aYoEPC6A/edit#slide=id.ga7ecb044cd_0_414) (limited access)


* [Learning Notes](https://www.notion.so/avantifellows/744c167f2afa4d1dae17b13ca01e5a17?v=9325e789fecd469c83f9b84d1b8bc67d) on [Question Bank](https://www.notion.so/avantifellows/Series-1-Question-Bank-for-Sensing-fde3406b6277443eb8f9c2beb3bdeab6) by one of the contributors ( _Thank you Aman Dalmia & Deepansh Mathur from Avanti Fellows_ )  



ReferenceTo know more about the editor and player tool


* Question Set Editor reference designs


* Question Set Player reference designs





< start of rough notes>

Sunbird inQuiry enables variety of use-cases leveraging question and question set such as Practice, Assessment, Quiz, Survey and many more. 

Sunbird inQuiry

is a building block

to enable ..

for use-cases ..

Question Bank is a curated bank of questions which can be used by any system for various use-cases

 _Sunbird RC Example_ :

 **Registry is a trusted system that enables consented actors to enroll and avail 3rd party services built on it** 

E.g. Motor Vehicle, Aadhaar, birth/death registry, land registry, internet domain registry etc.



inQuiry enables sensing by posing questions which people respond to and generating data that can be analysed it allows an individual or a system to sense what’s going on through practice, assessment, survey, .. Key verbs are

Create

Curate

Configure

Review

Reuse

Respond

View summary




## Key verbs powered by this building block:

* Creators to **ASSESS**  learners' learning via various question set categories such as practice question sets, quizzes, assessments etc


* Learners to **SENSE** theirunderstanding of their learning by taking these assets


* Administrators to **MAKE SENSE** of their learners' learning



This building block consists of tools and services that enables you to  **create** question(s) and question set(s),  **configure** their behaviour,  **curate** ,  **publish**  them for consumption and .  It comes with a ready to use reference editor & player to orchestrate these workflows. 


1. Publish Job for Question Set to enable offline consumption.


1. Monitoring of the publish job to monitor health of the job. 



Sunbird inQuiry is a building block that enables question banks that can contain questions and question sets of various categories such as practice, assessment, quiz, worksheet, survey, observations and many more for the sake of conducting formative assessments, summative assessments and surveys. 

< end of rough notes>





*****

[[category.storage-team]] 
[[category.confluence]] 
