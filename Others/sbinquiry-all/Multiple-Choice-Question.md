This category leverages  _simple choice_  and  _multiple choice_  interaction. Only  _simple choice_  is supported in Sunbird 3.9.

As a creator I should be able to create Multiple Choice Question


* with at least 2 and maximum 8 options


* mark any or none of the options as correct


    * Marking an option as correct will set its score as 1. In future we will enable editing of score for each option



    


## Multiple choice with multiple correct answers (MMCQ)

* Creator can mark more than one answers as correct. 


    * On marking an answer as correct, its weightage is set as 1. Which means on selecting this response, the player will get full marks allotted for the question



    
* The number of options that can be selected by  the Player will be the total number of correct answers marked.

    Example,


```
MCQ with one correct answer.
Q: What is 2 +2 ?
a)4 (marked as correct answer)
b)8-2
c)2*2
d)8

In this case the user will be allowed to choose only one option from the 4 options available.This works like a normal MCQ.

MMCQ with 2 correct answers.
Q: What is 2 +2 ?
a)4 (marked as correct answer)
b)8/2 (marked as correct answer)
c)2*2
d)8

In this case the user will be allowed to choose only two options from the 4 options available.
```



* There is no logical difference between the two questions types as MCQ & MMCQ. MCQ question is an MMCQ question with just one correct answer. The two of them will be considered as a single question type only.


* MCQ (or any question) with multiple correct answers will have Scoring Logic = PARTIAL by default. Thus, 


    * All responses marked as correct will get equal marks.The total marks of the question will be divided equally amongst all responses


    * Player will get the score for whichever option s/he has selected. 



    


### Scoring Logic

* A Scoring Logic can have the following values:


    * ALL


    * Full marks assigned only when all the correct options are selected



    
    * ANY


    * Full marks assigned when any one of the correct answers is selected



    
    * PARTIAL


    * Partial scores assigned of any one or more correct answers entered.The total marks of the question will be divided equally amongst all response.

    



    

    



|  |  **ALL**  |  **ANY**  |  **PARTIAL**  | 
| Select the correct option. What is 2+2?
1. 4


1. 22


1. 2


1. 8



User gets full marks for selecting option 1 | Select the correct option. What is 2+2?
1. 4


1. 22


1. 2


1. 8



User gets full marks for selecting option 1 | Select the correct option. What is 2+2?
1.  _4_ 


1.  _22_ 


1.  _2_ 


1. 8 User gets full marks for selecting option 1



 | 
|  **From the options given below, select all the synonyms for 'happy'?**  1.  Glad 2. Joyful 3. Merry 4. Angry _User gets full marks for selecting all the 3 correct options ie 1,2,3._  |  **From the options given below, select a synonym for 'happy'?** 
1. Glad


1. Joyful


1. Merry


1. Angry



User gets full marks for selecting either one of the 3 correct options ie 1 or 2 or 3 |  **From the options given below, select all the synonyms for 'happy'?** 
1. Glad


1. Joyful


1. Merry


1. Angry



