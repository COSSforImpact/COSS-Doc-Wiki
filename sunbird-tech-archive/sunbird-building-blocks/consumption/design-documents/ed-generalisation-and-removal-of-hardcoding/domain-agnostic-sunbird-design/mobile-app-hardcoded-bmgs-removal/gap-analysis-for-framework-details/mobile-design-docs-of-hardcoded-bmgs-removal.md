---
icon: elementor
---

# Mobile: Design docs of hardcoded BMGS removal

### Introduction: <a href="#mobile-designdocsofhardcodedbmgsremoval-introduction" id="mobile-designdocsofhardcodedbmgsremoval-introduction"></a>

This document describes the design approach of hardcoded BMGS removal and new framework introduced.

* Introduction:
* Background:
* Problem Statement:
* Onboarding flow of Framework Cateogories(BMGS)
  * Key design problems:
  * Design:
    * Solution 1
    * Pros:
* Support multiple framework categories in local DB
  * Key design problems:
  * Design:
    * Solution 1
    * Pros:
* Search filter (BMGS)
  * Key design problems:
  * Design:
    * Solution 1
    * Pros:

### Background: <a href="#mobile-designdocsofhardcodedbmgsremoval-background" id="mobile-designdocsofhardcodedbmgsremoval-background"></a>

Currently, sunbird mobile app uses hardcoded BMGS and it does not support multiple framework categories. It’s support only educational related frameworks.

### Problem Statement: <a href="#mobile-designdocsofhardcodedbmgsremoval-problemstatement" id="mobile-designdocsofhardcodedbmgsremoval-problemstatement"></a>

* How sunbird Adopter can use this application in any domain(education domain & non-educational domain)
* How can consume a course, getting certificate, report without any code change & only update the form-config.

### Onboarding flow of Framework Cateogories(BMGS) <a href="#mobile-designdocsofhardcodedbmgsremoval-onboardingflowofframeworkcateogories-bmgs" id="mobile-designdocsofhardcodedbmgsremoval-onboardingflowofframeworkcateogories-bmgs"></a>

In Existing code base the BMGS code are hardcoded to display the BMGS for onboarding, profile and content metadata, If non-BMGS framework comes the existing code will be break.

#### Key design problems: <a href="#mobile-designdocsofhardcodedbmgsremoval-keydesignproblems" id="mobile-designdocsofhardcodedbmgsremoval-keydesignproblems"></a>

* How to change the label, placeholder of the BMGS selection screen and profile page?
* What is the api’s request to get new framework details and categories terms in any domain?

BMGS selection screenshot



&#x20;

#### Design: <a href="#mobile-designdocsofhardcodedbmgsremoval-design" id="mobile-designdocsofhardcodedbmgsremoval-design"></a>

**Solution 1**

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

* Using the below form configuration, we can change the category label and add/remove the categories. When new framework introduced, we have to update the “label”, “placeHolder” and “categoryCode” according to framework categories.

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

* Remove BMGS hardcoded and use _**form-config code**_ like, category1 for board, category2 for medium, category3 for gradeLevel and category4 for subject
*   `DEFAULT_FRAMEWORK_CATEGORIES` will be the array of new framework categories for getting the framework categories details.

    ```
    this.framework = await this.frameworkService.getFrameworkDetails({
                from: CachedItemRequestSourceFrom.SERVER,
                frameworkId: value[0],
                requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
              }).toPromise();
    ```

**Pros:**

* Using the form Config changes Adopter can create their own framework categories.
* No code level changes required.

### **Support multiple framework categories in local DB** <a href="#mobile-designdocsofhardcodedbmgsremoval-supportmultipleframeworkcategoriesinlocaldb" id="mobile-designdocsofhardcodedbmgsremoval-supportmultipleframeworkcategoriesinlocaldb"></a>

Previously all categories were saved in individual columns which is not scalable and can't support if a specific framework will have more than 4 categories.

| **board** | **medium** | **gradeLevel** | **subject** |
| --------- | ---------- | -------------- | ----------- |
| cbse      | english    | class1         | mathematics |

#### Key design problems: <a href="#mobile-designdocsofhardcodedbmgsremoval-keydesignproblems-.1" id="mobile-designdocsofhardcodedbmgsremoval-keydesignproblems-.1"></a>

* How to add multiple framework categories in local DB?
* How it will work for existing users or old users?

#### Design: <a href="#mobile-designdocsofhardcodedbmgsremoval-design-.1" id="mobile-designdocsofhardcodedbmgsremoval-design-.1"></a>

**Solution 1**

* To support n number of categories a new column will be created where all categories will be stored in a stringified JSON formated.

| **categories**                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------ |
| "{\\"board\\":\[\\"CBSE\\"],\\"medium\\":\[\\"English\\"],\\"gradeLevel\\":\[\\"Class 4\\"],\\"subject\\":\[\\"Environmental Studies\\"]}" |

* For existing users, we have to remove the BMGS column and migrate the local DB.

**Pros:**

* Adopter can use 1 to n number of categories and it will work in offline also.
* No code level changes required.

### Search filter (BMGS) <a href="#mobile-designdocsofhardcodedbmgsremoval-searchfilter-bmgs" id="mobile-designdocsofhardcodedbmgsremoval-searchfilter-bmgs"></a>

We are using BMGS hardcoded in multiple places for search response, apply filter, event handling etc.

#### Key design problems: <a href="#mobile-designdocsofhardcodedbmgsremoval-keydesignproblems-.2" id="mobile-designdocsofhardcodedbmgsremoval-keydesignproblems-.2"></a>

* How to change the label,placeholder?
* How to handle the BMGS hardcorded code?
* How can add/remove filter?
* How to manage facet filters for searching in any domain with multiple framework categories?

#### Design: <a href="#mobile-designdocsofhardcodedbmgsremoval-design-.2" id="mobile-designdocsofhardcodedbmgsremoval-design-.2"></a>

**Solution 1**

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

* Using the form-config update we can add/remove the filter property.
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

**Pros:**

* Using the form Config changes Adopter can create their own search filter dropdown
* No code level changes required.
