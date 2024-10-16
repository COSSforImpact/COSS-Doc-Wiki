---
icon: elementor
---

# Agriculture Framework : Flow Analysis in ED-Portal

* On-boarding flow-User Type

### On-boarding flow-User Type <a href="#agricultureframework-flowanalysisined-portal-on-boardingflow-usertype" id="agricultureframework-flowanalysisined-portal-on-boardingflow-usertype"></a>

I have changed the below config teacher to farmer1

Click here to expand...

```
"fields": [
                    {
                        "code": "teacher" to "farmer1"
                        "name": "Teacher" to "Grain and oilseed farms"
                        "label": "frmelmnts.lbl.teacher", to "rmelmnts.lbl.teacher"
                        "visibility": true,
                        "image": "guest-img1.svg",
                        "index": 0,
                        "searchFilter": [
                            farmer1
                        ]
                    },
```

Impact: The label is not displaying because of translation method is not working they are expecting the key that should be present in the en.properties file.



so I have added the `frmelmnts.lbl.teacher=Teacher` key in en.properites file

then impact



on select of first user type flow is not breaking ita moving to second popup name as “**Grain and oilseed farms”**

BMGS popup is apperars BMGS is hardcorded .based on framework selection it should give the framework cateogories instead of BMGS hardcorded

To Achieve this below result . I have removed the hardcorde BMGS form the code base.

on framework selection api is called in response we are getting the cateogories associated with this

These below object we are gettnig from the framework read api

The below object can be used for postion indexing, Label, Placeholder

```
     "identifier": "agriculture_framework_commercialcrops",
        "code": "commercialcrops",
        "translations": null,
        "name": "commercialcrops",
        "description": null,
        "index": 2,
        "status": "Live",
```

The below object can be used for dropdown value

```
 
        "terms": [
            {
                "associations": [
                  ...  
                ],
                // dropdown 1
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
                "associations": [...],
               // dropdown 2
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

    },
```

* &#x20;