User gets 1/3 marks for entering options 1 or 1 & 4User gets 1/3 marks for entering options 2 or 2 & 4User gets 1/3 marks for entering options 3 or 3 & 4User gets 2/3 marks for entering options 1 & 2User gets 2/3 marks for entering options 1 & 3User gets 2/3 marks for entering options 2 & 3 | 
|  **Q: The color on the Indian flag are ____ , _____ , _____.**  A: The color on the Indian flag are saffron , white , green. User gets full marks for filling the blanks giving the all the 3 answersA: The color on the Indian flag are saffron , white , _____. _OR_ A: The color on the Indian flag are saffron, white, yellow. User does not score any marks for filling the blanks with 2 correct answers A:The color on the Indian flag are saffron , ______ , _____. _OR_ A: The color on the Indian flag are white , ______ , _____. User does not score any marks for filling the blank with 1 correct answer  |  **Q: The color on the Indian flag are ____ , _____ , _____.** A:The color on the Indian flag are saffron , _____ , _____. _OR_  A:The color on the Indian flag are white , _____ , _____. _OR_  A:The color on the Indian flag are green , _____ , _____.  User gets full marks for entering one(any) of the blanks with the correct answer |  **Q: The color on the Indian flag are ____ , _____ , _____.** A:The color on the Indian flag are saffron , _____ , _____. _OR_  A:The color on the Indian flag are white , _____ , _____. _OR_  A:The color on the Indian flag are green , _____ , _____.User gets 1/3 marks for entering one of the blanks with the correct answerA:The color on the Indian flag are saffron , white , ____.A.The color on the Indian flag are saffron , green , _____.A:The color on the Indian flag are green , white, _____.User gets 2/3 marks for entering two of the blanks with the correct answers | 
|  **Q: Match the following**      A:<ul><li>Apple ---> Fruit

</li><li>Dog   ---> Animal

</li><li>Table ---> Furniture  User gets full marks for matching all the 3 correctly  A:

</li><li>Apple ---> Fruit

</li><li>Dog   ---> Furniture

</li><li>Table ---> Animal 

</li><li>User does not score any marks for 1 (or more ) correct match

</li></ul> |  **Q: Match the following**  A:<ul><li>Apple ---> Fruit

</li><li>Dog   ---> Furniture

</li><li>Table ---> Animal  User gets full marks for matching at-least one(any) of the 3 correctly

</li></ul> |  **Q: Match the following**  A:<ul><li>Apple ---> Fruit

</li><li>Dog   ---> Furniture

</li><li>Table ---> Animal 

User gets 1/3 marks for matching at-least one(any) of the 3 correctly

</li></ul> | 
|  --- |  --- |  --- |  --- | 
|  --- | 
|  --- | 
|  --- | 
|  --- | 
| Select the correct option. What is 2+2?
1. 4


1. 22


1. 2


1. 8



User gets full marks for selecting option 1 | Select the correct option. What is 2+2?
1. 4


1. 22


1. 2


1. 8



User gets full marks for selecting option 1 | Select the correct option. What is 2+2?
1.  _4_ 


1.  _22_ 


1.  _2_ 


1. 8 User gets full marks for selecting option 1



 | 
|  **From the options given below, select all the synonyms for 'happy'?**  1.  Glad 2. Joyful 3. Merry 4. Angry _User gets full marks for selecting all the 3 correct options ie 1,2,3._  |  **From the options given below, select a synonym for 'happy'?** 
1. Glad


1. Joyful


1. Merry


1. Angry



User gets full marks for selecting either one of the 3 correct options ie 1 or 2 or 3 |  **From the options given below, select all the synonyms for 'happy'?** 
1. Glad


1. Joyful


1. Merry


1. Angry



User gets 1/3 marks for entering options 1 or 1 & 4User gets 1/3 marks for entering options 2 or 2 & 4User gets 1/3 marks for entering options 3 or 3 & 4User gets 2/3 marks for entering options 1 & 2User gets 2/3 marks for entering options 1 & 3User gets 2/3 marks for entering options 2 & 3 | 
|  **Q: The color on the Indian flag are ____ , _____ , _____.**  A: The color on the Indian flag are saffron , white , green. User gets full marks for filling the blanks giving the all the 3 answersA: The color on the Indian flag are saffron , white , _____. _OR_ A: The color on the Indian flag are saffron, white, yellow. User does not score any marks for filling the blanks with 2 correct answers A:The color on the Indian flag are saffron , ______ , _____. _OR_ A: The color on the Indian flag are white , ______ , _____. User does not score any marks for filling the blank with 1 correct answer  |  **Q: The color on the Indian flag are ____ , _____ , _____.** A:The color on the Indian flag are saffron , _____ , _____. _OR_  A:The color on the Indian flag are white , _____ , _____. _OR_  A:The color on the Indian flag are green , _____ , _____.  User gets full marks for entering one(any) of the blanks with the correct answer |  **Q: The color on the Indian flag are ____ , _____ , _____.** A:The color on the Indian flag are saffron , _____ , _____. _OR_  A:The color on the Indian flag are white , _____ , _____. _OR_  A:The color on the Indian flag are green , _____ , _____.User gets 1/3 marks for entering one of the blanks with the correct answerA:The color on the Indian flag are saffron , white , ____.A.The color on the Indian flag are saffron , green , _____.A:The color on the Indian flag are green , white, _____.User gets 2/3 marks for entering two of the blanks with the correct answers | 
|  **Q: Match the following**      A:<ul><li>Apple ---> Fruit

