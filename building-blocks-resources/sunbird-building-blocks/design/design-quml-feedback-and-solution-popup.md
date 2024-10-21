---
icon: elementor
---

# \[Design] QuML: Feedback and Solution Popup

### **Introduction:Background:Key Design Problems:Overview:Existing flow of Question evaluation and feedback popup :Solution I:Solution II:ECML Solution:Conclusion:** <a href="#id-design-quml-feedbackandsolutionpopup-less-than-cdata-div.rbtoc1729507888624-padding-0px-div.rbtoc" id="id-design-quml-feedbackandsolutionpopup-less-than-cdata-div.rbtoc1729507888624-padding-0px-div.rbtoc"></a>

### **Introduction:** <a href="#id-design-quml-feedbackandsolutionpopup-introduction" id="id-design-quml-feedbackandsolutionpopup-introduction"></a>

Show the feedback popup for QuML questions with a solution. After evaluating the question.

### **Background:** <a href="#id-design-quml-feedbackandsolutionpopup-background" id="id-design-quml-feedbackandsolutionpopup-background"></a>

By default Question set plugin is taking care of showing feedback popup once question evaluation is done. But if the unit plugins want to show its own feedback popup is the background.

### **Key Design Problems:** <a href="#id-design-quml-feedbackandsolutionpopup-keydesignproblems" id="id-design-quml-feedbackandsolutionpopup-keydesignproblems"></a>

1. QuML type of question wants to show its own feedback pop for question solutions.

### **Overview:**  <a href="#id-design-quml-feedbackandsolutionpopup-overview" id="id-design-quml-feedbackandsolutionpopup-overview"></a>

The current implementation of question evaluated result showing in feedback popup based on the result of the question. These popups can show only NEXT and TRY AGAIN buttons.

This logic is taken care of by the QuestionSet plugin. But the same used in QuML plugin also. But now QuML having different actions in feedback popup. NEXT, TRY AGAIN and SOLUTION.

Students would like to view Solution explanation for a Question to understand how to solve the question & arrive at the answer.

Solution view should be made available for following QuML Question types:

1. Multiple Choice Questions
2. Subjective Reference Questions (VSA, SA, LA)

Today QuML Question templates are accessible only via Program portal.

Please refer below invision for designs [https://projects.invisionapp.com/share/9XUJXW4ZR7A#/screens/390483008](https://projects.invisionapp.com/share/9XUJXW4ZR7A#/screens/390483008)

\


Jira ID:  [SB-15455](https://project-sunbird.atlassian.net/browse/SB-15455) - Getting issue details... STATUS

### **Existing flow of Question evaluation and feedback popup :**  <a href="#id-design-quml-feedbackandsolutionpopup-existingflowofquestionevaluationandfeedbackpopup" id="id-design-quml-feedbackandsolutionpopup-existingflowofquestionevaluationandfeedbackpopup"></a>



\


\


\


### **Solution I:**  <a href="#id-design-quml-feedbackandsolutionpopup-solutioni" id="id-design-quml-feedbackandsolutionpopup-solutioni"></a>

![](<../../../.gitbook/assets/1133084676 (1).png>)

\


### **Solution II:** <a href="#id-design-quml-feedbackandsolutionpopup-solutionii" id="id-design-quml-feedbackandsolutionpopup-solutionii"></a>

After question evaluation there is callback method is there to QuestionSet plugin evaluation method, from here if the `questionType: 'quml'` then dispatch an event from questionset to the same event listen in quml plugin.

This will take care of logging  ASSESS event and showing Feedback popup.

![](<../../../.gitbook/assets/1134100508 (1).png>)

\


### **ECML Solution:** <a href="#id-design-quml-feedbackandsolutionpopup-ecmlsolution" id="id-design-quml-feedbackandsolutionpopup-ecmlsolution"></a>

```
[
  {
    "question": "<div class='mcq-vertical cheveron-helper'><div class='mcq-title'><p>स्मृति पाठ के लेखक का नाम है-</p></div><i class='chevron down icon'></i><div class='mcq-options'><div data-simple-choice-interaction data-response-variable='responseValue' value=0 class='mcq-option'><p>जयशंकर प्रसाद   </p></div><div data-simple-choice-interaction data-response-variable='responseValue' value=1 class='mcq-option'><p>मैथिलीशरण गुप्त</p></div><div data-simple-choice-interaction data-response-variable='responseValue' value=2 class='mcq-option'><p> महादेवी वर्मा</p></div><div data-simple-choice-interaction data-response-variable='responseValue' value=3 class='mcq-option'><p>श्रीराम शर्मा</p></div></div></div>",
    "media": [],
    "responseDeclaration": {
      "responseValue": {
        "cardinality": "single",
        "type": "integer",
        "correct_response": {
          "value": "3"
        }
      }
    },
    "options": [
      {
        "answer": false,
        "value": {
          "type": "text",
          "body": "<p>जयशंकर प्रसाद   </p>",
          "resvalue": 0,
          "resindex": 0
        }
      }
      ...
    ],
     "solution": [{
      "value": "<div><p>Video as solution</p></div>",
      "type": "html",
	  "id": UUID //Generate while saving Question
    },
    {
       "vlaue": {mediaId},
       "type": "video",
	  "id": UUID //Generate while saving Question
    }]
]
```

\


Telemetry:

On click of "solution " button, log interact event with id as solution.id(UUID) in the edata.id;

### **Conclusion:** <a href="#id-design-quml-feedbackandsolutionpopup-conclusion" id="id-design-quml-feedbackandsolutionpopup-conclusion"></a>

As discussed with [Rayulu Villa](https://project-sunbird.atlassian.net/wiki/people/557058:cee0b254-59ea-4cde-9b36-aa4d8d417643?ref=confluence) and got a confirmation saying go ahead with solution 1.&#x20;

&#x20;[Asha Vade](https://project-sunbird.atlassian.net/wiki/people/5bfbd2945e2eee35d79f571f?ref=confluence)&#x20;

[Vinu Kumar](https://project-sunbird.atlassian.net/wiki/people/557058:461fa645-cdc5-460b-9212-9971d54e645e?ref=confluence)&#x20;

[Kartheek Palla](https://project-sunbird.atlassian.net/wiki/people/557058:9f800fda-c0d5-42bd-896d-d7b80b367795?ref=confluence)
