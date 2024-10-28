---
icon: elementor
---

# Custodian User OnBoarding,Menu bar, Banners, profile v2 forms

User Onboarding:

When user Opens the Sunbird Portal, User onboarding will be shown ![](<../../../../.gitbook/assets/0 (2) (1).png>)

Form:

1.First make a read call of the form staging of the payload request

request: {type: "user", action: "update", subType: "framework", rootOrgId: "01397984356699340824",…}

2.Copy the data of step4

3.In place of read give update and And in headers give Authorization key

4.Form which configured for user onboarding with new framework categories

"data": {

"templateName": "defaultTemplate",

"action": "update",

"fields": \[

{

"code": "board",

"dataType": "text",

"name": "Framework",

"label": "Framework",

"description": "Framework",

"editable": **true**,

"inputType": "multi-select",

"required": **true**,

"displayProperty": "Editable",

"visible": **true**,

"renderingHints": {

"semanticColumnWidth": "four"

},

"index": 1,

"translation": "frmelmnts.lbl.frameworkboard"

},

{

"code": "farmingtype",

"dataType": "text",

"name": "Farming Type",

"label": "Farming Type",

"description": "Farming Type",

"editable": **true**,

"inputType": "multi-select",

"required": **true**,

"displayProperty": "Editable",

"visible": **true**,

"renderingHints": {

"semanticColumnWidth": "four"

},

"index": 2,

"translation": "frmelmnts.lbl.Farming Type"

},

{

"code": "cropcategory",

"dataType": "text",

"name": "Crop Category",

"label": "Crop Category",

"description": "Crop Category",

"editable": **true**,

"inputType": "multi-select",

"required": **true**,

"displayProperty": "Editable",

"visible": **true**,

"renderingHints": {

"semanticColumnWidth": "four"

},

"index": 3,

"translation": "frmelmnts.lbl.cropcategory"

},

{

"code": "croptype",

"dataType": "text",

"name": "croptype",

"label": "Crop Type",

"description": "croptype",

"editable": **true**,

"inputType": "multi-select",

"required": **false**,

"displayProperty": "Editable",

"visible": **false**,

"renderingHints": {

"semanticColumnWidth": "four"

},

"index": 4,

"translation": "frmelmnts.lbl.croptype"

},

{

"code": "cropname",

"dataType": "text",

"name": "Crop Name",

"label": "Crop Name",

"description": "Crop Name",

"editable": **true**,

"inputType": "multi-select",

"required": **false**,

"displayProperty": "Editable",

"visible": **false**,

"renderingHints": {

"semanticColumnWidth": "four"

},

"index": 5,

"translation": "frmelmnts.lbl.cropname"

}

]

}

5\. If user want to Switch new framework, based on Framework the categories will be changed and same categories user have to use it in place of code, label, name

**Menubar Form:**

It is for to check the Filters in **Home,** **Digital textbooks,Courses,TV classes,Question Sets**

**All and Mydownloads(for Desktop APP)**

1. Make a read call of the Menubar form form(payload ex: request: {type: "contentcategory", action: "menubar", subType: "global", rootOrgId: "01347076031606784034",…})
2. Import it on postman
3. Copy the data and update

