---
icon: folder-open
---

# Content Meta data filters

* At present if want to filter content based on its meta data in sunbird portal,we have set those filters (like mimeType,contentType,createdBy) from portal/client side itself.
* In certain context content meta data filters should be set outside of client side.&#x20;

**Content Meta Filtering**

To avoid setting all content meta data filtering from client side Content meta filtering should do the followings:

* provision to set content meta filters configuration at content service layer through environment variables or service or wizard
* checking and decorating request filters at run time based on above content meta filters configuration

**Enviroment variables method**

&#x20;For content meta data filtering we use environment variables

1. `sunbird_content_metadata_filter = <meta-data-attribute=value>&<meta-data-attribute=value>&<meta-data-attribute=value>`

The '&' symbol is used as a seperator incase of multiple configurations.

\


#### Search Query Composition for content meta data <a href="#contentmetadatafilters-searchquerycompositionforcontentmetadata" id="contentmetadatafilters-searchquerycompositionforcontentmetadata"></a>

\
