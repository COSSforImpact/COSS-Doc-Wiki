---
icon: elementor
---

# \[Design] - Match the following Question (Editor & Player)

## **Introduction**  <a href="#id-design-matchthefollowingquestion-editor-and-player-introduction" id="id-design-matchthefollowingquestion-editor-and-player-introduction"></a>

This document describes the design approach for enhancing the inQuiry editor and player to support the creation and consumption of the MTF question.

## Background <a href="#id-design-matchthefollowingquestion-editor-and-player-background" id="id-design-matchthefollowingquestion-editor-and-player-background"></a>

QuML Player and Question Set Editor currently support two types of questions (MCQ and SA) we want to implement and enable MTF question in Editor and Player of sunbird inQuiry

## **Problem Statement** <a href="#id-design-matchthefollowingquestion-editor-and-player-problemstatement" id="id-design-matchthefollowingquestion-editor-and-player-problemstatement"></a>

Currently, the Question Set Editor/Player does not support MTF Question creation and consumption workflow.  How can we enable the MTF in the new QuestionSet Editor and Player with the same features supported by the existing Interactive editor and player?

* The creator should be able to create the Match the Following Questions.
* The creator should be able to add the image and Math & Scientific Text (Formulae & Equation) to the Question.
* The creator should be able to define score for the question.
* The consumer should be able to consume the MTF question created by the creator.
* Partial Scoring of Questions. (Currently no support for this in Questionset Editor and player for any question)

## **Design** <a href="#id-design-matchthefollowingquestion-editor-and-player-design" id="id-design-matchthefollowingquestion-editor-and-player-design"></a>

In this design approach, we will cover the creation and consumption workflow changes along with the MTF Data model as per QuML spec 1.1

### Creation Workflow: <a href="#id-design-matchthefollowingquestion-editor-and-player-creationworkflow" id="id-design-matchthefollowingquestion-editor-and-player-creationworkflow"></a>



* For creating the question, we will use the same question component used for other question types.
* For LHS and RHS options we will use ckeditor component used for MCQ options.
* The editor will throw a validation error if the question / options are empty or contains characters more than the character limit.
* The current QuestionSet editor has the capability to add the image and Math & Scientific Text to the question and options. So We will use the same component for adding the same.
* Partial scoring behaviour will be by default for MTF question as currently in editor/player there is no config to turn on/off partialScore and also backend does not have partialScore property in schema. So it will behave similary as it for MCQ and MMCQ questions. ( we can enhance the Partial Scoring behaviour in future for all types of questions)
* All media images will be stored the way we are storing the images for the others question type.
  * ```
    // LHS and RHS options with images
    "options": {
                        "left": [
                            {
                                "label": "<p>Apple&nbsp;</p><figure class=\"image resize-25 image-style-align-left\"><img src=\"/assets/public/content/do_113867310987550720172/artifact/do_113867310987550720172_1692786985884_540px-npm-logo.svg.png\" alt=\"540px-Npm-logo svg\" data-asset-variable=\"do_113867310987550720172\"></figure>",
                                "value": 0
                            },
                            {
                                "label": "<p>Grapes</p><figure class=\"image resize-25 image-style-align-left\"><img src=\"/assets/public/content/do_113867313360289792173/artifact/do_113867313360289792173_1692787284787_97_virtual-machine.21c22fa0f5.png\" alt=\"97 virtual-machine 21c22fa0f5\" data-asset-variable=\"do_113867313360289792173\"></figure>",
                                "value": 1
                            }
                        ],
                        "right": [
                            {
                                "label": "<p>Red&nbsp;</p><figure class=\"image resize-25 image-style-align-left\"><img src=\"/assets/public/content/do_113867310987550720172/artifact/do_113867310987550720172_1692786985884_540px-npm-logo.svg.png\" alt=\"540px-Npm-logo svg\" data-asset-variable=\"do_113867310987550720172\"></figure>",
                                "value": 0
                            },
                            {
                                "label": "<p>Green&nbsp;</p><figure class=\"image resize-25 image-style-align-left\"><img src=\"/assets/public/content/do_113867313360289792173/artifact/do_113867313360289792173_1692787284787_97_virtual-machine.21c22fa0f5.png\" alt=\"97 virtual-machine 21c22fa0f5\" data-asset-variable=\"do_113867313360289792173\"></figure>",
                                "value": 1
                            }
                        ]
                    }
    ```
