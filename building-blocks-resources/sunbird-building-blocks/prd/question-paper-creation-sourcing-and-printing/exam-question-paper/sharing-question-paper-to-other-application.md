---
icon: elementor
---

# Sharing question paper to other application

**Context:**

In the state of Haryana, Prashnavali is being envisioned as the single source of digital question repository for the state. (earlier planned for only offline printed question paper based testing)

In the scenario of COVID and schools shut down, online SATs will be conducted where students will attempt the assessment through the State’s Learning App.

_**State’s learning and assessment Apps**_ - In the case of Haryana, the Avsar app is currently being used for conducting online SATs and online quizzes.\
Avsar has: Student facing - Android App & Admin facing - Portal to manage content

**The current way of operation for Avsar App:**

_User steps involved:_

1. &#x20;For online exams and online quizzes -&#x20;
2. Teachers create questions and share the same in defined excel format/word format with the SCERT Admin team
3. SCERT Admin team creates the CSV(from word) or verifies the CSV format, and uses bulk upload feature on Avsar app to upload the questions
4. Caveat - Questions with images can not be included in the CSV format, these questions are uploaded separately one by one on the Avsar Frontend portal (which has a question editor to add text and images)

_Type of questions currently being used for online exams:_

1. &#x20;Multiple Choice Questions (MCQ)&#x20;

***

**Approach 1 - Standard API for any 3rd party APP to plugin into and use**

Further on this to be discussed.

&#x20;

***

**Approach 2 - CSV Download**&#x20;

1. Provision to download questions in the bulk of all questions in the question paper
2. Questions of **text type** to get downloaded in the bulk download format.
   1. Bulk download functionality to support **Hindi and English text.** (Questions to be downloaded in the same language in which they were created on the portal).
   2. For questions that have an **attachment (Image. Special Character, Mathematical symbol),** an **attachment url to be populated in the bulk download template.**\
      This will enable the user to download the questions to open the attachment url in Web and download the attachment from web.
3. Provision for Question Reviewer (Vidyadaan - Contribution Portal) to download the approved questions. (Option to be made available next to **Bulk Download button**)
4. Provision for Question Paper Creator (Reviewer : Vidyadaan - Sourcing Portal) to download the approved questions. (Options to be made available next to **Print and Preview Button**) The template in which questions should get downloaded is attached - [Link ](https://docs.google.com/spreadsheets/d/1XAvqLk3GC6OTSjG3RH53dZ7TnxZpnPaX3gJQApEdagE/edit#gid=0)
   1. Class&#x20;
   2. Subject
   3. Question Type
   4. Question
   5. Question contains attachments (indicator whether the question has any attachment)
   6. Options - 1:4 (For MCQ, provision to add options for the question)
   7. Answer
   8. Solution
   9. Question Name
   10. Chapter
   11. Competency
   12. Skills Tested
   13. Marks
   14. Copyright and Year
