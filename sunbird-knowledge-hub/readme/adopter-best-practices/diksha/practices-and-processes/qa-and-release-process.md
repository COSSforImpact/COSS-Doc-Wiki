---
icon: elementor
---

# QA & Release Process

{% embed url="https://drive.google.com/file/d/1B1qLaBlJLA4TDbFAUL9ttuOPIzAykNrA/view?usp=sharing" %}

### Overview

The document outlines the **Quality Assurance (QA) Release Process and Strategy** for DIKSHA, a digital platform for education.&#x20;

***

#### Objectives of the QA Process

The QA process ensures high-quality releases by:

* Validating new features, bug fixes, and enhancements.
* Identifying defects.
* Ensuring no regression issues in existing functionalities.
* Certifying system quality for optimal user satisfaction.

***

#### Key Elements of the QA Process

**1. Test Case Design**

* Test cases include features from Sunbird ED releases.
* Regression test suites encompass various modules like ETB, Courses, and User Onboarding.
* Specific tests for:
  * Backward compatibility.
  * Critical bugs (S1/P1) reported in the last three months.
  * Accessibility for key pages.
* Maintenance of an auto-updating execution tracker.

**2. Regression Entry Criteria**

* Artifacts from Sunbird ED releases, such as:
  * Functional scope.
  * API changes and documentation.
  * Infrastructure updates and configurations.
  * Deployment tracker and release notes.

**3. Regression Kick-off**

* Coordination with stakeholders to finalize features, configurations, and UAT (User Acceptance Testing) plans.
* Identification of known risks with mitigation strategies.

**4. Test Execution in Pre-Production**

* Sanity and regression testing for new and existing features.
* Defect triage meetings to resolve issues.

**5. Defect Management**

* Defects raised in DIKSHA JIRA are categorized and tracked.
* Collaboration with Sunbird ED teams for code-related fixes.

**6. User Acceptance Testing (UAT)**

* UAT conducted by program/solution teams in pre-production.
* Preparation of execution sheets for various modules like VidyaDaan and Manage Learn.

**7. Regression Exit Criteria**

* Defined criteria, such as closure of defects and UAT completion, determine readiness for production deployment.

**8. Status Reporting**

* Daily regression status emails to stakeholders, detailing execution status, defect progress, and risks.

***

#### Production QA

* Execution of test cases for all new features, regression defects, and backward compatibility.
* Mobile app testing includes partial rollout (20% users) for feedback before full deployment.

***

#### Hotfix Verification

* Urgent fixes for critical bugs involve a structured process:
  * Impact analysis and test case identification.
  * Pre-production testing.
  * Night-time deployment with detailed post-deployment validation.

***

#### Load Testing

* Load testing for APIs and modules using JMeter.
* Soak tests for the top 20 APIs.
* Analysis and sharing of results with stakeholders.

***

#### Release Cycles

* Stable releases occur quarterly, with two hotfix releases between stable versions.
* The release cycle aligns with Sunbird ED’s schedule.

***

This document emphasizes a comprehensive QA process for DIKSHA, ensuring robust testing, defect resolution, and a smooth transition from development to production. The strategy highlights collaboration, detailed documentation, and rigorous validation to maintain platform quality.

### Key Questions Answered

Here’s a list of questions that the document answers based on its content:

***

#### General Quality Assurance Process

1. What are the objectives of the DIKSHA Quality Assurance process?
2. How is the QA process structured for a release?
3. What are the responsibilities of the QA team in DIKSHA?

***

#### Test Case Design and Execution

4. What test cases are included in DIKSHA’s regression suite?
5. How are new features and bug fixes tested in DIKSHA?
6. How is backward compatibility ensured for mobile apps?
7. How are test cases maintained and tracked across releases?

***

#### Regression Testing

8. What criteria must be met to begin regression testing?
9. How is regression testing initiated and executed?
10. How are defects identified and managed during regression testing?

***

#### User Acceptance Testing (UAT)

11. What is the UAT process in DIKSHA’s QA strategy?
12. Who is responsible for UAT execution?
13. How are defects identified and resolved during UAT?

***

#### Pre-Production and Production Testing

14. What steps are involved in pre-production testing?
15. How are defects triaged in the pre-production environment?
16. How is the production environment tested after deployment?

***

#### Hotfix Management

17. How are critical hotfixes managed in DIKSHA?
18. What steps are taken to validate hotfixes before production deployment?

***

#### Load Testing

19. How is load testing performed in DIKSHA?
20. What tools are used for load testing?
21. How are the results of load tests analyzed and shared?

***

#### Release Management

22. What is DIKSHA’s release cycle strategy?
23. How are stable and hotfix releases planned and executed?
24. How are deployment schedules communicated to stakeholders?

***

#### Documentation and Reporting

25. What types of documentation are required for each release?
26. How is the status of testing communicated to stakeholders?
27. What details are included in daily regression status emails?

***

#### Risk Management

28. How are known risks identified and mitigated during the QA process?
29. What criteria are used to decide a "Go/No-Go" for production releases?

***

This document serves as a comprehensive guide for understanding the DIKSHA QA process, from planning and execution to defect management and post-deployment verification.
