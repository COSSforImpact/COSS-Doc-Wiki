---
icon: elementor
---

# Project-creation

This page details the definitions and items relevant to the project creation.

The proposed interaction flow for the Project creation is mentioned below:

\| Sl | User story | Present user interaction | Proposed user interaction | Open Items/ Decisions | | 1 | Admin can create a Project for sourcing question papers. |

1. Go to Diskha Portal, to create a new Question paper collection
2. Define metadata for the question paper
3. Define sections of the question paper
4. Define instructions for the question paper

\| Admin will go to sorucing (vdn sourcing) and create project along with the question set defining the scope.

1. Go to souricng portal, Create new project
2. Name the project, allow or not allow nominations
3. Define relevant dates
4. Select target object (of the type Collection or question paper set)
5. Selects the target assets (filtered list based on selected target object)
6. Create or select target Object(s)
   1. Creation flow
   2. Define metadata for question set \[Grade, Subject, medium, etc]
   3. Define sections for the question set
   4. Define Instructions for the question set
   5. Select from existing flow
   6. Admin can also search for past question sets, using filters for grade, subject, medium.
   7. Admin can select one or more existing question sets
7. Define blueprint for each of the question set(s)
8. Pubish project

\| Closed:

1. Question set on the dev portal now, does not allow to add sections. Is that a limitation? Creation of sections can be managed through configuration, we need to specify/limit levels at which sections can be created.
2. Question sets, can only be created/selected through this flow. There is no separate screen/ touchpoint where user can view/create question sets.
3. Blueprint definition will happen as per the current flow.
4. For point number 6 in the proposed flow:
   1. Object level value will be stored for
   2. Allow creation of new target → This will show the button of create new
   3. Allow selection from existing target → This will show the button of select from existing which will open a pop-up to create/select from the exisiting
5. Since we are already defining the question set definition what is the use of collection creator role? This has been removed from the design

Open Tasks:

1. Review by design team on the UI Mockup
2. Use case grooming session with Kartheek
3. Enginnering implementation design to be shared by Bharat

\| | 2 | Admin can assign users as Souricng reviewers (Question paper creator) |

1. Go to Souricng portal
2. Select a published project
3. Go to assign users tab (in project details page)
4. Search for user and assign them the role of reviewer

\| No interaction ChangeNo UI Change | Closed:

1. There will not be any change in this flow due to the change in project creation flow.

\| | 3 | Admin can assign users as Question contributors and Question reviwers |

1. Go to Contribution portal
2. Select a published project
3. Go to assign users tab (in project details page)
4. Search for user and assign them the role of reviewer

\| No interaction ChangeNo UI Change | Closed:

1. There will not be any change in this flow due to the change in project creation flow.
2. It is not possible to allow for contribution roles from the sourcing portal.

Open:

1. Design flow for taking user to the contribution role assignment page from souricng project.

|

### Details

1. **Flow for creating a new question set**
   1. User clicks on create new question set
   2. User provides the Metadata, sections, and Instructions for the question set
   3. User saves the question set by clicking the save button
   4. On save the question set is saved
   5. On save - The user redirected to the previous screen of selecting/creating a new question set
   6. To create a another question set
   7. User again clicks on the create new question set button
   8. Follow the flow explained above
2. **Metadata** - These define the details and the scope of the question set
   1. Name - Default value?
   2. Description
   3. Instruction
   4. Keywords
   5. Board \*
   6. Medium \*
   7. Class \*
   8. Subject \*
   9. Topics - NA
   10. Audience \* - Default - Student
   11. Max Attempts - NA
   12. Shuffle questions - Default not selected
   13. Max attempts - NA
   14. Max time - NA
   15. Waiting time - NA
3. **Sections** - These define the sections under which questions are added.
   1. No section can be added
   2. In this case, all the questions are sequentially added one after the another
   3. If the sections are added
   4. There would be only one level of sections
   5. A question can belong inside a particular section
   6. Or some question can be added directly to the question set after or before the section
   7. The sequence of questions in the question paper is fixed as per the sequence the questions are added.
4. **Instructions** - These are typically text which is shared at the start of the question paper, this is unique for each question paper/set.
   1. Requires support for numbering - Mandatory
   2. Requires support for Rich text editing - Good to have
   3. Image support - As per the current requirement/ understanding, this is not required.

No change in the current flow of Assigning roles on Sourcing or Contribution.

***

\[\[category.storage-team]] \[\[category.confluence]]
