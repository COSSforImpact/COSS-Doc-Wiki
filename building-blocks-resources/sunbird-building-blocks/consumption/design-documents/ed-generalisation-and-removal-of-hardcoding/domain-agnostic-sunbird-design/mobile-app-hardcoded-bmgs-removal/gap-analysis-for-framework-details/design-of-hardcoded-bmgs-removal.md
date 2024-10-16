---
icon: elementor
---

# Design of hardcoded BMGS removal

### Introduction: <a href="#designofhardcodedbmgsremoval-introduction" id="designofhardcodedbmgsremoval-introduction"></a>

This document describes the design approach of hardcoded BMGS removal and new framework introduced

* Introduction:
* Background:
* Design :
* Onboarding
  * User-type selection :
    * Problem
    * Solution
  * Framework selection page(BMGS removal):
    * Problem
    * Solution :
  * Location page :
    * Problem
    * Solution
* Skip the Onboarding Steps :
  * Problem
  * Solution
* Support multiple framework categories in local DB:
  * Problem
  * Solution
* Home Page :
  * Problem
  * Solution
* Update User Profile:
  * Problem
  * Solution
* Search Filter and Applied filter :
  * Problem
  * Solution
* Content Cosumption
  * Problem

### Background: <a href="#designofhardcodedbmgsremoval-background" id="designofhardcodedbmgsremoval-background"></a>

Currently, sunbird mobile app uses hardcoded BMGS and it does not support multiple framework categories. This design document describes how to remove the hardcoded and support n number of categories.

### **Design :** <a href="#designofhardcodedbmgsremoval-design" id="designofhardcodedbmgsremoval-design"></a>

### Onboarding <a href="#designofhardcodedbmgsremoval-onboarding" id="designofhardcodedbmgsremoval-onboarding"></a>

#### User-type selection : <a href="#designofhardcodedbmgsremoval-user-typeselection" id="designofhardcodedbmgsremoval-user-typeselection"></a>

**Problem**

How to configure user type selection page if a new framework introduced ?

How to handle the label translation?

User-type selection page

**Solution**

Update the userType details in below form config and add the translate text in "translations" key.

```
"request": {
    "type": "config",
    "subType": "userType",
    "action": "get",
    "component": "app"
  }
```

Form-config response for user types

