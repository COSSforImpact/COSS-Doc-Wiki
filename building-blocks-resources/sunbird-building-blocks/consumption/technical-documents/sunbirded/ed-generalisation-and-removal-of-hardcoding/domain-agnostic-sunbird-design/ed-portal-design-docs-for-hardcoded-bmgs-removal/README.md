---
icon: folder-open
---

# \[ED-Portal] - Design-Docs for Hardcoded BMGS removal

## Introduction <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-introduction" id="id-ed-portal-design-docsforhardcodedbmgsremoval-introduction"></a>

This document describes the design approach of BMGS removal in the portal.

* Introduction
  * Background :
  * Existing workflow:
  * Problem Statement:
    * Any adopter should be able to perform the following:
  * Onboarding - Flow
    * User Type:
      * Problem
      * Solution
    * Framework Cateogories(BMGS)
      * Problem
      * Solution
    * Location
      * Problem
      * Solution
  * Landing Page
    * Problem
    * Solution
  * Search filter (BMGS)
    * Problem
    * Solution
  * Content Cosumption
    * Problem
    * Solution

### Background : <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-background" id="id-ed-portal-design-docsforhardcodedbmgsremoval-background"></a>

Jira Ticket : [ED-2004](https://project-sunbird.atlassian.net/browse/ED-2004) - Getting issue details... STATUS

Observation Link : [https://tarento-my.sharepoint.com/:w:/r/personal/rajesh\_kumaravel\_tarento\_com/\_layouts/15/Doc.aspx?sourcedoc=%7BD950D821-5A6E-4ED5-83BB-EB04A8E38CC3%7D\&file=Portal%20-%20BMGS.docx\&action=default\&mobileredirect=true](https://tarento-my.sharepoint.com/:w:/r/personal/rajesh\_kumaravel\_tarento\_com/\_layouts/15/Doc.aspx?sourcedoc=%7BD950D821-5A6E-4ED5-83BB-EB04A8E38CC3%7D\&file=Portal%20-%20BMGS.docx\&action=default\&mobileredirect=true)

Currently, Sunbird -Portal uses hard-coded BMGS. that is tightly coupled with our code base

### Existing workflow: <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-existingworkflow" id="id-ed-portal-design-docsforhardcodedbmgsremoval-existingworkflow"></a>

Change request: As part of [ED-2004](https://project-sunbird.atlassian.net/browse/ED-2004) - Getting issue details... STATUS BMGS should be configurable.

### Problem Statement: <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-problemstatement" id="id-ed-portal-design-docsforhardcodedbmgsremoval-problemstatement"></a>

* Give the flexibility for Sunbird Ed Adopters from **any domain** will be able to install Sunbird Ed & update the required form configuration, and allow the end-to-end creation and consumption of course (+ certificate issuance), textbook and reports.

#### Any adopter should be able to perform the following: <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-anyadoptershouldbeabletoperformthefollowing" id="id-ed-portal-design-docsforhardcodedbmgsremoval-anyadoptershouldbeabletoperformthefollowing"></a>

* Create a new framework for any domain without any BMGS reference.
* Configure the home page. (For example, Diksha has 4 to 5 sections which is completely based on search API. Each section contains a different search query based upon the requirement.). So on the home page, these sections should be configured.
* Skip user selection & framework selection given we have a default value, and also skip selection of location.
* Add or remove categories in the framework selection page, ie. the user can configure the number of categories to be displayed in the framework selection page in portal.
* Create contents(Collection, Course, QuestionSet, Resource) in respective editors and tag it to the newly developed framework, and attach a certificate for trackable content.
* See / discover all the contents tagged to the selected framework on the home page.
* Configure filters depending on the requirement (post content discovery).
* Consume all trackable and non-trackable contents.
* Check the progress and get a certificate after consuming trackable content.
* View the reports after the consumption of trackable content - Hawkeye report should be configurable

### Onboarding - Flow <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-onboarding-flow" id="id-ed-portal-design-docsforhardcodedbmgsremoval-onboarding-flow"></a>

#### User Type: <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-usertype" id="id-ed-portal-design-docsforhardcodedbmgsremoval-usertype"></a>

**Problem**

How to change the label when a new framework is introduced?

How to configure user type popup if a new framework introduced?

How to handle the label translation?

UserType Screenshot![](../../../../../../../../.gitbook/assets/3371729088.png)

**Solution**

Update/Create the below userType form config for the new role “Farmer” \{{host\}}/api/data/v1/form/update

```
{
    "request": {
        "type": "config",
        "action": "get",
        "subType": "userType",
        "rootOrgId": "{{channel_id}}",
        "component": "portal",
        "data": {
            "templateName": "defaultTemplate",
            "action": "get",
            "fields": [
                {
                        "code": "teacher" to "farmer1"
                        "name": "Teacher" to "Grain and oilseed farms"
                        "label": "frmelmnts.lbl.farmer",
                        "visibility": true,
                        "image": "guest-img1.svg",
                        "index": 0,
                        "searchFilter": [
                            farmer1
                        ]
                    },
            ]
        }
    }
}
```

Create a new key for label `frmelmnts.lbl.farmer=Farmer` in en.properites file.

Remove the hardcoded user role from the code base and create an array in config/create a new form config service to add generic role check.

#### Framework Cateogories(BMGS) <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-frameworkcateogories-bmgs" id="id-ed-portal-design-docsforhardcodedbmgsremoval-frameworkcateogories-bmgs"></a>

**Problem**

How to change the label, placeholder of the below BMGS screen?

How to add the new dropdown fields if required?

How to handle the BMGS hardcoded keyword?

BMGS Screenshot![](../../../../../../../../.gitbook/assets/3371729094.png)

**Solution**

To render the framework categories dropdown screen(BMGS) we have 2 approach

1. We can provide an option to select the framewok from framework dropdown as per the below screenshot

![](../../../../../../../../.gitbook/assets/3371827294.png)

2. By default(on init) call the framework read API

Fetch the framework category details form the below framework read api response

```
{
    "id": "api.framework.read",
    "ver": "1.0",
    "ts": "2023-10-12T13:29:14.721Z",
    "params": {
        "resmsgid": "56353510-6903-11ee-979f-f91a1a05304d",
        "msgid": "1ed35094-c59d-46fb-8cd8-ca3ec6ef180c",
        "status": "successful",
        "err": null,
        "errmsg": null
    },
    "responseCode": "OK",
    "result": {
        "framework": {
            "identifier": "agriculture_framework",
            "code": "agriculture_framework",
            "name": "agriculture_framework",
            "description": "Sunbird TPD framework",
            "categories": [
                {
                    "identifier": "agriculture_framework_foodcrops",
                    "code": "foodcrops",
                    "terms": [
                        {
                            "associations": [
                                {
                                    "identifier": "agriculture_framework_livestockmanagement_geneticsandselection",
                                    "code": "geneticsandselection",
                                    "translations": null,
                                    "name": "geneticsandselection",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockmanagement",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_commercialcrops_crops",
                                    "code": "crops",
                                    "translations": null,
                                    "name": "crops",
                                    "description": null,
                                    "index": 0,
                                    "category": "commercialcrops",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockmanagement_feedingandnutrition",
                                    "code": "feedingandnutrition",
                                    "translations": null,
                                    "name": "feedingandnutrition",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockmanagement",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_animalwelfare_diseases",
                                    "code": "diseases",
                                    "translations": null,
                                    "name": "diseases",
                                    "description": null,
                                    "index": 0,
                                    "category": "animalwelfare",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_commercialcrops_pastures",
                                    "code": "pastures",
                                    "translations": null,
                                    "name": "pastures",
                                    "description": null,
                                    "index": 0,
                                    "category": "commercialcrops",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_beefcattle",
                                    "code": "beefcattle",
                                    "translations": null,
                                    "name": "beefcattle",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_bees",
                                    "code": "bees",
                                    "translations": null,
                                    "name": "bees",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                }
                            ],
                            "identifier": "agriculture_framework_foodcrops_grains",
                            "code": "grains",
                            "translations": null,
                            "name": "grains",
                            "description": null,
                            "index": 1,
                            "category": "foodcrops",
                            "status": "Live"
                        },
                        {
                            "associations": [
                                {
                                    "identifier": "agriculture_framework_commercialcrops_pastures",
                                    "code": "pastures",
                                    "translations": null,
                                    "name": "pastures",
                                    "description": null,
                                    "index": 0,
                                    "category": "commercialcrops",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_bees",
                                    "code": "bees",
                                    "translations": null,
                                    "name": "bees",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_commercialcrops_crops",
                                    "code": "crops",
                                    "translations": null,
                                    "name": "crops",
                                    "description": null,
                                    "index": 0,
                                    "category": "commercialcrops",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockmanagement_feedingandnutrition",
                                    "code": "feedingandnutrition",
                                    "translations": null,
                                    "name": "feedingandnutrition",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockmanagement",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_animalwelfare_diseases",
                                    "code": "diseases",
                                    "translations": null,
                                    "name": "diseases",
                                    "description": null,
                                    "index": 0,
                                    "category": "animalwelfare",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_beefcattle",
                                    "code": "beefcattle",
                                    "translations": null,
                                    "name": "beefcattle",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockmanagement_geneticsandselection",
                                    "code": "geneticsandselection",
                                    "translations": null,
                                    "name": "geneticsandselection",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockmanagement",
                                    "status": "Live"
                                }
                            ],
                            "identifier": "agriculture_framework_foodcrops_horticulture",
                            "code": "horticulture",
                            "translations": null,
                            "name": "horticulture",
                            "description": null,
                            "index": 2,
                            "category": "foodcrops",
                            "status": "Live"
                        }
                    ],
                    "translations": null,
                    "name": "foodcrops",
                    "description": null,
                    "index": 1,
                    "status": "Live"
                },
                {
                    "identifier": "agriculture_framework_commercialcrops",
                    "code": "commercialcrops",
                    "terms": [
                        {
                            "associations": [
                                {
                                    "identifier": "agriculture_framework_livestockmanagement_geneticsandselection",
                                    "code": "geneticsandselection",
                                    "translations": null,
                                    "name": "geneticsandselection",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockmanagement",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_beefcattle",
                                    "code": "beefcattle",
                                    "translations": null,
                                    "name": "beefcattle",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockmanagement_feedingandnutrition",
                                    "code": "feedingandnutrition",
                                    "translations": null,
                                    "name": "feedingandnutrition",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockmanagement",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_animalwelfare_diseases",
                                    "code": "diseases",
                                    "translations": null,
                                    "name": "diseases",
                                    "description": null,
                                    "index": 0,
                                    "category": "animalwelfare",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_bees",
                                    "code": "bees",
                                    "translations": null,
                                    "name": "bees",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                }
                            ],
                            "identifier": "agriculture_framework_commercialcrops_crops",
                            "code": "crops",
                            "translations": null,
                            "name": "crops",
                            "description": null,
                            "index": 1,
                            "category": "commercialcrops",
                            "status": "Live"
                        },
                        {
                            "associations": [
                                {
                                    "identifier": "agriculture_framework_livestockmanagement_feedingandnutrition",
                                    "code": "feedingandnutrition",
                                    "translations": null,
                                    "name": "feedingandnutrition",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockmanagement",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_animalwelfare_diseases",
                                    "code": "diseases",
                                    "translations": null,
                                    "name": "diseases",
                                    "description": null,
                                    "index": 0,
                                    "category": "animalwelfare",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_beefcattle",
                                    "code": "beefcattle",
                                    "translations": null,
                                    "name": "beefcattle",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_bees",
                                    "code": "bees",
                                    "translations": null,
                                    "name": "bees",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockmanagement_geneticsandselection",
                                    "code": "geneticsandselection",
                                    "translations": null,
                                    "name": "geneticsandselection",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockmanagement",
                                    "status": "Live"
                                }
                            ],
                            "identifier": "agriculture_framework_commercialcrops_pastures",
                            "code": "pastures",
                            "translations": null,
                            "name": "pastures",
                            "description": null,
                            "index": 2,
                            "category": "commercialcrops",
                            "status": "Live"
                        }
                    ],
                    "translations": null,
                    "name": "commercialcrops",
                    "description": null,
                    "index": 2,
                    "status": "Live"
                },
                {
                    "identifier": "agriculture_framework_livestockmanagement",
                    "code": "livestockmanagement",
                    "terms": [
                        {
                            "associations": [
                                {
                                    "identifier": "agriculture_framework_livestockspecies_bees",
                                    "code": "bees",
                                    "translations": null,
                                    "name": "bees",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_animalwelfare_diseases",
                                    "code": "diseases",
                                    "translations": null,
                                    "name": "diseases",
                                    "description": null,
                                    "index": 0,
                                    "category": "animalwelfare",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_beefcattle",
                                    "code": "beefcattle",
                                    "translations": null,
                                    "name": "beefcattle",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                }
                            ],
                            "identifier": "agriculture_framework_livestockmanagement_feedingandnutrition",
                            "code": "feedingandnutrition",
                            "translations": null,
                            "name": "feedingandnutrition",
                            "description": null,
                            "index": 1,
                            "category": "livestockmanagement",
                            "status": "Live"
                        },
                        {
                            "associations": [
                                {
                                    "identifier": "agriculture_framework_animalwelfare_diseases",
                                    "code": "diseases",
                                    "translations": null,
                                    "name": "diseases",
                                    "description": null,
                                    "index": 0,
                                    "category": "animalwelfare",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_beefcattle",
                                    "code": "beefcattle",
                                    "translations": null,
                                    "name": "beefcattle",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                },
                                {
                                    "identifier": "agriculture_framework_livestockspecies_bees",
                                    "code": "bees",
                                    "translations": null,
                                    "name": "bees",
                                    "description": null,
                                    "index": 0,
                                    "category": "livestockspecies",
                                    "status": "Live"
                                }
                            ],
                            "identifier": "agriculture_framework_livestockmanagement_geneticsandselection",
                            "code": "geneticsandselection",
                            "translations": null,
                            "name": "geneticsandselection",
                            "description": null,
                            "index": 2,
                            "category": "livestockmanagement",
                            "status": "Live"
                        }
                    ],
                    "translations": null,
                    "name": "livestockmanagement",
                    "description": null,
                    "index": 3,
                    "status": "Live"
                },
                {
                    "identifier": "agriculture_framework_livestockspecies",
                    "code": "livestockspecies",
                    "terms": [
                        {
                            "associations": [
                                {
                                    "identifier": "agriculture_framework_animalwelfare_diseases",
                                    "code": "diseases",
                                    "translations": null,
                                    "name": "diseases",
                                    "description": null,
                                    "index": 0,
                                    "category": "animalwelfare",
                                    "status": "Live"
                                }
                            ],
                            "identifier": "agriculture_framework_livestockspecies_beefcattle",
                            "code": "beefcattle",
                            "translations": null,
                            "name": "beefcattle",
                            "description": null,
                            "index": 1,
                            "category": "livestockspecies",
                            "status": "Live"
                        },
                        {
                            "associations": [
                                {
                                    "identifier": "agriculture_framework_animalwelfare_diseases",
                                    "code": "diseases",
                                    "translations": null,
                                    "name": "diseases",
                                    "description": null,
                                    "index": 0,
                                    "category": "animalwelfare",
                                    "status": "Live"
                                }
                            ],
                            "identifier": "agriculture_framework_livestockspecies_bees",
                            "code": "bees",
                            "translations": null,
                            "name": "bees",
                            "description": null,
                            "index": 2,
                            "category": "livestockspecies",
                            "status": "Live"
                        }
                    ],
                    "translations": null,
                    "name": "livestockspecies",
                    "description": null,
                    "index": 4,
                    "status": "Live"
                },
                {
                    "identifier": "agriculture_framework_animalwelfare",
                    "code": "animalwelfare",
                    "terms": [
                        {
                            "identifier": "agriculture_framework_animalwelfare_diseases",
                            "code": "diseases",
                            "translations": null,
                            "name": "diseases",
                            "description": null,
                            "index": 1,
                            "category": "animalwelfare",
                            "status": "Live"
                        }
                    ],
                    "translations": null,
                    "name": "animalwelfare",
                    "description": null,
                    "index": 5,
                    "status": "Live"
                }
            ],
            "type": "K-12",
            "objectType": "Framework"
        }
    }
}
```

Update/Create the below framework-update form config for framewok categories : \{{host\}}/api/data/v1/form/update

```
{
 
    "request": {
            "type": "user",
            "subtype": "framework",
            "action": "update",
            "component": "*",
            "framework": "agriculture_framework",
            "rootOrgId": "{{channel_id}}"
            "data": {
                "templateName": "defaultTemplate",
                "action": "update",
                "fields": [
                    {
                        "code": "foodcrops",
                        "dataType": "text",
                        "name": "foodcrops",
                        "label": "Foodcrops",
                        "description": "Education foodcrops",
                        "editable": true,
                        "inputType": "multi-select",
                        "required": true,
                        "displayProperty": "Editable",
                        "visible": true,
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "index": 1,
                        "translation": "frmelmnts.lbl.foodcrops"
                    },
                    {
                        "code": "commercialcrops",
                        "dataType": "text",
                        "name": "Commercial Crops",
                        "label": "Commercial Crops",
                        "description": "Commercial Crops of instruction",
                        "editable": true,
                        "inputType": "multi-select",
                        "required": true,
                        "displayProperty": "Editable",
                        "visible": true,
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "index": 2,
                        "translation": "frmelmnts.lbl.commercialcrops"
                    },
                    {
                        "code": "livestockmanagement",
                        "dataType": "text",
                        "name": "livestockmanagement",
                        "label": "Livestockmanagement",
                        "description": "livestockmanagement",
                        "editable": true,
                        "inputType": "multi-select",
                        "required": true,
                        "displayProperty": "Editable",
                        "visible": true,
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "index": 3,
                        "translation": "frmelmnts.lbl.livestockmanagement"
                    },
                    {
                        "code": "livestockspecies",
                        "dataType": "text",
                        "name": "Livestockspecies",
                        "label": "Livestockspecies",
                        "description": "livestockspecies of the Content to use to teach",
                        "editable": true,
                        "inputType": "multi-select",
                        "required": false,
                        "displayProperty": "Editable",
                        "visible": false,
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "index": 4,
                        "translation": "frmelmnts.lbl.livestockspecies"
                    },
                    {
                        "code": "animalwelfare",
                        "dataType": "text",
                        "name": "Animalwelfare",
                        "label": "Animalwelfare",
                        "description": "Animalwelfare of the Content to use to teach",
                        "editable": true,
                        "inputType": "multi-select",
                        "required": false,
                        "displayProperty": "Editable",
                        "visible": false,
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "index": 5,
                        "translation": "frmelmnts.lbl.animalwelfare"
                    }
                ]
            }
           
        
    },
    "ts": "2023-10-12T13:41:54.238Z",
    "ver": "1.0"
}
```

Create an new array & push the framework response data(dropdown range) with form config details(type,isEnable,label,placeholder,code…)

formOptions array that will contain the details of label, placeholder, formType and dropdown value etc to show on framework categories(BMGS) screen

```
[
    {
        "code": "foodcrops",
        "dataType": "text",
        "name": "foodcrops",
        "label": "Foodcrops",
        "description": "Education foodcrops",
        "editable": true,
        "inputType": "multi-select",
        "required": true,
        "displayProperty": "Editable",
        "visible": true,
        "renderingHints": {
            "semanticColumnWidth": "four"
        },
        "index": 1,
        "translation": "frmelmnts.lbl.foodcrops",
        "range": [
            {
                "associations": [
                    {
                        "identifier": "agriculture_framework_livestockmanagement_geneticsandselection",
                        "code": "geneticsandselection",
                        "translations": null,
                        "name": "geneticsandselection",
                        "description": null,
                        "index": 0,
                        "category": "livestockmanagement",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_commercialcrops_crops",
                        "code": "crops",
                        "translations": null,
                        "name": "crops",
                        "description": null,
                        "index": 0,
                        "category": "commercialcrops",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_livestockmanagement_feedingandnutrition",
                        "code": "feedingandnutrition",
                        "translations": null,
                        "name": "feedingandnutrition",
                        "description": null,
                        "index": 0,
                        "category": "livestockmanagement",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_animalwelfare_diseases",
                        "code": "diseases",
                        "translations": null,
                        "name": "diseases",
                        "description": null,
                        "index": 0,
                        "category": "animalwelfare",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_commercialcrops_pastures",
                        "code": "pastures",
                        "translations": null,
                        "name": "pastures",
                        "description": null,
                        "index": 0,
                        "category": "commercialcrops",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_livestockspecies_beefcattle",
                        "code": "beefcattle",
                        "translations": null,
                        "name": "beefcattle",
                        "description": null,
                        "index": 0,
                        "category": "livestockspecies",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_livestockspecies_bees",
                        "code": "bees",
                        "translations": null,
                        "name": "bees",
                        "description": null,
                        "index": 0,
                        "category": "livestockspecies",
                        "status": "Live"
                    }
                ],
                "identifier": "agriculture_framework_foodcrops_grains",
                "code": "grains",
                "translations": null,
                "name": "grains",
                "description": null,
                "index": 1,
                "category": "foodcrops",
                "status": "Live"
            },
            {
                "associations": [
                    {
                        "identifier": "agriculture_framework_commercialcrops_pastures",
                        "code": "pastures",
                        "translations": null,
                        "name": "pastures",
                        "description": null,
                        "index": 0,
                        "category": "commercialcrops",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_livestockspecies_bees",
                        "code": "bees",
                        "translations": null,
                        "name": "bees",
                        "description": null,
                        "index": 0,
                        "category": "livestockspecies",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_commercialcrops_crops",
                        "code": "crops",
                        "translations": null,
                        "name": "crops",
                        "description": null,
                        "index": 0,
                        "category": "commercialcrops",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_livestockmanagement_feedingandnutrition",
                        "code": "feedingandnutrition",
                        "translations": null,
                        "name": "feedingandnutrition",
                        "description": null,
                        "index": 0,
                        "category": "livestockmanagement",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_animalwelfare_diseases",
                        "code": "diseases",
                        "translations": null,
                        "name": "diseases",
                        "description": null,
                        "index": 0,
                        "category": "animalwelfare",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_livestockspecies_beefcattle",
                        "code": "beefcattle",
                        "translations": null,
                        "name": "beefcattle",
                        "description": null,
                        "index": 0,
                        "category": "livestockspecies",
                        "status": "Live"
                    },
                    {
                        "identifier": "agriculture_framework_livestockmanagement_geneticsandselection",
                        "code": "geneticsandselection",
                        "translations": null,
                        "name": "geneticsandselection",
                        "description": null,
                        "index": 0,
                        "category": "livestockmanagement",
                        "status": "Live"
                    }
                ],
                "identifier": "agriculture_framework_foodcrops_horticulture",
                "code": "horticulture",
                "translations": null,
                "name": "horticulture",
                "description": null,
                "index": 2,
                "category": "foodcrops",
                "status": "Live"
            }
        ]
    },
    {
        "code": "commercialcrops",
        "dataType": "text",
        "name": "Commercial Crops",
        "label": "Commercial Crops",
        "description": "Commercial Crops of instruction",
        "editable": true,
        "inputType": "multi-select",
        "required": true,
        "displayProperty": "Editable",
        "visible": true,
        "renderingHints": {
            "semanticColumnWidth": "four"
        },
        "index": 2,
        "translation": "frmelmnts.lbl.commercialcrops",
        "range": []
    },
    {
        "code": "livestockmanagement",
        "dataType": "text",
        "name": "livestockmanagement",
        "label": "Livestockmanagement",
        "description": "livestockmanagement",
        "editable": true,
        "inputType": "multi-select",
        "required": true,
        "displayProperty": "Editable",
        "visible": true,
        "renderingHints": {
            "semanticColumnWidth": "four"
        },
        "index": 3,
        "translation": "frmelmnts.lbl.livestockmanagement",
        "range": []
    },
    {
        "code": "livestockspecies",
        "dataType": "text",
        "name": "Livestockspecies",
        "label": "Livestockspecies",
        "description": "livestockspecies of the Content to use to teach",
        "editable": true,
        "inputType": "multi-select",
        "required": false,
        "displayProperty": "Editable",
        "visible": false,
        "renderingHints": {
            "semanticColumnWidth": "four"
        },
        "index": 4,
        "translation": "frmelmnts.lbl.livestockspecies",
        "range": []
    },
    {
        "code": "animalwelfare",
        "dataType": "text",
        "name": "Animalwelfare",
        "label": "Animalwelfare",
        "description": "Animalwelfare of the Content to use to teach",
        "editable": true,
        "inputType": "multi-select",
        "required": false,
        "displayProperty": "Editable",
        "visible": false,
        "renderingHints": {
            "semanticColumnWidth": "four"
        },
        "index": 5,
        "translation": "frmelmnts.lbl.animalwelfare",
        "range": []
    }
]
```

Using the above formOption config will render the framework categories screen

Using the above framework details reference create a `frameworkCategories` array config for reference & **remove the hardcoded BMGS keyword** which is used in code-base make it generic.

```
EX: export const frameworkCategories = ['frameworkCategorie1', 'frameworkCategories2', 'frameworkCategories3', 'frameworkCategories4'....];
```

Generic framework categories screenshot![](../../../../../../../../.gitbook/assets/3371729100.png)

On submit create a generic request & save in local-storage as per the existing design

Sample : Guest user details preference on framework submit :local-storage

```
{
    "name": "guest",
    "formatedName": "Guest",
    "framework": {
        "foodcrops": [
            "grains"
        ],
        "commercialcrops": [
            "crops"
        ],
        "livestockmanagement": [
            "feedingandnutrition"
        ],
        "livestockspecies": [
            "beefcattle"
        ],
        "animalwelfare": [
            "diseases"
        ],
        "board": [],
        "id": "agriculture_framework"
    },
    "role": "farmer1"
}
```

Sample : logged-in user details preference on framework submit : \{{host\}}/learner/user/v3/update

```
{
    "framework": {
        "foodcrops": [
            "grains"
        ],
        "commercialcrops": [
            "crops"
        ],
        "livestockmanagement": [
            "feedingandnutrition"
        ],
        "livestockspecies": [
            "beefcattle"
        ],
        "animalwelfare": [
            "diseases"
        ],
        "id": [
            "agriculture_framework"
        ]
    }
}
```

#### Location <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-location" id="id-ed-portal-design-docsforhardcodedbmgsremoval-location"></a>

**Problem**

How to show the State & District… dropdown if new role added exlculding Student,Parent,Teacher…?

Location screenshot without config![](../../../../../../../../.gitbook/assets/3371729050.png)

**Solution**

Update/Create the below profile\_config-\_v2 form config for new role "farmer" then location field will show below

Sample profile\_config-\_v2 request body : \{{host\}}/api/data/v1/form/update/create

```
{
    "request": {
        "type": "profileConfig_v2",
        "action": "get",
        "subType": "default",
        "rootOrgId": "0138934136407244800",
        "data": {
            "templateName": "profileconfig_v2",
            "action": "get",
            "fields": [
                {
                    "code": "name",
                    "type": "input",
                    "templateOptions": {
                        "labelHtml": {
                            "contents": "<span>$0&nbsp;<span class=\"required-asterisk\">*</span></span>",
                            "values": {
                                "$0": "Name"
                            }
                        },
                        "hidden": true,
                        "placeHolder": "Enter Name",
                        "multiple": false
                    },
                    "validations": [
                        {
                            "type": "required"
                        }
                    ]
                },
                {
                    "code": "persona",
                    "type": "nested_select",
                    "templateOptions": {
                        "hidden": true,
                        "labelHtml": {
                            "contents": "<span>$0&nbsp;<span class=\"required-asterisk\">*</span></span>",
                            "values": {
                                "$0": "Role"
                            }
                        },
                        "placeHolder": "Select Role",
                        "multiple": false,
                        "themeType": "material",
                        "dataSrc": {
                            "marker": "SUPPORTED_PERSONA_LIST"
                        }
                    },
                    "validations": [
                        {
                            "type": "required"
                        }
                    ],
                    "children": {
                        "administrator": [
                            {
                                "code": "state",
                                "type": "select",
                                "templateOptions": {
                                    "labelHtml": {
                                        "contents": "<span>$0&nbsp;<span class=\"required-asterisk\">*</span></span>",
                                        "values": {
                                            "$0": "State"
                                        }
                                    },
                                    "placeHolder": "Select State",
                                    "multiple": false,
                                    "dataSrc": {
                                        "marker": "STATE_LOCATION_LIST",
                                        "params": {
                                            "useCase": "SIGNEDIN_GUEST"
                                        }
                                    }
                                },
                                "validations": [
                                    {
                                        "type": "required"
                                    }
                                ]
                            },
                            {
                                "code": "district",
                                "type": "select",
                                "context": "state",
                                "default": null,
                                "templateOptions": {
                                    "labelHtml": {
                                        "contents": "<span>$0&nbsp;<span class=\"required-asterisk\">*</span></span>",
                                        "values": {
                                            "$0": "District"
                                        }
                                    },
                                    "placeHolder": "Select District",
                                    "multiple": false,
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "district",
                                            "useCase": "SIGNEDIN_GUEST"
                                        }
                                    }
                                },
                                "validations": [
                                    {
                                        "type": "required"
                                    }
                                ]
                            },
                            {
                                "code": "block",
                                "type": "select",
                                "context": "district",
                                "default": null,
                                "templateOptions": {
                                    "label": "Block",
                                    "placeHolder": "Select Block",
                                    "multiple": false,
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "block",
                                            "useCase": "SIGNEDIN"
                                        }
                                    }
                                },
                                "validations": []
                            },
                            {
                                "code": "cluster",
                                "type": "select",
                                "context": "block",
                                "default": null,
                                "templateOptions": {
                                    "label": "Cluster",
                                    "placeHolder": "Select Cluster",
                                    "multiple": false,
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "cluster",
                                            "useCase": "SIGNEDIN"
                                        }
                                    }
                                }
                            },
                            {
                                "code": "school",
                                "type": "select",
                                "context": "cluster",
                                "default": null,
                                "templateOptions": {
                                    "label": "School",
                                    "placeHolder": "Select School",
                                    "multiple": false,
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "school",
                                            "useCase": "SIGNEDIN"
                                        }
                                    }
                                }
                            }
                        ],
                        "farmer1": [
                            {
                                "code": "state",
                                "type": "select",
                                "templateOptions": {
                                    "labelHtml": {
                                        "contents": "<span>$0&nbsp;<span class=\"required-asterisk\">*</span></span>",
                                        "values": {
                                            "$0": "State"
                                        }
                                    },
                                    "placeHolder": "Select State",
                                    "multiple": false,
                                    "themeType": "material",
                                    "dataSrc": {
                                        "marker": "STATE_LOCATION_LIST",
                                        "params": {
                                            "useCase": "SIGNEDIN_GUEST"
                                        }
                                    }
                                },
                                "validations": [
                                    {
                                        "type": "required"
                                    }
                                ]
                            },
                            {
                                "code": "district",
                                "type": "select",
                                "context": "state",
                                "default": null,
                                "templateOptions": {
                                    "labelHtml": {
                                        "contents": "<span>$0&nbsp;<span class=\"required-asterisk\">*</span></span>",
                                        "values": {
                                            "$0": "District"
                                        }
                                    },
                                    "placeHolder": "Select District",
                                    "multiple": false,
                                    "themeType": "material",
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "district",
                                            "useCase": "SIGNEDIN_GUEST"
                                        }
                                    }
                                },
                                "validations": [
                                    {
                                        "type": "required"
                                    }
                                ]
                            },
                            {
                                "code": "block",
                                "type": "select",
                                "context": "district",
                                "default": null,
                                "templateOptions": {
                                    "label": "Block",
                                    "placeHolder": "Select Block",
                                    "multiple": false,
                                    "themeType": "material",
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "block",
                                            "useCase": "SIGNEDIN"
                                        }
                                    }
                                },
                                "validations": []
                            },
                            {
                                "code": "cluster",
                                "type": "select",
                                "context": "block",
                                "default": null,
                                "templateOptions": {
                                    "label": "Cluster",
                                    "placeHolder": "Select Cluster",
                                    "multiple": false,
                                    "themeType": "material",
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "cluster",
                                            "useCase": "SIGNEDIN"
                                        }
                                    }
                                }
                            },
                            {
                                "code": "school",
                                "type": "select",
                                "context": "cluster",
                                "default": null,
                                "templateOptions": {
                                    "label": "School",
                                    "placeHolder": "Select School",
                                    "multiple": false,
                                    "themeType": "material",
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "school",
                                            "useCase": "SIGNEDIN"
                                        }
                                    }
                                }
                            }
                        ],
                        "other": [
                            {
                                "code": "state",
                                "type": "select",
                                "templateOptions": {
                                    "placeHolder": "Select State",
                                    "multiple": false,
                                    "themeType": "material",
                                    "dataSrc": {
                                        "marker": "STATE_LOCATION_LIST",
                                        "params": {
                                            "useCase": "SIGNEDIN_GUEST"
                                        }
                                    }
                                },
                                "validations": [
                                    {
                                        "type": "required"
                                    }
                                ]
                            },
                            {
                                "code": "district",
                                "type": "select",
                                "context": "state",
                                "default": null,
                                "templateOptions": {
                                    "labelHtml": {
                                        "contents": "<span>$0&nbsp;<span class=\"required-asterisk\">*</span></span>",
                                        "values": {
                                            "$0": "District"
                                        }
                                    },
                                    "placeHolder": "Select District",
                                    "multiple": false,
                                    "themeType": "material",
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "district",
                                            "useCase": "SIGNEDIN_GUEST"
                                        }
                                    }
                                },
                                "validations": [
                                    {
                                        "type": "required"
                                    }
                                ]
                            },
                            {
                                "code": "block",
                                "type": "select",
                                "context": "district",
                                "default": null,
                                "templateOptions": {
                                    "label": "Block",
                                    "placeHolder": "Select Block",
                                    "multiple": false,
                                    "themeType": "material",
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "block",
                                            "useCase": "SIGNEDIN"
                                        }
                                    }
                                },
                                "validations": []
                            },
                            {
                                "code": "cluster",
                                "type": "select",
                                "context": "block",
                                "default": null,
                                "templateOptions": {
                                    "label": "Cluster",
                                    "placeHolder": "Select Cluster",
                                    "multiple": false,
                                    "themeType": "material",
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "cluster",
                                            "useCase": "SIGNEDIN"
                                        }
                                    }
                                }
                            },
                            {
                                "code": "school",
                                "type": "select",
                                "context": "cluster",
                                "default": null,
                                "templateOptions": {
                                    "label": "School",
                                    "placeHolder": "Select School",
                                    "multiple": false,
                                    "themeType": "material",
                                    "dataSrc": {
                                        "marker": "LOCATION_LIST",
                                        "params": {
                                            "id": "school",
                                            "useCase": "SIGNEDIN"
                                        }
                                    }
                                }
                            }
                        ]
                    }
                }
            ]
        }
    }
}
```

Location Screenshot: Using new role "farmer"![](../../../../../../../../.gitbook/assets/3371925658.png)

### Landing Page <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-landingpage" id="id-ed-portal-design-docsforhardcodedbmgsremoval-landingpage"></a>

**Problem**

How to use the dynamic label, value for new framework categories?

1. How to handle the BMGS hardcorded keyword in landing screen(Home), Profile page?

User-preference Screenshot

![](../../../../../../../../.gitbook/assets/3371761807.png)

**Solution**

Use the On-boarding user-preference details & write the genric code (array iteration) instead of hardcoded in html,ts

generic code for user preferences

```
         <p *ngFor = "let category of userPreference?.framework | keyvalue">
                  <!-- <p> -->
                  <span class="mr-24">
                    <span >{{category.key}}:
                    </span>
                    <p *ngFor="let item of category.value">
                    <span
                      class="font-weight-bold">{{item}}</span>
                    </p>
                  </span>
```

User-preference Screenshot using new framework![](../../../../../../../../.gitbook/assets/3371827344.png)Profile Page Screenshoot using new framework![](../../../../../../../../.gitbook/assets/3372679209.png)

### Search filter (BMGS) <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-searchfilter-bmgs" id="id-ed-portal-design-docsforhardcodedbmgsremoval-searchfilter-bmgs"></a>

In Portal there are two type of search filter i.e page-level search-filter(exclude the All tab) & global-search-filter(used in All tab & groups facets based) .

#### Problem <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-problem.4" id="id-ed-portal-design-docsforhardcodedbmgsremoval-problem.4"></a>

How to change the label,placeholder?

How to add a new search filter dropdown?

How to modify/remove the dropdown?

How to handle the filters event?

How to handle the BMGS hardcorded code?

How to handle the label transaltion?

Search filter screenshoot![](../../../../../../../../.gitbook/assets/3371729106.png)

#### Solution <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-solution.4" id="id-ed-portal-design-docsforhardcodedbmgsremoval-solution.4"></a>

To add/remove a new filter dropdown

Create/Upate the menubar form config tab based

```
"request": {
        "type": "contentcategory",
        "action": "menubar",
        "subType": "global",
        "rootOrgId": "0138934136407244800",
        "data": {
            "action": "list",
            "fields": [
                {
                    "index": 0,
                    "search": {
                        "fields": [
                            "name",
                            "appIcon",
                            "medium",
                            "subject",
                            "resourceType",
                            "contentType",
                            "organisation",
                            "topic",
                            "mimeType",
                            "trackable",
                            "foodcrops",
                            "livestockmanagement",
                            "commercialcrops",
                            "livestockspecies",
                            "animalwelfare"
                        ],
                        "facets": [
                            "subject",
                            "primaryCategory",
                            "medium",
                            "banner",
                            "additionalCategories",
                            "search",
                            "ContinueLearning",
                            "foodcrops",
                            "livestockmanagement",
                            "commercialcrops",
                            "livestockspecies",
                            "animalwelfare"
                        ],
                        "filters": {
                            "commercialcrops": [],
                            "livestockmanagement": [],
                            "audience": [],
                            "foodcrops": [],
                            "primaryCategory": [
                                "Digital Textbook",
                                "eTextbook",
                                "Course"
                            ],
                            "channel": [],
                            "subject": []
                        }
                    },
                    "contentType": "home",
                    "title": "frmelmnts.lbl.home",
                    "default": true,
                    "isEnabled": true,
                    "anonumousUserRoute": {
                        "route": "/explore",
                        "queryParam": "home"
                    },
                    "loggedInUserRoute": {
                        "route": "/resources",
                        "queryParam": "home"
                    },
                    "filter": {
                        "isEnabled": false,
                        "type": "facet"
                    },
                    "theme": {
                        "className": "home",
                        "baseColor": "",
                        "textColor": "",
                        "supportingColor": "",
                        "imageName": "courses-banner-img.svg"
                    },
                    "desc": "frmelmnts.lbl.home",
                    "isOnlineOnly": true,
                    "sections": [
                        {
                            "index": 4,
                            "apiConfig": {
                                "url": "",
                                "req": {
                                    "request": {
                                        "fields": [
                                            "name",
                                            "appIcon",
                                            "mimeType",
                                            "identifier",
                                            "pkgVersion",
                                            "resourceType",
                                            "contentType",
                                            "channel",
                                            "organisation",
                                            "trackable",
                                            "foodcrops",
                                            "livestockmanagement",
                                            "commercialcrops",
                                            "livestockspecies",
                                            "animalwelfare",
                                            "lastPublishedOn"
                                        ],
                                        "facets": [
                                            "se_subjects"
                                        ],
                                        "limit": 100,
                                        "filters": {
                                            "status": [
                                                "Live"
                                            ],
                                            "contentType": [
                                                "Course"
                                            ],
                                            "batches.status": [
                                                1
                                            ],
                                            "livestockmanagement": [
                                                "feedingandnutrition"
                                            ],
                                            "livestockspecies": [
                                                "bees"
                                            ],
                                            "animalwelfare": [
                                                "diseases"
                                            ],
                                            "batches.enrollmentType": "open",
                                            "commercialcrops": [
                                                "pastures"
                                            ],
                                            "foodcrops": [
                                                "grains"
                                            ],
                                            "primaryCategory": [
                                                "Course"
                                            ]
                                        },
                                        "sort_by": {
                                            "lastPublishedOn": "desc"
                                        }
                                    }
                                },
                                "params": "",
                                "sortBy": "lastPublishedOn",
                                "contextKey": "res.facet.search",
                                "method": ""
                            },
                            "title": "frmelmnts.lbl.recentlyPublishedCourses",
                            "isEnabled": true,
                            "facetKey": "search",
                            "desc": "Section for Searched contents"
                        },
                        {
                            "index": 0,
                            "facetKey": "ContinueLearning",
                            "title": "Continue Learning",
                            "isEnabled": true,
                            "desc": "Continue Learning"
                        },
                        {
                            "index": 5,
                            "apiConfig": {
                                "url": "",
                                "req": {
                                    "request": {
                                        "fields": [
                                            "name",
                                            "appIcon",
                                            "mimeType",
                                            "identifier",
                                            "pkgVersion",
                                            "resourceType",
                                            "contentType",
                                            "channel",
                                            "organisation",
                                            "trackable",
                                            "foodcrops",
                                            "livestockmanagement",
                                            "commercialcrops",
                                            "livestockspecies",
                                            "animalwelfare",
                                            "lastPublishedOn"
                                        ],
                                        "facets": [
                                            "se_subjects"
                                        ],
                                        "limit": 100,
                                        "filters": {
                                            "status": [
                                                "Live"
                                            ],
                                            "primaryCategory": [
                                                "Course",
                                                "Digital Textbook"
                                            ],
                                            "channel": "01329314824202649627"
                                        },
                                        "sort_by": {
                                            "lastPublishedOn": "desc"
                                        }
                                    }
                                },
                                "params": "",
                                "sortBy": "lastPublishedOn",
                                "contextKey": "res.facet.search",
                                "method": ""
                            },
                            "title": "frmelmnts.lbl.fromncert",
                            "isEnabled": true,
                            "defaultTitle": "From NCERT",
                            "facetKey": "search",
                            "desc": "Section for Searched contents"
                        },
                        {
                            "index": 3,
                            "apiConfig": {
                                "url": "",
                                "params": "",
                                "req": {
                                    "request": {
                                        "fields": [
                                            "name",
                                            "appIcon",
                                            "mimeType",
                                            "identifier",
                                            "pkgVersion",
                                            "resourceType",
                                            "primaryCategory",
                                            "contentType",
                                            "channel",
                                            "organisation",
                                            "trackable",
                                            "foodcrops",
                                            "livestockmanagement",
                                            "commercialcrops",
                                            "livestockspecies",
                                            "animalwelfare"
                                        ],
                                        "facets": [
                                            "se_subjects"
                                        ],
                                        "limit": 100,
                                        "filters": {
                                            "livestockmanagement": [
                                                "geneticsandselection"
                                            ],
                                            "audience": [],
                                            "commercialcrops": [
                                                "pastures"
                                            ],
                                            "foodcrops": [
                                                "grains"
                                            ],
                                            "primaryCategory": [
                                                "Digital Textbook"
                                            ],
                                            "channel": [],
                                            "livestockspecies": [],
                                            "animalwelfare": []
                                        }
                                    }
                                },
                                "contextKey": "res.facet.search",
                                "method": ""
                            },
                            "title": "frmelmnts.lbl.search",
                            "isEnabled": true,
                            "facetKey": "search",
                            "desc": "Section for Searched contents"
                        },
                        {
                            "index": 2,
                            "facetKey": "banner",
                            "title": "frmelmnts.lbl.bannerTitle",
                            "isEnabled": true,
                            "desc": "Section for Banner"
                        },
                        {
                            "index": 1,
                            "apiConfig": {
                                "url": "",
                                "params": "",
                                "req": {},
                                "contextKey": "res.facet.subject",
                                "method": ""
                            },
                            "anonumousUserRoute": {
                                "route": "/explore-course",
                                "queryParam": "course"
                            },
                            "isEnabled": true,
                            "title": "frmelmnts.lbl.subjects",
                            "loggedInUserRoute": {
                                "route": "/learn",
                                "queryParam": "course"
                            },
                            "landing": {
                                "description": "frmelmnts.lbl.exploredescription",
                                "title": "frmelmnts.lbl.exploretitle"
                            },
                            "theme": {
                                "component": "sb-pills-grid",
                                "limit": 10,
                                "colorMapping": [
                                    {
                                        "primary": "rgba(255,139,46,1)",
                                        "secondary": "rgba(255,139,46,0.3)"
                                    },
                                    {
                                        "primary": "rgba(163,99,255,1)",
                                        "secondary": "rgba(163,99,255,0.3)"
                                    },
                                    {
                                        "primary": "rgba(34,139,255,1)",
                                        "secondary": "rgba(34,139,255,0.3)"
                                    },
                                    {
                                        "primary": "rgba(95,192,32,1)",
                                        "secondary": "rgba(95,192,32,0.3)"
                                    },
                                    {
                                        "primary": "rgba(255,128,47,1)",
                                        "secondary": "rgba(255,128,47,0.3)"
                                    },
                                    {
                                        "primary": "rgba(251,70,70,1)",
                                        "secondary": "rgba(251,70,70,0.3)"
                                    },
                                    {
                                        "primary": "rgba(83,109,252,1)",
                                        "secondary": "rgba(83,109,252,0.3)"
                                    },
                                    {
                                        "primary": "rgba(15,186,208,1)",
                                        "secondary": "rgba(15,186,208,0.3)"
                                    }
                                ],
                                "infiniteCard": false,
                                "icons": {
                                    "default": "assets/images/book_default.svg",
                                    "science": "assets/images/globe.svg",
                                    "english": "assets/images/book_english.svg",
                                    "mathematics": "assets/images/calculator.svg"
                                }
                            },
                            "facetKey": "subject",
                            "desc": "Section for subjects"
                        },
                        {
                            "index": 6,
                            "apiConfig": {
                                "url": "",
                                "params": "",
                                "req": {},
                                "contextKey": "res.facet.primaryCategory",
                                "method": ""
                            },
                            "anonumousUserRoute": {
                                "route": "/explore-course",
                                "queryParam": "course"
                            },
                            "isEnabled": true,
                            "search": {
                                "facets": [
                                    "foodcrops",
                                    "livestockmanagement",
                                    "commercialcrops",
                                    "livestockspecies",
                                    "animalwelfare",
                                    "primaryCategory",
                                    "additionalCategories"
                                ]
                            },
                            "title": "frmelmnts.lbl.dscfrmctgries",
                            "loggedInUserRoute": {
                                "route": "/learn",
                                "queryParam": "course"
                            },
                            "landing": {
                                "description": "frmelmnts.lbl.exploredescription",
                                "title": "frmelmnts.lbl.exploretitle"
                            },
                            "filter": {
                                "additionalCategories": [
                                    "tv lesson"
                                ],
                                "primaryCategory": [
                                    "course",
                                    "digital textbook",
                                    "etextbook"
                                ]
                            },
                            "merge": {
                                "source": "primaryCategory",
                                "destination": "additionalCategories"
                            },
                            "theme": {
                                "component": "sb-pills-grid",
                                "limit": 10,
                                "colorMapping": [
                                    {
                                        "primary": "rgba(255,255,255,1)",
                                        "secondary": "rgba(255,255,255,1)"
                                    }
                                ],
                                "infiniteCard": false,
                                "icons": {
                                    "digital textbooks": "assets/images/textbook.svg",
                                    "documents": "assets/images/documents.svg",
                                    "videos": "assets/images/videos.svg",
                                    "default": "assets/images/all_content.svg",
                                    "courses": "assets/images/course.svg",
                                    "tv programs": "assets/images/tv.svg"
                                }
                            },
                            "facetKey": "primaryCategory",
                            "desc": "Section for category"
                        },
                        {
                            "index": 7,
                            "apiConfig": {
                                "url": "",
                                "params": "",
                                "req": {},
                                "contextKey": "res.facet.medium",
                                "method": ""
                            },
                            "anonumousUserRoute": {
                                "route": "/home",
                                "queryParam": "course"
                            },
                            "isEnabled": false,
                            "title": "frmelmnts.lbl.medium",
                            "loggedInUserRoute": {
                                "route": "/learn",
                                "queryParam": "course"
                            },
                            "theme": {
                                "component": "sb-pills-grid",
                                "limit": 10,
                                "colorMapping": [
                                    {
                                        "primary": "rgba(255,139,46,1)",
                                        "secondary": "rgba(255,139,46,0.3)"
                                    },
                                    {
                                        "primary": "rgba(163,99,255,1)",
                                        "secondary": "rgba(163,99,255,0.3)"
                                    },
                                    {
                                        "primary": "rgba(34,139,255,1)",
                                        "secondary": "rgba(34,139,255,0.3)"
                                    },
                                    {
                                        "primary": "rgba(95,192,32,1)",
                                        "secondary": "rgba(95,192,32,0.3)"
                                    },
                                    {
                                        "primary": "rgba(255,128,47,1)",
                                        "secondary": "rgba(255,128,47,0.3)"
                                    },
                                    {
                                        "primary": "rgba(251,70,70,1)",
                                        "secondary": "rgba(251,70,70,0.3)"
                                    },
                                    {
                                        "primary": "rgba(83,109,252,1)",
                                        "secondary": "rgba(83,109,252,0.3)"
                                    },
                                    {
                                        "primary": "rgba(15,186,208,1)",
                                        "secondary": "rgba(15,186,208,0.3)"
                                    }
                                ],
                                "infiniteCard": false
                            },
                            "facetKey": "medium",
                            "desc": "Section for medium"
                        }
                    ],
                    "menuType": "Content",
                    "metaData": {
                        "defaultFilters": {
                            "commercialcrops": [],
                            "foodcrops": [
                                "grains"
                            ],
                            "livestockmanagement": [
                                ""
                            ]
                        },
                        "groupByKey": "subject",
                        "filters": [
                            "foodcrops",
                            "livestockmanagement",
                            "commercialcrops",
                            "livestockspecies",
                            "animalwelfare",
                            "publisher",
                            "audience",
                            "channel"
                        ]
                    }
                },
                {
                    "index": 1,
                    "search": {
                        "fields": [
                            "audience",
                            "name",
                            "appIcon",
                            "mimeType",
                            "gradeLevel",
                            "identifier",
                            "medium",
                            "pkgVersion",
                            "resourceType",
                            "primaryCategory",
                            "contentType",
                            "channel",
                            "organisation",
                            "trackable",
                            "foodcrops",
                            "livestockmanagement",
                            "commercialcrops",
                            "livestockspecies",
                            "animalwelfare",
                            "creator"
                        ],
                        "facets": [
                            "audience",
                            "foodcrops",
                            "livestockmanagement",
                            "commercialcrops",
                            "livestockspecies",
                            "animalwelfare",
                            "organisation",
                            "creator"
                        ],
                        "filters": {
                            "primaryCategory": [
                                "Digital Textbook",
                                "eTextbook"
                            ]
                        }
                    },
                    "contentType": "textbook",
                    "title": "frmelmnts.lbl.textbooks",
                    "isLoginMandatory": false,
                    "isEnabled": true,
                    "anonumousUserRoute": {
                        "route": "/explore",
                        "queryParam": "textbook"
                    },
                    "loggedInUserRoute": {
                        "route": "/resources",
                        "queryParam": "textbook"
                    },
                    "theme": {
                        "className": "textbooks",
                        "baseColor": "",
                        "textColor": "",
                        "supportingColor": "",
                        "imageName": "textbooks-banner-img.svg"
                    },
                    "desc": "frmelmnts.lbl.textbooks",
                    "isOnlineOnly": true,
                    "menuType": "Content",
                    "metaData": {
                        "defaultFilters": {
                            "commercialcrops": [],
                            "foodcrops": [],
                            "livestockmanagement": []
                        },
                        "cacheTimeout": 86400000,
                        "groupByKey": "subject",
                        "filters": [
                            "publisher",
                            "audience",
                            "channel",
                            "creator",
                            "organisation"
                        ],
                        "searchFilterConfig": [
                            {
                                "category": "foodcrops",
                                "type": "dropdown",
                                "placeholderText": "frmelmnts.lbl.selectFoodcrops",
                                "defaultPlaceholderText": "select foodcrops",
                                "dataSource": "framework",
                                "multiple": false
                            },
                            {
                                "category": "livestockmanagement",
                                "type": "dropdown",
                                "placeholderText": "frmelmnts.lbl.selectLivestockmanagement",
                                "defaultPlaceholderText": "select livestockmanagement",
                                "dataSource": "framework",
                                "multiple": true
                            },
                            {
                                "category": "commercialcrops",
                                "type": "dropdown",
                                "placeholderText": "frmelmnts.lbl.selectCommercialcrops",
                                "defaultPlaceholderText": "select commercialcrops",
                                "dataSource": "framework",
                                "multiple": true
                            },
                            {
                                "category": "livestockspecies",
                                "type": "dropdown",
                                "placeholderText": "frmelmnts.lbl.selectLivestockspecies",
                                "dataSource": "framework",
                                "defaultPlaceholderText": "select livestockspecies",
                                "multiple": true
                            },
                            {
                                "category": "animalwelfare",
                                "type": "dropdown",
                                "placeholderText": "frmelmnts.lbl.selectAnimalwelfare",
                                "dataSource": "framework",
                                "defaultPlaceholderText": "Select animalwelfare",
                                "multiple": true
                            },
                            {
                                "category": "creator",
                                "type": "dropdown",
                                "placeholderText": "Select Creator",
                                "dataSource": "facet",
                                "defaultPlaceholderText": "Select creator",
                                "multiple": true
                            }
                        ]
                    }
                },
               
                {
                    "index": 3,
                    "search": {
                        "fields": [
                            "name",
                            "appIcon",
                            "mimeType",
                            "identifier",
                            "pkgVersion",
                            "resourceType",
                            "contentType",
                            "channel",
                            "organisation",
                            "trackable",
                            "foodcrops",
                            "livestockmanagement",
                            "commercialcrops",
                            "livestockspecies",
                            "animalwelfare",
                            "creator"
                        ],
                        "facets": [
                            "foodcrops",
                            "livestockmanagement",
                            "commercialcrops",
                            "livestockspecies",
                            "animalwelfare",
                            "creator",
                            "organisation"
                        ],
                        "filters": {
                            "status": [
                                "Live"
                            ],
                            "contentType": [
                                "Course"
                            ],
                            "primaryCategory": [
                                "Course",
                                "Course Assessment"
                            ]
                        }
                    },
                    "contentType": "course",
                    "title": "frmelmnts.tab.courses",
                    "isLoginMandatory": false,
                    "isEnabled": true,
                    "anonumousUserRoute": {
                        "route": "/explore",
                        "queryParam": "course"
                    },
                    "loggedInUserRoute": {
                        "route": "/resources",
                        "queryParam": "course"
                    },
                    "theme": {
                        "className": "courses",
                        "baseColor": "",
                        "textColor": "",
                        "supportingColor": "",
                        "imageName": "courses-banner-img.svg"
                    },
                    "batchEndCounter": 4,
                    "desc": "frmelmnts.tab.courses",
                    "isOnlineOnly": true,
                    "menuType": "Content",
                    "metaData": {
                        "defaultFilters": {
                            "commercialcrops": [],
                            "foodcrops": [
                                "grains"
                            ],
                            "livestockmanagement": [
                                "feedingandnutrition"
                            ]
                        },
                        "cacheTimeout": 86400000,
                        "groupByKey": "subject",
                        "filters": [
                            "publisher",
                            "audience",
                            "channel",
                            "creator",
                            "organisation"
                        ],
                        "searchFilterConfig": [
                            {
                                "category": "foodcrops",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.foodcrops",
                                "defaultLabelText": "foodcrops",
                                "placeholderText": "frmelmnts.lbl.selectFoodcrops",
                                "defaultPlaceholderText": "select foodcrops",
                                "dataSource": "framework",
                                "multiple": false
                            },
                            {
                                "category": "commercialcrops",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.commercialcrops",
                                "defaultLabelText": "commercialcrops",
                                "placeholderText": "frmelmnts.lbl.selectCommercialcrops",
                                "defaultPlaceholderText": "select commercialcrops",
                                "dataSource": "framework",
                                "multiple": true
                            },
                            {
                                "category": "livestockspecies",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.livestockspecies",
                                "defaultLabelText": "livestockspecies",
                                "placeholderText": "frmelmnts.lbl.selectLivestockspecies",
                                "defaultPlaceholderText": "select livestockspecies",
                                "dataSource": "framework",
                                "multiple": true
                            },
                            {
                                "category": "animalwelfare",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.animalwelfare",
                                "defaultLabelText": "animalwelfare",
                                "placeholderText": "frmelmnts.lbl.selectanimalwelfare",
                                "dataSource": "framework",
                                "defaultPlaceholderText": "select animalwelfare",
                                "multiple": true
                            },
                            {
                                "category": "livestockmanagement",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.livestockmanagement",
                                "defaultLabelText": "livestockmanagement",
                                "placeholderText": "frmelmnts.lbl.selectLivestockmanagement",
                                "dataSource": "framework",
                                "defaultPlaceholderText": "Select livestockmanagement",
                                "multiple": true
                            },
                            {
                                "category": "creator",
                                "type": "dropdown",
                                "labelText": "Creator",
                                "defaultLabelText": "creator",
                                "placeholderText": "Select Creator",
                                "dataSource": "facet",
                                "defaultPlaceholderText": "Select creator",
                                "multiple": true
                            },
                            {
                                "category": "organisation",
                                "type": "dropdown",
                                "labelText": "Organisation",
                                "defaultLabelText": "org",
                                "placeholderText": "Select Organisation",
                                "dataSource": "facet",
                                "defaultPlaceholderText": "Select org",
                                "multiple": true
                            }
                        ]
                    }
                },
              
                {
                    "index": 5,
                    "search": {
                        "fields": [
                            "name",
                            "appIcon",
                            "mimeType",
                            "identifier",
                            "pkgVersion",
                            "resourceType",
                            "primaryCategory",
                            "contentType",
                            "channel",
                            "organisation",
                            "trackable",
                            "foodcrops",
                            "livestockmanagement",
                            "commercialcrops",
                            "livestockspecies",
                            "animalwelfare"
                        ],
                        "facets": [
                            "foodcrops",
                            "livestockmanagement",
                            "commercialcrops",
                            "livestockspecies",
                            "animalwelfare",
                            "primaryCategory",
                            "mediaType",
                            "mimeType"
                        ],
                        "filters": {
                            "primaryCategory": [
                                "Collection",
                                "Resource",
                                "Content Playlist",
                                "Course",
                                "Course Assessment",
                                "Digital Textbook",
                                "eTextbook",
                                "Explanation Content",
                                "Learning Resource",
                                "Lesson Plan Unit",
                                "Practice Question Set",
                                "Teacher Resource",
                                "Textbook Unit",
                                "LessonPlan",
                                "FocusSpot",
                                "Learning Outcome Definition",
                                "Curiosity Questions",
                                "MarkingSchemeRubric",
                                "ExplanationResource",
                                "ExperientialResource",
                                "Practice Resource",
                                "TVLesson",
                                "Course Unit",
                                "Exam Question",
                                "Question paper"
                            ],
                            "visibility": [
                                "Default",
                                "Parent"
                            ]
                        }
                    },
                    "contentType": "all",
                    "title": "frmelmnts.tab.all",
                    "isLoginMandatory": false,
                    "isEnabled": true,
                    "anonumousUserRoute": {
                        "route": "/explore/1",
                        "queryParam": "all"
                    },
                    "loggedInUserRoute": {
                        "route": "/search/Library/1",
                        "queryParam": "all"
                    },
                    "theme": {
                        "className": "all",
                        "baseColor": "",
                        "textColor": "",
                        "supportingColor": "",
                        "imageName": "all-banner-img.svg"
                    },
                    "desc": "frmelmnts.tab.all",
                    "isOnlineOnly": true,
                    "menuType": "Content",
                    "metaData": {
                        "cacheTimeout": 3600000
                    }
                }
            ],
            "templateName": "menuConfig"
        }
    }
```

Update the new filter key in below schemas form config

```
 "request": {
        "type": "schemas",
        "action": "get",
        "subType": "search",
        "rootOrgId": "0138934136407244800",
        "data": {
            "templateName": "defaultTemplate",
            "action": "get",
            "fields": [
                {
                    "id": "content",
                    "schema": {
                        "properties": [
                            "name",
                            "code",
                            "createdOn",
                            "lastUpdatedOn",
                            "status",
                            "channel",
                            "mimeType",
                            "osId",
                            "contentEncoding",
                            "contentDisposition",
                            "mediaType",
                            "os",
                            "minOsVersion",
                            "compatibilityLevel",
                            "minGenieVersion",
                            "minSupportedVersion",
                            "filter",
                            "variants",
                            "config",
                            "visibility",
                            "audience",
                            "posterImage",
                            "badgeAssertions",
                            "targets",
                            "contentCredits",
                            "appIcon",
                            "grayScaleAppIcon",
                            "thumbnail",
                            "screenshots",
                            "format",
                            "duration",
                            "size",
                            "idealScreenSize",
                            "idealScreenDensity",
                            "releaseNotes",
                            "pkgVersion",
                            "semanticVersion",
                            "versionKey",
                            "resources",
                            "downloadUrl",
                            "artifactUrl",
                            "previewUrl",
                            "streamingUrl",
                            "objects",
                            "organization",
                            "createdFor",
                            "developer",
                            "source",
                            "notes",
                            "pageNumber",
                            "publication",
                            "edition",
                            "publisher",
                            "author",
                            "owner",
                            "attributions",
                            "collaborators",
                            "creators",
                            "contributors",
                            "voiceCredits",
                            "soundCredits",
                            "imageCredits",
                            "copyright",
                            "license",
                            "language",
                            "words",
                            "text",
                            "forkable",
                            "translatable",
                            "ageGroup",
                            "interactivityLevel",
                            "contentType",
                            "resourceType",
                            "category",
                            "templateType",
                            "genre",
                            "theme",
                            "themes",
                            "rating",
                            "rating_a",
                            "quality",
                            "genieScore",
                            "authoringScore",
                            "popularity",
                            "downloads",
                            "launchUrl",
                            "activity_class",
                            "draftImage",
                            "scaffolding",
                            "feedback",
                            "feedbackType",
                            "teachingMode",
                            "skills",
                            "keywords",
                            "domain",
                            "dialcodes",
                            "optStatus",
                            "description",
                            "instructions",
                            "body",
                            "oldBody",
                            "stageIcons",
                            "editorState",
                            "data",
                            "loadingMessage",
                            "checksum",
                            "learningObjective",
                            "createdBy",
                            "creator",
                            "reviewer",
                            "lastUpdatedBy",
                            "lastSubmittedBy",
                            "lastSubmittedOn",
                            "lastPublishedBy",
                            "lastPublishedOn",
                            "versionDate",
                            "origin",
                            "originData",
                            "versionCreatedBy",
                            "me_totalSessionsCount",
                            "me_creationSessions",
                            "me_creationTimespent",
                            "me_totalTimespent",
                            "me_totalInteractions",
                            "me_averageInteractionsPerMin",
                            "me_averageSessionsPerDevice",
                            "me_totalDevices",
                            "me_averageTimespentPerSession",
                            "me_averageRating",
                            "me_totalDownloads",
                            "me_totalSideloads",
                            "me_totalRatings",
                            "me_totalComments",
                            "me_totalUsage",
                            "me_totalLiveContentUsage",
                            "me_usageLastWeek",
                            "me_deletionsLastWeek",
                            "me_lastUsedOn",
                            "me_lastRemovedOn",
                            "me_hierarchyLevel",
                            "me_totalDialcodeAttached",
                            "me_totalDialcodeLinkedToContent",
                            "me_totalDialcode",
                            "flagReasons",
                            "flaggedBy",
                            "flags",
                            "lastFlaggedOn",
                            "tempData",
                            "copyType",
                            "pragma",
                            "publishChecklist",
                            "publishComment",
                            "rejectReasons",
                            "rejectComment",
                            "totalQuestions",
                            "totalScore",
                            "ownershipType",
                            "reservedDialcodes",
                            "dialcodeRequired",
                            "lockKey",
                            "badgeAssociations",
                            "framework",
                            "lastStatusChangedOn",
                            "uploadError",
                            "appId",
                            "s3Key",
                            "consumerId",
                            "organisation",
                            "nodeType",
                            "prevState",
                            "publishError",
                            "publish_type",
                            "ownedBy",
                            "purpose",
                            "toc_url",
                            "reviewError",
                            "mimeTypesCount",
                            "contentTypesCount",
                            "childNodes",
                            "leafNodesCount",
                            "depth",
                            "SYS_INTERNAL_LAST_UPDATED_ON",
                            "assets",
                            "version",
                            "qrCodeProcessId",
                            "migratedUrl",
                            "totalCompressedSize",
                            "programId",
                            "leafNodes",
                            "editorVersion",
                            "unitIdentifiers",
                            "questionCategories",
                            "certTemplate",
                            "topic",
                            "subDomains",
                            "subjectCodes",
                            "difficultyLevel",
                            "licenseterms",
                            "copyrightYear",
                            "organisationId",
                            "itemSetPreviewUrl",
                            "textbook_name",
                            "level1Name",
                            "level1Concept",
                            "level2Name",
                            "level2Concept",
                            "level3Name",
                            "level3Concept",
                            "sourceURL",
                            "me_totalTimeSpentInSec",
                            "me_totalPlaySessionCount",
                            "me_totalRatingsCount",
                            "monitorable",
                            "userConsent",
                            "trackable",
                            "credentials",
                            "processId",
                            "primaryCategory",
                            "additionalCategories",
                            "prevStatus",
                            "cloudStorageKey",
                            "batches",
                            "year",
                            "plugins",
                            "showNotification",
                            "collectionId",
                            "learningOutcome",
                            "displayScore",
                            "topicsIds",
                            "targetFWIds",
                            "targetTopicIds",
                            "maxAttempts",
                            "se_frameworkIds",
                            "se_topicIds",
                            "targetfoodcropsIds",
                            "targetlivestockmanagementIds",
                            "targetlivestockmanagementIds",
                            "targetcommercialcropsIds",
                            "targetlivestockspeciesIds",
                            "targetanimalwelfareIds",
                            "foodcropsIds",
                            "livestockmanagementIds",
                            "commercialcropsIds",
                            "livestockspeciesIds",
                            "animalwelfareIds",
                            "foodcrops",
                            "livestockmanagement",
                            "commercialcrops",
                            "se_topics",
                            "livestockspecies",
                            "animalwelfare",
                            ""
                        ]
                    }
                }
            ]
        }
    }
```

Steps to add a filter config:

```
formType: 'contentcategory', formAction: 'menubar', contentType: 'global'
```

To add a new filter dropdown "foodcrops" user have to add a new object in below config(searchFilterConfig)

```
 "searchFilterConfig": [
                                {
                                    "category": "foodcrops",
                                    "type": "dropdown",
                                    "placeholderText": "frmelmnts.lbl.selectFoodcrops",
                                    "defaultPlaceholderText": "select foodcrops",
                                    "dataSource": "framework",
                                    "multiple": false
                                },
                                ]
```

Update the new key "foodcrops" in the below config (filters)

```
 "filters": [
                                "board",
                                "gradeLevel",
                                "subject",
                                "medium",
                                "publisher",
                                "audience",
                                "channel",
                                "se_subjects",
                                "creator",
                                "foodcrops"
                            ],
```

Update the new key "foodcrops" in the below config (search>fields) , (search>facets)

```
     "search": {
                            "fields": [
                                "name",
                                "appIcon",
                                "mimeType",
                                "gradeLevel",
                                "identifier",
                                "medium",
                                "pkgVersion",
                                "board",
                                "subject",
                                "resourceType",
                                "primaryCategory",
                                "contentType",
                                "channel",
                                "organisation",
                                "trackable",
                                "foodcrops"
                                
                            ],
                            "facets": [
                                "se_boards",
                                "se_gradeLevels",
                                "se_subjects",
                                "se_mediums",
                                "primaryCategory",
                                "mediaType",
                                "mimeType",
                                "foodcrops"
                                
                            ],
                            "filters": {
                                "primaryCategory": [
                                    "Collection",
                                    "Resource",
                                    "Content Playlist",
                                    "Course",
                                    "Course Assessment",
                                    "Digital Textbook",
                                    "eTextbook",
                                    "Explanation Content",
                                    "Learning Resource",
                                    "Lesson Plan Unit",
                                    "Practice Question Set",
                                    "Teacher Resource",
                                    "Textbook Unit",
                                    "LessonPlan",
                                    "FocusSpot",
                                    "Learning Outcome Definition",
                                    "Curiosity Questions",
                                    "MarkingSchemeRubric",
                                    "ExplanationResource",
                                    "ExperientialResource",
                                    "Practice Resource",
                                    "TVLesson",
                                    "Course Unit",
                                    "Exam Question",
                                    "Question paper"
                                ],
                                "visibility": [
                                    "Default",
                                    "Parent"
                                ]
                            }
                        },
```

Fetch the search response & update the facets data for search filter

Sample Response : api.content.search

```
{
    "id": "api.content.search",
    "ver": "1.0",
    "ts": "2023-10-13T10:22:11.599Z",
    "params": {
        "resmsgid": "5f1e71f0-69b2-11ee-b204-070a60b74f80",
        "msgid": "9dbce44e-5292-4318-871f-88346281485f",
        "status": "successful",
        "err": null,
        "errmsg": null
    },
    "responseCode": "OK",
    "result": {
        "count": 1,
        "content": [
            {
                "trackable": {
                    "enabled": "No",
                    "autoBatch": "No"
                },
                "identifier": "do_11390265103267430411",
                "livestockmanagement": "feedingandnutrition",
                "foodcrops": "grains",
                "channel": "0138934136407244800",
                "organisation": [
                    "agriculture"
                ],
                "livestockspecies": "beefcattle",
                "animalwelfare": "diseases",
                "mimeType": "video/mp4",
                "pkgVersion": 1,
                "objectType": "Content",
                "primaryCategory": "Explanation Content",
                "name": "agriculture Test content",
                "commercialcrops": "crops",
                "contentType": "Resource",
                "resourceType": "Learn",
                "orgDetails": {
                    "orgName": "agriculture"
                }
            }
        ],
        "facets": [
            {
                "values": [
                    {
                        "name": "grains",
                        "count": 1
                    }
                ],
                "name": "foodcrops"
            },
            {
                "values": [
                    {
                        "name": "feedingandnutrition",
                        "count": 1
                    }
                ],
                "name": "livestockmanagement"
            },
            {
                "values": [
                    {
                        "name": "explanation content",
                        "count": 1
                    }
                ],
                "name": "primaryCategory"
            },
            {
                "values": [
                    {
                        "name": "crops",
                        "count": 1
                    }
                ],
                "name": "commercialcrops"
            },
            {
                "values": [
                    {
                        "name": "beefcattle",
                        "count": 1
                    }
                ],
                "name": "livestockspecies"
            },
            {
                "values": [
                    {
                        "name": "diseases",
                        "count": 1
                    }
                ],
                "name": "animalwelfare"
            },
            {
                "values": [
                    {
                        "name": "content",
                        "count": 1
                    }
                ],
                "name": "mediaType"
            },
            {
                "values": [
                    {
                        "name": "video/mp4",
                        "count": 1
                    }
                ],
                "name": "mimeType"
            }
        ]
    }
}
```

To change label, placeholder

Write the generic code logic for facets data instead of hardcorded in code

```
 updateFacetsData(facets) {
    return _.map(facets, facet => {
      switch (_.get(facet, 'name')) {
        case 'foodcrops':
        case 'se_foodcrops':
          facet['index'] = '2';
          facet['label'] = 'foodcrops'
          facet['placeholder'] = 'select foodcrops'
          break;
        case 'commercialcrops':
        case 'se_commercialcrops':
          facet['index'] = '3';
          facet['label'] = 'commercialcrops'
          facet['placeholder'] = 'Select Commercialcrops';
          break;
        case 'livestockmanagement':
        case 'se_livestockmanagement':
          facet['index'] = '4';
          facet['label'] = 'livestockmanagement';
          facet['placeholder'] = 'Selct livestockmanagement ';
          break;
        case 'livestockspecies':
        case 'se_livestockspecies':
          facet['index'] = '5';
          facet['label'] = 'livestockspecies';
          facet['placeholder'] = 'Select livestockspecies';
          break;
        case 'animalwelfare':
            case 'se_animalwelfare':
              facet['index'] = '5';
              facet['label'] = 'animalwelfare';
              facet['placeholder'] = 'Select animalwelfare';
        break;
        case 'publisher':
          facet['index'] = '6';
          facet['label'] = this.resourceService.frmelmnts.lbl.publisher;
          facet['placeholder'] = this.resourceService.frmelmnts.lbl.selectPublisher;
          break;
        case 'primaryCategory':
          facet['index'] = '7';
          facet['label'] = this.resourceService.frmelmnts.lbl.contentType;
          facet['placeholder'] = this.resourceService.frmelmnts.lbl.selectContentType;
          break;
        case 'mimeType':
          facet['index'] = '8';
          facet['name'] = 'mediaType';
          facet['label'] = this.resourceService.frmelmnts.lbl.mediaType;
          facet['mimeTypeList'] = this.mimeTypeList;
          break;
        case 'mediaType':
            facet['index'] = '8';
            facet['label'] = this.resourceService.frmelmnts.lbl.mediaType;
            facet['mimeTypeList'] = this.mimeTypeList;
            break;
        case 'audience':
            facet['index'] = '9';
            facet['label'] =  this.resourceService.frmelmnts.lbl.userType;
            facet['placeholder'] =  this.resourceService.frmelmnts.lbl.selectMeantFor;
            break;
        case 'channel':
          facet['index'] = '1';
          facet['label'] = _.get(this.resourceService, 'frmelmnts.lbl.orgname');
          facet['placeholder'] =  _.get(this.resourceService, 'frmelmnts.lbl.orgname');
          facet['values'] = _.map(facet.values || [], value => ({ ...value, name: value.orgName }));
          break;
          case 'additionalCategories':
            facet['index'] = '71';
            facet['label'] = this.resourceService.frmelmnts.lbl.additionalCategories;
            facet['placeholder'] = this.resourceService.frmelmnts.lbl.selectAdditionalCategory;
            break;
      }
      return facet;
    });
  }
```

Create a generic form config for ““`supportedFilterAttributes`" facets keywords instead of hardcoded BMGS keyword in code.

Search filter screenshot with new framework![](../../../../../../../../.gitbook/assets/3372646439.png)

### Content Cosumption <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-contentcosumption" id="id-ed-portal-design-docsforhardcodedbmgsremoval-contentcosumption"></a>

#### Problem <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-problem.5" id="id-ed-portal-design-docsforhardcodedbmgsremoval-problem.5"></a>

How to change the label with value when a new framework is introduced?

How to handle the label translation

Course Details Screenshot![](../../../../../../../../.gitbook/assets/3372744781.png)

#### Solution <a href="#id-ed-portal-design-docsforhardcodedbmgsremoval-solution.5" id="id-ed-portal-design-docsforhardcodedbmgsremoval-solution.5"></a>

Fetch the content read response details & write generic method to show the course details label with value

api/content/v1/read/do\_11390265103267430411

```
    let response = {
          "id": "api.course.hierarchy",
          "ver": "1.0",
          "ts": "2023-10-11T06:34:48.560Z",
          "params": {
              "resmsgid": "46686700-6800-11ee-af4c-9bc8d99a1601",
              "msgid": "6109bc1b-958d-46ab-b3c6-5a5a4641daec",
              "status": "successful",
              "err": null,
              "errmsg": null
          },
          "responseCode": "OK",
          "result": {
              "content": {
                  "ownershipType": [
                      "createdBy"
                  ],
                  "publish_type": "public",
                  "se_gradeLevelIds": [
                      "ncf_gradelevel_grade1"
                  ],
                  "keywords": [],
                  "targetMediumIds": [
                      "ncf_medium_telugu"
                  ],
                  "channel": "0137541424673095687",
                  "downloadUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113788048780771328112/rajcourse001_1683111611570_do_113788048780771328112_1_SPINE.ecar",
                  "organisation": [],
                  "language": [
                      "English"
                  ],
                  "mimeType": "application/vnd.ekstep.content-collection",
                  "variants": "{\"spine\":{\"ecarUrl\":\"https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113788048780771328112/rajcourse001_1683111611570_do_113788048780771328112_1_SPINE.ecar\",\"size\":\"10458\"},\"online\":{\"ecarUrl\":\"https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113788048780771328112/rajcourse001_1683111612008_do_113788048780771328112_1_ONLINE.ecar\",\"size\":\"5875\"}}",
                  "body": null,
                  "leafNodes": [
                      "do_113762457386450944167",
                      "do_113762457976889344169",
                      "do_113762457691021312168"
                  ],
                  "targetGradeLevelIds": [
                      "ncf_gradelevel_grade1"
                  ],
                  "objectType": "Content",
                  "commercialcrops": [
                      "pastures"
                  ],
                  "appIcon": "",
                  "children": [
                      {
                          "lastStatusChangedOn": "2023-05-03T10:57:58.197+0000",
                          "parent": "do_113788048780771328112",
                          "children": [
                              {
                                  "copyright": "Sunbird Org",
                                  "lastStatusChangedOn": "2023-03-28T07:14:31.184+0000",
                                  "parent": "do_113788049229389824113",
                                  "organisation": [
                                      "Sunbird Org"
                                  ],
                                  "mediaType": "content",
                                  "name": "Content - 3",
                                  "discussionForum": "{\"enabled\":\"No\"}",
                                  "createdOn": "2023-03-28T07:12:26.011+0000",
                                  "createdFor": [
                                      "0137541424673095687"
                                  ],
                                  "channel": "0137541424673095687",
                                  "lastUpdatedOn": "2023-03-28T07:44:20.523+0000",
                                  "subject": [
                                      "Telugu"
                                  ],
                                  "size": 13992641,
                                  "streamingUrl": "https://sunbirdspikemedia-inct.streaming.media.azure.net/cdcfd08e-c2b4-4dc8-9608-bbd66fa10203/mp4_14.ism/manifest(format=m3u8-aapl-v3)",
                                  "identifier": "do_113762457976889344169",
                                  "resourceType": "Learn",
                                  "livestockmanagement": [
                                      "feedingandnutrition",
                                      "geneticsandselection"
                                  ],
                                  "ownershipType": [
                                      "createdBy"
                                  ],
                                  "compatibilityLevel": 1,
                                  "audience": [
                                      "Student"
                                  ],
                                  "foodcrops": [
                                      "Other"
                                  ],
                                  "os": [
                                      "All"
                                  ],
                                  "primaryCategory": "Explanation Content",
                                  "appIcon": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457976889344169/artifact/do_11376182181755289617_1679909890013_logo-test.thumb.png",
                                  "commercialcrops": [
                                      "pastures"
                                  ],
                                  "downloadUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457976889344169/content-3_1679987669566_do_113762457976889344169_1.ecar",
                                  "livestockmanagements": [
                                      "feedingandnutrition"
                                  ],
                                  "lockKey": "110c8e7d-1dbc-4deb-b56c-eee31217f463",
                                  "commercialcropss": [
                                      "pastures"
                                  ],
                                  "framework": "NCF",
                                  "posterImage": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_11376182181755289617/artifact/do_11376182181755289617_1679909890013_logo-test.png",
                                  "creator": "contentCreator Creator",
                                  "versionKey": "1679989460523",
                                  "mimeType": "video/mp4",
                                  "code": "d325130c-2846-4520-a0d3-6c655a7a14c7",
                                  "license": "CC BY 4.0",
                                  "version": 2,
                                  "prevStatus": "Processing",
                                  "contentType": "Resource",
                                  "prevState": "Review",
                                  "language": [
                                      "English"
                                  ],
                                  "foodcrops": "Other",
                                  "lastPublishedOn": "2023-03-28T07:14:29.213+0000",
                                  "objectType": "Content",
                                  "lastUpdatedBy": "155ce3c5-713e-4749-bc1c-95d09c640914",
                                  "status": "Live",
                                  "createdBy": "155ce3c5-713e-4749-bc1c-95d09c640914",
                                  "dialcodeRequired": "No",
                                  "lastSubmittedOn": "2023-03-28T07:12:47.331+0000",
                                  "interceptionPoints": "{}",
                                  "idealScreenSize": "normal",
                                  "contentEncoding": "identity",
                                  "depth": 2,
                                  "lastPublishedBy": "469dc732-04f3-42d9-9a85-30957a797acc",
                                  "livestockspecies": [
                                      "bees"
                                  ],
                                  "osId": "org.ekstep.quiz.app",
                                  "se_FWIds": [
                                      "NCF"
                                  ],
                                  "contentDisposition": "inline",
                                  "previewUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/assets/do_113762457976889344169/mp4_14.mp4",
                                  "artifactUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/assets/do_113762457976889344169/mp4_14.mp4",
                                  "visibility": "Default",
                                  "credentials": "{\"enabled\":\"No\"}",
                                  "variants": "{\"full\":{\"ecarUrl\":\"https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457976889344169/content-3_1679987669566_do_113762457976889344169_1.ecar\",\"size\":\"13809410\"},\"spine\":{\"ecarUrl\":\"https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457976889344169/content-3_1679987670981_do_113762457976889344169_1_SPINE.ecar\",\"size\":\"2039\"}}",
                                  "index": 1,
                                  "pkgVersion": 1,
                                  "idealScreenDensity": "hdpi"
                              },
                              {
                                  "copyright": "Sunbird Org",
                                  "lastStatusChangedOn": "2023-03-28T07:14:10.380+0000",
                                  "parent": "do_113788049229389824113",
                                  "organisation": [
                                      "Sunbird Org"
                                  ],
                                  "mediaType": "content",
                                  "name": "Content -1",
                                  "discussionForum": "{\"enabled\":\"No\"}",
                                  "createdOn": "2023-03-28T07:11:13.936+0000",
                                  "createdFor": [
                                      "0137541424673095687"
                                  ],
                                  "channel": "0137541424673095687",
                                  "lastUpdatedOn": "2023-03-28T07:44:18.230+0000",
                                  "subject": [
                                      "Telugu"
                                  ],
                                  "size": 2523606,
                                  "streamingUrl": "https://sunbirdspikemedia-inct.streaming.media.azure.net/a8e9ea76-cb46-4f65-8901-599e3d5aca90/poem.ism/manifest(format=m3u8-aapl-v3)",
                                  "identifier": "do_113762457386450944167",
                                  "resourceType": "Learn",
                                  "livestockmanagement": [
                                      "geneticsandselection",
                                     
                                  ],
                                  "ownershipType": [
                                      "createdBy"
                                  ],
                                  "compatibilityLevel": 1,
                                  "audience": [
                                      "Student"
                                  ],
                                  "foodcrops": [
                                      "grains"
                                  ],
                                  "os": [
                                      "All"
                                  ],
                                  "primaryCategory": "Explanation Content",
                                  "appIcon": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457386450944167/artifact/do_11376182181755289617_1679909890013_logo-test.thumb.png",
                                  "commercialcrops": [
                                      "crops"
                                  ],
                                  "downloadUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457386450944167/content-1_1679987649315_do_113762457386450944167_1.ecar",
                                  "livestockspecies": [
                                      "bees"
                                  ],
                                  "lockKey": "aaa610be-af98-4607-b665-ed416056107c",
                                  "commercialcropss": [
                                      "pastures"
                                  ],
                                  "framework": "NCF",
                                  "posterImage": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_11376182181755289617/artifact/do_11376182181755289617_1679909890013_logo-test.png",
                                  "creator": "contentCreator Creator",
                                  "versionKey": "1679989458230",
                                  "mimeType": "video/mp4",
                                  "code": "6187c892-3ba2-49e1-a192-15bc328e65eb",
                                  "license": "CC BY 4.0",
                                  "version": 2,
                                  "prevStatus": "Processing",
                                  "contentType": "Resource",
                                  "prevState": "Review",
                                  "language": [
                                      "English"
                                  ],
                                  "foodcropss": "Other",
                                  "lastPublishedOn": "2023-03-28T07:14:09.017+0000",
                                  "objectType": "Content",
                                  "lastUpdatedBy": "155ce3c5-713e-4749-bc1c-95d09c640914",
                                  "status": "Live",
                                  "createdBy": "155ce3c5-713e-4749-bc1c-95d09c640914",
                                  "dialcodeRequired": "No",
                                  "lastSubmittedOn": "2023-03-28T07:11:33.229+0000",
                                  "interceptionPoints": "{}",
                                  "idealScreenSize": "normal",
                                  "contentEncoding": "identity",
                                  "depth": 2,
                                  "lastPublishedBy": "469dc732-04f3-42d9-9a85-30957a797acc",
                                  "livestockmanagements": [
                                      "feedingandnutrition"
                                  ],
                                  "osId": "org.ekstep.quiz.app",
                                  "se_FWIds": [
                                      "NCF"
                                  ],
                                  "contentDisposition": "inline",
                                  "previewUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/assets/do_113762457386450944167/poem.mp4",
                                  "artifactUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/assets/do_113762457386450944167/poem.mp4",
                                  "visibility": "Default",
                                  "credentials": "{\"enabled\":\"No\"}",
                                  "variants": "{\"full\":{\"ecarUrl\":\"https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457386450944167/content-1_1679987649315_do_113762457386450944167_1.ecar\",\"size\":\"2492085\"},\"spine\":{\"ecarUrl\":\"https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457386450944167/content-1_1679987650089_do_113762457386450944167_1_SPINE.ecar\",\"size\":\"2030\"}}",
                                  "index": 2,
                                  "pkgVersion": 1,
                                  "idealScreenDensity": "hdpi"
                              },
                              {
                                  "copyright": "Sunbird Org",
                                  "lastStatusChangedOn": "2023-03-28T07:14:21.098+0000",
                                  "parent": "do_113788049229389824113",
                                  "organisation": [
                                      "Sunbird Org"
                                  ],
                                  "mediaType": "content",
                                  "name": "Content - 2",
                                  "discussionForum": "{\"enabled\":\"No\"}",
                                  "createdOn": "2023-03-28T07:11:51.115+0000",
                                  "createdFor": [
                                      "0137541424673095687"
                                  ],
                                  "channel": "0137541424673095687",
                                  "lastUpdatedOn": "2023-03-28T07:44:16.190+0000",
                                  "category5": "Category5 Term1",
                                  "size": 1055736,
                                  "streamingUrl": "https://sunbirdspikemedia-inct.streaming.media.azure.net/5d2643e3-fcae-42a8-8a22-ac291a317ed4/samplevideo_1280x720_1mb.ism/manifest(format=m3u8-aapl-v3)",
                                  "identifier": "do_113762457691021312168",
                                  "resourceType": "Learn",
                                  "ownershipType": [
                                      "createdBy"
                                  ],
                                  "category2": "Category2 Term1",
                                  "compatibilityLevel": 1,
                                  "audience": [
                                      "Student"
                                  ],
                                  "os": [
                                      "All"
                                  ],
                                  "primaryCategory": "Explanation Content",
                                  "appIcon": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457691021312168/artifact/do_11376182453272576019_1679910221428_287-2876925_test-image-png-unit-testing-png-transparent-png.thumb.png",
                                  "downloadUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457691021312168/content-2_1679987660391_do_113762457691021312168_1.ecar",
                                  "lockKey": "1a558750-41dd-43d3-9d4f-9f12184a902e",
                                  "framework": "framework1",
                                  "posterImage": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_11376182453272576019/artifact/do_11376182453272576019_1679910221428_287-2876925_test-image-png-unit-testing-png-transparent-png.png",
                                  "creator": "contentCreator Creator",
                                  "category1": "Category1 Term1",
                                  "versionKey": "1679989456190",
                                  "mimeType": "video/mp4",
                                  "code": "62ada120-13c4-4e94-aad6-56cebe6a089c",
                                  "license": "CC BY 4.0",
                                  "version": 2,
                                  "prevStatus": "Processing",
                                  "contentType": "Resource",
                                  "prevState": "Review",
                                  "language": [
                                      "English"
                                  ],
                                  "lastPublishedOn": "2023-03-28T07:14:20.009+0000",
                                  "objectType": "Content",
                                  "lastUpdatedBy": "155ce3c5-713e-4749-bc1c-95d09c640914",
                                  "status": "Live",
                                  "createdBy": "155ce3c5-713e-4749-bc1c-95d09c640914",
                                  "dialcodeRequired": "No",
                                  "lastSubmittedOn": "2023-03-28T07:12:10.623+0000",
                                  "interceptionPoints": "{}",
                                  "category3": "Category3 Term1",
                                  "idealScreenSize": "normal",
                                  "contentEncoding": "identity",
                                  "depth": 2,
                                  "lastPublishedBy": "469dc732-04f3-42d9-9a85-30957a797acc",
                                  "osId": "org.ekstep.quiz.app",
                                  "se_FWIds": [
                                      "NCF"
                                  ],
                                  "contentDisposition": "inline",
                                  "previewUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/assets/do_113762457691021312168/samplevideo_1280x720_1mb.mp4",
                                  "artifactUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/assets/do_113762457691021312168/samplevideo_1280x720_1mb.mp4",
                                  "visibility": "Default",
                                  "credentials": "{\"enabled\":\"No\"}",
                                  "variants": "{\"full\":{\"ecarUrl\":\"https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457691021312168/content-2_1679987660391_do_113762457691021312168_1.ecar\",\"size\":\"1058720\"},\"spine\":{\"ecarUrl\":\"https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113762457691021312168/content-2_1679987660892_do_113762457691021312168_1_SPINE.ecar\",\"size\":\"4153\"}}",
                                  "index": 3,
                                  "pkgVersion": 1,
                                  "idealScreenDensity": "hdpi",
                                  "category4": "Category4 Term1"
                              }
                          ],
                          "mediaType": "content",
                          "name": "Course Unit1",
                          "discussionForum": {
                              "enabled": "No"
                          },
                          "createdOn": "2023-05-03T10:57:58.197+0000",
                          "channel": "0137541424673095687",
                          "generateDIALCodes": "No",
                          "lastUpdatedOn": "2023-05-03T10:58:21.192+0000",
                          "identifier": "do_113788049229389824113",
                          "ownershipType": [
                              "createdBy"
                          ],
                          "compatibilityLevel": 1,
                          "audience": [
                              "Student"
                          ],
                          "trackable": {
                              "enabled": "Yes",
                              "autoBatch": "Yes"
                          },
                          "os": [
                              "All"
                          ],
                          "primaryCategory": "Course Unit",
                          "languageCode": [
                              "en"
                          ],
                          "downloadUrl": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113788048780771328112/rajcourse001_1683111611570_do_113788048780771328112_1_SPINE.ecar",
                          "attributions": [],
                          "versionKey": "1683111478197",
                          "mimeType": "application/vnd.ekstep.content-collection",
                          "code": "da5ecc02-9c0d-4030-ab52-65cd3976839f",
                          "license": "CC BY 4.0",
                          "leafNodes": [
                              "do_113762457386450944167",
                              "do_113762457976889344169",
                              "do_113762457691021312168"
                          ],
                          "version": 2,
                          "contentType": "CourseUnit",
                          "language": [
                              "English"
                          ],
                          "lastPublishedOn": "2023-05-03T11:00:11.366+0000",
                          "objectType": "Content",
                          "status": "Live",
                          "dialcodeRequired": "No",
                          "userConsent": "Yes",
                          "idealScreenSize": "normal",
                          "contentEncoding": "gzip",
                          "leafNodesCount": 3,
                          "depth": 1,
                          "osId": "org.ekstep.launcher",
                          "contentDisposition": "inline",
                          "visibility": "Parent",
                          "credentials": {
                              "enabled": "Yes"
                          },
                          "variants": "{\"spine\":{\"ecarUrl\":\"https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113788048780771328112/rajcourse001_1683111611570_do_113788048780771328112_1_SPINE.ecar\",\"size\":\"10458\"},\"online\":{\"ecarUrl\":\"https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113788048780771328112/rajcourse001_1683111612008_do_113788048780771328112_1_ONLINE.ecar\",\"size\":\"5875\"}}",
                          "index": 1,
                          "pkgVersion": 1,
                          "idealScreenDensity": "hdpi"
                      }
                  ],
                  "primaryCategory": "Course",
                  "contentEncoding": "gzip",
                  "lockKey": "f4a04e84-4a4b-4b4b-9e47-159622eefc29",
                  "generateDIALCodes": "No",
                  "totalCompressedSize": 17571983,
                  "mimeTypesCount": "{\"video/mp4\":3,\"application/vnd.ekstep.content-collection\":1}",
                  "sYS_INTERNAL_LAST_UPDATED_ON": "2023-05-03T11:00:11.569+0000",
                  "contentType": "Course",
                  "livestockmanagement": [
                      "feedingandnutrition"
                  ],
                  "trackable": {
                      "enabled": "Yes",
                      "autoBatch": "Yes"
                  },
                  "identifier": "do_113788048780771328112",
                  "audience": [
                      "Student"
                  ],
                  "foodcrops": [
                      "horticulture"
                  ],
                  "toc_url": "https://sunbirddev.blob.core.windows.net/sunbird-content-dev/content/do_113788048780771328112/artifact/do_113788048780771328112_toc.json",
                  "visibility": "Default",
                  "contentTypesCount": "{\"Resource\":3,\"CourseUnit\":1}",
                  "author": "contentCreator Creator",
                  "consumerId": "bfe5883f-ac66-4744-a064-3ed88d986eba",
                  "childNodes": [
                      "do_113762457976889344169",
                      "do_113788049229389824113",
                      "do_113762457386450944167",
                      "do_113762457691021312168"
                  ],
                  "discussionForum": {
                      "enabled": "No"
                  },
                  "mediaType": "content",
                  "osId": "org.ekstep.quiz.app",
                  "lastPublishedBy": "469dc732-04f3-42d9-9a85-30957a797acc",
                  "version": 2,
                  "livestockspecies": [
                      "bees"
                  ],
                  "license": "CC BY 4.0",
                  "size": 10458,
                  "lastPublishedOn": "2023-05-03T11:00:11.366+0000",
                  "name": "RajCourse001",
                  "attributions": [],
                  "targetBoardIds": [
                      "ncf_board_apboard"
                  ],
                  "status": "Live",
                  "code": "org.sunbird.EghlUV",
                  "publishError": null,
                  "credentials": {
                      "enabled": "Yes"
                  },
                  "description": "Enter description for Course",
                  "idealScreenSize": "normal",
                  "createdOn": "2023-05-03T10:57:03.440+0000",
                  "batches": [
                      {
                          "createdFor": [
                              "0137541424673095687"
                          ],
                          "endDate": null,
                          "name": "Test",
                          "batchId": "01379356137943040032",
                          "enrollmentType": "open",
                          "enrollmentEndDate": null,
                          "startDate": "2023-05-11",
                          "status": 1
                      }
                  ],
                  "foodcropss": [
                      "horticulture"
                  ],
                  "commercialcropss": [
                      "crops"
                  ],
                  "livestockmanagements": [
                      "geneticsandselection"
                  ],
                  "copyrightYear": 2023,
                  "contentDisposition": "inline",
                  "lastUpdatedOn": "2023-05-03T10:58:21.192+0000",
                  "dialcodeRequired": "No",
                  "lastStatusChangedOn": "2023-05-03T10:57:03.440+0000",
                  "createdFor": [
                      "0137541424673095687"
                  ],
                  "creator": "contentCreator Creator",
                  "os": [
                      "All"
                  ],
                  "flagReasons": null,
                  "livestockmanagementss": [
                      "geneticsandselection"
                  ],
                  "se_FWIds": [
                      "framework1",
                      "NCF"
                  ],
                  "targetFWIds": [
                      "NCF"
                  ],
                  "pkgVersion": 1,
                  "versionKey": "1683111501192",
                  "idealScreenDensity": "hdpi",
                  "framework": "framework1",
                  "dialcodes": null,
                  "depth": 0,
                  "s3Key": "content/do_113788048780771328112/artifact/do_113788048780771328112_toc.json",
                  "lastSubmittedOn": "2023-05-03T10:58:21.180+0000",
                  "createdBy": "155ce3c5-713e-4749-bc1c-95d09c640914",
                  "compatibilityLevel": 4,
                  "leafNodesCount": 3,
                  "userConsent": "Yes",
                  "resourceType": "Course",
                  "orgDetails": {
                      "email": null,
                      "orgName": "Sunbird Org"
                  },
                  "licenseDetails": {
                      "name": "CC BY 4.0",
                      "url": "https://creativecommons.org/licenses/by/4.0/legalcode",
                      "description": "This is the standard license of any content/youtube"
                  }
              }
          }
      }
```
