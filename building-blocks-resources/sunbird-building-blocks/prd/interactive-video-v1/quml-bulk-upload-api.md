---
icon: elementor
---

# QuML Bulk Upload API

* [Introduction and Overview](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2820767758/QuML+Bulk+Upload+API#Introduction-and-Overview)
* [Proposal](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2820767758/QuML+Bulk+Upload+API#Proposal)
* [Requirement Specifications](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2820767758/QuML+Bulk+Upload+API#Requirement-Specifications)
* [Proposed workflow](https://project-sunbird.atlassian.net/wiki/spaces/PRD/pages/2820767758/QuML+Bulk+Upload+API#Proposed-workflow)

&#x20;

## Introduction and Overview <a href="#introduction-and-overview" id="introduction-and-overview"></a>

Sunbird is updating the question model to QuML 2.0. There is a strong need from stakeholders to have a method of porting their existing question content onto Diksha. To satisfy this use case, it will be useful to design a bulk upload mechanism.

For the ECML question model, there was a CSV upload tool that was used by multiple tenants to upload their question content onto Diksha. However, a CSV has some limitations inherent to the format, for example, with respect to mathematical equations, images, and more.

Jira for this task: [![](https://project-sunbird.atlassian.net/rest/api/2/universal\_avatar/view/type/issuetype/avatar/10315)SB-25750: Bulk Question Upload APIGathering Requirements](https://project-sunbird.atlassian.net/browse/SB-25750)

## Proposal <a href="#proposal" id="proposal"></a>

We propose to implement a Bulk Upload API on the backend to enable uploading multiple (to the order of thousands) questions at once onto Diksha.

## Requirement Specifications <a href="#requirement-specifications" id="requirement-specifications"></a>

The use case we are targeting is as follows:

As a user or organization, I would like to upload my current question content on to Diksha so that it is available to a wide audience.

For 4.2: I already have access to the API and specifications, and with these

1. I should be able to create a file or multiple files containing my question bank in the specified format.
2. I should be able to call an API, or contact the tech team to call an API that will then import the questions.
3. I should be able to receive updates on progress and of success/failure of individual question creation.

## Proposed workflow <a href="#proposed-workflow" id="proposed-workflow"></a>

For example, let us say an organization has 50000 questions in their question bank. To use the bulk upload API, they would internally:

1. Convert their questions to the QuML format,
2. Create a single file containing all the questions to upload
3. Call the newly created bulk upload API with a link to this file

The bulk upload API would then work in the following way:

1. Download the file
2. Validate each of the questions in the array. For questions that are not valid, return an array of failed questions
3. For valid questions, they would be put into a queue
4. The queue process would pick up each of the questions and call the Question Creation API
5. The progress can be monitored at any time using existing Sunbird functionality (To Be Investigated)