```
  "fields": [
                {
                    "code": "teacher",
                    "name": "Teacher",
                    "translations": "{\\"en\\":\\"Teacher\\",\\"as\\":\\"শিক্ষক\\",\\"bn\\":\\"শিক্ষক\\",\\"gu\\":\\"શિક્ષક\\",\\"hi\\":\\"शिक्षक\\",\\"kn\\":\\"ಶಿಕ್ಷಕ/ಕಿ\\",\\"mr\\":\\"शिक्षक\\",\\"or\\":\\"ଶିକ୍ଷକ\\",\\"pa\\":\\"ਅਧਿਆਪਕ\\",\\"ta\\":\\"ஆசிரியர்\\",\\"te\\":\\"ఉపాధ్యాయుడు\\",\\"ur\\":\\"استاد\\"}",
                    "image": "ic_teacher.svg",
                    "ambiguousFilters": [
                        "teacher",
                        "instructor"
                    ],
                    "searchFilter": [
                        "Teacher",
                        "Instructor"
                    ],
                    "attributes": {
                        "mandatory": [
                            "board",
                            "medium",
                            "gradeLevel"
                        ],
                        "optional": [
                            "subject"
                        ]
                    }
                },
                {
                    "code": "student",
                    "name": "Student",
                    "translations": "{\\"en\\":\\"Student\\",\\"as\\":\\"শিক্ষাৰ্থী\\",\\"bn\\":\\"ছাত্র\\",\\"gu\\":\\"વિદ્યાર્થી\\",\\"hi\\":\\"विद्यार्थी\\",\\"kn\\":\\"ವಿದ್ಯಾರ್ಥಿ\\",\\"mr\\":\\"विद्यार्थी\\",\\"or\\":\\"ଛାତ୍ର ଛାତ୍ରୀ\\",\\"pa\\":\\"ਵਿਦਿਆਰਥੀ\\",\\"ta\\":\\"மாணவர்\\",\\"te\\":\\"విద్యార్థి\\",\\"ur\\":\\"طالب علم\\"}",
                    "image": "ic_student.svg",
                    "ambiguousFilters": [
                        "learner",
                        "student"
                    ],
                    "searchFilter": [
                        "Student",
                        "Learner"
                    ],
                    "attributes": {
                        "mandatory": [
                            "board",
                            "medium",
                            "gradeLevel"
                        ],
                        "optional": [
                            "subject"
                        ]
                    }
                },
                {
                    "code": "administrator",
                    "name": "Admin",
                    "translations": "{\\"en\\":\\"Admin\\"}",
                    "image": "ic_admin.svg",
                    "ambiguousFilters": [],
                    "searchFilter": [
                        "administrator"
                    ],
                    "attributes": {
                        "mandatory": [
                            "board"
                        ],
                        "optional": []
                    }
                },
                {
                    "code": "other",
                    "name": "Other",
                    "translations": "{\\"en\\":\\"Other\\",\\"as\\":\\"অন্য\\",\\"bn\\":\\"অন্যান্য\\",\\"gu\\":\\"અન્ય\\",\\"hi\\":\\"अन्य\\",\\"kn\\":\\"ಇತರೆ\\",\\"mr\\":\\"इतर\\",\\"or\\":\\"ଅନ୍ୟ\\",\\"pa\\":\\"ਹੋਰ\\",\\"ta\\":\\"மற்றவை\\",\\"te\\":\\"ఇతర\\",\\"ur\\":\\"دوسرے\\"}",
                    "image": "ic_other.svg",
                    "ambiguousFilters": [
                        "student, teacher",
                        "instructor and learner",
                        "learner & instructor"
                    ],
                    "searchFilter": [
                        "Student",
                        "Teacher",
                        "Instructor",
                        "Learner"
                    ],
                    "attributes": {
                        "mandatory": [
                            "board",
                            "medium",
                            "gradeLevel"
                        ],
                        "optional": [
                            "subject"
                        ]
                    }
                }
            ]
```

#### Framework selection page(BMGS removal): <a href="#designofhardcodedbmgsremoval-frameworkselectionpage-bmgsremoval" id="designofhardcodedbmgsremoval-frameworkselectionpage-bmgsremoval"></a>

**Problem**

How to change the label and placeholder of the below BMGS screen?

How to handle the BMGS hardcorded keyword?

BMGS selection screenshot

**Solution :**

* In the case of one channel having multiple frameworks with different different categories, then we have to configure a default framework form-config for label and when user select the framework, the framework label should be changed according to framework. use the below form-config for multiple different categories framework.

multiple framework form-config

