---
icon: elementor
---

# \[ED-Portal]: Config Changes as per the BMGS Hardcoded Removal

* Framework Selection Screen Form Configuration for Sunbird ED (BMGS) Reference
* Menu-Bar Form Configuration for Sunbird ED (BMGS) Reference
* CustomResourcebundles Form Configuration for Sunbird ED (BMGS) Reference
* Schemas\_get\_search Form Configuration for Sunbird ED (BMGS) Reference
* Config\_\_get\_\_segmentation\_v2 Form Configuration for Sunbird ED (BMGS) Reference
* Regional Language Label Transaltion
* Skip Onboarding Flow
  * Form Create (onboardingpopupvisibility\_global\_onboarding)\_O
* Reference links

### Framework Selection Screen Form Configuration for Sunbird ED (BMGS) Reference <a href="#id-ed-portal-configchangesasperthebmgshardcodedremoval-frameworkselectionscreenformconfigurationfors" id="id-ed-portal-configchangesasperthebmgshardcodedremoval-frameworkselectionscreenformconfigurationfors"></a>

As per the release-7.0.0, the framework selection screen has been transitioned to a configuration-based approach rather than being hardcoded.

By default, the framework selection screen will dynamically display all the categories retrieved from CSL (framework read API call).

To customize the framework selection screen, users are required to create a form configuration using the Form Create (user\_\_update\_\_framework)\_O. This configuration allows users to implement various customizations such as setting fields as mandatory, modifying labels, and enabling/disabling specific fields according to their requirements.

This user\_\_update\_\_framework form serves as a reference for Sunbird Education (BMGS) system. It facilitates the customization of framework selection features such as board, medium, grade level, and subject.

The form is structured with the following conventions:

* **board** is treated as framework-category1 code,
* **medium** is treated as framework-category2 code,
* **gradeLevel** is treated as framework-category3 code, and
* **subject** is treated as framework-category4 code.

Adopters intending to utilize this form for their infrastructure can follow these guidelines:

* Replace the existing framework-category codes with their own categories, as needed.
* Customize the labels and placeholders according to their specific usage requirements.

Furthermore, adopters have the flexibility to incorporate additional categories beyond the standard four, tailoring the form to suit their unique needs.

Sample :: user\_\_update\_\_framework \{{host\}}/api/data/v1/form/create

```
{
    "request": {
        "type": "user",
        "action": "update",
        "subType": "framework",
        "rootOrgId": "{{adopter_channel}}",
        "framework": "{{adopter_framework}}",
         "data": {
                "templateName": "defaultTemplate",
                "action": "update",
                "fields": [
                    {
                        "code": "board",
                        "visible": true,
                        "editable": true,
                        "displayProperty": "Editable",
                        "dataType": "text",
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "name": "Board",
                        "description": "Education Board (Like MP Board, NCERT, etc)",
                        "index": 1,
                        "inputType": "multi-select",
                        "label": "Board",
                        "required": true
                    },
                    {
                        "code": "medium",
                        "visible": true,
                        "editable": true,
                        "displayProperty": "Editable",
                        "dataType": "text",
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "name": "Medium",
                        "description": "Medium of instruction",
                        "index": 2,
                        "inputType": "multi-select",
                        "label": "Medium",
                        "required": true
                    },
                    {
                        "code": "gradeLevel",
                        "visible": true,
                        "editable": true,
                        "displayProperty": "Editable",
                        "dataType": "text",
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "name": "Class",
                        "description": "Grade",
                        "index": 3,
                        "inputType": "multi-select",
                        "label": "Class",
                        "required": true
                    },
                    {
                        "code": "subject",
                        "visible": true,
                        "editable": true,
                        "displayProperty": "Editable",
                        "dataType": "text",
                        "renderingHints": {
                            "semanticColumnWidth": "four"
                        },
                        "name": "Subject",
                        "description": "Subject of the Content to use to teach",
                        "index": 4,
                        "inputType": "multi-select",
                        "label": "Subject",
                        "required": false
                    }
                ]
            }
    }
}
```

### Menu-Bar Form Configuration for Sunbird ED (BMGS) Reference <a href="#id-ed-portal-configchangesasperthebmgshardcodedremoval-menu-barformconfigurationforsunbirded-bmgs-re" id="id-ed-portal-configchangesasperthebmgshardcodedremoval-menu-barformconfigurationforsunbirded-bmgs-re"></a>

As per release-7.0.0, a significant enhancement has been introduced in the Page-level search-filter & global-filter mechanism. In the event where the user form configuration is unavailable, the system will seamlessly fallback and retrieve configurations from CSL (framework read API call).

The provided menu-bar form configuration serves as a reference for Sunbird Education (BMGS) system. This configuration is tailored to support features such as board selection, medium selection, grade level selection, and subject selection.

It's worth noting that the configuration is structured in a way where:

* **board** is treated as framework-category1 code,
* **medium** is treated as framework-category2 code,
* **gradeLevel** is treated as framework-category3 code, and
* **subject** is treated as framework-category4 code.

Adopters looking to implement this configuration in their infrastructure with different frameworks - categories may need to make certain adjustments. For instance, if an adopter has additional categories beyond the standard four, **they can replace the existing framework-category codes with their own.** Additionally, adopters may introduce new categories based on their specific requirements.

In cases where Sunbird ED utilizes categories like `se_boards`, `se_mediums`, `se_gradeLevel`, and `se_subjects`, adopters should map these to their target framework-category codes accordingly. For instance, `se_boards` can be mapped to the target framework-category1 code, `se_mediums` to framework-category2, `se_gradeLevel` to target framework-category3 code, and `se_subjects` to target framework-category4 code so on.. (e.g., `se_` + frameworkCategory1 + `'s'`).

Ultimately, the number and nature of categories may vary depending on the adopter's specific needs. As per the Sunbird ED system, we currently utilize four main categories: board, medium, gradeLevel, and subject. However, adopters are free to customize and extend these categories as necessary to suit their unique requirements.

Sample :: contentcategory\_global\_menubar \{{host\}}/api/data/v1/form/create

