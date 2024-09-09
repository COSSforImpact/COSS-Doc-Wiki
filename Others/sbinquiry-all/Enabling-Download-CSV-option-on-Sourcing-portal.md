 **Overview** 

To enable a download CSV option on the front end for an Exam Question Set 

 **Problem Statement** 

 After the review of Questions by contribution reviewer & sourcing reviewer, the Question set/ collection Is finalized.

The sourcing reviewer has the ability to download the finalized Questions in a Word document (Question Paper format).

Additionally, the sourcing reviewer also should have an access to download the finalized questions in a csv format where the sourcing reviewer can see the Questions, options, Correct answer, Topic, LO, Skill, Question type in one view for all the Questions.



 **Functional Solution** 

Enable an option for download csv on front end for sourcing reviewer.


1. A ‘Download excel’ button is added to the sourcing portal


1. Clicking on the ‘Download excel’ gives a downloaded CSV/Excel file







 **Technical Implementation -** 


* Call Read Hierarchy API - Get question ids from Project ID.  



   – questionset/v4/hierarchy/


* Call Read Question API to get each question’s Details. 



– question/v4/read/


* Form the values, needed for CSV file generation.



-Class

-Subject

-Topic Name

-Questions

-Option1

-Option 2

-Option 3

-Option 4

-Correct answer

-Competencies

-Skills

-Question Image URL

-Chapter Name

-Question Type

-Right column

-Left column


* Call the CSV file generation method.







Points for discussion:


* Format for storing Match the following question types - 


* Here for MTF, we have 2 columns as fixed, but the number of rows is different for every MTF question.



            **Approach** : We can keep 2 columns named “Right column”, “Left Column”, so that we  

                can create a string with a comma(,) separated and assign it to “Right column” ,                  

  “Left Column”.



Sample CSV file to be generated - 

[CSV format ](https://docs.google.com/spreadsheets/d/1WRQSlz3qX2JXfaf6j4afkFuLMb5KyavH/edit?usp=sharing&ouid=110522290077284485945&rtpof=true&sd=true)





*****

[[category.storage-team]] 
[[category.confluence]] 
