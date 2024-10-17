---
icon: elementor
---

# Survey

1. **Matrix** : A question set which is meant for multi-entity.
   1. Entity can be school / child / teacher / principal (not predefined, not related to any user entity in system) OR user profile (switch user, etc)
   2. can have a limit to number of responses allowed or can have a minimum number of responses required
   3. On play, should show required number of entity responses (Child 1, Child 2, ..)
   4. On play, should show ‘Add Child’ to add more responses → Entity ID (Unique ID), Entity Name (Child 1), Entity type (Child)
   5. Show questions for each entity response → Name, Age, Gender, School, Fav subject, etc
   6. Does not cover multiplayer quiz like scenario - either on same device or on different devices. Since entity is not understood by system - not related to any object in the system. (Not covering TN Assessment use-case, switch profile in player etc)
2. Language translation for question, hints, tip at question level
   1. Translations - supported as part of the model. Creation & consumption is yet to be imagined.
   2. Hint - at question level only, always visible → _make it part of body with specific styling_
   3. Tip - at question & options level, and on-demand only → _store it as Hint in QuML. Enhancement: Hint is not just at interaction level but also at question level_
3. date, auto-capture date,
   1. Text, validation as date (dd-MM-yyyy)
   2. auto-capture enabled
   3. player should insert the timestamp
4. slider type of questions.
   1. range / series with a step: 1 - 10,
   2. lower end, upper end: 1, 10
   3. On play, show slider
   4. Response, single value from the range
5. text, number, select, multi-select type of questions.
   1. Add to interaction types
   2. Update spec
6. Pagination (= Question set)
   1. View mode of question set - normal, page
   2. Questions grouped by question sets to provide page or normal play
7. Section (= Question set within Page question set)
   1. Question Set Name: wherever it is set - show as section name
8. define parent-child questions, with the scenario of one child question being dependent on multiple parents and the condition can be any **and,or,not** or other expressions.
   1. Question set pre-condition at the beginning of the question set
   2. Branching at the end of question set
   3. Convert to question set object wherever these rules are applicable
9. emoji/image as a question option, along with the text description for it.
   1. Only sample
10. if remarks are allowed and can be added for questions.
    1. ‘Add Remark’ to add paragraph remark
    2. Optional - provide response on-demand
    3. Accept text, files, or both
    4. _QuML spec update_ , question object update
11. capture question group(s) (entity types) for which the question is to be answered.
    1. Question is meant for : Schools, Students
    2. Is this correct?
    3. Questions meant for primary school. School is an entity, and Primary school is a meta of school entity.
12. whether the question is to be auto rated or not ?
    1. Evaluation mode:
    2. Correct?
13. File upload
    1. min , max no of files
    2. size limit
    3. mime types allowed
    4. Definition and _Spec update_
14. regex validation for the response to the question.
    1. sample
15. Ability to define if the question can be allowed to be marked as “Not applicable”
    1. If MCQ, create an option called NA
    2. What does NA mean in scoring?
16. Ability to define if a user can upload audio recording as a response to the question
    1. File upload
17. Ability to define question Number - Custom numbers like 1.a or 1.1
    1. Question set behaviour - numbering scheme
    2. Use-case - is it a real need? Is it always “1.a”? Can this be standardised? What is the value?
18. Ability to define the entity meta key to prefil value of question from.
    1. Need clarity
    2. School - number of teachers - pre-filled, can be changed
19. Ability to define the question weightage to be used in scoring.
    1. Sample
20. Ability to define scores at option level for radio/multiselect questions
    1. Sample
21. Capability to define if the question is to be shown in preview
    1. Can it be random? What’s the real value?
22. Ability to define if there is a voice over enabled for question.
    1. Update definition and spec
23. Ability to uniquely identify a question in the solution
    1. Identifier is available

***

\[\[category.storage-team]] \[\[category.confluence]]