```
{
    "request": {
        "type": "contentcategory",
        "subType": "global",
        "action": "menubar",
        "rootOrgId": "{{adopter_channel}}}",
        "framework": "{{adopter_framework}}",
        "data": {
            "action": "list",
            "fields": [
                {
                    "index": 2,
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
                            "trackable"
                        ],
                        "facets": [
                            "board",
                            "gradeLevel",
                            "subject",
                            "medium",
                            "primaryCategory",
                            "mimeType",
                            "publisher",
                            "audience"
                        ],
                        "filters": {
                            "mimeType": [
                                {
                                    "values": [
                                        "application/vnd.ekstep.ecml-archive",
                                        "application/vnd.sunbird.questionset",
                                        "application/vnd.ekstep.html-archive",
                                        "application/vnd.android.package-archive",
                                        "application/vnd.ekstep.content-archive",
                                        "application/vnd.ekstep.content-collection",
                                        "application/vnd.ekstep.plugin-archive",
                                        "application/vnd.ekstep.h5p-archive",
                                        "application/epub",
                                        "text/x-url",
                                        "video/x-youtube",
                                        "application/octet-stream",
                                        "application/msword",
                                        "application/pdf",
                                        "image/jpeg",
                                        "image/jpg",
                                        "image/png",
                                        "image/tiff",
                                        "image/bmp",
                                        "image/gif",
                                        "image/svg+xml",
                                        "video/avi",
                                        "video/mpeg",
                                        "video/quicktime",
                                        "video/3gpp",
                                        "video/mpeg",
                                        "video/mp4",
                                        "video/ogg",
                                        "video/webm",
                                        "audio/mp3",
                                        "audio/mp4",
                                        "audio/mpeg",
                                        "audio/ogg",
                                        "audio/webm",
                                        "audio/x-wav",
                                        "audio/wav"
                                    ],
                                    "name": "all"
                                },
                                {
                                    "values": [
                                        "video/avi",
                                        "video/mpeg",
                                        "video/quicktime",
                                        "video/3gpp",
                                        "video/mpeg",
                                        "video/mp4",
                                        "video/ogg",
                                        "video/webm"
                                    ],
                                    "name": "video"
                                },
                                {
                                    "values": [
                                        "application/pdf",
                                        "application/epub",
                                        "application/msword"
                                    ],
                                    "name": "documents"
                                },
                                {
                                    "values": [
                                        "application/vnd.ekstep.ecml-archive",
                                        "application/vnd.ekstep.h5p-archive",
                                        "application/vnd.ekstep.html-archive"
                                    ],
                                    "name": "interactive"
                                },
                                {
                                    "values": [
                                        "audio/mp3",
                                        "audio/mp4",
                                        "audio/mpeg",
                                        "audio/ogg",
                                        "audio/webm",
                                        "audio/x-wav",
                                        "audio/wav"
                                    ],
                                    "name": "audio"
                                }
                            ],
                            "primaryCategory": [
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
                    "isOnlineOnly": false,
                    "menuType": "Content",
                    "desc": "frmelmnts.lbl.desktop.mylibrary"
                },
                {
                    "index": 6,
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
                            "contentType",
                            "channel",
                            "organisation",
                            "trackable",
                            "se_boards",
                            "se_subjects",
                            "se_mediums",
                            "se_gradeLevels",
                            "creator"
                        ],
                        "facets": [
                            "se_subjects",
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
                            "medium": [],
                            "board": [
                                "CBSE"
                            ],
                            "gradeLevel": [
                                "Class 10"
                            ]
                        },
                        "cacheTimeout": 86400000,
                        "groupByKey": "subject",
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
                            "organisation"
                        ],
                        "searchFilterConfig": [
                            {
                                "category": "board",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.board",
                                "defaultLabelText": "board",
                                "placeholderText": "frmelmnts.lbl.selectBoard",
                                "defaultPlaceholderText": "select board",
                                "dataSource": "framework",
                                "multiple": false
                            },
                            {
                                "category": "medium",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.medium",
                                "defaultLabelText": "medium",
                                "placeholderText": "frmelmnts.lbl.selectMedium",
                                "defaultPlaceholderText": "select medium",
                                "dataSource": "framework",
                                "multiple": true
                            },
                            {
                                "category": "gradeLevel",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.class",
                                "defaultLabelText": "grade",
                                "placeholderText": "frmelmnts.lbl.selectClass",
                                "defaultPlaceholderText": "select grade",
                                "dataSource": "framework",
                                "multiple": true
                            },
                            {
                                "category": "subject",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.subject",
                                "defaultLabelText": "subjects",
                                "placeholderText": "frmelmnts.lbl.selectSubject",
                                "dataSource": "framework",
                                "defaultPlaceholderText": "select subjects",
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
                        "fields": [
                            "audience",
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
                            "se_boards",
                            "se_subjects",
                            "se_mediums",
                            "se_gradeLevels",
                            "creator"
                        ],
                        "facets": [
                            "audience",
                            "se_subjects",
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
                            "medium": [],
                            "board": [],
                            "gradeLevel": []
                        },
                        "cacheTimeout": 86400000,
                        "groupByKey": "subject",
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
                            "organisation"
                        ],
                        "searchFilterConfig": [
                            {
                                "category": "board",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.board",
                                "defaultLabelText": "board",
                                "placeholderText": "frmelmnts.lbl.selectBoard",
                                "defaultPlaceholderText": "select board",
                                "dataSource": "framework",
                                "multiple": false
                            },
                            {
                                "category": "medium",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.medium",
                                "defaultLabelText": "medium",
                                "placeholderText": "frmelmnts.lbl.selectMedium",
                                "defaultPlaceholderText": "select medium",
                                "dataSource": "framework",
                                "multiple": true
                            },
                            {
                                "category": "gradeLevel",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.class",
                                "defaultLabelText": "grade",
                                "placeholderText": "frmelmnts.lbl.selectClass",
                                "defaultPlaceholderText": "select grade",
                                "dataSource": "framework",
                                "multiple": true
                            },
                            {
                                "category": "subject",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.subject",
                                "defaultLabelText": "subject",
                                "placeholderText": "frmelmnts.lbl.selectSubject",
                                "dataSource": "framework",
                                "defaultPlaceholderText": "select subject",
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
                            "se_boards",
                            "se_subjects",
                            "se_mediums",
                            "se_gradeLevels"
                        ],
                        "facets": [
                            "se_subject"
                        ],
                        "filters": {
                            "primaryCategory": [
                                "Explanation Content"
                            ],
                            "additionalCategories": [
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
                            "medium": [],
                            "board": [
                                "CBSE"
                            ],
                            "gradeLevel": [
                                "Class 10"
                            ]
                        },
                        "cacheTimeout": 86400000,
                        "groupByKey": "subject",
                        "filters": [
                            "board",
                            "gradeLevel",
                            "subject",
                            "medium",
                            "publisher",
                            "audience",
                            "channel",
                            "se_subjects"
                        ],
                        "searchFilterConfig": [
                            {
                                "category": "board",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.board",
                                "defaultLabelText": "board",
                                "placeholderText": "frmelmnts.lbl.selectBoard",
                                "defaultPlaceholderText": "select board",
                                "dataSource": "framework",
                                "multiple": false
                            },
                            {
                                "category": "medium",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.medium",
                                "defaultLabelText": "medium",
                                "placeholderText": "frmelmnts.lbl.selectMedium",
                                "defaultPlaceholderText": "select medium",
                                "dataSource": "framework",
                                "multiple": true
                            },
                            {
                                "category": "gradeLevel",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.class",
                                "defaultLabelText": "grade",
                                "placeholderText": "frmelmnts.lbl.selectClass",
                                "defaultPlaceholderText": "select grade",
                                "dataSource": "framework",
                                "multiple": true
                            },
                            {
                                "category": "subject",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.subject",
                                "defaultLabelText": "subject",
                                "placeholderText": "frmelmnts.lbl.selectSubject",
                                "dataSource": "framework",
                                "defaultPlaceholderText": "select subject",
                                "multiple": true
                            }
                        ]
                    }
                },
                {
                    "index": 10,
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
                            "trackable"
                        ],
                        "facets": [
                            "se_boards",
                            "se_gradeLevels",
                            "se_subjects",
                            "se_mediums",
                            "primaryCategory"
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
                        "globalFilterConfig": [
                            {
                                "index": 1,
                                "code": "board",
                                "alternativeCode": "se_boards",
                                "label": "board",
                                "placeHolder": "selectBoard",
                                "type": "framework"
                            },
                            {
                                "index": 2,
                                "code": "medium",
                                "alternativeCode": "se_mediums",
                                "label": "medium",
                                "placeHolder": "selectMedium",
                                "type": "framework"
                            },
                            {
                                "index": 3,
                                "code": "gradeLevel",
                                "alternativeCode": "se_gradeLevels",
                                "label": "grade",
                                "placeHolder": "selectClass",
                                "type": "framework"
                            },
                            {
                                "index": 4,
                                "code": "subject",
                                "alternativeCode": "se_subjects",
                                "label": "subject",
                                "placeHolder": "selectSubject",
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
                            "se_boards",
                            "se_subjects",
                            "se_mediums",
                            "se_gradeLevels"
                        ],
                        "facets": [
                            "se_subjects"
                        ],
                        "filters": {
                            "primaryCategory": [
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
                            "medium": [],
                            "board": [],
                            "gradeLevel": []
                        },
                        "cacheTimeout": 86400000,
                        "groupByKey": "subject",
                        "filters": [
                            "board",
                            "gradeLevel",
                            "subject",
                            "medium",
                            "channel"
                        ],
                        "searchFilterConfig": [
                            {
                                "category": "board",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.board",
                                "defaultLabelText": "board",
                                "placeholderText": "frmelmnts.lbl.selectBoard",
                                "defaultPlaceholderText": "select board",
                                "dataSource": "framework",
                                "multiple": false
                            },
                            {
                                "category": "medium",
                                "type": "dropdown",
                                "labelText": "frmelmnts.lbl.medium",
                                "defaultLabelText": "medium",
                                "placeholderText": "frmelmnts.lbl.selectMedium",
                                "defaultPlaceholderText": "select medium",
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
                            "gradeLevel",
                            "se_boards",
                            "se_subjects",
                            "se_mediums",
                            "se_gradeLevels"
                        ],
                        "facets": [
                            "subject",
                            "primaryCategory",
                            "medium",
                            "banner",
                            "additionalCategories",
                            "search",
                            "ContinueLearning"
                        ],
                        "filters": {
                            "medium": [],
                            "gradeLevel": [],
                            "audience": [],
                            "board": [],
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
                                            "gradeLevel",
                                            "identifier",
                                            "medium",
                                            "pkgVersion",
                                            "board",
                                            "subject",
                                            "resourceType",
                                            "contentType",
                                            "channel",
                                            "organisation",
                                            "trackable",
                                            "se_boards",
                                            "se_subjects",
                                            "se_mediums",
                                            "se_gradeLevels",
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
                                            "se_gradeLevels": [
                                                "Class 1",
                                                "Class 2",
                                                "Class 5"
                                            ],
                                            "batches.enrollmentType": "open",
                                            "se_mediums": [
                                                "English",
                                                "Tamil"
                                            ],
                                            "se_boards": [
                                                "State (Tamil Nadu)"
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
                                            "gradeLevel",
                                            "identifier",
                                            "medium",
                                            "pkgVersion",
                                            "board",
                                            "subject",
                                            "resourceType",
                                            "contentType",
                                            "channel",
                                            "organisation",
                                            "trackable",
                                            "se_boards",
                                            "se_subjects",
                                            "se_mediums",
                                            "se_gradeLevels",
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
                                            "se_boards",
                                            "se_subjects",
                                            "se_mediums",
                                            "se_gradeLevels"
                                        ],
                                        "facets": [
                                            "se_subjects"
                                        ],
                                        "limit": 100,
                                        "filters": {
                                            "se_gradeLevels": [
                                                "Class 4"
                                            ],
                                            "audience": [],
                                            "se_mediums": [
                                                "English"
                                            ],
                                            "se_boards": [
                                                "State (Tamil Nadu)"
                                            ],
                                            "primaryCategory": [
                                                "Digital Textbook"
                                            ],
                                            "channel": [],
                                            "subject": []
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
                                    "se_boards",
                                    "se_gradeLevels",
                                    "se_subjects",
                                    "se_mediums",
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
                            "medium": [],
                            "board": [
                                "CBSE"
                            ],
                            "gradeLevel": [
                                "Class 10"
                            ]
                        },
                        "groupByKey": "subject",
                        "filters": [
                            "board",
                            "gradeLevel",
                            "subject",
                            "medium",
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
                            "gradeLevel",
                            "se_boards",
                            "se_subjects",
                            "se_mediums",
                            "se_gradeLevels"
                        ],
                        "facets": [
                            "primaryCategory",
                            "se_boards"
                        ],
                        "filters": {
                            "medium": [],
                            "gradeLevel": [],
                            "audience": [],
                            "board": [],
                            "primaryCategory": [
                                "Digital Textbook",
                                "eTextbook"
                            ],
                            "channel": [],
                            "subject": []
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
                    "sections": [
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
                                "colorMapping": [],
                                "infiniteCard": false,
                                "icons": {
                                    "digital textbooks": "assets/images/textbook.svg",
                                    "documents": "assets/images/documents.svg",
                                    "tv classes": "assets/images/tv.svg",
                                    "videos": "assets/images/videos.svg",
                                    "default": "assets/images/all_content.svg",
                                    "courses": "assets/images/course.svg"
                                }
                            },
                            "facetKey": "primaryCategory",
                            "data": [
                                {
                                    "index": 0,
                                    "name": "Digital Textbook",
                                    "value": "digital textbook",
                                    "searchCriteria": {
                                        "facets": [],
                                        "primaryCategories": [
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
                                        "facets": [],
                                        "primaryCategories": [
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
                                "contextKey": "res.facet.subject",
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
                                "colorMapping": [],
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
                            "facetKey": "se_boards",
                            "data": [
                                {
                                    "index": 0,
                                    "name": "CBSE/NCERT",
                                    "value": "cbse",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "CBSE"
                                        ]
                                    }
                                },
                                {
                                    "index": 1,
                                    "name": "IGOT-Health",
                                    "value": "igot-health",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "IGOT-Health"
                                        ]
                                    }
                                },
                                {
                                    "index": 2,
                                    "name": "State (Arunachal Pradesh)",
                                    "value": "state (arunachal pradesh)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Arunachal Pradesh)"
                                        ]
                                    }
                                },
                                {
                                    "index": 3,
                                    "name": "State (Andhra Pradesh)",
                                    "value": "state (andhra pradesh)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Andhra Pradesh)"
                                        ]
                                    }
                                },
                                {
                                    "index": 4,
                                    "name": "State (Assam)",
                                    "value": "state (assam)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Assam)"
                                        ]
                                    }
                                },
                                {
                                    "index": 5,
                                    "name": "State (Bihar)",
                                    "value": "state (bihar)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Bihar)"
                                        ]
                                    }
                                },
                                {
                                    "index": 6,
                                    "name": "State (Chandigarh)",
                                    "value": "state (chandigarh)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Chandigarh)"
                                        ]
                                    }
                                },
                                {
                                    "index": 7,
                                    "name": "State (Chhattisgarh)",
                                    "value": "state (chhattisgarh)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Chhattisgarh)"
                                        ]
                                    }
                                },
                                {
                                    "index": 8,
                                    "name": "State (Delhi)",
                                    "value": "state (delhi)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Delhi)"
                                        ]
                                    }
                                },
                                {
                                    "index": 9,
                                    "name": "State (Goa)",
                                    "value": "state (goa)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Goa)"
                                        ]
                                    }
                                },
                                {
                                    "index": 10,
                                    "name": "State (Gujarat)",
                                    "value": "state (gujarat)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Gujarat)"
                                        ]
                                    }
                                },
                                {
                                    "index": 11,
                                    "name": "State (Haryana)",
                                    "value": "state (haryana)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Haryana)"
                                        ]
                                    }
                                },
                                {
                                    "index": 12,
                                    "name": "State (Himachal Pradesh)",
                                    "value": "state (himachal pradesh)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Himachal Pradesh)"
                                        ]
                                    }
                                },
                                {
                                    "index": 13,
                                    "name": "State (Jammu And Kashmir)",
                                    "value": "state (jammu and kashmir)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Jammu And Kashmir)"
                                        ]
                                    }
                                },
                                {
                                    "index": 14,
                                    "name": "State (Jharkhand)",
                                    "value": "state (jharkhand)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Jharkhand)"
                                        ]
                                    }
                                },
                                {
                                    "index": 15,
                                    "name": "State (Karnataka)",
                                    "value": "state (karnataka)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Karnataka)"
                                        ]
                                    }
                                },
                                {
                                    "index": 16,
                                    "name": "State (Kerala)",
                                    "value": "state (kerala)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Kerala)"
                                        ]
                                    }
                                },
                                {
                                    "index": 17,
                                    "name": "State (Madhya Pradesh)",
                                    "value": "state (madhya pradesh)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Madhya Pradesh)"
                                        ]
                                    }
                                },
                                {
                                    "index": 18,
                                    "name": "State (Maharashtra)",
                                    "value": "state (maharashtra)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Maharashtra)"
                                        ]
                                    }
                                },
                                {
                                    "index": 19,
                                    "name": "State (Manipur)",
                                    "value": "state (manipur)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Manipur)"
                                        ]
                                    }
                                },
                                {
                                    "index": 20,
                                    "name": "State (Meghalya)",
                                    "value": "state (meghalya)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Meghalya)"
                                        ]
                                    }
                                },
                                {
                                    "index": 21,
                                    "name": "State (Mizoram)",
                                    "value": "state (mizoram)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Mizoram)"
                                        ]
                                    }
                                },
                                {
                                    "index": 22,
                                    "name": "State (Nagaland)",
                                    "value": "state (nagaland)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Nagaland)"
                                        ]
                                    }
                                },
                                {
                                    "index": 23,
                                    "name": "State (Odisha)",
                                    "value": "state (odisha)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Odisha)"
                                        ]
                                    }
                                },
                                {
                                    "index": 24,
                                    "name": "State (Punjab)",
                                    "value": "state (punjab)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Punjab)"
                                        ]
                                    }
                                },
                                {
                                    "index": 25,
                                    "name": "State (Rajasthan)",
                                    "value": "state (rajasthan)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Rajasthan)"
                                        ]
                                    }
                                },
                                {
                                    "index": 26,
                                    "name": "State (Sikkim)",
                                    "value": "state (sikkim)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Sikkim)"
                                        ]
                                    }
                                },
                                {
                                    "index": 27,
                                    "name": "State (Tamil Nadu)",
                                    "value": "state (tamil nadu)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Tamil Nadu)"
                                        ]
                                    }
                                },
                                {
                                    "index": 28,
                                    "name": "State (Telangana)",
                                    "value": "state (telangana)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Telangana)"
                                        ]
                                    }
                                },
                                {
                                    "index": 29,
                                    "name": "State (Tripura)",
                                    "value": "state (tripura)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Tripura)"
                                        ]
                                    }
                                },
                                {
                                    "index": 30,
                                    "name": "State (Uttar Pradesh)",
                                    "value": "state (uttar pradesh)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Uttar Pradesh)"
                                        ]
                                    }
                                },
                                {
                                    "index": 31,
                                    "name": "State (Uttarakhand)",
                                    "value": "state (uttarakhand)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "State (Uttarakhand)"
                                        ]
                                    }
                                },
                                {
                                    "index": 32,
                                    "name": "UT (Andaman and Nicobar Islands)",
                                    "value": "ut (andaman and nicobar islands)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "UT (Andaman and Nicobar Islands)"
                                        ]
                                    }
                                },
                                {
                                    "index": 33,
                                    "name": "UT (DNH and DD)",
                                    "value": "ut (dnh and dd)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "UT (DNH and DD)"
                                        ]
                                    }
                                },
                                {
                                    "index": 34,
                                    "name": "UT (Ladakh)",
                                    "value": "ut (ladakh)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
                                            "UT (Ladakh)"
                                        ]
                                    }
                                },
                                {
                                    "index": 35,
                                    "name": "UT (Puducherry)",
                                    "value": "ut (puducherry)",
                                    "searchCriteria": {
                                        "facets": [
                                            "board"
                                        ],
                                        "board": [
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
                                "colorMapping": [],
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
                            "data": [
                                {
                                    "index": 0,
                                    "name": "School head OR Officials",
                                    "value": "administrator",
                                    "searchCriteria": {
                                        "facets": [],
                                        "audience": [
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
                                        "facets": [],
                                        "audience": [
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
                                        "facets": [],
                                        "audience": [
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
                                        "facets": [],
                                        "audience": [
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
                                        "facets": [],
                                        "audience": [
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
                            "medium": [],
                            "board": [
                                "CBSE"
                            ],
                            "gradeLevel": [
                                "Class 10"
                            ]
                        },
                        "groupByKey": "subject",
                        "filters": [
                            "board",
                            "gradeLevel",
                            "subject",
                            "medium",
                            "publisher",
                            "audience",
                            "channel"
                        ]
                    }
                }
            ],
            "templateName": "menuConfig"
        }
    }
}
```

