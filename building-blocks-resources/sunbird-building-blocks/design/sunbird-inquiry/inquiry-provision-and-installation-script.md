---
icon: elementor
---

# inQuiry - provision & installation script

#### Background: <a href="#inquiry-provision-and-installationscript-background" id="inquiry-provision-and-installationscript-background"></a>

* inQuiry need to document all steps for server installation to provide ease of installation experience for adopters.

#### Problem Statement: <a href="#inquiry-provision-and-installationscript-problemstatement" id="inquiry-provision-and-installationscript-problemstatement"></a>

As of now, below problems identified in scripts and variables:

* inQuiry provision & installation scripts are present across multiple repos (e.g: project-sunbird/sunbird-learning-platform & project-sunbird/sunbird-devops github repo) and these repos are having multiple scripts in different folders for different services of Sunbird-Ed, which is enough to create confusion.
* private repository template is having entire variables for sunbird-Ed.
* few setup script like api-onboarding & kafka setup need to cleanup as it has all sunbird-Ed data.
* there is no service need to be installed in Yarn but still KnowledgePlatform folder is in use under inventory & jenkins jobs. With this folder structure, we are maintaining duplicate variables in two different files.
* need to have clear approach on inQuiry installation without or with Knowlg (only for components on which inquiry depends)

#### Solution: <a href="#inquiry-provision-and-installationscript-solution" id="inquiry-provision-and-installationscript-solution"></a>

* inQuiry will have its own public & private devops repo ([https://github.com/Sunbird-inQuiry/devops](https://github.com/Sunbird-inQuiry/devops))
* only inQuiry specific provisioning script will be moved in above repo.
* private devops repo template will have variables specific to inQuiry & dependent Knowlg components.
* a new folder structure will be introduced under jenkins for Build, ArtifactUpload & Deploy. (e.g: Build/inQuiry/Assessment, deploy/dev/inQuiry/Assessment).
* Above folder structure will help in separating dependent Knowlg BB components under jenkins & ansible variables.

Open Question (for devops team):

1. Can we run api-onboarding job from two different folder in same env (e.g: once for inQuiry & another one for Knowlg api)?
2. Can we run kafka setup from two different folder in same env?
