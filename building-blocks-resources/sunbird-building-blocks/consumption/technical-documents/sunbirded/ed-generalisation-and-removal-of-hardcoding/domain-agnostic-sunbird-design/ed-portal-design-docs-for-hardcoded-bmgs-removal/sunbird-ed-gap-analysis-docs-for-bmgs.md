---
icon: elementor
---

# Sunbird-ED: Gap Analysis Docs for BMGS

## Introduction : <a href="#sunbird-ed-gapanalysisdocsforbmgs-introduction" id="sunbird-ed-gapanalysisdocsforbmgs-introduction"></a>

This document describes the design approach of BMGS removal in the portal.

* Introduction :
  * Existing workflow:
  * Problem Statement:
    * Any adopter should be able to perform the following:
  * Onboarding Pop up -User Type
    * Solution : Approach
  * Onboarding Pop up -BMGS
    * Solution : Approach
  * Onboarding popup - Location
    * Solution : Approach
  * Landing Page
    * Solution: Approach
  * Search filter (BMGS)
    * Solution:Approach
  * User Profile Update
  * Course Consumption
    * Problem
    * Solution: Approach
  * URL QueryParms
    * Problem
  * How to skip the onboarding steps?

### Existing workflow: <a href="#sunbird-ed-gapanalysisdocsforbmgs-existingworkflow" id="sunbird-ed-gapanalysisdocsforbmgs-existingworkflow"></a>

In accordance with the existing design. If the user wants to use this portal for different organisations. Their preference is for different framework categories instead of BMGS. In order to achieve this, they will need to do code cleanup and modify the BMGS hardcoded with their own framework categories. it's a tedious job to complete this activity.