### CustomResourcebundles Form Configuration for Sunbird ED (BMGS) Reference <a href="#id-ed-portal-configchangesasperthebmgshardcodedremoval-customresourcebundlesformconfigurationforsunb" id="id-ed-portal-configchangesasperthebmgshardcodedremoval-customresourcebundlesformconfigurationforsunb"></a>

This form provides users with the ability to update or create mappings for framework category labels at the root level. By configuring this form, users can replace standard labels such as Board, Medium, Class, and Subject with their own category labels, tailored to their specific framework.

Sample Form Create (customResourcebundles\_list\_ global) \{{host\}}/api/data/v1/form/create

```
{
    "request": {
        "type": "customResourcebundles",
        "action": "list",
        "subType": "global",
        "component": "portal",
        "rootOrgId": "{{adopter_channel}}",
        "framework": "{{adopter_framework}}",
         "data": {
                "defaultLanguage": "en",
                "en": {
                frameworkCategory1": "Board",
                "frameworkCategory2": "Medium",
                "frameworkCategory3": "Grade",
                "frameworkCategory4": "Subject"
                }
            }
    }
} 
```

### Schemas\_get\_search Form Configuration for Sunbird ED (BMGS) Reference <a href="#id-ed-portal-configchangesasperthebmgshardcodedremoval-schemas_get_searchformconfigurationforsunbird" id="id-ed-portal-configchangesasperthebmgshardcodedremoval-schemas_get_searchformconfigurationforsunbird"></a>