Issues faced on staging( in my downloads of desktop applications added the mimetype on global filter confi,[ED-3424](https://project-sunbird.atlassian.net/browse/ED-3424) , and for TV lessons on index 7 have added the

"filters": {

"primaryCategory": \[

"Explanation Content"

],

"additionalCategories": \[

"TV Lesson"

]

}

"facets": \[

"se\_croptype"

],

[https://project-sunbird.atlassian.net/browse/ED-3494](https://project-sunbird.atlassian.net/browse/ED-3494)

[https://project-sunbird.atlassian.net/browse/ED-3491](https://project-sunbird.atlassian.net/browse/ED-3491)

**Menu form:**

"data": {

"action": "list",

"fields": \[

{

"index": 2,

"search": {

"fields": \[

"name",

"appIcon",

"mimeType",

"cropcategory",

"identifier",

"farmingtype",

"pkgVersion",

"board",

"croptype",

"resourceType",

"primaryCategory",

"contentType",

"channel",

"organisation",

"trackable"

],

"facets": \[

"board",

"cropcategory",

"croptype",

"farmingtype",

"primaryCategory",

"publisher",

"audience"

],

"filters": {

"primaryCategory": \[

"Digital Textbook",

"eTextbook"

]

}

},

"contentType": "mydownloads",

"title": "frmelmnts.lbl.desktop.mylibrary",

"isLoginMandatory": false,

"isEnabled": true,

"anonumousUserRoute": {

"route": "/mydownloads",

"queryParam": "mydownloads"

},

"loggedInUserRoute": {

"route": "/mydownloads",

"queryParam": "mydownloads"

},

"theme": {

"className": "myDownloads",

"baseColor": "",

"textColor": "",

"supportingColor": "",

"imageName": "textbooks-banner-img.svg"

},

"metaData": {

"defaultFilters": {

"farmingtype": \[],

"board": \[

"agriculture\_framework\_20"

],

"cropcategory": \[

"Class 10"

]

},

"cacheTimeout": 86400000,

"groupByKey": "croptype",

"filters": \[

"board",

"cropcategory",

"croptype",

"farmingtype",

"publisher",

"audience",

"channel",

"creator",

"organisation"

],

"searchFilterConfig": \[

{

"category": "board",

"type": "dropdown",

"labelText": "frmelmnts.lbl.Framework",

"defaultLabelText": "Framework",

"placeholderText": "frmelmnts.lbl.selectframework",

"defaultPlaceholderText": "select framework",

"dataSource": "framework",

"multiple": false

},

{

"category": "farmingtype",

"type": "dropdown",

"labelText": "frmelmnts.lbl.farmingtype",

"defaultLabelText": "Farming Type",

"placeholderText": "frmelmnts.lbl.selectfarmingtype",

"defaultPlaceholderText": "select Farming Type",

"dataSource": "framework",

"multiple": true

},

{

"category": "cropcategory",

"type": "dropdown",

"labelText": "frmelmnts.lbl.cropcategory",

"defaultLabelText": "cropcategory",

"placeholderText": "frmelmnts.lbl.selectcropcategory",

"defaultPlaceholderText": "select cropcategory",

"dataSource": "framework",

"multiple": true

},

{

"category": "croptype",

"type": "dropdown",

"labelText": "frmelmnts.lbl.croptype",

"defaultLabelText": "croptypes",

"placeholderText": "frmelmnts.lbl.selectcroptype",

"dataSource": "framework",

"defaultPlaceholderText": "select croptypes",

"multiple": true

},

{

"category": "audience",

"type": "dropdown",

"labelText": "frmelmnts.lbl.publishedUserType",

"defaultLabelText": "audience",

"placeholderText": "Select User Type",

"dataSource": "framework",

"defaultPlaceholderText": "Select User Type",

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

"defaultLabelText": "Orgsssss",

"placeholderText": "Select Organisation",

"dataSource": "facet",

"defaultPlaceholderText": "Select Orgssssss",

"multiple": true

}

]

},

"isOnlineOnly": false,

"menuType": "Content",

"desc": "frmelmnts.lbl.desktop.mylibrary"

},

{

"index": 6,

"search": {

"fields": \[

"name",

"appIcon",

"mimeType",

"cropcategory",

"identifier",

"farmingtype",

"pkgVersion",

"board",

"croptype",

"resourceType",

"contentType",

"channel",

"organisation",

"trackable",

"farmingtype",

"creator"

],

"facets": \[

"creator",

"organisation"

],

"filters": {

"status": \[

"Live"

],

"contentType": \[

"Course"

],

"primaryCategory": \[

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

"farmingtype": \[],

"board": \[

"agriculture\_framework\_20"

],

"cropcategory": \[

"Class 10"

]

},

"cacheTimeout": 86400000,

"groupByKey": "croptype",

"filters": \[

"board",

"cropcategory",

"croptype",

"farmingtype",

"publisher",

"audience",

"channel",

"creator",

"organisation"

],

"searchFilterConfig": \[

{

"category": "board",

"type": "dropdown",

"labelText": "frmelmnts.lbl.Framework",

"defaultLabelText": "Framework",

"placeholderText": "frmelmnts.lbl.selectframework",

"defaultPlaceholderText": "select framework",

"dataSource": "framework",

"multiple": false

},

{

"category": "farmingtype",

"type": "dropdown",

"labelText": "frmelmnts.lbl.farmingtype",

"defaultLabelText": "Farming Type",

"placeholderText": "frmelmnts.lbl.selectfarmingtype",

"defaultPlaceholderText": "select Farming Type",

"dataSource": "framework",

"multiple": true

},

{

"category": "cropcategory",

"type": "dropdown",

"labelText": "frmelmnts.lbl.cropcategory",

"defaultLabelText": "cropcategory",

"placeholderText": "frmelmnts.lbl.selectcropcategory",

"defaultPlaceholderText": "select cropcategory",

"dataSource": "framework",

"multiple": true

},

{

"category": "croptype",

"type": "dropdown",

"labelText": "frmelmnts.lbl.croptype",

"defaultLabelText": "croptypes",

"placeholderText": "frmelmnts.lbl.selectcroptype",

"dataSource": "framework",

"defaultPlaceholderText": "select croptypes",

"multiple": true

},

{

"category": "audience",

"type": "dropdown",

"labelText": "frmelmnts.lbl.publishedUserType",

"defaultLabelText": "audience",

"placeholderText": "Select User Type",

"dataSource": "framework",

"defaultPlaceholderText": "Select User Type",

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

"defaultLabelText": "Orgsssss",

"placeholderText": "Select Organisation",

"dataSource": "facet",

"defaultPlaceholderText": "Select Orgssssss",

"multiple": true

}

]

}

},

{

"index": 3,

"search": {

"fields": \[

"audience",

"name",

"appIcon",

"mimeType",

"cropcategory",

"identifier",

"farmingtype",

"pkgVersion",

"board",

"croptype",

"resourceType",

"primaryCategory",

"contentType",

"channel",

"organisation",

"trackable",

"farmingtype",

"creator"

],

"facets": \[

"board",

"farmingtype",

"audience",

"croptype",

"organisation",

"creator"

],

"filters": {

"primaryCategory": \[

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

"farmingtype": \[],

"board": \[],

"cropcategory": \[]

},

"cacheTimeout": 86400000,

"groupByKey": "croptype",

"filters": \[

"board",

"cropcategory",

"croptype",

"farmingtype",

"publisher",

"audience",

"channel",

"creator",

"organisation"

],

"searchFilterConfig": \[

{

"category": "board",

"type": "dropdown",

"labelText": "frmelmnts.lbl.Framework",

"defaultLabelText": "Framework",

"placeholderText": "frmelmnts.lbl.selectFramework",

"defaultPlaceholderText": "select framework",

"dataSource": "framework",

"multiple": false

},

{

"category": "farmingtype",

"type": "dropdown",

"labelText": "frmelmnts.lbl.farmingtype",

"defaultLabelText": "farmingtype",

"placeholderText": "frmelmnts.lbl.selectfarmingtype",

"defaultPlaceholderText": "select farmingtype",

"dataSource": "framework",

"multiple": true

},

{

"category": "cropcategory",

"type": "dropdown",

"labelText": "frmelmnts.lbl.cropcategory",

"defaultLabelText": "cropcategory",

"placeholderText": "frmelmnts.lbl.selectcropcategory",

"defaultPlaceholderText": "select cropcategory",

"dataSource": "framework",

"multiple": true

},

{

"category": "croptype",

"type": "dropdown",

"labelText": "frmelmnts.lbl.croptype",

"defaultLabelText": "croptype",

"placeholderText": "frmelmnts.lbl.selectcroptype",

"dataSource": "framework",

"defaultPlaceholderText": "select croptype",

"multiple": true

},

{

"category": "audience",

"type": "dropdown",

"labelText": "frmelmnts.lbl.publishedUserType",

"defaultLabelText": "audience",

"placeholderText": "Select User Type",

"dataSource": "framework",

"defaultPlaceholderText": "Select User Type",

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

}

]

}

},

{

"index": 7,

"search": {

"fields": \[

"name",

"appIcon",

"mimeType",

"cropcategory",

"identifier",

"farmingtype",

"pkgVersion",

"board",

"croptype",

"resourceType",

"primaryCategory",

"contentType",

"channel",

"organisation",

"trackable",

"farmingtype",

"se\_boards",

"se\_farmingTypes",

"se\_cropCategorys",

"se\_cropTypes"

],

"facets": \[

"se\_cropTypes"

],

"filters": {

"primaryCategory": \[

"Explanation Content"

],

"additionalCategories": \[

"TV Lesson"

]

}

},

"contentType": "tvProgram",

"title": "frmelmnts.lbl.tvProgram",

"isLoginMandatory": false,

"isEnabled": true,

"anonumousUserRoute": {

"route": "/explore",

"queryParam": "tvProgram"

},

"loggedInUserRoute": {

"route": "/resources",

"queryParam": "tvProgram"

},

"theme": {

"className": "tv",

"baseColor": "",

"textColor": "",

"supportingColor": "",

"imageName": "tv-banner-img.svg"

},

"desc": "frmelmnts.lbl.tvProgram",

"isOnlineOnly": true,

"menuType": "Content",

"metaData": {

"defaultFilters": {

"farmingtype": \[],

"board": \[

"CBSE"

],

"cropcategory": \[

"Class 10"

]

},

"cacheTimeout": 86400000,

"groupByKey": "croptype",

"filters": \[

"board",

"cropcategory",

"croptype",

"farmingtype",

"publisher",

"audience",

"channel"

],

"searchFilterConfig": \[

{

"category": "board",

"type": "dropdown",

"labelText": "frmelmnts.lbl.framework",

"defaultLabelText": "Framework",

"placeholderText": "frmelmnts.lbl.selectframewowrk",

"defaultPlaceholderText": "select framework",

"dataSource": "framework",

"multiple": false

},

{

"category": "farmingtype",

"type": "dropdown",

"labelText": "frmelmnts.lbl.farmingtype",

"defaultLabelText": "farmingtype",

"placeholderText": "frmelmnts.lbl.selectfarmingtype",

"defaultPlaceholderText": "select farmingtype",

"dataSource": "framework",

"multiple": true

},

{

"category": "cropcategory",

"type": "dropdown",

"labelText": "frmelmnts.lbl.cropcategory",

"defaultLabelText": "cropcategory",

"placeholderText": "frmelmnts.lbl.selectcropcategory",

"defaultPlaceholderText": "select cropcategory",

"dataSource": "framework",

"multiple": true

},

{

"category": "croptype",

"type": "dropdown",

"labelText": "frmelmnts.lbl.croptype",

"defaultLabelText": "croptype",

"placeholderText": "frmelmnts.lbl.selectcroptype",

"dataSource": "framework",

"defaultPlaceholderText": "select croptype",

"multiple": true

}

]

}

},

{

"index": 10,

"search": {

"fields": \[

"name",

"appIcon",

"mimeType",

"cropcategory",

"identifier",

"farmingtype",

"pkgVersion",

"board",

"croptype",

"resourceType",

"primaryCategory",

"contentType",

"channel",

"organisation",

"trackable"

],

"facets": \[

"se\_boards",

"se\_farmingTypes",

"se\_cropCategorys",

"se\_cropTypes",

"primaryCategory"

],

"filters": {

"primaryCategory": \[

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

"visibility": \[

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

"globalFilterConfig": \[

{

"index": 1,

"code": "board",

"alternativeCode": "se\_boards",

"label": "Framework",

"placeHolder": "select Framework",

"type": "framework"

},

{

"index": 2,

"code": "farmingtype",

"alternativeCode": "se\_farmingTypes",

"label": "farmingtype",

"placeHolder": "selectfarmingtype",

"type": "framework"

},

{

"index": 3,

"code": "cropcategory",

"alternativeCode": "se\_cropCategorys",

"label": "Crop Category",

"placeHolder": "select cropcategory",

"type": "framework"

},

{

"index": 4,

"code": "croptype",

"alternativeCode": "se\_cropTypes",

"label": "croptype",

"placeHolder": "selectcroptype",

"type": "framework"

},

{

"index": 5,

"code": "primaryCategory",

"alternativeCode": "",

"label": "contentType",

"placeHolder": "selectContentType",

"type": "filter"

},

{

"index": 6,

"code": "additionalCategories",

"alternativeCode": "",

"label": "additionalCategories",

"placeHolder": "selectAdditionalCategories",

"type": "filter"

}

]

}

},

{

"index": 9,

"search": {

"fields": \[

"name",

"appIcon",

"mimeType",

"cropcategory",

"identifier",

"farmingtype",

"pkgVersion",

"board",

"croptype",

"resourceType",

"primaryCategory",

"contentType",

"channel",

"organisation",

"trackable",

"cropcategory"

],

"facets": \[

"croptype"

],

"filters": {

"primaryCategory": \[

"Exam Question Set",

"Practice Set"

]

}

},

"contentType": "questionSets",

"title": "frmelmnts.lbl.questionSets",

"isLoginMandatory": false,

"isEnabled": true,

"anonumousUserRoute": {

"route": "/explore",

"queryParam": "questionSets"

},

"loggedInUserRoute": {

"route": "/resources",

"queryParam": "questionSets"

},

"theme": {

"className": "questionSet",

"baseColor": "",

"textColor": "",

"supportingColor": "",

"imageName": "textbooks-banner-img.svg"

},

"desc": "frmelmnts.lbl.questionSets",

"isOnlineOnly": true,

"menuType": "Content",

"metaData": {

"defaultFilters": {

"farmingtype": \[],

"board": \[],

"cropcategory": \[]

},

"cacheTimeout": 86400000,

"groupByKey": "croptype",

"filters": \[

"board",

"farmingtype",

"channel"

],

"searchFilterConfig": \[

{

"category": "board",

"type": "dropdown",

"labelText": "frmelmnts.lbl.framework",

"defaultLabelText": "Framework",

"placeholderText": "frmelmnts.lbl.selectframework",

"defaultPlaceholderText": "select framework",

"dataSource": "framework",

"multiple": false

},

{

"category": "farmingtype",

"type": "dropdown",

"labelText": "frmelmnts.lbl.farmingtype",

"defaultLabelText": "farmingtype",

"placeholderText": "frmelmnts.lbl.selectfarmingtype",

"defaultPlaceholderText": "select farmingtype",

"dataSource": "framework",

"multiple": true

}

]

}

},

{

"index": 8,

"contentType": "observation",

"anonumousUserRoute": {

"route": "/observation",

"queryParam": "observation"

},

"isLoginMandatory": true,

"isEnabled": true,

"title": "frmelmnts.lbl.observation",

"loggedInUserRoute": {

"route": "/observation",

"queryParam": "observation"

},

"theme": {

"className": "tests",

"baseColor": "",

"textColor": "",

"supportingColor": "",

"imageName": "observation.svg"

},

"isOnlineOnly": true,

"menuType": "Content",

"desc": "frmelmnts.lbl.observation"

},

{

"index": 0,

"search": {

"fields": \[

"name",

"appIcon",

"farmingtype",

"croptype",

"resourceType",

"contentType",

"organisation",

"topic",

"mimeType",

"trackable",

"cropcategory"

],

"facets": \[

"croptype",

"primaryCategory",

"farmingtype",

"banner",

"additionalCategories",

"search",

"ContinueLearning"

],

"filters": {

"farmingtype": \[],

"cropcategory": \[],

"audience": \[],

"board": \[],

"primaryCategory": \[

"Digital Textbook",

"eTextbook",

"Course"

],

"channel": \[],

"croptype": \[]

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

"sections": \[

{

"index": 4,

"apiConfig": {

"url": "",

"req": {

"request": {

"fields": \[

"name",

"appIcon",

"mimeType",

"cropcategory",

"identifier",

"farmingtype",

"pkgVersion",

"board",

"croptype",

"resourceType",

"contentType",

"channel",

"organisation",

"trackable",

"lastPublishedOn"

],

"facets": \[

"croptype"

],

"limit": 100,

"filters": {

"status": \[

"Live"

],

"contentType": \[

"Course"

],

"batches.status": \[

1

],

"cropcategory": \[

"Class 1",

"Class 2",

"Class 5"

],

"batches.enrollmentType": "open",

"farmingtype": \[

"English",

"Tamil"

],

"board": \[

"State (Tamil Nadu)"

],

"primaryCategory": \[

"Course"

]

},

"sort\_by": {

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

"fields": \[

"name",

"appIcon",

"mimeType",

"cropcategory",

"identifier",

"farmingtype",

"pkgVersion",

"board",

"croptype",

"resourceType",

"contentType",

"channel",

"organisation",

"trackable",

"cropcategory",

"lastPublishedOn"

],

"facets": \[

"croptype"

],

"limit": 100,

"filters": {

"status": \[

"Live"

],

"primaryCategory": \[

"Course",

"Digital Textbook"

],

"channel": "01329314824202649627"

},

"sort\_by": {

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

"fields": \[

"name",

"appIcon",

"mimeType",

"cropcategory",

"identifier",

"farmingtype",

"pkgVersion",

"board",

"croptype",

"resourceType",

"primaryCategory",

"contentType",

"channel",

"organisation",

"trackable",

"farmingtype"

],

"facets": \[

"croptype"

],

"limit": 100,

"filters": {

"cropcategory": \[

"Class 4"

],

"audience": \[],

"farmingtype": \[

"English"

],

"board": \[

"State (Tamil Nadu)"

],

"primaryCategory": \[

"Digital Textbook"

],

"channel": \[],

"croptype": \[]

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

"contextKey": "res.facet.croptype",

"method": ""

},

"anonumousUserRoute": {

"route": "/explore-course",

"queryParam": "course"

},

"isEnabled": true,

"title": "frmelmnts.lbl.croptypes",

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

"colorMapping": \[

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

"default": "assets/images/book\_default.svg",

"science": "assets/images/globe.svg",

"english": "assets/images/book\_english.svg",

"mathematics": "assets/images/calculator.svg"

}

},

"facetKey": "croptype",

"desc": "Section for croptypes"

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

"facets": \[

"board",

"cropcategory",

"croptype",

"farmingtype",

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

"additionalCategories": \[

"tv lesson"

],

"primaryCategory": \[

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

"colorMapping": \[

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

"default": "assets/images/all\_content.svg",

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

"contextKey": "res.facet.farmingtype",

"method": ""

},

"anonumousUserRoute": {

"route": "/home",

"queryParam": "course"

},

"isEnabled": false,

"title": "frmelmnts.lbl.farmingtype",

"loggedInUserRoute": {

"route": "/learn",

"queryParam": "course"

},

"theme": {

"component": "sb-pills-grid",

"limit": 10,

"colorMapping": \[

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

"facetKey": "farmingtype",

"desc": "Section for farmingtype"

}

],

"menuType": "Content",

"metaData": {

"defaultFilters": {

"farmingtype": \[],

"board": \[

"CBSE"

],

"cropcategory": \[

"Class 10"

]

},

"groupByKey": "croptype",

"filters": \[

"board",

"cropcategory",

"croptype",

"farmingtype",

"publisher",

"audience",

"channel"

]

}

},

{

"index": 1,

"search": {

"fields": \[

"name",

"appIcon",

"farmingtype",

"croptype",

"resourceType",

"contentType",

"organisation",

"topic",

"mimeType",

"trackable",

"cropcategory"

],

"facets": \[

"primaryCategory",

"board"

],

"filters": {

"farmingtype": \[],

"cropcategory": \[],

"audience": \[],

"board": \[],

"primaryCategory": \[

"Digital Textbook",

"eTextbook"

],

"channel": \[],

"croptype": \[]

}

},

"contentType": "explore",

"title": "frmelmnts.lbl.explore",

"isEnabled": false,

"anonumousUserRoute": {

"route": "/explore",

"queryParam": "explore"

},

"loggedInUserRoute": {

"route": "/resources",

"queryParam": "explore"

},

"filter": {

"isEnabled": false,

"type": "facet"

},

"theme": {

"className": "explore",

"baseColor": "",

"textColor": "",

"supportingColor": "",

"imageName": "courses-banner-img.svg"

},

"desc": "frmelmnts.lbl.explore",

"isOnlineOnly": true,

"sections": \[

{

"index": 0,

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

"title": "frmelmnts.lbl.dscfrmctgries",

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

"colorMapping": \[],

"infiniteCard": false,

"icons": {

"digital textbooks": "assets/images/textbook.svg",

"documents": "assets/images/documents.svg",

"tv classes": "assets/images/tv.svg",

"videos": "assets/images/videos.svg",

"default": "assets/images/all\_content.svg",

"courses": "assets/images/course.svg"

}

},

"facetKey": "primaryCategory",

"data": \[

{

"index": 0,

"name": "Digital Textbook",

"value": "digital textbook",

"searchCriteria": {

"facets": \[],

"primaryCategories": \[

"Digital Textbook"

],

"mode": "soft",

"searchType": "search"

}

},

{

"index": 1,

"name": "Course",

"value": "course",

"searchCriteria": {

"facets": \[],

"primaryCategories": \[

"Course"

],

"mode": "soft",

"searchType": "search"

}

}

],

"desc": "Section for category"

},

{

"index": 0,

"apiConfig": {

"url": "",

"params": "",

"req": {},

"contextKey": "res.facet.croptype",

"method": ""

},

"anonumousUserRoute": {

"route": "/explore-course",

"queryParam": "course"

},

"isEnabled": true,

"title": "frmelmnts.lbl.board",

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

"colorMapping": \[],

"infiniteCard": false,

"icons": {

"state (telangana)": "https://diksha.gov.in/ts/logo.png",

"state (haryana)": "https://diksha.gov.in/hr/logo.png",

"ut (ladakh)": "https://diksha.gov.in/ld/appLogo.png",

"state (kerala)": "https://diksha.gov.in/logo.png",

"state (uttar pradesh)": "https://diksha.gov.in/up/appLogo.png",

"state (andhra pradesh)": "https://diksha.gov.in/ap/logo.png",

"state (nagaland)": "https://diksha.gov.in/nl/logo.png",

"state (tamil nadu)": "https://diksha.gov.in/tn/appLogo.png",

"state (himachal pradesh)": "https://diksha.gov.in/logo.png",

"state (jammu and kashmir)": "https://diksha.gov.in/jk/logo.png",

"state (goa)": "https://diksha.gov.in/ga/logo.png",

"state (punjab)": "https://diksha.gov.in/pb/appLogo.png",

"igot-health": "https://diksha.gov.in/igot/logo.png",

"ut (dnh and dd)": "https://diksha.gov.in/dd/appLogo.png",

"state (jharkhand)": "https://diksha.gov.in/jh/logo.png",

"state (mizoram)": "https://diksha.gov.in/mz/logo.png",

"state (manipur)": "https://diksha.gov.in/mn/appLogo.png",

"state (uttarakhand)": "https://diksha.gov.in/logo.png",

"state (rajasthan)": "https://diksha.gov.in/rj/appLogo.png",

"state (odisha)": "https://diksha.gov.in/od/appLogo.png",

"state (delhi)": "https://diksha.gov.in/dl/logo.png",

"ut (puducherry)": "https://diksha.gov.in/py/appLogo.png",

"state (chandigarh)": "https://diksha.gov.in/logo.png",

"state (meghalya)": "https://diksha.gov.in/ml/logo.png",

"cbse": "https://diksha.gov.in/cbse/cbse-logo.png",

"state (sikkim)": "https://diksha.gov.in/sk/logo.png",

"state (karnataka)": "https://diksha.gov.in/ka/appLogo.png",

"state (gujarat)": "https://diksha.gov.in/gj/logo.png",

"state (madhya pradesh)": "https://diksha.gov.in/mp/logo.png",

"state (arunachal pradesh)": "https://diksha.gov.in/ar/logo.png",

"state (maharashtra)": "https://diksha.gov.in/mh/logo.png",

"state (assam)": "https://diksha.gov.in/as/logo.png",

"state (tripura)": "https://diksha.gov.in/logo.png",

"state (bihar)": "https://diksha.gov.in/br/logo.png",

"ut (andaman and nicobar islands)": "https://diksha.gov.in/an/logo.png",

"state (chhattisgarh)": "https://diksha.gov.in/cg/logo.png"

}

},

"facetKey": "board",

"data": \[

{

"index": 0,

"name": "CBSE/NCERT",

"value": "cbse",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"CBSE"

]

}

},

{

"index": 1,

"name": "IGOT-Health",

"value": "igot-health",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"IGOT-Health"

]

}

},

{

"index": 2,

"name": "State (Arunachal Pradesh)",

"value": "state (arunachal pradesh)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Arunachal Pradesh)"

]

}

},

{

"index": 3,

"name": "State (Andhra Pradesh)",

"value": "state (andhra pradesh)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Andhra Pradesh)"

]

}

},

{

"index": 4,

"name": "State (Assam)",

"value": "state (assam)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Assam)"

]

}

},

{

"index": 5,

"name": "State (Bihar)",

"value": "state (bihar)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Bihar)"

]

}

},

{

"index": 6,

"name": "State (Chandigarh)",

"value": "state (chandigarh)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Chandigarh)"

]

}

},

{

"index": 7,

"name": "State (Chhattisgarh)",

"value": "state (chhattisgarh)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Chhattisgarh)"

]

}

},

{

"index": 8,

"name": "State (Delhi)",

"value": "state (delhi)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Delhi)"

]

}

},

{

"index": 9,

"name": "State (Goa)",

"value": "state (goa)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Goa)"

]

}

},

{

"index": 10,

"name": "State (Gujarat)",

"value": "state (gujarat)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Gujarat)"

]

}

},

{

"index": 11,

"name": "State (Haryana)",

"value": "state (haryana)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Haryana)"

]

}

},