```
   fields: [
        {
          id: 'default',
          code: 'default',
          name: 'board',
          options: [
            {
              "code": "category1",
              "label": "{\"en\":\"Board\"}",
              "placeHolder": "{\"en\":\"Selected Board\"}",
              "frameworkCode": "board",
              "supportedUserTypes": [
                "teacher",
                "student",
                "administrator",
                "parent",
                "other",
                "farmer",
                "user1"
              ]
            },
            {
              "code": "category2",
              "label": "{\"en\":\"Medium\"}",
              "placeHolder": "{\"en\":\"Selected Medium\"}",
              "frameworkCode": "medium",
              "supportedUserTypes": [
                "teacher",
                "student",
                "parent",
                "other",
                "farmer",
                "user1"
              ]
            },
            {
              "code": "category3",
              "label": "{\"en\":\"Class\"}",
              "placeHolder": "{\"en\":\"Selected Class\"}",
              "frameworkCode": "gradeLevel",
              "supportedUserTypes": [
                "teacher",
                "student",
                "parent",
                "other",
                "farmer",
                "user1"
              ]
            }
          ]
        },
        {
          id: 'framework1',
          code: 'framework1',
          name: 'Organization',
          options: [
            {
              "code": "category1",
              "label": "{\"en\":\"Organisation\"}",
              "placeHolder": "{\"en\":\"Selected Organisation\"}",
              "frameworkCode": "category1",
              "supportedUserTypes": [
                 "teacher",
                "student",
                "parent",
                "other"
              ]
            },
            {
              "code": "category2",
              "label": "{\"en\":\"Category\"}",
              "placeHolder": "{\"en\":\"Selected Category\"}",
              "frameworkCode": "category2",
              "supportedUserTypes": [
                 "teacher",
                "student",
                "parent",
                "other"
              ]
            },
            {
              "code": "category3",
              "label": "{\"en\":\"TYpe\"}",
              "placeHolder": "{\"en\":\"Selected Type\"}",
              "frameworkCode": "category3",
              "supportedUserTypes": [
                 "teacher",
                "student",
                "parent",
                "other"
              ]
            }
          ]
        },
        {
          id: 'agriculture_framework',
          code: 'agriculture_framework',
          name: 'agriculture',
          options: [
            {
              "code": "category1",
              "label": "{\"en\":\"Foodcrops\"}",
              "placeHolder": "{\"en\":\"Selected foodcrops\"}",
              "frameworkCode": "foodcrops",
              "supportedUserTypes": [
                 "teacher",
                "student",
                "parent",
                "other",
                "farmer",
                "user1"
              ]
            },
            {
              "code": "category2",
              "label": "{\"en\":\"Commercialcrops\"}",
              "placeHolder": "{\"en\":\"Selected commercialcrops\"}",
              "frameworkCode": "commercialcrops",
              "supportedUserTypes": [
                 "teacher",
                "student",
                "parent",
                "other",
                "farmer",
                "user1"
              ]
            },
            {
              "code": "category3",
              "label": "{\"en\":\"livestockmanagement\"}",
              "placeHolder": "{\"en\":\"Selected livestockmanagement\"}",
              "frameworkCode": "livestockmanagement",
              "supportedUserTypes": [
                 "teacher",
                "student",
                "parent",
                "other",
                "farmer",
                "user1"
              ]
            },{
              "code": "category4",
              "label": "{\"en\":\"livestockspecies\"}",
              "placeHolder": "{\"en\":\"Selected livestockspecies\"}",
              "frameworkCode": "livestockspecies",
              "supportedUserTypes": [
                 "teacher",
                "student",
                "parent",
                "other",
                "farmer",
                "user1"
              ]
            },{
              "code": "category5",
              "label": "{\"en\":\"animalwelfare\"}",
              "placeHolder": "{\"en\":\"Selected animalwelfare\"}",
              "frameworkCode": "animalwelfare",
              "supportedUserTypes": [
                 "teacher",
                "student",
                "parent",
                "other",
                "farmer",
                "user1"
              ]
            }
          ]
        }
      ]
    };
```

* This is our new form configuration for dynamic label and support multiple categories. When new framework introduced, we have to change “label”, “placeHolder” and “categoryCode” according to framework categories.

Form-config for framework label

```
response={
  fields: [
    {
      id: 'framework_id_2',
      code: 'framework_id_2',
      name: 'Framework2',
      options: [
   {
          "code": "category1",
          "label": "{\"en\":\"Foodcrops\"}",
          "placeHolder": "{\"en\":\"Selected foodcrops\"}",
          "categoryCode": "foodcrops",
          "supportedUserTypes": [
            "other",
            "farmer",
            "user1"
          ]
        },
        {
          "code": "category2",
          "label": "{\"en\":\"Commercialcrops\"}",
          "placeHolder": "{\"en\":\"Selected commercialcrops\"}",
          "categoryCode": "commercialcrops",
          "supportedUserTypes": [
            "other",
            "farmer",
            "user1"
          ]
        },
        {
          "code": "category3",
          "label": "{\"en\":\"livestockmanagement\"}",
          "placeHolder": "{\"en\":\"Selected livestockmanagement\"}",
          "categoryCode": "livestockmanagement",
          "supportedUserTypes": [
            "other",
            "farmer",
            "user1"
          ]
        },{
          "code": "category4",
          "label": "{\"en\":\"livestockspecies\"}",
          "placeHolder": "{\"en\":\"Selected livestockspecies\"}",
          "categoryCode": "livestockspecies",
          "supportedUserTypes": [
            "other",
            "farmer",
            "user1"
          ]
        },{
          "code": "category5",
          "label": "{\"en\":\"animalwelfare\"}",
          "placeHolder": "{\"en\":\"Selected animalwelfare\"}",
          "categoryCode": "animalwelfare",
          "supportedUserTypes": [
            "other",
            "farmer",
            "user1"
          ]
        }
      ]
    }
  ]
}
```

