---
icon: elementor
---

# KB - Onboard yourself

### Some history <a href="#kb-onboardyourself-somehistory" id="kb-onboardyourself-somehistory"></a>

Until 3.0, the learner-service was split into 3 repositories - sunbird-lms-service, sunbird-lms-mw and sunbird-utils. In 3.0, it was decided to unify, copy the relevant modules from dependent repos and retain in sunbird-lms-service. Officially, this is called ‘learner’ even though the repo indicates ‘lms’.

### Terms <a href="#kb-onboardyourself-terms" id="kb-onboardyourself-terms"></a>

The following definitions are created in the context of a developer and therefore APIs. The terms are ordered in a way to build a story and create a logical flow to them. The UI and teams could call it slightly altered to benefit the end user. Please use communication channels to understand the context better.

**User** - the end user who is interacting with the SB system.

**User type** - Types are ‘Student’, ‘Teacher’ and ‘Other’. This is used primarily for UI experience. The user is given a chance every time upon login.

**Username / ID** - Often the friendly name that the learner-service generates. Example: raje5478. A concatenation of the users' firstname followed by a set of N random characters.

**Credentials (Certificates)** - The online awards the user has received by virtue of completing a course or participating in a quiz or an event that presents an award in the SB LMS.

**Stronger credentials** - User’s password

**Less stronger/light credentials** - Used to denote the not-yet-implemented PIN based access mechanism.

**LUA** - Logged in user account - user who has stronger credentials.

**MUA** - Managed user account - user who has no stronger credentials, often a child or a profile of the user. These could be assumed as similar to FB accounts that allow you to switch users on the same device.

**Org** - a logical grouping of a set of users.

**RootOrg** - a specialised org that has ‘isRootOrg=true’. These are also called ‘tenants’.

**Sub-org** - a specialised org that has ‘isRootOrg=false’ and is lively only within a RootOrg. The sub-orgs could be imagined as schools, departments or business units within the tenant.

**Role** - a privilege a user has. Example: CONTENT\_CREATOR, CONTENT\_REVIEWER, ORG\_ADMIN. The backend doesn’t have any understanding nor even validates this. Neither does Keycloak. All this logic resides in consumption layers only. The role is applicable only within an org.

**Migrate** - The process of updation of rootOrg id of the user. Migration is supported only from custodian org to other tenant org. This can happen in any of these times - a) SSO onboarding b) shadow db upload c)self-declaration migration.

**Merge** - Two accounts exist a and b. The account a is of custodian and b is state. Both belongs to the same user and the user wants to use b. In such cases, a merge is initiated as user ‘b'. So the course progress, certificates move from a → b. This doesn’t take care of MUA child users and their progress, certs of ‘a' (still a feature gap). The merge from non-custodian to custodian is disallowed. Before this operation, the user b has to prove ownership of a. Upon a successful initiation of merge operation, the account 'a’ is freed-up.

**Free up** - API is used to nullify the email and phone identifiers of the user. To allow users to recover, these identifiers are still preserved in prevUsedPhone and prevUsedEmail columns. These are used in the time of ‘Recover account’ or ‘Forgot password’ workflows.

More details about the schema and some meaning to each of the attribute can be found [here](https://docs.google.com/document/d/1Q7kdLNihihIpY0fRaLJy2s5\_I-2IctldJBbvqesuknc/edit?usp=sharing).

### Redis <a href="#kb-onboardyourself-redis" id="kb-onboardyourself-redis"></a>

Install on Mac - [https://medium.com/@petehouston/install-and-config-redis-on-mac-os-x-via-homebrew-eb8df9a4f298](https://medium.com/@petehouston/install-and-config-redis-on-mac-os-x-via-homebrew-eb8df9a4f298)

### Functional tests <a href="#kb-onboardyourself-functionaltests" id="kb-onboardyourself-functionaltests"></a>

Job path - jenkins/job/Deploy/job/dev/job/Kubernetes/job/FuntionalTestCases

### Debugging Play based projects in IDE <a href="#kb-onboardyourself-debuggingplaybasedprojectsinide" id="kb-onboardyourself-debuggingplaybasedprojectsinide"></a>

```
mvnDebug play2:run
Change the port to 8000 in remote jvm [Edit configuration - IDE]
```

### Devops <a href="#kb-onboardyourself-devops" id="kb-onboardyourself-devops"></a>

1. Docker Java options are picked up from here -

[https://github.com/project-sunbird/sunbird-devops/blob/release-2.10.0/kubernetes/helm\_charts/core/learner/values.j2#L9](https://github.com/project-sunbird/sunbird-devops/blob/release-2.10.0/kubernetes/helm\_charts/core/learner/values.j2#L9)\
[Dockerfile](https://github.com/project-sunbird/sunbird-lms-service/blob/release-2.10.0/Dockerfile) - refers to java options