{

"index": 12,

"name": "State (Himachal Pradesh)",

"value": "state (himachal pradesh)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Himachal Pradesh)"

]

}

},

{

"index": 13,

"name": "State (Jammu And Kashmir)",

"value": "state (jammu and kashmir)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Jammu And Kashmir)"

]

}

},

{

"index": 14,

"name": "State (Jharkhand)",

"value": "state (jharkhand)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Jharkhand)"

]

}

},

{

"index": 15,

"name": "State (Karnataka)",

"value": "state (karnataka)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Karnataka)"

]

}

},

{

"index": 16,

"name": "State (Kerala)",

"value": "state (kerala)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Kerala)"

]

}

},

{

"index": 17,

"name": "State (Madhya Pradesh)",

"value": "state (madhya pradesh)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Madhya Pradesh)"

]

}

},

{

"index": 18,

"name": "State (Maharashtra)",

"value": "state (maharashtra)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Maharashtra)"

]

}

},

{

"index": 19,

"name": "State (Manipur)",

"value": "state (manipur)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Manipur)"

]

}

},

{

"index": 20,

"name": "State (Meghalya)",

"value": "state (meghalya)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Meghalya)"

]

}

},

{

"index": 21,

"name": "State (Mizoram)",

"value": "state (mizoram)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Mizoram)"

]

}

},