* Remove BMGS hardcoded and use category1 for board, category2 for medium, category3 for gradeLevel and category4 for subject

```
{categories: "new_category1,new_category2,new_category3,......new_categoryN"}
```

* `DEFAULT_FRAMEWORK_CATEGORIES` should be the new framework categories for getting the framework categories details.

#### Location page : <a href="#designofhardcodedbmgsremoval-locationpage" id="designofhardcodedbmgsremoval-locationpage"></a>

**Problem**

How to configure user location page, so we can change the label and add the label without any code change?

Location page screenshot

**Solution**

User location is dynamic and we can add/remove the fields in the location through the form-config change. We can easily skip the location and set the default value of location.

1. Users have to update the location fields in the below form config

```
  "request": {
    "type": "profileConfig_v2",
    "subType": "default",
    "action": "get"
  }
```

Location Config

```
response: {
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
                            ]
```

### Skip the Onboarding Steps : <a href="#designofhardcodedbmgsremoval-skiptheonboardingsteps" id="designofhardcodedbmgsremoval-skiptheonboardingsteps"></a>

**Problem**

How can skip the onboarding page and land to the Home page?

**Solution**

Currently, mobile app can skip the onboarding step through the set default value of user type, framework and location but this configuration is in our code, we have to create a form-config for below configuaration.

Form-config for skip the onboarding steps

4. ```
   "onboarding": [
           {
               "name": "language-setting",
               "skip": false,
               "default": {
                   "code": "en",
                   "label": "English"
               }
           },
           {
               "name": "user-type-selection",
               "skip": false,
               "default": "teacher"
           },
           {
               "name": "profile-settings",
               "skip": false,
               "params": {
                   "showQrScanPage": true
               },
               "default": {
                   "syllabus": [
                       "ekstep_ncert_k-12"
                   ],
                   "board": [
                       "cbse"
                   ],
                   "medium": [
                       "english"
                   ],
                   "grade": [
                       "class5",
                       "class6"
                   ]
               }
           },
           {
               "name": "district-mapping",
               "skip": false,
               "default": {
                   "state": "Andaman & Nicobar Islands",
                   "stateId": "1e01c46f-6b5a-4aa4-8cce-aae729c7670c",
                   "district": "Nicobars",
                   "districtId": "6daef899-1e83-4b87-9c67-779985c3fd41"
               }
           }
       ]
   ```

### **Support multiple framework categories in local DB:** <a href="#designofhardcodedbmgsremoval-supportmultipleframeworkcategoriesinlocaldb" id="designofhardcodedbmgsremoval-supportmultipleframeworkcategoriesinlocaldb"></a>

**Problem**

How to add multiple framework categories in local DB?

Previously all categories were saved in individual columns which is not scalable and can't support if a specific framework will have more than 4 categories.

| **board** | **medium** | **gradeLevel** | **subject** |
| --------- | ---------- | -------------- | ----------- |
| cbse      | english    | class1         | mathematics |

**Solution**

To support n number of categories a new column will be created where all categories will be stored in a stringified JSON formated.

| **categories**                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------ |
| "{\\"board\\":\[\\"CBSE\\"],\\"medium\\":\[\\"English\\"],\\"gradeLevel\\":\[\\"Class 4\\"],\\"subject\\":\[\\"Environmental Studies\\"]}" |

