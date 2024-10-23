---
icon: elementor
---

# \[ED-Portal]: Framework Agnostics Release: 7.0.0

* Introduction
  * Key Configuration Considerations:
  * Main Form Configurations:
  * Points to Remember for Adopters:
* Form: user\_\_update\_\_framework
* Form: contentcategory\_global\_menubar (exclude All Tab filter Configuration)
* Form: contentcategory\_global\_menubar (All Tab , Group, mydownloads Filter Configuration)
* Form: customResourcebundles\_list\_global
* Form: Schemas\_get\_search
* Form: config\_get\_segmentation\_v2
* Form API : System setting for UserProfile userProfileConfig
* Reference links

### **Introduction** <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-introduction" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-introduction"></a>

This documentation guides on implementing new frameworks within the Sunbird education platform, emphasizing flexibility and minimal code changes. By following this documentation, users will gain an understanding of key configurations and form configurations necessary for introducing a new framework with new categories in their infrastructure.

#### **Key Configuration Considerations:** <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-keyconfigurationconsiderations" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-keyconfigurationconsiderations"></a>

1. **Form Configuration Preference:** Users are encouraged to prioritize form configuration over code changes when implementing a new framework. This approach ensures adaptability and ease of integration.

#### **Main Form Configurations:** <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-mainformconfigurations" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-mainformconfigurations"></a>

The following form configurations play a crucial role in stabilizing the portal's functionality:

**Onboarding Popup:** Utilize the `user__update__framework` form configuration for the framework selection screen during the onboarding process.

**Tab-Level Search Filter (Except All Tab Screen):** Configure the tab-level(page-level) search filter, excluding the All tab screen, using the `contentcategory_global_menubar` and `SearchFilterConfig` forms.

**Global Search Filter (All Tab Screen):** Customize the global search filter for the All Tab screen using the `contentcategory_global_menubar` and `globalFilterConfig` forms.

**Category Label Screen:** Display category labels on screens by configuring the customResourcebundles\_list\_global form.

**Schemas**: add the search schemas by configuring the `schemas`\_`get`\_`search`

These form configurations are instrumental in ensuring the stability and functionality of the Sunbird platform when introducing new frameworks and categories.

**Banner configuration** : Configuring banners in home page `config`\_`get`\_`segmentation_v2`

**System setting for UserProfile**: This system setting allows user to add the newly added framework values into the database. `{{host}}/api/data/v1/system/settings/set`

#### Points to Remember for Adopters: <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-pointstorememberforadopters" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-pointstorememberforadopters"></a>

* If this configuration is not created, category data will be fetched from the framework read call.
* For existing frameworks, if a new framework is introduced, users have to create this configuration based on rootOrgID and framework input.
* Ensure that the `code` metadata value corresponds to the framework categories code to maintain the functionality of the framework selection dropdown.

### [Form: user\_\_update\_\_framework](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#Framework-Selection-Screen--Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference) <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-form-user__update__framework" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-form-user__update__framework"></a>

This form is utilized to configure the user framework selection screen, allowing users to customize it according to their requirements. When introducing a new framework, users must configure this form using the rootOrgId and framework-based inputs.

Screenshot :: FrameWork Selection Screen

When configuring this form, ensure that the `code` metadata value is referenced from the framework categories code. Failure to do so may result in the framework selection dropdown malfunctioning or behaving improperly.