{

"index": 22,

"name": "State (Nagaland)",

"value": "state (nagaland)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Nagaland)"

]

}

},

{

"index": 23,

"name": "State (Odisha)",

"value": "state (odisha)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Odisha)"

]

}

},

{

"index": 24,

"name": "State (Punjab)",

"value": "state (punjab)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Punjab)"

]

}

},

{

"index": 25,

"name": "State (Rajasthan)",

"value": "state (rajasthan)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Rajasthan)"

]

}

},

{

"index": 26,

"name": "State (Sikkim)",

"value": "state (sikkim)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Sikkim)"

]

}

},

{

"index": 27,

"name": "State (Tamil Nadu)",

"value": "state (tamil nadu)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Tamil Nadu)"

]

}

},

{

"index": 28,

"name": "State (Telangana)",

"value": "state (telangana)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Telangana)"

]

}

},

{

"index": 29,

"name": "State (Tripura)",

"value": "state (tripura)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Tripura)"

]

}

},

{

"index": 30,

"name": "State (Uttar Pradesh)",

"value": "state (uttar pradesh)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Uttar Pradesh)"

]

}

},

{

"index": 31,

"name": "State (Uttarakhand)",

"value": "state (uttarakhand)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"State (Uttarakhand)"

]

}

},

{

"index": 32,

"name": "UT (Andaman and Nicobar Islands)",

"value": "ut (andaman and nicobar islands)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"UT (Andaman and Nicobar Islands)"

]

}

},