### Home Page : <a href="#designofhardcodedbmgsremoval-homepage" id="designofhardcodedbmgsremoval-homepage"></a>

**Problem**

How to remove all the hardcoded BMGS for user preferences and content search ?

How To config the section on home page ?

Home page screenshot

**Solution**

All the sections are coming from form-configuration so we can easily update the form and remove hardcoded BMGS and use “framework\_category1” to “framework\_categoryN” for categories.

### Update User Profile: <a href="#designofhardcodedbmgsremoval-updateuserprofile" id="designofhardcodedbmgsremoval-updateuserprofile"></a>

**Problem**

How to update profile framework with category key instead of BMGS?

**Solution**

Remove the BMGS hardcoded from update profile request and use new framework categories.

Profile update screenshot

**New Profile update request for agriculture\_framework:**

```
{
    "userId": "e14df618-2e5d-49f5-80fa-2ba5012a97cb",
    "framework": {
            "id": [
                "agriculture_framework"
            ],
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
            ]
    }
}
```

### Search Filter and Applied filter : <a href="#designofhardcodedbmgsremoval-searchfilterandappliedfilter" id="designofhardcodedbmgsremoval-searchfilterandappliedfilter"></a>

**Problem**

How to manage facet filters for searching in multiple framework categories?

Search filter for BMGS screenshot

**Solution**

* Now, search filter labels are dynamic, it is a form-config and set the filter value by using code, If new framework introduced then have to update the form-config of “code”, "translations" and “name” in below filer configuration. We have to pass Framework’s form-config “categoryCode” as a search filter request.

```
 filter form request: 
 "request": {
    "type": "config",
    "subType": "search",
    "action": "filter_v3",
    "component": "app"
  }
```

Filter Config

