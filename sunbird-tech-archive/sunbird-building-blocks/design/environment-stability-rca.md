---
icon: elementor
---

# Environment Stability - RCA

\


1. ETL job not being executed for 1.14 pre-prod deployment - steps were missed though provided in the deployment tracker
2. Swarm update due to change in a particular node by Azure
3. Refactoring of the variable values (500 variables to 60 variables), Communication to the larger group was not done.&#x20;
4. Peer-review on pre-prod was not for validating this change
5. Possible risk in going to production

\


\


Suggested resolution

1. Can there be a peer review post deployment ?
2. Big refactoring activities DevOps changes could be done in off peak hours, engineering must be involved to help validate. Communication must be done to all the stakeholders before hand.
3. &#x20;Can a dry run on a new instance happen ?
4. Can there be a dev ops process kit for every env ?
5. Can there be a common deployment request tracker ?
6. Can there be only weekly two times deployment requests for devops
7. Can Jira be leveraged for deployment ?
8. How can there be stories that are moving sprint to sprint be minimised ?