{

"index": 33,

"name": "UT (DNH and DD)",

"value": "ut (dnh and dd)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"UT (DNH and DD)"

]

}

},

{

"index": 34,

"name": "UT (Ladakh)",

"value": "ut (ladakh)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"UT (Ladakh)"

]

}

},

{

"index": 35,

"name": "UT (Puducherry)",

"value": "ut (puducherry)",

"searchCriteria": {

"facets": \[

"board"

],

"board": \[

"UT (Puducherry)"

]

}

}

],

"desc": "Section for explore"

},

{

"index": 2,

"apiConfig": {

"url": "",

"params": "",

"req": {},

"contextKey": "res.facet.audience",

"method": ""

},

"anonumousUserRoute": {

"route": "/explore-course",

"queryParam": "course"

},

"isEnabled": true,

"title": "frmelmnts.lbl.audience",

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

"colorMapping": \[],

"infiniteCard": false,

"icons": {

"default": "assets/images/guest-img3.svg",

"administrator": "assets/images/guest-img5.svg",

"teacher": "assets/images/guest-img1.svg",

"parent": "assets/images/guest-img4.svg",

"student": "assets/images/guest-img2.svg"

}

},

"facetKey": "audience",

"data": \[

{

"index": 0,

"name": "School head OR Officials",

"value": "administrator",

"searchCriteria": {

"facets": \[],

"audience": \[

"Administrator"

],

"searchType": "search",

"mode": "soft"

}

},

{

"index": 1,

"name": "Other",

"value": "other",

"searchCriteria": {

"facets": \[],

"audience": \[

"Other"

],

"searchType": "search",

"mode": "soft"

}

},

{

"index": 2,

"name": "Parent/Guardian",

"value": "parent",

"searchCriteria": {

"facets": \[],

"audience": \[

"Parent"

],

"searchType": "search",

"mode": "soft"

}

},

{

"index": 4,

"name": "Teacher",

"value": "teacher",

"searchCriteria": {

"facets": \[],

"audience": \[

"Teacher"

],

"searchType": "search",

"mode": "soft"

}

},

{

"index": 3,

"name": "Student",

"value": "student",

"searchCriteria": {

"facets": \[],

"audience": \[

"Student"

],

"searchType": "search",

"mode": "soft"

}

}

],

