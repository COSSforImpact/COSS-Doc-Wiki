---
icon: elementor
---

# Assessment Report - Total scores of the assessment

### Introduction <a href="#assessmentreport-totalscoresoftheassessment-introduction" id="assessmentreport-totalscoresoftheassessment-introduction"></a>

This wiki explains that how to calculate the Total score of assessment.

### Background <a href="#assessmentreport-totalscoresoftheassessment-background" id="assessmentreport-totalscoresoftheassessment-background"></a>

Currently total score is dependent on telemetry from the player. Listing the telemetry for each assessment for that content and doing the sum of max score for each assessment attempted by user. &#x20;

### Problem Statement <a href="#assessmentreport-totalscoresoftheassessment-problemstatement" id="assessmentreport-totalscoresoftheassessment-problemstatement"></a>

When user is consuming any assessment which is having suppose 10 questions (assuming each question is having max score 1) and user has consumed partially (6 out of 10 and kill the app or click on exit from hamburger menu), then in report showing only 6/6 instead of 6/10.

### Key Design Problems <a href="#assessmentreport-totalscoresoftheassessment-keydesignproblems" id="assessmentreport-totalscoresoftheassessment-keydesignproblems"></a>

* Total score should display always same whether user has consumed fully or partially any assessment.

### Proposed Design <a href="#assessmentreport-totalscoresoftheassessment-proposeddesign" id="assessmentreport-totalscoresoftheassessment-proposeddesign"></a>

**Solution 1:**

* Read the attribute **totalScore** from content metadata and show in UI.
* Fallback - As the **totalScore** is not available for older content so as a fallback calculate the total score from number of question attended by the user (current implementation).

**Solution 2:**

* Read the attribute **totalScore** from content metadata and show in UI.
* Migrate the old content so fallback is not required in solution 1.

\


[Swayangjit Parida](https://project-sunbird.atlassian.net/wiki/people/557058:69780b52-eed2-43e4-b273-6473bac18bac?ref=confluence) [Sharath Prasad](https://project-sunbird.atlassian.net/wiki/people/5c8a05cf53f3d02a237eebe7?ref=confluence)
