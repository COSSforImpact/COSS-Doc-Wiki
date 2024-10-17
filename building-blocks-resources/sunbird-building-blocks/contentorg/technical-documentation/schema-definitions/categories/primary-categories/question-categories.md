---
icon: elementor
---

# Question categories

List of categories of Question

## Multiple Choice Question <a href="#multiple-choice-question" id="multiple-choice-question"></a>

* Is Primary Category? Yes
* displayLabel: Multiple Choice Question
* objectType: Question
* mimeType:
* Interaction types: \[“select“] ?
* Name: (used to be `title` in Assessment Item spec)\
  → Editor will auto-generate name so that it can be displayed in Question Search
* Description: (used to be `Short Description` in Assessment Item spec)
* Instructions: Not required, no default
* Organisation Framework: derived from Question Set category definition
  * Board, Medium, Class, Subject, Topic, Learning Outcome - No default, Not mandatory. Tenant specific configuration might differ from each other.
* Target Framework: will be mostly blank. Not required.
* Audience: derived from Question Set category definition
* Visibility: set by Question Set category definition
* License: derived from Question Set category definition. Defaulted to default license of the tenant (user can change), Mandatory
* Owner: set by system
* Author: Defaulted to creator name (user can change), Mandatory
* Copyright: Defaulted to Tenant Name (user can change), Mandatory
* Attributions: No default, , Not Mandatory
* Additional Categories: Not required, no default
* Trackable: Not required, no default
* Max Score: set by creator, no default, not required
* Body: provided by creator, required, at least two options, no default
* Feedback: not required, no default
* Answer: not required, no default
* Solution: not required, no default
* Response declaration: at least two options
* Response processing: award marks as per response mapping
* Interactions: at least two options
* Scoring Mode: default = system, can be none, derived from Question Set category definition
* TimeLimit: not required, no default. TimeLimit with Max time, Warning time
* ShowTimer: not required, no default
