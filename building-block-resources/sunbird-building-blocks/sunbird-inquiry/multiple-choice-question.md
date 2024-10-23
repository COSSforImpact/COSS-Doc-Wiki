---
icon: elementor
---

# Multiple Choice Question

This category leverages _simple choice_ and _multiple choice_ interaction. Only _simple choice_ is supported in Sunbird 3.9.

As a creator I should be able to create Multiple Choice Question

* with at least 2 and maximum 8 options
* mark any or none of the options as correct
  * Marking an option as correct will set its score as 1. In future we will enable editing of score for each option

### Multiple choice with multiple correct answers (MMCQ) <a href="#multiplechoicequestion-multiplechoicewithmultiplecorrectanswers-mmcq" id="multiplechoicequestion-multiplechoicewithmultiplecorrectanswers-mmcq"></a>

* Creator can mark more than one answers as correct.
  * On marking an answer as correct, its weightage is set as 1. Which means on selecting this response, the player will get full marks allotted for the question
*   The number of options that can be selected by the Player will be the total number of correct answers marked.\
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

#### Scoring Logic <a href="#multiplechoicequestion-scoringlogic" id="multiplechoicequestion-scoringlogic"></a>

* A Scoring Logic can have the following values:
  * ALL
    * Full marks assigned only when all the correct options are selected
  * ANY
    * Full marks assigned when any one of the correct answers is selected
  * PARTIAL
    * Partial scores assigned of any one or more correct answers entered.The total marks of the question will be divided equally amongst all response.\


|          | **ALL**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | **ANY**                                                                                                                                                                                                                                                                                                                                                                                                                | **PARTIAL**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **MCQ**  | <p>Select the correct option. What is 2+2?</p><ol start="1"><li>4</li><li>22</li><li>2</li><li>8</li></ol><p><code>User gets full marks for selecting option 1</code></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | <p>Select the correct option. What is 2+2?</p><ol start="1"><li>4</li><li>22</li><li>2</li><li>8</li></ol><p><code>User gets full marks for selecting option 1</code></p>                                                                                                                                                                                                                                              | <p>Select the correct option. What is 2+2?</p><ol start="1"><li><em>4</em></li><li><em>22</em></li><li><em>2</em></li><li>8<br><code>User gets full marks for selecting option 1</code></li></ol>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **MMCQ** | <p><strong>From the options given below, select all the synonyms for 'happy'?</strong><br>1. Glad<br>2. Joyful<br>3. Merry<br>4. Angry</p><p><em>User gets full marks for selecting all the 3 correct options ie 1,2,3.</em><br></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | <p><strong>From the options given below, select a synonym for 'happy'?</strong></p><ol start="1"><li>Glad</li><li>Joyful</li><li>Merry</li><li>Angry</li></ol><p><code>User gets full marks for selecting either one of the 3 correct options ie 1 or 2 or 3</code></p>                                                                                                                                                | <p><strong>From the options given below, select all the synonyms for 'happy'?</strong></p><ol start="1"><li>Glad</li><li>Joyful</li><li>Merry</li><li>Angry</li></ol><p><code>User gets 1/3 marks for entering options 1 or 1 &#x26; 4</code><br><code>User gets 1/3 marks for entering options 2 or 2 &#x26; 4</code><br><code>User gets 1/3 marks for entering options 3 or 3 &#x26; 4</code><br><code>User gets 2/3 marks for entering options 1 &#x26; 2</code><br><code>User gets 2/3 marks for entering options 1 &#x26; 3</code><br><code>User gets 2/3 marks for entering options 2 &#x26; 3</code></p>                                                                                                  |
| **FTB**  | <p><strong>Q: The color on the Indian flag are ____ , _____ , _____.</strong><br>A: The color on the Indian flag are saffron , white , green.<br><code>User gets full marks for filling the blanks giving the all the 3 answers</code></p><p>A: The color on the Indian flag are saffron , white , _____.</p><p><em>OR</em></p><p>A: The color on the Indian flag are saffron, white, yellow.<br><code>User does not score any marks for filling the blanks with 2 correct answers</code><br></p><p>A:The color on the Indian flag are saffron , ______ , _____.</p><p><em>OR</em></p><p>A: The color on the Indian flag are white , ______ , _____.<br><code>User does not score any marks for filling the blank with 1 correct answer</code><br></p> | <p><strong>Q: The color on the Indian flag are ____ , _____ , _____.</strong></p><p>A:The color on the Indian flag are saffron , _____ , _____.</p><p><em>OR</em><br>A:The color on the Indian flag are white , _____ , _____.</p><p><em>OR</em><br>A:The color on the Indian flag are green , _____ , _____.<br><br><code>User gets full marks for entering one(any) of the blanks with the correct answer</code></p> | <p><strong>Q: The color on the Indian flag are ____ , _____ , _____.</strong></p><p>A:The color on the Indian flag are saffron , _____ , _____.</p><p><em>OR</em><br>A:The color on the Indian flag are white , _____ , _____.</p><p><em>OR</em><br>A:The color on the Indian flag are green , _____ , _____.</p><p><code>User gets 1/3 marks for entering one of the blanks with the correct answer</code></p><p>A:The color on the Indian flag are saffron , white , ____.</p><p>A.The color on the Indian flag are saffron , green , _____.</p><p>A:The color on the Indian flag are green , white, _____.</p><p><code>User gets 2/3 marks for entering two of the blanks with the correct answers</code></p> |
| **MTF**  | <p><strong>Q: Match the following</strong><br>A:</p><ul><li>Apple ---> Fruit</li><li>Dog ---> Animal</li><li>Table ---> Furniture<br><br><code>User gets full marks for matching all the 3 correctly</code><br><br>A:</li><li>Apple ---> Fruit</li><li>Dog ---> Furniture</li><li>Table ---> Animal<br></li><li><code>User does not score any marks for 1 (or more ) correct match</code><br></li></ul>                                                                                                                                                                                                                                                                                                                                                | <p><strong>Q: Match the following</strong><br>A:</p><ul><li>Apple ---> Fruit</li><li>Dog ---> Furniture</li><li>Table ---> Animal<br><br><code>User gets full marks for matching at-least one(any) of the 3 correctly</code></li></ul>                                                                                                                                                                                 | <p><strong>Q: Match the following</strong><br>A:</p><ul><li>Apple ---> Fruit</li><li>Dog ---> Furniture</li><li><p>Table ---> Animal<br></p><p><code>User gets 1/3 marks for matching at-least one(any) of the 3 correctly</code></p></li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