Form API Ref Link: [Framework Selection Screen Form Configuration for Sunbird ED (BMGS) Reference](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#Framework-Selection-Screen--Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference)

### [Form: contentcategory\_global\_menubar (exclude All Tab filter Configuration)](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#Menu-Bar-Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference) <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-form-contentcategory_global_menubar-excludealltabfilter" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-form-contentcategory_global_menubar-excludealltabfilter"></a>

This form plays a crucial role in configuring multiple features within the Sunbird platform, particularly in organizing and managing the top bar menu tabs. Each tab within the top bar is configured within this form, with specific metadata defining its position and functionality.

Screenshot :: Page-Level Search Filter

**Fields:**

* **Index Metadata:** Defines the position of the tab within the menu bar.
* **Facets Metadata:** Specifies metadata for search API responses, particularly regarding content facets. Facets key-value pairs are utilized to organize search results, such as categorizing content by organization.
* **Filters Metadata:** Determines the default filters applied when clicking on a tab, specifying primary categories and additional filters for relevant data retrieval.
* **Theme-related Information:** Configuration options related to the visual theme of the tab.
* **loggedInUserRoute Key:** Specifies routes to be loaded for logged-in users.
* **anonymousUserRoute Key:** Specifies routes to be loaded for anonymous users.
* **MetaData Key:**
  1. **Default Filters:** Allows users to set default filters upon clicking the tab.
  2. **SearchFilterConfig Metadata:** Contains page-level filter configurations, essential for displaying filter dropdowns within individual tabs. Users can customize this object according to their requirements, ensuring alignment with the framework category code.

**Note:** if a user intends to incorporate a new filter alongside the framework categories dropdown, along with customizing the label name, the following steps should be followed:

1. Create a new object inside the **searchFilterConfig** metadata.
2. Assign the **dataSource** property of the new object as "facet".

This approach allows users to seamlessly integrate additional filters into the existing framework, ensuring flexibility and customization according to their specific requirements.

Sample Object of the SearchFilter

```
{
    "category": "use framework code",
    "type": "dropdown",
    "placeholderText": "Use placeholder name",
    "defaultPlaceholderText": "Use default placeholder name",
    "dataSource": "framework",
    "multiple": false // Change to true for multiple selection
}
```

**Note:** Ensure that the category specified in the searchFilter aligns with the framework category code to avoid issues with page-level filter functionality.

**Additional Metadata:**

* **Filter Key:** Supports filters to be passed in the search API call upon tab click.

This form's configurations are vital for organizing and customizing the top bar menu tabs, enhancing the user experience and facilitating efficient content navigation within the Sunbird platform.

### [Form: contentcategory\_global\_menubar (All Tab , Group, mydownloads Filter Configuration)](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#Menu-Bar-Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference) <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-form-contentcategory_global_menubar-alltab-group-mydown" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-form-contentcategory_global_menubar-alltab-group-mydown"></a>

Screenshot :: All Tab Search FilterScreenshot :: Group Page Search Filter

The All tab configuration within the contentcategory\_global\_menubar form exhibits similar behavior to other tabs but with minor differences, particularly in filter configurations. Instead of utilizing the **searchFilterConfig**, the **globalFilterConfig** is used. Here are the key specifications:

1. **Index Key:** Defines the positioning of dropdowns within the All tab.
2. **"code" Metadata:** This metadata is crucial as the value of the code must match the framework categories. Mismatched codes may lead to issues in the filter dropdowns.
3. **"alternativeCode":** Introduced in Sunbird release 6.0.0, this metadata serves as an alternative code for categories like se\_boards, which may not have a reference in the framework read call. Users need to provide mappings for such categories within the alternativeCode metadata.
4. **Type Metadata:** Used to differentiate between framework and filter categories.
5. **Label and Placeholder:** Utilize default labels and placeholders, which work only for English language. For supporting multiple languages, configure the regional config accordingly.

**Note:** If a user intends to incorporate a new filter alongside the framework categories dropdown, along with customizing the label name, the following steps should be followed:

1. Create a new object inside the **globalFilterConfig** metadata.
2. Assign the **type** property of the new object as "filter".

This approach allows users to seamlessly integrate additional filters into the existing framework, ensuring flexibility and customization according to their specific requirements.

Sample Object of globalFilterConfig:

```
{
    "index": 1,
    "code": "your_framework_category_code",
    "alternativeCode": "use_target_framework_category_code",
    "label": "Your Label",
    "placeHolder": "Your Placeholder",
    "translation": "{\"en\":\"Foodcrops\"}",
    "type": "framework" // or "filter" to differentiate between framework and filter categories
}
```

These configurations ensure the proper functioning of the All tab, allowing users to efficiently navigate and filter content within the Sunbird platform.

Form API Ref Link: [Menu-Bar Form Configuration for Sunbird ED (BMGS) Reference](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#Menu-Bar-Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference)

### [Form: customResourcebundles\_list\_global](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#CustomResourcebundles-Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference) <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-form-customresourcebundles_list_global" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-form-customresourcebundles_list_global"></a>

The form serves as a central configuration point for defining framework category labels, allowing adopters to map the desired labels to be used within the portal. This flexibility enables adopters to align the framework category labels with their organizational terminology or specific requirements.

Screenshot :: Category Label

Adopters can utilize this form to:

* Update existing framework category labels.
* Create new mappings for additional framework categories as needed.
* Customize labels to better reflect the terminology used within their organization or context.

Overall, the customResourcebundles\_list form empowers adopters to tailor framework category labels according to their preferences, ensuring alignment with their unique framework configurations and enhancing the user experience within the portal.\


Form API Ref Link: [CustomResourcebundles Form Configuration for Sunbird ED (BMGS) Reference](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#CustomResourcebundles-Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference)

### [Form: Schemas\_get\_search](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#Schemas\_get\_search-Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference) <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-form-schemas_get_search" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-form-schemas_get_search"></a>

The form is utilized to configure the schema keywords employed within the portal for content search. In the event that new keywords are introduced in Sunbird ED, adopters are required to add these keys and update the form accordingly.

Form API Ref Link: [Schemas\_get\_search Form Configuration for Sunbird ED (BMGS) Reference](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#Schemas\_get\_search-Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference)

### [Form: config\_get\_segmentation\_v2](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#Config\_\_get\_\_segmentation\_v2-Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference%5BhardBreak%5D) <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-form-config_get_segmentation_v2" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-form-config_get_segmentation_v2"></a>

The Form is used to create segmentation for notifications and banner. In the event that new framework keywords are introduced in Sunbird ED, adopters are required to add these keys and update the form accordingly.

Screenshot :: Banner



Form API Ref Link: [Config\_\_get\_\_segmentation\_v2 Form Configuration for Sunbird ED (BMGS) Reference](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3398729734/ED-Portal+Config+Changes+as+per+the+BMGS+Hardcoded+Removal#Config\_\_get\_\_segmentation\_v2-Form-Configuration-for-Sunbird-ED-\(BMGS\)-Reference%5BhardBreak%5D)

### &#x20;Form API : System setting for UserProfile `userProfileConfig`  <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-formapi-systemsettingforuserprofileuserprofileconfig" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-formapi-systemsettingforuserprofileuserprofileconfig"></a>

This system setting allows user to add the newly added framework values into the database.\
\{{host\}}/api/data/v1/system/settings/set\
Add the new framework category in the request body as below in framework section

Sample API Reference \{{host\}}/api/data/v1/system/settings/set

```
{
    "request": {
        "id": "userProfileConfig",
        "field": "userProfileConfig",
        "value": "{\"fields\":[\"firstName\",\"lastName\",\"profileSummary\",\"avatar\",\"countryCode\",\"dob\",\"email\",\"gender\",\"grade\",\"language\",\"location\",\"phone\",\"subject\",\"userName\",\"webPages\",\"jobProfile\",\"address\",\"education\",\"skills\",\"badgeAssertions\"],\"publicFields\":[\"firstName\",\"lastName\",\"profileSummary\",\"userName\"],\"privateFields\":[\"email\",\"phone\"],\"csv\":{\"supportedColumns\":{\"NAME\":\"firstName\",\"MOBILE PHONE\":\"phone\",\"EMAIL\":\"email\",\"SCHOOL ID\":\"orgId\",\"USER_TYPE\":\"userType\",\"ROLES\":\"roles\",\"USER ID\":\"userId\",\"SCHOOL EXTERNAL ID\":\"orgExternalId\"},\"outputColumns\":{\"userId\":\"USER ID\",\"firstName\":\"NAME\",\"phone\":\"MOBILE PHONE\",\"email\":\"EMAIL\",\"orgId\":\"SCHOOL ID\",\"orgName\":\"SCHOOL NAME\",\"userType\":\"USER_TYPE\",\"orgExternalId\":\"SCHOOL EXTERNAL ID\"},\"outputColumnsOrder\":[\"userId\",\"firstName\",\"phone\",\"email\",\"organisationId\",\"orgName\",\"userType\",\"orgExternalId\"],\"mandatoryColumns\":[\"firstName\",\"userType\",\"roles\"]},\"read\":{\"excludedFields\":[\"avatar\",\"jobProfile\",\"address\",\"education\",\"webPages\",\"skills\"]},\"framework\":{\"fields\":[\"board\",\"gradeLevel\",\"medium\",\"subject\",\"id\",\"category1\",\"category2\",\"category3\",\"category4\",\"commercialcrops\",\"foodcrops\",\"livestockmanagement\",\"livestockspecies\",\"farmingtype\",\"cropcategory\",\"croptype\",\"cropname\"],\"mandatoryFields\":[\"id\"]}}"
    }
}
```

### **Reference links** <a href="#id-ed-portal-frameworkagnosticsrelease-7.0.0-referencelinks" id="id-ed-portal-frameworkagnosticsrelease-7.0.0-referencelinks"></a>

Jira Ticket: [ED-3042: \[ED-Portal\]: Generic implementation of Hardcoded BMGS IN DEVELOPMENT](https://project-sunbird.atlassian.net/browse/ED-3042)

GitHub PR Link : [ED-3042 feat : \[ED-Portal\]: Generic implementation of Hardcoded BMGS by princegupta1131 · Pull Request #9063 · Sunbird-Ed/SunbirdEd-portal](https://github.com/Sunbird-Ed/SunbirdEd-portal/pull/9063)

Design Docs: [\[ED-Portal\] DC: Design-Docs for Hardcoded BMGS removal](broken-reference)

Gap Analysis Docs : [Sunbird-ED: Gap Analysis Docs for BMGS](https://project-sunbird.atlassian.net/wiki/spaces/SUN/pages/3369369685)
