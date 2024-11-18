---
icon: elementor
---

# Defect Workflow

### Overview

The document outlines **Defect Workflow**, detailing the steps and statuses in managing defects within a development process.

#### Workflow Changes:

1. **New Status**: Added "INVALID" for invalid defects.
2. **Mandatory Field**: "Sprint" must be updated when a defect is assigned for fixing.
3. **Validation Rules**:
   * "Valid Defect" field must be "No" when a defect is marked "INVALID."
   * Additional checks to ensure data correctness.

#### Workflow Steps and Transitions:

* **OPEN**:
  * Created by QA with mandatory fields (severity, module, component, etc.).
  * Actions: Move to "IN PROGRESS" (Development team) or "INVALID" (invalid defects).
* **IN PROGRESS**:
  * Fixed by Development.
  * Actions: Move to "READY FOR RELEASE" (ready for testing) or "INVALID."
* **READY FOR RELEASE**:
  * Tested on staging.
  * Moves to "RELEASED."
* **RELEASED**:
  * Can transition to "REOPENED" (if fix fails) or "CLOSED" (if successfully fixed).
* **INVALID**:
  * Can be reassessed and moved to "REOPENED" if found valid by QA.

#### Mandatory Fields by Status:

* Each status has specific fields to be filled (e.g., severity for "OPEN," "Valid Defect" for "INVALID," etc.).

#### Defects Conversion to Bugs:

Three options are discussed:

1. **Convert defects directly to bugs** (risk of traceability loss).
2. **Clone defect and convert clone to bug** (preserves defect count but requires additional QA effort).
3. **Create a new bug and close defect** (ensures accurate defect count but adds QA effort).

#### Discussion Points:

* A final approach for handling defects that need bug creation needs consensus.

The workflow emphasizes data validation, traceability, and structured transitions to ensure defect handling is efficient and accurate.

### Key Questions Answered:

#### General Workflow

1. What is the purpose of Defect Workflow 2.0?
2. What are the key statuses in the defect workflow?
3. What transitions are allowed between defect statuses?

#### Workflow Changes

4. What changes have been made to the previous defect workflow?
5. Why was the "INVALID" status added to the workflow?
6. What validation rules are introduced in Defect Workflow 2.0?

#### Field Requirements

7. What mandatory fields are required for each defect status?
8. When should the "Sprint" field be updated in the workflow?
9. What happens if the "Valid Defect" field is marked as "No"?

#### Workflow Transitions

10. What actions can a QA team take on defects in the "OPEN" status?
11. What is the process for defects that transition to the "IN PROGRESS" status?
12. What happens to defects marked as "INVALID"?
13. How does a defect move from "READY FOR RELEASE" to "RELEASED"?
14. Under what conditions can a "RELEASED" defect be reopened?
15. When is a defect considered "CLOSED"?

#### Bug Conversion

16. What are the three options for converting defects into bugs?
17. What are the advantages and disadvantages of directly converting defects to bugs?
18. Why might cloning a defect to create a bug not be the best option?
19. How does creating a bug and closing the defect affect defect count accuracy?

#### Validation and Data Accuracy

20. What validations are performed to ensure data correctness in the workflow?
21. How is traceability ensured in the defect-to-bug conversion process?

#### Discussion Points

22. What considerations are required for handling defects that require bug creation?
23. What additional effort is needed from the QA team for various bug conversion methods?

#### Miscellaneous

24. Who is responsible for opening a defect in the workflow?
25. What is the process for marking a defect as fixed?
26. How does the workflow handle retesting of defects after deployment?
27. What is the role of the "Defect Root Cause" field in the workflow?

{% embed url="https://docs.google.com/presentation/d/1XWUm0rjqVWjjNHeMQycHFs-RDCdNoBxOlQA8zLC-V40/edit?usp=sharing" %}