The schemas\_get\_search form necessitates that adopters substitute occurrences of "board," "medium," "grade," and "subject" with their respective framework category codes.

Furthermore, the **"boardIds"** key should be replaced with a reference to the adopter's framework category code **appended with "Ids**." Similarly, the **"se\_boardIds"** key should be replaced with a reference to **"se\_" concatenated with the adopter's framework category1 code appended with "Ids."** Additionally, the **"se\_board"** key should be replaced with **"se\_" concatenated with the adopter's framework category1 code,**

Sample Form Create (schemas\_get\_search)

```
{
    "request": {
        "type": "schemas",
        "action": "get",
        "subType": "search",
        "rootOrgId": {{adopter_channel}},
        "framework": "{{adopter_framework}}",
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
                                "subject",
                                "medium",
                                "gradeLevel",
                                "topic",
                                "subDomains",
                                "subjectCodes",
                                "difficultyLevel",
                                "board",
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
                                "boardIds",
                                "gradeLevelIds",
                                "subjectIds",
                                "mediumIds",
                                "topicsIds",
                                "targetFWIds",
                                "targetBoardIds",
                                "targetGradeLevelIds",
                                "targetSubjectIds",
                                "targetMediumIds",
                                "targetTopicIds",
                                "maxAttempts",
                                "se_frameworkIds",
                                "se_boardIds",
                                "se_subjectIds",
                                "se_mediumIds",
                                "se_topicIds",
                                "se_gradeLevelIds",
                                "se_boards",
                                "se_subjects",
                                "se_mediums",
                                "se_topics",
                                "se_gradeLevels"
                            ]
                        }
                    }
                ]
            }
    }
}
```