* Questions which are part of any question set  will have the effective Scoring Logic set at the immediate parent level.
  * If questions are present in a section (within a question set), the Scoring Logic of the section will be applied for all the questions in the section.
  * If the question set does not contain any sections and the questions are the immediate children, the Scoring Logic of the question set will be inherited to the questions within.
* Default value of Scoring Logic will be `PARTIAL`

#### Assumptions: <a href="#multiplechoicequestion-assumptions" id="multiplechoicequestion-assumptions"></a>

* There is no negative marking. Score is always positive.
  * In future, Score can be any number, system will award whether it is positive or negative.
* While shuffle is turned on, all questions in a question-set will be assigned score as 1, which is handled at the Player end, without modifying the maxScore in the metadata.
  * We will stick to the same logic for MMCQ

***

#### User flow <a href="#multiplechoicequestion-userflow" id="multiplechoicequestion-userflow"></a>

* As a creator, I will create MCQ, enter options, and mark some of the options as correct.
* When an option is marked as correct, system by default gives it a score of 1. This means that all options carry equal weightage when marked as correct.
  * In future, there will be an option to edit option level score.
* Scoring logic will be set as `PARTIAL` by default. Scoring logic can be made `ALL` ,or `ANY` based on the scoring logic that has to be followed.

|   | **User action**                         | **System behaviour**                                                                                                                                                                                                                                                                                                               | **Status**                                                      |
| - | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| 1 | Create at least 2 and maximum 8 options | <ol start="1"><li>System launched editor with default 2 options</li><li>User can create more options as long as total number of options are not more than 8</li></ol>                                                                                                                                                              | <ol start="1"><li>Available in 3.9</li><li>To be done</li></ol> |
| 2 | Delete options                          | <ol start="1"><li>Deleting an option gives a warning as this cannot be undone</li><li>Options once deleted cannot be ‘undone’</li><li>User can delete options as long as there are at least 2 options</li></ol>                                                                                                                    | Available in 3.9                                                |
| 3 | Mark one (or more) option as correct    | <ol start="1"><li>Set score (weightage) for that option as 1</li><li>System will set default maximum marks for the question as 1, when at least one option is marked as correct</li><li>User must mark at least one option correct. <em>This will change in future when we support</em> <code>scoring mode = none</code></li></ol> |                                                                 |
| 4 | Scoring Logic - ALL / ANY / PARTIAL     | <ol start="1"><li>PARTIAL - User will get partial marks for any of the correct options selected</li><li>ANY - User will get full marks for any one of the correct options selected</li><li>ALL - User will get full marks for the question only when all correct options are selected</li></ol>                                    |                                                                 |

* Player will be able to select one or more responses based on the number options marked as the correct answer.