"desc": "Section for audience"

}

],

"menuType": "Content",

"metaData": {

"defaultFilters": {

"farmingtype": \[],

"board": \[

"CBSE"

],

"cropcategory": \[

"Class 10"

]

},

"groupByKey": "croptype",

"filters": \[

"board",

"cropcategory",

"croptype",

"farmingtype",

"publisher",

"audience",

"channel"

]

}

}

],

"templateName": "menuConfig"

}

**Custom Resource Bundles Form:**

Make a read call of customresourcebundle

request: {type: "customResourcebundles", action: "list", subType: "global", component: "portal",…}

Update it based on categories of framework

"data": {

"defaultLanguage": "en",

"en": {

"frameworkCategory1": "Framework",

"frameworkCategory2": "Farming Type",

"frameworkCategory3": "Crop Category",

"frameworkCategory4": "Crop Type",

"frameworkCategory5": "Crop Name"

}

}

**Banner configuration for portal:** Configuring banners in home page

**Form:**

"type": "config",

"subType": "segmentation\_v2",

Steps to configure:

1.Launch the sunbird portal go to home page

2.Find the form with below preview

"type": "config",

"action": "get",

"subType": "segmentation\_v2",

"rootOrgId": "01347076031606784034",

"framework": "agriculture\_framework\_20"