</li><li>Dog   ---> Animal

</li><li>Table ---> Furniture  User gets full marks for matching all the 3 correctly  A:

</li><li>Apple ---> Fruit

</li><li>Dog   ---> Furniture

</li><li>Table ---> Animal 

</li><li>User does not score any marks for 1 (or more ) correct match

</li></ul> |  **Q: Match the following**  A:<ul><li>Apple ---> Fruit

</li><li>Dog   ---> Furniture

</li><li>Table ---> Animal  User gets full marks for matching at-least one(any) of the 3 correctly

</li></ul> |  **Q: Match the following**  A:<ul><li>Apple ---> Fruit

</li><li>Dog   ---> Furniture

</li><li>Table ---> Animal 

User gets 1/3 marks for matching at-least one(any) of the 3 correctly

</li></ul> | 




* Questions which are part of any question set  will have the effective Scoring Logic set at the immediate parent level.


    * If questions are present in a section (within a question set), the Scoring Logic of the section will be applied for all the questions in the section.


    * If the question set does not contain any sections and the questions are the immediate children, the Scoring Logic of the question set will be inherited to the questions within.



    
* Default value of Scoring Logic will be PARTIAL




### Assumptions:

* There is no negative marking. Score is always positive. 


    * In future, Score can be any number, system will award whether it is positive or negative.



    
* While shuffle is turned on, all questions in a question-set will be assigned score as 1, which is handled at the Player end, without modifying the maxScore in the metadata.


    * We will stick to the same logic for MMCQ



    


### User flow

* As a creator, I will create MCQ, enter options, and mark some of the options as correct. 


* When an option is marked as correct, system by default gives it a score of 1. This means that all options carry equal weightage when marked as correct.


    * In future, there will be an option to edit option level score. 



    
* Scoring logic will be set as PARTIAL by default. Scoring logic can be made ALL ,or ANY based on the scoring logic that has to be followed.





|  |  **User action**  |  **System behaviour**  |  **Status**  | 
|  --- |  --- |  --- |  --- | 
| 1 | Create at least 2 and maximum 8 options | 
1. System launched editor with default 2 options


1. User can create more options as long as total number of options are not more than 8



 | 
1. Available in 3.9Blue


1. To be done



 | 
| 2 | Delete options | 
1. Deleting an option gives a warning as this cannot be undone


1. Options once deleted cannot be ‘undone’


1. User can delete options as long as there are at least 2 options



 | Available in 3.9Blue | 
| 3 | Mark one (or more) option as correct | 
1. Set score (weightage) for that option as 1


1. System will set default maximum marks for the question as 1, when at least one option is marked as correct


1. User must mark at least one option correct.  _This will change in future when we support_ scoring mode = none



 |  | 
| 4 | Scoring Logic - ALL / ANY / PARTIAL | 
1. PARTIAL - User will get partial marks for any of the correct options selected


1. ANY - User will get full marks for any one of the correct options selected


1. ALL - User will get full marks for the question only when all correct options are selected



 |  | 


* Player will be able to select one or more responses based on the number options marked as the correct answer.





*****

[[category.storage-team]] 
[[category.confluence]] 
