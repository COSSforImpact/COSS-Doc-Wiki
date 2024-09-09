While comparing the existing inQuiry question and question set metadata with QuML specs we found a few gaps. Below are the properties having some differences from the QuML specs:

This design only talks about QuML compliance  not about the multi-lingual 


### responseDeclaration
A "responseDeclaration" contains information about the response to a question: When is it correct, and (optionally) how is it scored?


* responseDeclaration.mapping


* maxScore



Here are the differences for each question type:

Subjective Question:



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```
"responseDeclaration": {
    "response1": {
        "type": "string"
    }
}
```
 | Not applicable for subjective question. | 

Multiple Choice Question:



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
"responseDeclaration": {
    "response1": {
        "maxScore": 1,
        "cardinality": "single",
        "type": "integer",
        "correctResponse": {
            "value": "0",
            "outcomes": {
                "SCORE": 1
            }
        },
        "mapping": [
            {
                "response": 0,
                "outcomes": {
                    "score": 1
                }
            }
        ]
    }
}

```
 | 
```json
"responseDeclaration": {
    "response1": {
      "cardinality": "single",
      "type": "integer",
      "correctResponse": {
        "value": 0
      },
      "mapping": [
        {
          "value": 0,
          "score": 1
        }
      ]
    }
},
"outcomeDeclaration": {
    "maxScore": {
      "cardinality": "single",
      "type": "integer",
      "defaultValue": 1
    }
}
```
 | 

Multi-select MCQ:



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
"responseDeclaration": {
    "response1": {
        "maxScore": 1,
        "cardinality": "multiple",
        "type": "integer",
        "correctResponse": {
            "value": [1,0],
            "outcomes": {
                "SCORE": 1
            }
        },
        "mapping": [
            {
                "response": 1,
                "outcomes": {
                    "score": 0.5
                }
            },
            {
                "response": 0,
                "outcomes": {
                    "score": 0.5
                }
            }
      ]
    }
}
```
 | 
```json
"responseDeclaration": {
    "response1": {
      "cardinality": "multiple",
      "type": "integer",
      "correctResponse": {
        "value": [1,0]
      },
      "mapping": [
        {
          "value": 1,
          "score": 0.5
        },
        {
          "value": 0,
          "score": 0.5
        }
      ]
    }
},
"outcomeDeclaration": {
    "maxScore": {
      "cardinality": "multiple",
      "type": "integer",
      "defaultValue": 1
    }
  }
  
```
 | 

 **Open Question:** 

For MMCQ, What would be the value of type?  if correctResponse has value as an array.


### media
No changes are required from the editor and player side.


### timeLimits

* showWarningTimer


* warningTime(%)