### Config\_\_get\_\_segmentation\_v2 Form Configuration for Sunbird ED (BMGS) Reference  <a href="#id-ed-portal-configchangesasperthebmgshardcodedremoval-config__get__segmentation_v2formconfiguration" id="id-ed-portal-configchangesasperthebmgshardcodedremoval-config__get__segmentation_v2formconfiguration"></a>

Update **tagFilters** values of "**commandId": 1619548201250** which has "**targetedClient": "portal"**

The "tagFilters" array contains values such as "USERFRAMEWORK\_State (Tamil Nadu)", "USERFRAMEWORK\_English", and "USERFRAMEWORK\_Class 1" in shared form reference

When displayed on the homepage, the keyword "State (Tamil Nadu)" will be dynamically replaced by values from the adopter's framework categories, such as "**frameworkcategory1value**", "**frameworkcategory2value**", "**frameworkcategory3value**", and so on.

This replacement is based on the configured tagFilters, ultimately determining which banners are displayed on the homepage.

Sample Form Create (config\_get\_segmentation\_v2) \{{host\}}/api/data/v1/form/create

```
{
    "request": {
        "type": "config",
        "action": "get",
        "subType": "segmentation_v2",
        "rootOrgId": {{adopter_channel}},
        "framework": "{{adopter_framework}}",
        "component": "portal",
        "data": {
            "templateName": "segmentation_v2",
            "action": "get",
            "fields": [
                {
                    "commandId": 1619548200000,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "LOCAL_NOTIF",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "USERLANG_en"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": [
                        {
                            "code": "localNotification",
                            "name": "LocalNotification",
                            "type": 1,
                            "config": [
                                {
                                    "msg": "Welcome! You've choosen English",
                                    "isEnabled": true,
                                    "id": 1005,
                                    "title": "Welcome! You've choosen English"
                                }
                            ]
                        }
                    ]
                },
                {
                    "commandId": 1619548200290,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "LOCAL_NOTIF",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "USERLANG_kn"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": [
                        {
                            "code": "localNotification",
                            "name": "LocalNotification",
                            "type": 1,
                            "config": [
                                {
                                    "msg": "ಕನ್ನಡ ಆಯ್ಕೆ ಮಾಡಿದ್ದಕ್ಕೆ ಧನ್ಯವಾದಗಳು",
                                    "isEnabled": true,
                                    "id": 1006,
                                    "title": "ಕನ್ನಡ ಆಯ್ಕೆ ಮಾಡಿದ್ದಕ್ಕೆ ಧನ್ಯವಾದಗಳು"
                                }
                            ]
                        }
                    ]
                },
                {
                    "commandId": 1619548200020,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "LOCAL_NOTIF",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "USERFRAMEWORK_stateandhrapradesh",
                        "USERFRAMEWORK_class10",
                        "USERFRAMEWORK_english"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": [
                        {
                            "code": "localNotification",
                            "name": "LocalNotification",
                            "type": 1,
                            "config": [
                                {
                                    "msg": "Board AP Class 10 English",
                                    "isEnabled": true,
                                    "id": 1004,
                                    "title": "Board AP Class 10 English",
                                    "action": "ACTION_PLAY",
                                    "data": {
                                        "request": {
                                            "objectId": "do_31269113788995174417318",
                                            "collection": "do_31269113788995174417318"
                                        }
                                    }
                                }
                            ]
                        }
                    ]
                },
                {
                    "commandId": 1619548204000,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "LOCAL_NOTIF",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "CONTENT_do_2130251541941534721178"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": [
                        {
                            "code": "localNotification",
                            "name": "LocalNotification",
                            "type": 1,
                            "config": [
                                {
                                    "msg": "Content: State Course",
                                    "isEnabled": true,
                                    "id": 1003,
                                    "title": "Content: State Course",
                                    "action": "ACTION_PLAY",
                                    "data": {
                                        "request": {
                                            "objectId": "do_2130251541941534721178",
                                            "collection": "do_2130251541941534721178"
                                        }
                                    }
                                }
                            ]
                        }
                    ]
                },
                {
                    "commandId": 1619548200600,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "LOCAL_NOTIF",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "USERFRAMEWORK_stateandhrapradesh",
                        "USERFRAMEWORK_class8",
                        "USERFRAMEWORK_english"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": [
                        {
                            "code": "localNotification",
                            "name": "LocalNotification",
                            "type": 1,
                            "config": [
                                {
                                    "msg": "Board AP class 8 english",
                                    "isEnabled": true,
                                    "id": 1002,
                                    "title": "Board AP class 8 english"
                                }
                            ]
                        }
                    ]
                },
                {
                    "commandId": 1619548200050,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "LOCAL_NOTIF",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "USERLOCATION_Tamil Nadu"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": [
                        {
                            "code": "localNotification",
                            "name": "LocalNotification",
                            "type": 1,
                            "config": [
                                {
                                    "msg": "Location Tamil Nadu",
                                    "isEnabled": true,
                                    "id": 1001,
                                    "title": "Location Tamil Nadu"
                                }
                            ]
                        }
                    ]
                },
                {
                    "commandId": 1619548201250,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "BANNER_CONFIG",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "USERFRAMEWORK_statetamilnadu",
                        "USERFRAMEWORK_english",
                        "USERFRAMEWORK_class1"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": {
                        "showBanner": true,
                        "values": [
                            {
                                "code": "banner_external_url",
                                "ui": {
                                    "background": "https://cdn.pixabay.com/photo/2015/10/29/14/38/web-1012467_960_720.jpg",
                                    "text": "Sample External Url"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "externalUrl",
                                    "params": {
                                        "route": "https://diksha.gov.in/"
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_internal_url",
                                "ui": {
                                    "background": "https://cdn.pixabay.com/photo/2015/10/29/14/38/web-1012467_960_720.jpg",
                                    "text": "Sample Internal Url"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "internalUrl",
                                    "params": {
                                        "route": "profile"
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "ui": {
                                    "background": "https://cdn.pixabay.com/photo/2015/10/29/14/38/web-1012467_960_720.jpg",
                                    "text": "Sample Search"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_content",
                                "ui": {
                                    "background": "https://ae01.alicdn.com/kf/H9e3986d0c2434909a0cc26654e766dad7/Custom-fullcolor-Vinyl-Flex-Banner-3-X-4-FT-Outdoor-Advertise-Signs-2-X6-FT-Can.jpg_Q90.jpg_.webp",
                                    "text": "Sample content"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "content",
                                    "params": {
                                        "identifier": "do_21302358976737280014"
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "",
                                "type": "secondary",
                                "ui": {
                                    "text": "NISHTHA FLN COurses",
                                    "icon": "assets/imgs/ic_nishtha_courses.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "",
                                    "params": {
                                        "route": ""
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "",
                                "type": "secondary",
                                "ui": {
                                    "text": "NISHTHA FLN COurses",
                                    "icon": "assets/imgs/ic_nishtha_courses.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "",
                                    "params": {
                                        "route": ""
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "",
                                "type": "secondary",
                                "ui": {
                                    "text": "NISHTA  Secondary Courses",
                                    "icon": "assets/imgs/ic_secondary_course.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "",
                                    "params": {
                                        "route": ""
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "",
                                "type": "secondary",
                                "ui": {
                                    "text": "Revision Preperation",
                                    "icon": "assets/imgs/ic_revision_preperation.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "",
                                    "params": {
                                        "route": ""
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "",
                                "type": "secondary",
                                "ui": {
                                    "text": "FLN Programme",
                                    "icon": "assets/imgs/ic_fln_programme.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "",
                                    "params": {
                                        "route": ""
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "",
                                "type": "secondary",
                                "ui": {
                                    "text": "Administration  Programme",
                                    "icon": "assets/imgs/ic_administration_programme.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "",
                                    "params": {
                                        "route": ""
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "",
                                "type": "secondary",
                                "ui": {
                                    "text": "Quiz",
                                    "icon": "assets/imgs/ic_quiz.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "",
                                    "params": {
                                        "route": ""
                                    }
                                },
                                "expiry": "1841807258"
                            }
                        ]
                    }
                },
                {
                    "commandId": 1619548208500,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "BANNER_CONFIG",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "USERFRAMEWORK_cbse",
                        "USERFRAMEWORK_english",
                        "USERFRAMEWORK_class6"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": {
                        "showBanner": true,
                        "values": [
                            {
                                "code": "banner_external_url",
                                "ui": {
                                    "background": "https://cdn.pixabay.com/photo/2015/10/29/14/38/web-1012467_960_720.jpg",
                                    "text": "Sample External Url"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "externalUrl",
                                    "params": {
                                        "route": "https://diksha.gov.in/"
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_internal_url",
                                "ui": {
                                    "background": "https://cdn.pixabay.com/photo/2015/10/29/14/38/web-1012467_960_720.jpg",
                                    "text": "Sample Internal Url"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "internalUrl",
                                    "params": {
                                        "route": "profile"
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "ui": {
                                    "background": "https://cdn.pixabay.com/photo/2015/10/29/14/38/web-1012467_960_720.jpg",
                                    "text": "Sample Search"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_content",
                                "ui": {
                                    "background": "https://cdn.pixabay.com/photo/2015/10/29/14/38/web-1012467_960_720.jpg",
                                    "text": "Sample content"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "content",
                                    "params": {
                                        "identifier": "do_21302358976737280014"
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "NISHTHA FLN COurses",
                                    "icon": "assets/imgs/ic_nishtha_courses.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "NISHTA  Secondary Courses",
                                    "icon": "assets/imgs/ic_secondary_course.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "Revision Preperation",
                                    "icon": "assets/imgs/ic_revision_preperation.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "FLN Programme",
                                    "icon": "assets/imgs/ic_fln_programme.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "Administration  Programme",
                                    "icon": "assets/imgs/ic_administration_programme.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "Quiz",
                                    "icon": "assets/imgs/ic_quiz.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "filterIdentifier": "nlp",
                                "expiry": "1841807258"
                            }
                        ]
                    }
                },
                {
                    "commandId": 1619548201298,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "DEBUGGING_MODE",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "OR",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "ALL_android"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": {
                        "traceId": "TID_123445"
                    }
                },
                {
                    "commandId": 1619548200012,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "BANNER_CONFIG",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "APPVERSION_DIKSHA v4.4.104staging.97"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": {
                        "showBanner": true,
                        "values": [
                            {
                                "code": "banner_external_url",
                                "ui": {
                                    "background": "https://image.freepik.com/free-vector/minimalist-watercolor_91008-209.jpg",
                                    "text": "Sample External Url"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "externalUrl",
                                    "params": {
                                        "route": "https://diksha.gov.in/"
                                    }
                                },
                                "expiry": "1653031067"
                            }
                        ]
                    }
                },
                {
                    "commandId": 1619548200013,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "BANNER_CONFIG",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "DEVCONFIG_7fb8fbb3a2bb521689ff04d7f31097676adf101d"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": {
                        "showBanner": true,
                        "values": [
                            {
                                "code": "banner_external_url",
                                "ui": {
                                    "background": "https://image.freepik.com/free-vector/minimalist-watercolor_91008-209.jpg",
                                    "text": "Device Based Banner"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "externalUrl",
                                    "params": {
                                        "route": "https://diksha.gov.in/"
                                    }
                                },
                                "expiry": "1653031067"
                            }
                        ]
                    }
                },
                {
                    "commandId": 1619548200014,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "LOCAL_NOTIF",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "USERROLE_teacher"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": [
                        {
                            "code": "localNotification",
                            "name": "LocalNotification",
                            "type": 1,
                            "config": [
                                {
                                    "msg": "Registred as Teacher",
                                    "isEnabled": true,
                                    "id": 1006,
                                    "title": "Registred as Teacher"
                                }
                            ]
                        }
                    ]
                },
                {
                    "commandId": 1619548200015,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "LOCAL_NOTIF",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "tagFilters": [
                        "USERROLE_teacher",
                        "USERLOCATION_Bengaluru U North",
                        "USERLOCATION_Karnataka"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": [
                        {
                            "code": "localNotification",
                            "name": "LocalNotification",
                            "type": 1,
                            "config": [
                                {
                                    "msg": "Welcome to Karnataka",
                                    "isEnabled": true,
                                    "id": 1006,
                                    "title": "Welcome to Karnataka"
                                }
                            ]
                        }
                    ]
                },
                {
                    "commandId": 1619548201250,
                    "commandType": "SEGMENT_COMMAND",
                    "controlFunction": "BANNER_CONFIG",
                    "expiresAfter": 1841807258000,
                    "tagCriteria": "AND",
                    "tagFilterUpto": null,
                    "targetedClient": "portal",
                    "tagFilters": [
                        "USERFRAMEWORK_State (Tamil Nadu)",
                        "USERFRAMEWORK_English",
                        "USERFRAMEWORK_Class 1"
                    ],
                    "targetDeviceIds": null,
                    "targetVersion": null,
                    "controlFunctionPayload": {
                        "showBanner": true,
                        "values": [
                            {
                                "code": "banner_external_url",
                                "ui": {
                                    "background": "https://cdn.pixabay.com/photo/2015/10/29/14/38/web-1012467_960_720.jpg",
                                    "text": "Sample External Url"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "externalUrl",
                                    "params": {
                                        "route": "https://diksha.gov.in/"
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_internal_url",
                                "ui": {
                                    "background": "https://cdn.pixabay.com/photo/2015/10/29/14/38/web-1012467_960_720.jpg",
                                    "text": "Sample Internal Url"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "internalUrl",
                                    "params": {
                                        "route": "profile"
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "ui": {
                                    "background": "https://cdn.pixabay.com/photo/2015/10/29/14/38/web-1012467_960_720.jpg",
                                    "text": "Sample Search"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_content",
                                "ui": {
                                    "background": "https://5.imimg.com/data5/RN/UY/AT/SELLER-90246361/printed-rectangle-flex-banner-500x500.jpg",
                                    "text": "Sample content"
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "content",
                                    "params": {
                                        "identifier": "do_21302358976737280014"
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "NISHTHA FLN COurses",
                                    "icon": "assets/images/ic_nishtha_courses.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "NISHTHA FLN COurses",
                                    "icon": "assets/images/ic_nishtha_courses.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "NISHTA  Secondary Courses",
                                    "icon": "assets/images/ic_secondary_course.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "Revision Preperation",
                                    "icon": "assets/images/ic_revision_preperation.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "FLN Programme",
                                    "icon": "assets/images/ic_fln_programme.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "Administration  Programme",
                                    "icon": "assets/images/ic_administration_programme.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            },
                            {
                                "code": "banner_search",
                                "type": "secondary",
                                "ui": {
                                    "text": "Quiz",
                                    "icon": "assets/images/ic_quiz.svg",
                                    "theme": {
                                        "iconBgColor": "#FFFFFF",
                                        "pillBgColor": "#FFFFFF"
                                    }
                                },
                                "action": {
                                    "type": "navigate",
                                    "subType": "search",
                                    "params": {
                                        "query": "limited attempt course",
                                        "filter": {
                                            "offset": 0,
                                            "filters": {
                                                "audience": [],
                                                "objectType": [
                                                    "Content"
                                                ]
                                            }
                                        }
                                    }
                                },
                                "expiry": "1841807258"
                            }
                        ]
                    }
                }
            ]
        }
    }
}
```

