---
icon: elementor
---

# Knowledge Platform License Support

### Problem Definition <a href="#knowledgeplatformlicensesupport-problemdefinition" id="knowledgeplatformlicensesupport-problemdefinition"></a>

Knowledge Platform should support multiple types of License.

* License should be passed by the Creator of the content.
* If the license is not passed by user, default license for the tenant should be considered for the content.
* If tenant is also not having any default license, content should be linked with system specific default license.

### Problem statement <a href="#knowledgeplatformlicensesupport-problemstatement" id="knowledgeplatformlicensesupport-problemstatement"></a>

* Each content should be linked to the license value.
* License can have list of attributes, like, name, description and url.

### Implementation Design <a href="#knowledgeplatformlicensesupport-implementationdesign" id="knowledgeplatformlicensesupport-implementationdesign"></a>

**License should be added as object in Knowledge Platform data store**

* License can be added frequently and it will have some other metadata properties as well.
* So the license will be added as Object in KP data store with relevant metadata properties like, name, description and url.
* Using license name, we will generate identifier, so the name will be unique.
* License can be created, updated, read and retire.
* Once license Created, updated or retired - license cache will be reset with the list of license name.
* License cache will be utilised in content-license validation and channel-defaultLicense validation.
* Since license name can not be updated, we need not to do any content license value migration during license update.
* While retiring license - license cache will be updated and (**NEED DISCUSSION:** content tagged with the license can be updated with default license value).

**Channel will have default license value**

* As part of channel create and update API, default license can be added as metadata.
* **defaultLicense** is not mandatory field.
* if **defaultLicense** is coming in channel create or update request, it will be validated against the list of license list coming from the cache
* If license cache is not available - fetch list of live license, validated default license and set license cache.

**Content will be tagged with license as text**

* License validation will be handled in Graph engine layer by using trait.
* In content schema, license will be of type String.
* In config.json, we will have licenseValidation as true.
* LicenseValidator (trait) will have validation implementation which will execute license specific validation (if licenseValidation is true).
* Content Create (KP 2.0)
  * if license is part of request - it will get validated from the list of license coming in the cache (if cache is not available - fetch list of license, validate license and set cache).
  * if license is not part of request - channel's defaultLicense will be passed as license value (channel object will be coming from cache - if cache is not available - fetch channel from data store, set defaultLicense and set channel cache).
  * if channel also have no defaultLicense - system configured default license value will be passed as license value.
* Update API (KP 2.0)
  * if license is part of request - it will get validated from the list of license coming in the cache (if cache is not available - fetch list of license, validate license and set cache).
  * if license is not part of request and content does not have license - channel's defaultLicense will be passed as license value (channel object will be coming from cache - if cache is not available - fetch channel from data store, set defaultLicense and set channel cache).
  * if channel also have no defaultLicense - system configured default license value will be passed as license value.
  * if the content is copied content (having origin field) - license can not be updated.
  * if the content id copied content (having origin field) - origin can not be updated **(This is additional implementation)**
* Content Upload API
  * only for youtube content - license value will be updated with youtube specific license.
* Content Copy API (KP 1.0)
  * copied content will be having same license value of origin content.
  * if request contains license value, we will throw client exception.