The use of maxTime is to show the timer on the QuML player and the use of warningTime is to indicate the time remaining to complete the question set.



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
timeLimits: {
   "maxTime": "240",
   "warningTime": "60"
}
```
 | 
```json
{
    “timeLimits”: {
        “questionSet”: { // time limits for the question set and for any member sets
            “min”: <seconds>,
            “max”: <seconds>
        },
        “question”: { // time limits for the questions in the question set
            “min”: <seconds>,
            “max”: <seconds>
        }
    }
}
```
 | 

Warning time will be removed from the editor and moved to the player side. 

In order to achieve this, the player will introduce two new properties as part of the player configuration.



|  **Name**  |  **Type**  |  **Default**  | 
|  --- |  --- |  --- | 
| warningTime (% ) | number | 75(%) | 
| showWarningTimer | boolean | true | 


1. Warning time will not be present in timeLimitsand will be calculated based on the warningTime config and the Max time


1. warningTime \[number (%) ] to be introduced as part of the global config. Default value of Warning timer can be 75(%) of the max time


    1. ie, Warning timer will start showing once the user finishes 75% (default) of the max time


    1. For eg, max time is 100 seconds, warning timer will start showing from the 75 seconds



    
1. showWarningTimer \[boolean] to be introduced as part of the global config - Player


    1. This will decide if the WarningTimer has to be displayed or not



    

Here’s the sample player configuration.


```
{
    'context': {
      ...
    },
    'metadata': {
      ...
    },
    'config': {
      'sideMenu': {
          'enable': true,
          'showShare': true,
          'showDownload': true,
          'showReplay': false,
          'showExit': false,
      },
      showWarningTimer: true, // true or false 
      warningTime: 75 // [number (%) ]
    }
}
```
 **(Note: Existing behavior of the player will be continuing as it is for the warning indicator)** 

 **Editor Changes:** 


* The warning timer will be removed from the editor form and will not save the warning time value in timeLimits.


* min time will be stored inside timeLimits as timeLimits.questionSet.min


* There will not be any field for taking user input for min time, editor will store the min time as 0 by default.



The timeLimts for the questionset will be stored in below format:


```
timeLimits:
{
  "description": "Time limits for the complete set and/or for each question in the question set.",
   questionSet: {
           min: number,
           max: number
        }
}
```
Example:-

For storing max time( max ) as 5 minutes. It will be stored in below format.


* 5 minutes is to be converted to  seconds to store the value.


* 5 minutes = 5 \* 60 seconds = 300 seconds



The default value of min time ( min ) will be stored as 0


```
timeLimits:
{
   questionSet: {
           min: 0,
           max: 300
        }
}
```
 **Open Question** 

Need confirmation if timeLimits is to be stored as seconds or milli-seconds ? 


### maxScore
For question:

Currently, maxScore property is getting stamped in two places at the question metadata level.

As per QuML spec, maxScore should be stored under the outcomeDeclaration property.



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
// Question metadata

{
  maxScore: 1,
  "responseDeclaration": {
    "response1": {
        "maxScore": 1,
        "cardinality": "multiple",
        "type": "integer",
        "correctResponse": {
            "value": [1,0],
            "outcomes": {
                "SCORE": 1
            }
        },
        .....
    }     
  } 
}
```
 | 
```
{
  "outcomeDeclaration": {
    "maxScore": {
      "cardinality": "single",
      "type": "integer",
      "defaultValue": 1
    }
  }
}
```
 | 

(Notes: Samagra is using this property while printing the question paper). 

For Questionset:



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
// QuestionSet metadata