### Regional Language Label Transaltion <a href="#id-ed-portal-configchangesasperthebmgshardcodedremoval-regionallanguagelabeltransaltion" id="id-ed-portal-configchangesasperthebmgshardcodedremoval-regionallanguagelabeltransaltion"></a>

As per the release-7.0.0 “**framework categories**” is generalized. so any new framework is introduced In ED-Portal. User has to create a translation label in (en,kn, hi properties files..)\
Please use the **framework categories** code as a translation label key\
sample: `frmelmnts.lbl.{{framework_code}}={{framework_label}`\
Ex : `frmelmnts.lbl.board= Board`

### Skip Onboarding Flow <a href="#id-ed-portal-configchangesasperthebmgshardcodedremoval-skiponboardingflow" id="id-ed-portal-configchangesasperthebmgshardcodedremoval-skiponboardingflow"></a>

As per the release-7.0.0 onbording flow is configurable(form based) user able to enable/disable the onboarding flow as per their use-case.

1. User can skip the entire onboarding flow
2. User can only skip the userType flow
3. User can only skip the framework selection flow
4. User can only skip the location flow

#### Form Create (onboardingpopupvisibility\_global\_onboarding)\_O <a href="#id-ed-portal-configchangesasperthebmgshardcodedremoval-formcreate-onboardingpopupvisibility_global_o" id="id-ed-portal-configchangesasperthebmgshardcodedremoval-formcreate-onboardingpopupvisibility_global_o"></a>