3.Copy the curl and import it to postman and read the form

4.copy the “data” field from response and copy it in the request body and update the read word in the API end point and update to “update”

4.Replace the values of "commandId": 1619548201250 which has "targetedClient": "portal" with below values

**"tagFilters": \[**

**"USERFRAMEWORK\_agriculture\_framework\_20",**

**"USERFRAMEWORK\_Plantation Agriculture",**

**"USERFRAMEWORK\_Commercial crop",**

**"USERFRAMEWORK\_agriculture\_framework\_20",**

**"USERFRAMEWORK\_teacher"**

**],**

**System setting for UserProfile:** This system setting allows user to add the newly added framework values into the database.

1.\{{host\}}/api/data/v1/system/settings/set

2.add the new framework category in the request body as below in framework section

{

"request": {

"id": "userProfileConfig",

"field": "userProfileConfig",

"value": "{\\"fields\\":\[\\"firstName\\",\\"lastName\\",\\"profileSummary\\",\\"avatar\\",\\"countryCode\\",\\"dob\\",\\"email\\",\\"gender\\",\\"grade\\",\\"language\\",\\"location\\",\\"phone\\",\\"subject\\",\\"userName\\",\\"webPages\\",\\"jobProfile\\",\\"address\\",\\"education\\",\\"skills\\",\\"badgeAssertions\\"],\\"publicFields\\":\[\\"firstName\\",\\"lastName\\",\\"profileSummary\\",\\"userName\\"],\\"privateFields\\":\[\\"email\\",\\"phone\\"],\\"csv\\":{\\"supportedColumns\\":{\\"NAME\\":\\"firstName\\",\\"MOBILE PHONE\\":\\"phone\\",\\"EMAIL\\":\\"email\\",\\"SCHOOL ID\\":\\"orgId\\",\\"USER\_TYPE\\":\\"userType\\",\\"ROLES\\":\\"roles\\",\\"USER ID\\":\\"userId\\",\\"SCHOOL EXTERNAL ID\\":\\"orgExternalId\\"},\\"outputColumns\\":{\\"userId\\":\\"USER ID\\",\\"firstName\\":\\"NAME\\",\\"phone\\":\\"MOBILE PHONE\\",\\"email\\":\\"EMAIL\\",\\"orgId\\":\\"SCHOOL ID\\",\\"orgName\\":\\"SCHOOL NAME\\",\\"userType\\":\\"USER\_TYPE\\",\\"orgExternalId\\":\\"SCHOOL EXTERNAL ID\\"},\\"outputColumnsOrder\\":\[\\"userId\\",\\"firstName\\",\\"phone\\",\\"email\\",\\"organisationId\\",\\"orgName\\",\\"userType\\",\\"orgExternalId\\"],\\"mandatoryColumns\\":\[\\"firstName\\",\\"userType\\",\\"roles\\"]},\\"read\\":{\\"excludedFields\\":\[\\"avatar\\",\\"jobProfile\\",\\"address\\",\\"education\\",\\"webPages\\",\\"skills\\"]},\\"framework\\":{\\"fields\\":\[\\"board\\",\\"gradeLevel\\",\\"medium\\",\\"subject\\",\\"id\\",\\"category1\\",\\"category2\\",\\"category3\\",\\"category4**\\",\\"commercialcrops\\",\\"foodcrops\\",\\"livestockmanagement\\",\\"livestockspecies\\",\\"farmingtype\\",\\"cropcategory\\",\\"croptype\\",\\"cropname\\"],\\"**mandatoryFields\\":\[\\"id\\"]\}}"

}

}

3.Send the API request

[https://project-sunbird.atlassian.net/browse/ED-3453](https://project-sunbird.atlassian.net/browse/ED-3453)