{
  ...
  maxScore: 10,
  ...
}
```
 | 
```
{
  "outcomeDeclaration": {
    "maxScore": {
      "cardinality": "single",
      "type": "integer",
      "defaultValue": 1
    }
  }
}
```
 | 

 **Open Question:** 

For QuestionSet, What would be the value of cardinality?

(Need to be checked with  and  )


### answer
In the current implementation, We are not storing the answer property for MCQ and MMCQ. but as per QuML spec, An answer is mandatory for all types of questions.


* SA – HTML


* MCQ/MMCQ – reference value for data OR actual value ?

    For example: “1,2” OR “India, US”

    (Need to be checked with  and 



Subjective Question:



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
"answer": "<p>This is test data</p>"
```
 | [Click here to see the proposed solution](https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player#Proposed-Solution) | 

Multiple Choice Question:



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| Not Applicable  | [Click here to see the proposed solution](https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player#Proposed-Solutionhttps://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player#Proposed-Solution) | 

Multi-select MCQ:



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| Not Applicable  | [Click here to see the proposed solution](https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player#Proposed-Solutionhttps://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3317628929/QuML+compliance+implementation+changes+for+editor+and+player#Proposed-Solution) | 

Proposed SolutionHere are the solutions for different types of the question.

 **Solution 1** 

Datatype: String

In this solution, All answers will be concatenated together under an HTML element and stamped to the answer property.

Here’s the sample HTML template for single & multi answers:


```
// Single answer

<div class="anwser-container">
    <div class="anwser-body">
        // Anwser HTML 
    </div>  
</div>
```



```
// Multiple answers 

<div class="anwser-container">
    <div class="anwser-body">
        // Anwser1 HTML
    </div>  
    <div class="anwser-body">
       // Anwser2 HTML
    </div>  
</div>
```


|  **SA**  |  **MCQ**  |  **MMCQ**  | 
|  --- |  --- |  --- | 
|  **Single Language:** 
```
anwser: '<div class="anwser-container">
    <div class="anwser-body">
        <p>Delhi</p>
    </div>    
</div>'
```
 **Multi Language:** 
```
answer: {
  en: "<div class="anwser-container">
          <div class="anwser-body">
              <p>Delhi</p>
          </div>    
       </div>",
  hi: "<div class="anwser-container">
          <div class="anwser-body">
              <p>दिल्ली</p>
          </div>    
       </div>"
}
```
 |  **Single Language:** 
```
anwser: `<div class="anwser-container">
    <div class="anwser-body">
        <p>Delhi</p>
    </div>    
</div>'
```
 **Multi Language:** 
```
answer: {
  en: "<div class="anwser-container">
          <div class="anwser-body">
              <p>Delhi</p>
          </div>    
       </div>",
  hi: "<div class="anwser-container">
          <div class="anwser-body">
              <p>दिल्ली</p>
          </div>    
       </div>"
}
```
 |  **Single Language:** 
```
anwser: `<div class="anwser-container">
    <div class="anwser-body">
        <p>Delhi</p>
    </div>
    <div class="anwser-body">
        <p>Bangalore</p>
    </div>
</div>'
```
 **Multi Language:** 
```
answer: {
  en: "<div class="anwser-container">
          <div class="anwser-body">
              <p>Delhi</p>
          </div>
          <div class="anwser-body">
              <p>bangalore</p>
          </div>    
       </div>",
  hi: "<div class="anwser-container">
          <div class="anwser-body">
              <p>दिल्ली</p>
          </div> 
          <div class="anwser-body">
              <p>बैंगलोर</p>
          </div>   
       </div>"
}

```
 | 

Pros:


* No QuML spec changes are needed.


* No additional data transformation is required for older questions by API.



Cons:


* Difficult to differentiate each answer by the player as it’s concatenated together under an HTML element.


* Some extra effort is required to support this format by the editor /player.





 **Solution 2** 

In this solution, Each answer will be stored separately as an element in an array.

Datatype: Array  (An array of strings)



|  **SA**  |  **MCQ**  |  **MMCQ**  | 
|  --- |  --- |  --- | 
|  **Single Language:** answer: \["<p>Delhi</p>"] **Multi Language:** 
```
answer: {
  en: ["<p>Delhi</p>"]
  hi: ["<p>दिल्ली</p>"]
}
```
 |  **Single Language:** answer: \["<p>Delhi</p>"] **Multi Language:** 
```
answer: {
  en: ["<p>Delhi</p>"]
  hi: ["<p>दिल्ली</p>"]
}
```
 |  **Single Language:** 
```
answer: [
  "<p>Delhi</p>, 
  "<p>Bangalore</p>"
]] ]></ac:plain-text-body></ac:structured-macro><p><strong>Multi Language:</strong></p><ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="a3a907d5-8e0b-4e88-9311-0daba0138b63"><ac:plain-text-body><![CDATA[answer: {
  en: ["<p>Delhi</p>","<p>Bangalore</p>"]
  hi: ["<p>दिल्ली</p>", "<p>बैंगलोर</p>"]
}
```
 | 

Pros:


* Easy to differentiate each answer by the player as it’s not concatenated together under an HTML element.


* Easy to manipulate UI by the player.


* Minimal changes are required by the editor and player.



Cons:


* QuML spec changes are required to support this format.


* Data transformation is required in API for older questions as it’s an array of strings.



 **Answer attribute conclusion** :-

Solution 1 is  finalised for the implementation of answer.

As the answer attribute is used only for printing/display so for the simplicity answer will be stored in the form of string with the html template as mentioned above in solution 1.


```
<div class="anwser-container">
    <div class="anwser-body">
        // Anwser HTML 
    </div>  
</div>
```
In the // Anwser HTML actual values of answers will be stored.

For “Multiple choice Questions” the label presents in interaction options will be stored in the place of  

// Anwser HTML


### interactions
As part of the new implementation, We will be moving only the validation field under the response1 property. No other change.



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```
"interactions": {
    "response1": {
        "type": "choice",
        "options": [
            {
                "label": "<p>New Delhi</p>",
                "value": 0
            },
            {
                "label": "<p>Mumbai</p>",
                "value": 1
            }
        ]
    },
    "validation": {
        "required": "Yes"
    }
}
```
 | 
```json
"interactions": {
    "response1": {
        "type": "choice",
        "options": [
            {
                "label": "<p>New Delhi</p>",
                "value": 0
            },
            {
                "label": "<p>Mumbai</p>",
                "value": 1
            }
        ],
        "validation": {
          "required": "Yes"
        }
    }
}
```
 | 


### solutions
Solutions are used to provide exemplary answers to questions aid candidates in-depth learning and enhance user’s understanding of the concepts. Multiple solutions can be configured for a question

This property supports the following types:


1. Image + Text





|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```
"solutions": [
    {
        "id": "7015c7e4-461a-4032-b29e-fbb7e8155e44",
        "type": "html",
        "value": "<figure class=\"image\"><img src=\"/assets/public/content/assets/do_2137916546057256961374/indiagate.jpeg\" alt=\"indiaGate\" data-asset-variable=\"do_2137916546057256961374\"></figure>"
    }
]] ]></ac:plain-text-body></ac:structured-macro></td><td><ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="27566252-2f3b-4872-98ea-d746ce3a390e"><ac:parameter ac:name="language">json</ac:parameter><ac:plain-text-body><![CDATA["solutions": {
    "7015c7e4-461a-4032-b29e-fbb7e8155e44": "<figure class=\"image\"><img src=\"/assets/public/content/assets/do_2137916546057256961374/indiagate.jpeg\" alt=\"indiaGate\" data-asset-variable=\"do_2137916546057256961374\"></figure>",
}



// Key = UUID / Solution ID
```
 | 

 2. Video



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
"solutions": [
    {
        "id": "70c82bf5-9459-4c43-8897-0e58b7e1da62",
        "type": "video",
        "value": "do_2137930190247526401388"
    }
]] ]></ac:plain-text-body></ac:structured-macro></td><td><ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="8ea06acf-b69e-4e0d-a934-50ff8f77b812"><ac:parameter ac:name="language">json</ac:parameter><ac:plain-text-body><![CDATA["solutions": {
    "70c82bf5-9459-4c43-8897-0e58b7e1da62": "<video data-asset-variable="do_2137930187513200641386" width="400" controls="" poster="/assets/public/content/assets/do_2137930188655902721387/gateway-of-india.jpg"> <source type="video/mp4" src="/assets/public/content/assets/do_2137980528723230721410/sample-5s.mp4"> <source type="video/webm" src="/assets/public/content/assets/do_2137980528723230721410/sample-5s.mp4"> </video>",
}



// Key = UUID
```
 | 


* Solutions is a JSON object in key-value format. The keys in the JSON are the identifiers of different solutions for the question and values are HTML snippets for solutions.


* Solutions HTML must contain only structural and media HTML elements. There should be interactions in a solution and hence no input HTML elements. QuML players should allow the users to view the solutions if the context in which the question is being used allows the users to view the solution.




### 

feedback
[Feedback](https://quml.sunbird.org/v1/question#feedback) is a JSON object in key-value format. The keys in the JSON are the identifiers of different feedbacks for the question and values are HTML snippet to be shown to the student. After the response processing, the QuML player renders the feedback HTML mapped to the value that is set to the FEEDBACK outcome variable.

Feedback:



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
// Not applicable 
```
 | 
```json
“feedback”: {
  “70c82bf5-9459-4c43-8897-0e58b7e1da62”: “<h1>Well done!!!</h1>”,
  “70c82bf5-9459-4c43-8897-0e58b7e1da63”: “<h1>Better luck next time!!!</h1>”
  “70c82bf5-9459-4c43-8897-0e58b7e1da64”: “<h1>You need to work harder!!!</h1>”
}

// key = UUID
```
 | 

For more information, please refer to this document: [https://quml.sunbird.org/v1/question#feedback](https://quml.sunbird.org/v1/question#feedback)

hints (This has to be modified by an adopter)Similar to feedback, Hints are shown to the candidates after response processing or when the student requests for hints.



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
// Question Metadata
{ 
  hints: { 
    en : "string"
  }
}
```
 | 
```json
“hints”: {
  “70c82bf5-9459-4c43-8897-0e58b7e1da62”: “<HTML>...</HTML>”,
  “70c82bf5-9459-4c43-8897-0e58b7e1da63”: “<HTML>...</HTML>”
  “70c82bf5-9459-4c43-8897-0e58b7e1da64”: “<HTML>...</HTML>”
}

// key = UUID
```
 | 

Hints is a JSON object in key-value format. The keys in the JSON are the identifiers of different hints for the question and values are HTML snippet for hints.

For more information, please refer to this documentation: [https://quml.sunbird.org/v1/question#hints](https://quml.sunbird.org/v1/question#hints)

Only Shikshalokam is using the following format.


* Question - { hints: { en : \["string"]}}


* Also, they are storing the hints for each option under the interactions property.



Here is an example from Shikshalokam storing hint for the Question :


```
{ // question metadata
  ......,
  
  "hints": {
    "en": [
      "delhi"
    ]
  },
  .....
}
```
Proposed format for storing hint of question and for storing question hint reference in outcomeDeclaration to differentiate it from the  hints of options 


```diff
{ // question metadata
  ......,
+  hints: {
+    "70c82bf5-9459-4c43-8897-0e58b7e2er76": { "en": "delhi" } 
+  },
+ "outcomeDeclaration": {
+    "hint": {
+     "cardinality": "single",
+        "type": "string",
+         "defaultValue": "70c82bf5-9459-4c43-8897-0e58b7e2er76"
+    }
+  }
}
```
Here is an example from Shikshalokam storing hints for each options under interactions :


```
{ // question metadata
  .....,
  
  interactions: {
    response1: {
      type: "choice",
        options: [
          {
            label: "<p>option 1</p>",
            value: 0,
            hints: {
              en: "test hint 1", // hints for option 1
            },
          },
          {
            label: "<p>option 2</p>",
            value: 1,
            hints: {
              en: "test hint 2", // hints for option 2
            },
          },
          {
            label: "<p>option 3</p>",
            value: 2,
            hints: {
              en: "test hint 3", // hints for option 3
            },
          },
        ],
          autoCapture: "Yes",
            validation: {
        limit: {
          maxLength: 100
        },
        required: "Yes",
          pattern: "dd/mm/yyyy",
      },
    },
  },
  .....
}
```
Proposed  format for storing  hints for each options under interactions :


```diff
{ // question metadata
  ......,
  
  interactions: {
    response1: {
      type: "choice",
        options: [
          {
            label: "<p>option 1</p>",
            value: 0,
+           hint: "70c82bf5-9459-4c43-8897-0e58b7e1da64", // hints for option 1
          },
          {
            label: "<p>option 2</p>",
            value: 1,
+           hint: "70c82bf5-9459-4c43-8897-0e58b7e1as73", // hints for option 2
          },
          {
            label: "<p>option 3</p>",
            value: 2,
+           hint: "70c82bf5-9459-4c43-8897-0e58b7e1gf87", // hints for option 3
          },
        ],
          autoCapture: "Yes",
            validation: {
        limit: {
          maxLength: 100
        },
        required: "Yes",
          pattern: "dd/mm/yyyy",
      },
    },
  },
+  hints: {
+    "70c82bf5-9459-4c43-8897-0e58b7e1da64": { en: "test hint 1" },
+    "70c82bf5-9459-4c43-8897-0e58b7e1as73": { en: "test hint 2" },
+    "70c82bf5-9459-4c43-8897-0e58b7e1gf87": { en: "test hint 3" },
+  }
}
```
Note - interaction design is on hold and is tracked as part of this Jira ticket- [IQ-427 System JIRA](https:///browse/IQ-427)


### instructions (This has to be modified by an adopter)
Instructions on how to understand, attempt, or how the question will be evaluated.

Currently, instructions are being stored in the following format:

For QuestionSet:



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
{ 
  instructions: { 
    default : "<html>...</html>"
  }
}
```
 | 
```json
instructions:  : "<html>"
```
 | 

For Question:



|  **Current Format**  |  **New format as per QuML Spec**  | 
|  --- |  --- | 
| 
```json
{ 
  instructions: { 
    en : "<html>...</html>"
  }
}

//Only Shikshalokam is using the above format.
// Not used by inQuiry

```
 | 
```json
instructions:  : "<html>"
```
 | 

Instructions HTML also must contain only structural and media HTML elements. There should be interactions in a solution and hence no input HTML elements.





*****

[[category.storage-team]] 
[[category.confluence]] 