**onboardingPopups metadata** - Refers to skip the entire onboarding flow by setting isVisible = false & defaultFormatedName.

**userTypePopup metadata** - Refers to skip the userType popup by setting isVisble=false & defaultUserType,defaultGuestUserType.

**frameworkPopup metdata** - Refers to skip the frameworkPopup by setting isVisble=false & defaultFormatedName

**locationPopup metadata** - Refers to skip the locationPopup by setting the isVisble = false

**Note**: onboardingPopups isVisible property should be true to skip above individual flow. if false then entire flow will be skipped.

Sample form request for onboardingpopupvisibility

```
{
    "request": {
        "type": "onboardingpopupvisibility",
        "subType": "global",
        "action": "onboarding",
        "component": "portal",
        "data": {
            "fields": {
                "onboardingPopups": {
                    "isVisible": true,
                    "defaultFormatedName": "Guest"
                },
                "userTypePopup": {
                    "isVisible": true,
                    "defaultUserType": "Teacher",
                    "defaultGuestUserType": "Teacher"
                },
                "frameworkPopup": {
                    "isVisible": true,
                    "defaultFormatedName": "Guest"
                },
                "locationPopup": {
                    "isVisible": true
                }
            }
        }
    }
}
```

### **Reference links** <a href="#id-ed-portal-configchangesasperthebmgshardcodedremoval-referencelinks" id="id-ed-portal-configchangesasperthebmgshardcodedremoval-referencelinks"></a>

Jira Ticket: [ED-3042](https://project-sunbird.atlassian.net/browse/ED-3042) - Getting issue details... STATUS

GitHub PR Link : [https://github.com/Sunbird-Ed/SunbirdEd-portal/pull/9063](https://github.com/Sunbird-Ed/SunbirdEd-portal/pull/9063)

Design Docs: [\[ED-Portal\] DC: Design-Docs for Hardcoded BMGS removal](broken-reference)

Gap Analysis Docs : [Sunbird-ED: Gap Analysis Docs for BMGS](broken-reference)