* The audio workflow will be not enabled in the new MTF workflow as the new question set editor does not have any audio feature support in question and options. ( we can enhance this in future for all types of questions)

### **Consumption workflow:** <a href="#id-design-matchthefollowingquestion-editor-and-player-consumptionworkflow" id="id-design-matchthefollowingquestion-editor-and-player-consumptionworkflow"></a>

For Quml Player we will make the consumption UI similar to interactive player MTF questions



* Here the LHS options will not be draggable, only right options can be re-arranged.
* All the telemetry event will be handled which were getting generated in interactive player for MTF type of question.
* We will handle the both the horizontal and vertical layout of MTF question in the player similar to interactive player.
* For developing of drag/drop feature we will use [angular cdk](https://material.angular.io/cdk/drag-drop/overview) (Recommended)

#### Approaches for Drag and Drop <a href="#id-design-matchthefollowingquestion-editor-and-player-approachesfordraganddrop" id="id-design-matchthefollowingquestion-editor-and-player-approachesfordraganddrop"></a>

**1. Using Angular CDK (Component Dev Kit) Drag and Drop Module**

The Angular CDK provides a high-level abstraction for drag-and-drop functionality, making it easy to implement without dealing with the lower-level details.

**Pros:**

* **Integration**: Directly integrates with Angular, providing seamless drag-and-drop capabilities.
* **Ease of Use**: Simplifies the implementation with a high-level API.
* **Customization**: Offers a good balance between ease of use and flexibility for customization.
* **Active Maintenance**: Regular updates and support from the Angular team.

**Cons:**

* **Learning Curve**: Some initial learning curve if you are not familiar with Angular CDK.
* **Limited Out-of-the-Box Features**: For very complex requirements, additional coding might be needed.

**2. Using Angular Material Drag and Drop**

Angular Material, which depends on the CDK, also includes drag-and-drop functionality. The implementation is similar to using the CDK directly but often includes more styling and pre-built components.

**Pros:**

* **Built on CDK**: Provides additional styling and component features on top of Angular CDK.
* **Material Design**: Consistent with Material Design principles, which is beneficial if you are using Angular Material in your project.

**Cons:**

* **Heavyweight**: Adds additional weight to your project due to Material dependencies.
* **Styling**: Might require additional customization to fit specific non-material design requirements.

**3. Using Native HTML5 Drag and Drop**

**Pros:**

* **Control**: Offers fine-grained control over the drag-and-drop functionality.
* **Lightweight**: No additional libraries required, minimal overhead.

**Cons:**

* **Complexity**: Requires more effort to implement and manage state.
* **Browser Inconsistencies**: Need to handle browser-specific quirks and inconsistencies.

**4. Using Third-Party Libraries**

* ngx-drag-drop
  * Pros:
    * **Flexibility**: Offers extensive configuration options.
    * **Ease of Use**: Simplifies complex drag-and-drop tasks.
  * Cons:
    * **Additional Dependency**: Adds another dependency to your project.
    * **Community Support**: May not be as widely supported or updated as Angular CDK.
* ng2-dragula
  * Pros:
    * **Ease of Use**: Very user-friendly and quick to set up.
    * **Complex Scenarios**: Handles complex drag-and-drop scenarios effectively.
  * Cons:
    * **Learning Curve**: Different API and setup process.
    * **Dependency**: Another dependency in your project.
    * **Integration Challenge:** Facing challenge in integration in angular

The Angular CDK is usually the preferred choice for most Angular applications due to its ease of use and flexibility

#### MTF Data model <a href="#id-design-matchthefollowingquestion-editor-and-player-mtfdatamodel" id="id-design-matchthefollowingquestion-editor-and-player-mtfdatamodel"></a>

Data model for MTF question is detailed in [\[Data Model\] Match the Following Question](https://project-sunbird.atlassian.net/wiki/spaces/QB/pages/3416326145/Data+Model+Match+The+Following+Question) document.