**Change request:** As part of [ED-2004](https://project-sunbird.atlassian.net/browse/ED-2004) - Getting issue details... STATUS BMGS should be configurable.

### Problem Statement: <a href="#sunbird-ed-gapanalysisdocsforbmgs-problemstatement" id="sunbird-ed-gapanalysisdocsforbmgs-problemstatement"></a>

* Give the flexibility for Sunbird Ed Adopters from **any domain** will be able to install Sunbird Ed & update the required form configuration, and allow the end-to-end creation and consumption of course (+ certificate issuance), textbook and reports.

#### Any adopter should be able to perform the following: <a href="#sunbird-ed-gapanalysisdocsforbmgs-anyadoptershouldbeabletoperformthefollowing" id="sunbird-ed-gapanalysisdocsforbmgs-anyadoptershouldbeabletoperformthefollowing"></a>

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

These are the flow to be considered for BMGS hardcoding

* [‍‍‍Onboarding flow](https://project-sunbird.atlassian.net/wiki/spaces/\~634794ed8bb342276b5158ab/pages/edit-v2/3365666843?draftShareId=0dd5cd59-0aa1-4598-95d1-52b76483e39b\&inEditorTemplatesPanel=auto\_closed#User-Onboarding-flow)
* [landing page (user preference)](https://project-sunbird.atlassian.net/wiki/spaces/\~634794ed8bb342276b5158ab/pages/edit-v2/3365666843?draftShareId=0dd5cd59-0aa1-4598-95d1-52b76483e39b\&inEditorTemplatesPanel=auto\_closed#Onboarding-Pop-up--BMGS)
* [Search filter (BMGS)](https://project-sunbird.atlassian.net/wiki/spaces/\~634794ed8bb342276b5158ab/pages/edit-v2/3365666843?draftShareId=0dd5cd59-0aa1-4598-95d1-52b76483e39b\&inEditorTemplatesPanel=auto\_closed#Search-filter-\(BMGS\))
* [User profile update](https://project-sunbird.atlassian.net/wiki/spaces/\~634794ed8bb342276b5158ab/pages/edit-v2/3365666843?draftShareId=0dd5cd59-0aa1-4598-95d1-52b76483e39b\&inEditorTemplatesPanel=auto\_closed#User-Profile-Update)
* Course consumption
* URL query Parms([https://staging.sunbirded.org/explore/1?id=br\_k-12\&selectedTab=all\&se\_boards=cbse\&se\_mediums=english\&se\_gradeLevels=class 10\&se\_subjects=bengali](https://staging.sunbirded.org/explore/1?id=br\_k-12\&selectedTab=all\&se\_boards=cbse\&se\_mediums=english\&se\_gradeLevels=class%2010\&se\_subjects=bengali)) -
* How to handle the resource service for translation in genric-case?

Flow-Summary

1.  On load of portal **custodianOrgid api** is called

    [https://staging.sunbirded.org/learner/data/v1/system/settings/get/custodianOrgId](https://staging.sunbirded.org/learner/data/v1/system/settings/get/custodianOrgId) in response will get the channel id & onboarding popup will appears with user Type screen.
2. On click of userType selection **channel read** api is called [https://staging.sunbirded.org/api/channel/v1/read/01268904781886259221](https://staging.sunbirded.org/api/channel/v1/read/01268904781886259221) in response will get the list of framework associated with the channel and based on the respones we are showing the BMGS screen dropdown where array is hardcorded as per the BMGS. first dropdown will show the framework list for that channel.
3.  On click of framework dropdown “**framework read api** “is called

    [https://staging.sunbirded.org/api/framework/v1/read/ekstep\_ncert\_k-12](https://staging.sunbirded.org/api/framework/v1/read/ekstep\_ncert\_k-12) in respones will get the list of framework cateogories to be used . based on this response we are constructing the new dropdown value label and placeholder
4. on submit of BMGS data creating a object and storing into localstorage for the further user case in portal.

### Onboarding Pop up -User Type <a href="#sunbird-ed-gapanalysisdocsforbmgs-onboardingpopup-usertype" id="sunbird-ed-gapanalysisdocsforbmgs-onboardingpopup-usertype"></a>

* Will work as per the proposed system with config changes ?
* Will work as per the proposed system with config changes & minor code changes ?
* Hardcoded & major code changes required to work as per the proposed system ?

User have to update the userType form config as per their needs. but UI label will not appears because of the resource service translation is used in portal code. so user have to create a variable in en.properties file to fix this label issue.

UserType ScreenshootCurl

```
curl --location --globoff '{{host}}/api/data/v1/form/read' \
--header 'Content-Type: application/json' \
--header 'Authorization: {{kong_api_key}}' \
--data '{
    "request": {
        "type": "config",
        "action": "get",
        "subType": "userType",
        "component": "portal"
    }
}'
```

#### Solution : [Approach](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3358392350/ED-Portal+-+Design-Docs+for+Hardcoded+BMGS+removal#User-Type%3A) <a href="#sunbird-ed-gapanalysisdocsforbmgs-solution-approach" id="sunbird-ed-gapanalysisdocsforbmgs-solution-approach"></a>

### Onboarding Pop up -BMGS <a href="#sunbird-ed-gapanalysisdocsforbmgs-onboardingpopup-bmgs" id="sunbird-ed-gapanalysisdocsforbmgs-onboardingpopup-bmgs"></a>

* Will work as per the proposed system with config changes ?
* Will work as per the proposed system with config changes & minor code changes ?
* Hardcoded & major code changes required to work as per the proposed system ?

BMGS Screenshoot

In Existing code base the below code are used to display the BMGS popup for non-logged-in & logged-in user. where medium grade and subject are hardcoded in this method **getFormOptionsForCustodianOrgForGuestUser()**

HTML BMGS Hardcoded

```
     <div *ngFor="let field of formFieldOptions">
          <div class="required sb-field-form-group"
            *ngIf="field.code === 'board' && allowedFields.includes(field.code)">
            <div class="sb-field">
                <mat-form-field id={{field.code}} appearance="fill" class="sb-mat__dropdown w-100 mb-8">
                  <mat-label>{{( field?.translation || field?.label) | frameworkCatLabelTranslate | transposeTerms: ( field?.translation || field?.label) : resourceService?.selectedLang}}
                    <span class="mr-8 sb-color-red" *ngIf="field.required"> * </span>
                  </mat-label>
                  <mat-select name={{field.code}} role="listbox" aria-label="field?.label"
                  class="selection" [(ngModel)]="selectedOption[field.code]" (selectionChange)="handleFieldChange($event, field)">
                    <mat-option class="mat-dropdown__options" role="option" *ngFor="let option of field.range | sortBy:'name':'asc'" [value]="option?.name"
                    attr.aria-label="{{option?.name}}">{{option?.name}}</mat-option>
                  </mat-select>
                </mat-form-field>
            </div>
          </div>
```

Method to getFormOptionsForCustodianOrgForGuestUser

```
private getFormOptionsForCustodianOrgForGuestUser() {
    return this.getCustodianOrgDataForGuest().pipe(mergeMap((data) => {
      this.custodianOrgBoard = data;
      const boardObj = _.cloneDeep(this.custodianOrgBoard);
      boardObj.range = _.sortBy(boardObj.range, 'index');
      const board = boardObj;
      this.boardOptions = board;
      if (_.get(this.selectedOption, 'board[0]')) { // update mode, get 1st board framework and update all fields
        this.selectedOption.board = _.get(this.selectedOption, 'board[0]');
        this.frameWorkId = _.get(_.find(this.custOrgFrameworks, { 'name': this.selectedOption.board }), 'identifier');
        return this.getFormatedFilterDetails().pipe(map((formFieldProperties) => {
          this._formFieldProperties = formFieldProperties;
          this.mergeBoard(); // will merge board from custodian org and board from selected framework data
          return this.getUpdatedFilters(board, true);
        }));
      } else {
        let userType = localStorage.getItem('userType');
        userType == "administrator" ? board.required = true  : null;
        const fieldOptions = [board,
          { code: 'medium', label: 'Medium', index: 2 },
          { code: 'gradeLevel', label: 'Class', index: 3 },
          { code: 'subject', label: 'Subject', index: 4 }];
        return of(fieldOptions);
      }
    }));
  }
```

Method to getCustodianOrgDataForGuest

```
  private getCustodianOrgDataForGuest() {
    return this.channelService.getFrameWork(this.guestUserHashTagId).pipe(map((channelData: any) => {
      this.custOrgFrameworks = _.get(channelData, 'result.channel.frameworks') || [];
      this.custOrgFrameworks = _.sortBy(this.custOrgFrameworks, 'index');
      return {
        range: this.custOrgFrameworks,
        label: 'Board',
        code: 'board',
        index: 1
      };
    }));
  }
```

formFieldOptions json object used in BMGS screen to show the dropdown fileds

```
[
    {
        "range": [
            {
                "name": "sunbird_TPD",
                "relation": "hasSequenceMember",
                "identifier": "sunbird_TPD",
                "description": "Sunbird k-12 framework",
                "objectType": "Framework",
                "status": "Live",
                "type": "TPD"
            },
            {
                "name": "NCF",
                "relation": "hasSequenceMember",
                "identifier": "NCF",
                "description": "Sunbird K-12 framework",
                "objectType": "Framework",
                "status": "Live",
                "type": "K-12"
            }
        ],
        "label": "Board",
        "code": "board",
        "index": 1
    },
    {
        "code": "medium",
        "label": "Medium",
        "index": 2
    },
    {
        "code": "gradeLevel",
        "label": "Class",
        "index": 3
    },
    {
        "code": "subject",
        "label": "Subject",
        "index": 4
    }
]
```

**Analysis**

In existing code base if we change the code, label to cateogary1,2,3,4

```
return {
        range: this.custOrgFrameworks,
        label: 'Category1',
        code: 'Category1',
        index: 1
      };
```

```
  const fieldOptions = [board,
          { code: 'Category2', label: 'Category2', index: 2 },
          { code: 'Category3', label: 'Category3', index: 3 },
          { code: 'Category4', label: 'Category4', index: 4 }];
        return of(fieldOptions);
```

popup will appears like this bcz of we are using this below line code. it wont accept the category 1 as a code we need change this allowedFields array value as well

```
   this.allowedFields = ['board', 'medium', 'gradeLevel']; 
```



Post changing the `allowedFields` to `Category..`

```
      this.allowedFields = ['Category1', 'Category2', 'Category3'];
```

BMGS Popup will appears like this

On select of category 1 dropdown value below framwork api is trigreed

Framework API Curl

```
curl 'http://localhost:3000/api/framework/v1/read/NCF' \
  -H 'Accept: application/json' \
  -H 'Accept-Language: en-US,en;q=0.9' \
  -H 'Connection: keep-alive' \
  -H 'Cookie: connect.sid=s%3AQ06CXdV0jGX5WfrsIZzBPufBtoSYwC2l.fNPHPej3gShvf0Zvv8Po32sydBocjvOW99xBYdf%2B2jE' \
  -H 'If-None-Match: W/"478c-vtRM+GJu4Pidoh6H6ouzwSz/Cko"' \
  -H 'Referer: http://localhost:3000/explore?selectedTab=home' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Site: same-origin' \
  -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36' \
  -H 'X-App-Id: local.sunbird.portal' \
  -H 'X-App-Version: 6.0.0' \
  -H 'X-Channel-Id: 0135261634806579203' \
  -H 'X-Device-ID: 74a24ae60c543cff0124871d82786817' \
  -H 'X-Org-code: 0135261634806579203' \
  -H 'X-Request-ID: 315a7500-1198-471c-8b04-12e7475d2d42' \
  -H 'X-Session-ID: a1e6b219-1c89-4316-95fa-97903e463ba9' \
  -H 'X-Source: web' \
  -H 'X-msgid: 315a7500-1198-471c-8b04-12e7475d2d42' \
  -H 'sec-ch-ua: "Chromium";v="116", "Not)A;Brand";v="24", "Google Chrome";v="116"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "macOS"' \
  -H 'ts: 2023-09-28T19:44:17+05:30' \
  --compressed
```

And using the above api response and mapping using below code and setting the medium, grade with in dropdown value

Code to mapped the response with BMGS

```
 mergeMap((frameworkDetails) => {
        if (!frameworkDetails.err) {
          const framework = this.frameWorkId ? this.frameWorkId : 'defaultFramework';
          const frameworkData = _.get(frameworkDetails.frameworkdata, framework);
          this.frameWorkId = frameworkData.identifier;
          this.categoryMasterList = frameworkData.categories;
          return this.getFormDetails();
        } else {
          return throwError(frameworkDetails.err);
        }
```

This Read form service is called when the user select the framework to update the dropdown config for label , translation, index, input type,isrequired field.

```
{
    "request": {
        "type": "user",
        "action": "update",
        "subType": "framework",
        "component": "portal"
    }
}
```

Framewok update form with BMGS config

```
"result": {
        "form": {
            "type": "user",
            "subtype": "framework",
            "action": "update",
            "component": "portal",
            "framework": "*",
            "data": {
                "templateName": "defaultTemplate",
                "action": "update",
                "fields": [
                    {
                        "code": "board",
                        "dataType": "text",
                        "name": "Board",
                        "label": "Board",
                        "description": "Education Board (Like MP Board, NCERT, etc)",
                        "editable": true,
                        "inputType": "multi-select",
                        "required": true,
                        "displayProperty": "Editable",
                        "visible": true,
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "index": 1,
                        "translation": "frmelmnts.lbl.boards"
                    },
                    {
                        "code": "medium",
                        "dataType": "text",
                        "name": "Medium",
                        "label": "Medium",
                        "description": "Medium of instruction",
                        "editable": true,
                        "inputType": "multi-select",
                        "required": true,
                        "displayProperty": "Editable",
                        "visible": true,
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "index": 2,
                        "translation": "frmelmnts.lbl.medium"
                    },
                    {
                        "code": "gradeLevel",
                        "dataType": "text",
                        "name": "Class",
                        "label": "Class",
                        "description": "Grade",
                        "editable": true,
                        "inputType": "multi-select",
                        "required": true,
                        "displayProperty": "Editable",
                        "visible": true,
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "index": 3,
                        "translation": "frmelmnts.lbl.class"
                    },
                    {
                        "code": "subject",
                        "dataType": "text",
                        "name": "Subject",
                        "label": "Subject",
                        "description": "Subject of the Content to use to teach",
                        "editable": true,
                        "inputType": "multi-select",
                        "required": false,
                        "displayProperty": "Editable",
                        "visible": false,
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "index": 4,
                        "translation": "frmelmnts.lbl.subject"
                    }
                ]
            },
            "created_on": "2023-08-18T09:20:14.538Z",
            "last_modified_on": null,
            "rootOrgId": "*"
        }
    }
```

currently its breaking the UI because of framwork cateogary is not matching with the harcoded



To fix the above Issue we have to add this line of code `this.allowedFields` in below method

Code for restrict the framework cateogaries

```
private getFormatedFilterDetails() {
    this.allowedFields = ['board', 'medium', 'gradeLevel'];
    if (this.isGuestUser) {
      this.frameworkService.initialize(this.frameWorkId, this.guestUserHashTagId);
    } else {
      this.frameworkService.initialize(this.frameWorkId);
    }
```

then Board medium will show because of it fetching the data from framework api

To fix this issue we need to create a new framework with proper matching data on **submit** of BMGS it will store the **guestUserDetails in localstorage** for further reference .

Localstorage user data

```
 {
  "name": "guest",
  "formatedName": "Guest",
  "framework": {
    "Category1": [
      "NCF"
    ],
    "medium": [
      "English"
    ],
    "gradeLevel": [
      "Class 1",
      "Class 2"
    ],
    "subject": [],
    "board": [],
    "id": "NCF"
  },
  "role": "teacher"
}
```

Post BMGS submit it will set the userDetails in localstorage then location popup will apperars.

#### Solution : [Approach](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3358392350/ED-Portal+-+Design-Docs+for+Hardcoded+BMGS+removal#Framework-Cateogories\(BMGS\)) <a href="#sunbird-ed-gapanalysisdocsforbmgs-solution-approach.1" id="sunbird-ed-gapanalysisdocsforbmgs-solution-approach.1"></a>

### Onboarding popup - Location <a href="#sunbird-ed-gapanalysisdocsforbmgs-onboardingpopup-location" id="sunbird-ed-gapanalysisdocsforbmgs-onboardingpopup-location"></a>

* Will work as per the proposed system with config changes ?
* Will work as per the proposed system with config changes & minor code changes ?
* Hardcoded & major code changes required to work as per the proposed system ?

State ,District dropdown is not visble when new role is added form config is dependent on userType to show the location fileds.

The below form config is used show the location popup dropdown fields

```
  "request": {
        "type": "profileConfig_v2",
        "action": "get",
        "subType": "default",
        "rootOrgId": "*",
        "component": "*",
```

Location poup screenshoot

#### Solution :[ Approach](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3358392350/ED-Portal+-+Design-Docs+for+Hardcoded+BMGS+removal#Location) <a href="#sunbird-ed-gapanalysisdocsforbmgs-solution-approach.2" id="sunbird-ed-gapanalysisdocsforbmgs-solution-approach.2"></a>

Have to update the below "profileconfig\_v2" form config as per the requirements

```
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
                            "teacher": [
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
                            "student": [
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
                            ],
                            "parent": [
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
                            ]
                        }
                    }
                ]
```

### Landing Page <a href="#sunbird-ed-gapanalysisdocsforbmgs-landingpage" id="sunbird-ed-gapanalysisdocsforbmgs-landingpage"></a>

* Will work as per the proposed system with config changes ?
* Will work as per the proposed system with config changes & minor code changes ?
* Hardcoded & major code changes required to work as per the proposed system ?

On Submit of location popup landing page will apperers BMGS label with value is not showing as per the new framework as we are fetching the user prefence details from the localstorage and displaying in explore page where label (BMGS)is hardcorded in code base.



The below code is responsible to display your preferences data in explore page

```
 setUserPreferences() {
        try {
            if (this.isUserLoggedIn()) {
                this.userPreference = { framework: this.userService.defaultFrameworkFilters };
            } else {
                this.userService.getGuestUser().subscribe((response) => {
                    this.userPreference = response;
                });
            }
        } catch (error) {
            return null;
        }
    }
```

HTML code for User Prefrence

```
 <span class="mr-24">
                    <span *ngIf="userPreference?.framework?.board?.length">{{resourceService?.frmelmnts?.lbl?.boards | transposeTerms: 'frmelmnts.lbl.boards': resourceService?.selectedLang}}:
                    </span>
                    <span *ngIf="userPreference?.framework?.board?.length"
                      class="font-weight-bold">{{convertToString(userPreference?.framework?.board)}}</span>
                  </span>

                  <span class="mr-24">
                    <span *ngIf="userPreference?.framework?.medium?.length">{{resourceService?.frmelmnts?.lbl?.medium | transposeTerms: 'frmelmnts.lbl.medium': resourceService?.selectedLang}}:
                    </span>
                    <span  *ngIf="userPreference?.framework?.medium?.length" class="font-weight-bold">{{userPreference?.framework?.medium[0]}}</span>
                    <span class="font-weight-bold" *ngIf="userPreference?.framework?.medium?.length > 1">
                      ... + {{userPreference?.framework?.medium?.length-1}}
                    </span>
                  </span>

                  <span class="mr-24">
                    <span
                      *ngIf="userPreference?.framework?.gradeLevel?.length">{{resourceService?.frmelmnts?.lbl?.classes | transposeTerms: 'frmelmnts.lbl.classes': resourceService?.selectedLang}}:
                    </span>
                    <span *ngIf="userPreference?.framework?.gradeLevel?.length" class="font-weight-bold">{{userPreference?.framework?.gradeLevel[0]}}</span>
                    <span class="font-weight-bold" *ngIf="userPreference?.framework?.gradeLevel?.length > 1">
                      ... + {{userPreference?.framework?.gradeLevel?.length-1}}
                    </span>
                  </span>
```

#### Solution: [Approach](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3358392350/ED-Portal+-+Design-Docs+for+Hardcoded+BMGS+removal#Landing-Page) <a href="#sunbird-ed-gapanalysisdocsforbmgs-solution-approach.3" id="sunbird-ed-gapanalysisdocsforbmgs-solution-approach.3"></a>

### Search filter (BMGS) <a href="#sunbird-ed-gapanalysisdocsforbmgs-searchfilter-bmgs" id="sunbird-ed-gapanalysisdocsforbmgs-searchfilter-bmgs"></a>

* Will work as per the proposed system with config changes ?
* Will work as per the proposed system with config changes & minor code changes ?
* Hardcoded & major code changes required to work as per the proposed system ?

Filter Event handling and Url Query Parms

In Portal there are two type of search filter i.e page-level search-filter(exclude the All tab) & global-search-filter(used in All tab & groups facets based) .

In multiple places BMGS keyword is hardcoded for event handling and creating a new dropdown object array for facets using search response

Search filter screenshootIn Portal BMGS is hardcorded for categories mapping (content-search-service)

```
  get getCategoriesMapping() {
    return {
      subject: 'se_subjects',
      medium: 'se_mediums',
      gradeLevel: 'se_gradeLevels',
      board: 'se_boards'
    };
  }

  public mapCategories({ filters = {} }) {
    return _.reduce(filters, (acc, value, key) => {
      const mappedValue = _.get(this.getCategoriesMapping, [key]);
      if (mappedValue && key !== 'subject') { acc[mappedValue] = value; delete acc[key]; }
      return acc;
    }, filters);
  }
}
```

Global search filter is not dependent on menubar form config instead using facets of search service

```
  contentSearch(requestParam: SearchParam, addDefaultContentTypesInRequest: boolean = true):
    Observable<ServerResponse> {
    const option = {
      url: this.config.urlConFig.URLS.CONTENT.SEARCH,
      param: { ...requestParam.params },
      data: {
        request: {
          filters: requestParam.filters,
          limit: requestParam.limit,
          query: requestParam.query,
          sort_by: requestParam.sort_by,
          exists: requestParam.exists,
          fields: requestParam.fields,
          softConstraints: requestParam.softConstraints,
          mode: requestParam.mode,
          facets: requestParam.facets && requestParam.facets
        }
      }
    };
    option['data'] = this.updateOption(option);
    if (requestParam['pageNumber'] && requestParam['limit']) {
      option.data.request['offset'] = (requestParam.pageNumber - 1) * requestParam.limit;
    }
    return this.publicDataService.post(option);
  }
  
  // ts code 
  this.facets = this.searchService.updateFacetsData(_.get(data, 'result.facets'));
  this.facetsList = this.searchService.processFilterData(_.get(data, 'result.facets'));
```

Re-modifying the filter json object by using the below code(search-service)

```
  updateFacetsData(facets) {
    return _.map(facets, facet => {
      switch (_.get(facet, 'name')) {
        case 'se_boards':
        case 'board':
          facet['index'] = '2';
          facet['label'] = this.resourceService.frmelmnts.lbl.boards;
          facet['placeholder'] = this.resourceService.frmelmnts.lbl.selectBoard;
          break;
        case 'se_mediums':
        case 'medium':
          facet['index'] = '3';
          facet['label'] = this.resourceService.frmelmnts.lbl.medium;
          facet['placeholder'] = this.resourceService.frmelmnts.lbl.selectMedium;
          break;
        case 'se_gradeLevels':
        case 'gradeLevel':
          facet['index'] = '4';
          facet['label'] = this.resourceService.frmelmnts.lbl.class;
          facet['placeholder'] = this.resourceService.frmelmnts.lbl.selectClass;
          break;
        case 'se_subjects':
        case 'subject':
          facet['index'] = '5';
          facet['label'] = this.resourceService.frmelmnts.lbl.subject;
          facet['placeholder'] = this.resourceService.frmelmnts.lbl.selectSubject;
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

#### Solution:[Approach](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3358392350/ED-Portal+-+Design-Docs+for+Hardcoded+BMGS+removal#Search-filter-\(BMGS\)) <a href="#sunbird-ed-gapanalysisdocsforbmgs-solution-approach.4" id="sunbird-ed-gapanalysisdocsforbmgs-solution-approach.4"></a>

### User Profile Update <a href="#sunbird-ed-gapanalysisdocsforbmgs-userprofileupdate" id="sunbird-ed-gapanalysisdocsforbmgs-userprofileupdate"></a>

* Will work as per the proposed system with config changes ?
* Will work as per the proposed system with config changes & minor code changes ?
* Hardcoded & major code changes required to work as per the proposed system ?

Update API : https://staging.sunbirded.org/learner/user/v3/update

```
{
    "framework": {
        "board": [
            "CBSE"
        ],
        "medium": [
            "English"
        ],
        "gradeLevel": [
            "Class 6"
        ],
        "id": "ekstep_ncert_k-12",
        "subject": []
    }
}
```

Post update profile response data should show as per the new framework cateogories

Profile Response

```
{
    "trackable": {
        "enabled": "No",
        "autoBatch": "No"
    },
    "identifier": "do_213558790575513600110307",
    "subject": [
        "English"
    ],
    "channel": "01345815127107174426",
    "mimeType": "audio/mp3",
    "medium": [
        "English"
    ],
    "pkgVersion": 2,
    "objectType": "Content",
    "gradeLevel": [
        "Class 1"
    ],
    "appIcon": "",
    "primaryCategory": "Explanation Content",
    "name": "exp-mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp3mp",
    "contentType": "ClassroomTeachingVideo",
    "board": "CBSE",
    "orgDetails": {
        "email": null,
        "orgName": "Globe"
    }
}
```

### Course Consumption <a href="#sunbird-ed-gapanalysisdocsforbmgs-courseconsumption" id="sunbird-ed-gapanalysisdocsforbmgs-courseconsumption"></a>

#### Problem <a href="#sunbird-ed-gapanalysisdocsforbmgs-problem" id="sunbird-ed-gapanalysisdocsforbmgs-problem"></a>

* Will work as per the proposed system with config changes ?
* Will work as per the proposed system with config changes & minor code changes ?
* Hardcoded & major code changes required to work as per the proposed system ?

**Configuration Type** : Hardcoded

In course details page the BMGS is used as label

HTML code for Course Details

```
 <div class="training-info" *ngIf="courseHierarchy">
          <h4 class="font-weight-bold">{{generaliseLabelService?.frmelmnts?.lbl?.courseDetails}}</h4>
          <div class="training-relevant mb-16">
            <h6 class="mt-0 mb-8 fsmall training-relevant__heading">
              {{generaliseLabelService?.frmelmnts?.lbl?.courseRelevantFor}}</h6>
              <div class="training-relevant__class mb-4 sb-color-gray-400 fnormal" *ngIf="courseHierarchy?.se_boards">
                <span>{{resourceService?.frmelmnts?.lbl?.board | transposeTerms: 'frmelmnts.lbl.board' : resourceService?.selectedLang}}:&nbsp;</span><span>{{ courseHierarchy?.se_boards?.join(', ')}}</span>
              </div>
              <div class="training-relevant__medium mb-4 sb-color-gray-400 fnormal" *ngIf="courseHierarchy?.se_mediums">
                <span>{{resourceService?.frmelmnts?.lbl?.medium | transposeTerms: 'frmelmnts.lbl.medium' : resourceService?.selectedLang}}:&nbsp;</span><span>{{ courseHierarchy?.se_mediums?.join(', ')}}</span>
              </div>
              <div class="training-relevant__subject mb-4 sb-color-gray-400 fnormal" *ngIf="courseHierarchy?.se_gradeLevels">
                <span>{{resourceService?.frmelmnts?.lbl?.class | transposeTerms: 'frmelmnts.lbl.class' : resourceService?.selectedLang}}:&nbsp;</span><span>{{ courseHierarchy?.se_gradeLevels?.join(', ')}}</span>
              </div>
              <!-- <div class="training-relevant__medium mb-4 sb-color-gray-400 fnormal" *ngIf="courseHierarchy?.se_subjects">
                <span>{{resourceService?.frmelmnts?.lbl?.subject}}:&nbsp;</span><span>{{ courseHierarchy?.se_subjects?.join(', ')}}</span>
              </div> -->
              <div class="training-relevant__medium mb-4 sb-color-gray-400 fnormal" *ngIf="courseHierarchy?.audience">
                <span>{{resourceService?.frmelmnts?.lbl?.userType}}:&nbsp;</span><span>{{ courseHierarchy?.audience?.join(', ')}}</span>
              </div>
            <div *ngIf="courseHierarchy?.description">
              <label class="fsmall mt-16 mb-8">{{resourceService?.frmelmnts?.lbl?.description}}</label>
              <p *ngIf="!readMore" class="traning-relevant__description sb-color-gray-400 fnormal">
                {{ courseHierarchy?.description | slice:0:200 }}&nbsp;
                <span class="ui cardsKnowMore mouse-pointer"
                  *ngIf="courseHierarchy?.description?.length > 200 && readMore === false"
                  tabindex="0" (click)="readMore = !readMore;">{{resourceService?.frmelmnts?.lbl?.readmore}}</span>
              </p>
              <p *ngIf="readMore" class="traning-relevant__description sb-color-gray-400">
                {{ courseHierarchy?.description}}&nbsp;
                <span class="ui cardsKnowMore mouse-pointer"
                  tabindex="0" (click)="readMore = false;">{{resourceService?.frmelmnts?.lbl?.readless}}</span>
              </p>
            </div>
```

On click of course tab serach api is getting called for course

Course Search API CURL

```
curl 'https://staging.sunbirded.org/api/content/v1/search?orgdetails=orgName,email&framework=ap_k-12_1' \
  -H 'Accept: application/json' \
  -H 'Accept-Language: en-US,en;q=0.9' \
  -H 'Connection: keep-alive' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: connect.sid=s%3AjJRj0Ny1dWmDK4OVf9RS0UINsJa2U9JU.5D8KuhMiWL7C1s5okocgsCyxifNLDHapfhA9GYy2y%2BQ' \
  -H 'Origin: https://staging.sunbirded.org' \
  -H 'Referer: https://staging.sunbirded.org/explore?board=State%20(Andhra%20Pradesh)&medium=English&gradeLevel=Class%201&id=ap_k-12_1&selectedTab=course' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Site: same-origin' \
  -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36' \
  -H 'X-App-Id: staging.sunbird.portal' \
  -H 'X-App-Version: 6.0.0' \
  -H 'X-Channel-Id: 01268904781886259221' \
  -H 'X-Device-ID: 39ac67738aa183b686794b7ca0c9fb12' \
  -H 'X-Org-code: 01268904781886259221' \
  -H 'X-Request-ID: c4dca399-601e-46e5-85bc-b297508d65e0' \
  -H 'X-Session-ID: 21a1dffa-4a94-4efe-aaed-1faf748601d6' \
  -H 'X-Source: web' \
  -H 'X-msgid: c4dca399-601e-46e5-85bc-b297508d65e0' \
  -H 'sec-ch-ua: "Chromium";v="116", "Not)A;Brand";v="24", "Google Chrome";v="116"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "macOS"' \
  -H 'ts: 2023-10-04T19:55:02+05:30' \
  --data-raw '{"request":{"filters":{"subject":[],"publisher":[],"audience":[],"channel":[],"status":["Live"],"contentType":["Course"],"primaryCategory":["Course","Course Assessment"],"se_boards":["State (Andhra Pradesh)"],"se_gradeLevels":["Class 1"],"se_mediums":["English"]},"limit":100,"fields":["name","appIcon","mimeType","gradeLevel","identifier","medium","pkgVersion","board","subject","resourceType","contentType","channel","organisation","trackable","se_boards","se_subjects","se_mediums","se_gradeLevels","creator"],"facets":["se_subjects","creator","organisation"]}}' \
  --compressed
```

On click of any course content course/v1/hierarchy/do\_2132529765462425601505?orgdetails APi is used in response BMGS is hardcorded as metadata.



```
se_FWIds: ["tn_k-12_5"] 

se_boardIds: ["tn_k-12_5_board_statetamilnadu"] 

se_boards: ["State (Tamil Nadu)"] 

se_gradeLevelIds: ["tn_k-12_5_gradelevel_class1"] 

se_gradeLevels: ["Class 1"] 

se_mediumIds: ["tn_k-12_5_medium_english"] 

se_mediums: ["English"] 

se_subjectIds: ["tn_k-12_5_subject_accountancy", "tn_k-12_5_subject_english"] 

se_subjects: ["Accountancy"] 
```

CURL - course/v1/hierarchy

```
curl 'https://staging.sunbirded.org/api/course/v1/hierarchy/do_2132529765462425601505?orgdetails=orgName,email&licenseDetails=name,description,url' \
  -H 'Accept: application/json' \
  -H 'Accept-Language: en-US,en;q=0.9' \
  -H 'Connection: keep-alive' \
  -H 'Cookie: connect.sid=s%3AjJRj0Ny1dWmDK4OVf9RS0UINsJa2U9JU.5D8KuhMiWL7C1s5okocgsCyxifNLDHapfhA9GYy2y%2BQ' \
  -H 'Referer: https://staging.sunbirded.org/explore-course/course/do_2132529765462425601505' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Site: same-origin' \
  -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36' \
  -H 'X-App-Id: staging.sunbird.portal' \
  -H 'X-App-Version: 6.0.0' \
  -H 'X-Channel-Id: 01268904781886259221' \
  -H 'X-Device-ID: 39ac67738aa183b686794b7ca0c9fb12' \
  -H 'X-Org-code: 01268904781886259221' \
  -H 'X-Request-ID: 1d7bff91-2403-4aab-8d0c-b26c59cd16f2' \
  -H 'X-Session-ID: 21a1dffa-4a94-4efe-aaed-1faf748601d6' \
  -H 'X-Source: web' \
  -H 'X-msgid: 1d7bff91-2403-4aab-8d0c-b26c59cd16f2' \
  -H 'sec-ch-ua: "Chromium";v="116", "Not)A;Brand";v="24", "Google Chrome";v="116"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "macOS"' \
  -H 'ts: 2023-10-04T20:02:48+05:30' \
  --compressed
```

#### Solution: [Approach](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3358392350/ED-Portal+-+Design-Docs+for+Hardcoded+BMGS+removal#Content-Cosumption) <a href="#sunbird-ed-gapanalysisdocsforbmgs-solution-approach.5" id="sunbird-ed-gapanalysisdocsforbmgs-solution-approach.5"></a>

### URL QueryParms <a href="#sunbird-ed-gapanalysisdocsforbmgs-urlqueryparms" id="sunbird-ed-gapanalysisdocsforbmgs-urlqueryparms"></a>

* Will work as per the proposed system with config changes ?

But its depends on the menubar-config and schemas form service

* Will work as per the proposed system with config changes & minor code changes ?
* Hardcoded & major code changes required to work as per the proposed system ?

#### Problem <a href="#sunbird-ed-gapanalysisdocsforbmgs-problem.1" id="sunbird-ed-gapanalysisdocsforbmgs-problem.1"></a>

**Configuration :**form config dependent on menubar and schemas form service

Query parms

```
private fetchAndFormatQueryParams() {
    return this.activatedRoute.queryParams
      .pipe(
        map(
          queryParams => {
            const queryFilters: Record<string, string[]> = {};
            _.forIn(queryParams, (value, key) => {
              if (this.filterData.includes(key)) {
                queryFilters[key] = _.isArray(value) ? value : [value];
              }
            });
            this.queryFilters = _.cloneDeep(queryFilters);
            return queryFilters;
          }
        )
      );
  }
```

### How to skip the onboarding steps? <a href="#sunbird-ed-gapanalysisdocsforbmgs-howtoskiptheonboardingsteps" id="sunbird-ed-gapanalysisdocsforbmgs-howtoskiptheonboardingsteps"></a>

To skip the onboarding flow have to create a new from config to set the flag as **isOnboardingRequired: false** & need to write a logic inside the app component if false disable the onboarding popup.

Impact: preference will not displayed