```
  "fields": [
                    {
                        "code": "se_boards",
                        "translations": "{\"en\":\"Board/Syllabus\",\"as\":\"ব'ৰ্ড\",\"bn\":\"পর্ষদ\",\"gu\":\"બોર્ડ\",\"hi\":\"बोर्ड\",\"kn\":\"ಮಂಡಳಿ\",\"mr\":\"बोर्ड\",\"or\":\"ବୋର୍ଡ\",\"pa\":\"ਬੋਰਡ\",\"ta\":\"வாரியம்\",\"te\":\"బోర్డు\",\"ur\":\"بورڈ\"}",
                        "values": [],
                        "name": "Board/Syllabus",
                        "index": 1
                    },
                    {
                        "code": "se_gradeLevels",
                        "translations": "{\"en\":\"Class\",\"as\":\"শ্ৰেণী\",\"bn\":\"শ্রেনী\",\"gu\":\"વર્ગ\",\"hi\":\"कक्षा\",\"kn\":\"ತರಗತಿ\",\"mr\":\"इयत्ता\",\"or\":\"ଶ୍ରେଣୀ\",\"pa\":\"ਜਮਾਤ\",\"ta\":\"வகுப்பு\",\"te\":\"క్లాసు\",\"ur\":\"کلاس\"}",
                        "values": [],
                        "name": "Class",
                        "index": 2
                    },
                    {
                        "code": "subject",
                        "translations": "{\"en\":\"Subject\",\"as\":\"বিষয়\",\"bn\":\"বিষয়\",\"gu\":\"વિષય\",\"hi\":\"विषय\",\"kn\":\"ವಿಷಯ\",\"mr\":\"विषय\",\"or\":\"ବିଷୟ\",\"pa\":\"ਵਿਸ਼ਾ\",\"ta\":\"பாடம்\",\"te\":\"పాఠ్యాంశము\",\"ur\":\"مضامین\"}",
                        "values": [],
                        "name": "Subject",
                        "index": 3
                    },
                    {
                        "code": "se_mediums",
                        "translations": "{\"en\":\"Medium\",\"as\":\"মাধ্যম\",\"bn\":\"মাধ্যাম\",\"gu\":\"માધ્યમ\",\"hi\":\"माध्यम\",\"kn\":\"ಮಾಧ್ಯಮ\",\"mr\":\"माध्यम\",\"or\":\"ମାଧ୍ୟମ\",\"pa\":\"ਮਾਧਿਅਮ\",\"ta\":\"மீடியம்\",\"te\":\"మాధ్యమం\",\"ur\":\"میڈیم\"}",
                        "values": [],
                        "name": "Medium",
                        "index": 4
                    },
                    {
                        "code": "primaryCategory",
                        "translations": "{\"en\":\"Content Type\"}",
                        "values": [],
                        "name": "Resource Type",
                        "index": 5
                    },
                    {
                        "code": "channel",
                        "translations": "{\"en\":\"Publisher\",\"as\":\"প্ৰকাশক\",\"bn\":\"প্রকাশক\",\"gu\":\"પ્રકાશક\",\"hi\":\"प्रकाशक\",\"kn\":\"ಪ್ರಕಾಶಕರು\",\"mr\":\"प्रकाशक\",\"or\":\"ପ୍ରକାଶକ\",\"pa\":\"ਪ੍ਰਕਾਸ਼ਕ\",\"ta\":\"வெளியீட்டாளர்\",\"te\":\"ప్రచురణకర్త\",\"ur\":\"ناشر\"}",
                        "values": [],
                        "name": "Publisher",
                        "index": 6
                    },
                    {
                        "code": "mimeType",
                        "translations": "{\"en\":\"Media Type\",\"as\":\"মাধ্যমৰ ধৰণ\",\"bn\":\"মিডিয়ার ধরণ\",\"gu\":\"મીડિયાનો પ્રકાર\",\"hi\":\"मीडिया प्रकार\",\"kn\":\"ಮಾಧ್ಯಮದ ವಿಧ\",\"mr\":\"माध्यम प्रकार\",\"or\":\"ମିଡ଼ିଆ ପ୍ରକାର\",\"pa\":\"ਮੀਡੀਆ ਦੀ ਕਿਸਮ\",\"ta\":\"ஊடக வகை\",\"te\":\"మీడియా రకం\",\"ur\":\"میڈیا کی قسم\"}",
                        "values": [],
                        "name": "Publisher",
                        "index": 7
                    },
                    {
                        "code": "audience",
                        "translations": "{\"en\":\"Meant for\"}",
                        "values": [],
                        "name": "Meant For",
                        "index": 8
                    },
                    {
                        "code": "additionalCategories",
                        "translations": "{\"en\":\"Additional Categories\"}",
                        "values": [],
                        "name": "Additional Categories",
                        "index": 9
                    }
                ]
```

* New api’s path for agriculture framework:

```
path: '/api/content/v1/search?framework=agriculture_framework&lang=en&orgdetails=orgName'
```

New search request for agriculture framework

```
{
    "request": {
        "query": "content",
        "offset": 0,
        "limit": 10,
        "mode": "soft",
        "exists": [],
        "facets": [
            "foodcrops",
            "commercialcrops",
            "livestockmanagement",
            "livestockspecies",
            "animalwelfare",
            "primaryCategory",
            "channel",
            "mimeType",
            "audience",
            "additionalCategories"
        ],
        "sort_by": {},
        "filters": {
            "audience": [],
            "objectType": [
                "Content",
                "QuestionSet"
            ],
            "contentType": [],
            "primaryCategory": [],
            "se_mediums": [],
            "se_boards": [],
            "language": [],
            "topic": [],
            "purpose": [],
            "channel": [],
            "mimeType": [],
            "subject": []
        }
    }
}
```

### Content Cosumption <a href="#designofhardcodedbmgsremoval-contentcosumption" id="designofhardcodedbmgsremoval-contentcosumption"></a>

**Problem**

How to handle the content metadata UI in “about content section” when a new framework is introduced?

content metadata of BMGS

**Solution**

We can use the Framework form-config labels for the content metadata categories label. If the new framework comes the “about content section” label will be change then without code change it will work.
