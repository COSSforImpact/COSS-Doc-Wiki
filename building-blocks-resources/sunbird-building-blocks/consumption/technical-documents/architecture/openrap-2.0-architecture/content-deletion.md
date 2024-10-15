---
icon: elementor
---

# Content deletion

### Background <a href="#contentdeletion-background" id="contentdeletion-background"></a>

There is a need to provide the option for content delete in the desktop app so that the user can manage the space in his machine and it should be designed such a way that the deletion should be performed in async fashion so that  app main thread is not blocked because of content delete in case of  large contents and user can have smooth experience.

\


![](https://project-sunbird.atlassian.net/wiki/download/thumbnails/1121517612/content%20delete.png?version=1\&modificationDate=1573728161586\&cacheVersion=1\&api=v2\&width=632\&height=591)

\


\


### Migration <a href="#contentdeletion-migration" id="contentdeletion-migration"></a>

\


we will be adding a new key in content's **desktopAppMetadata**  to know whether the content is available offline or now for this we need to migrate the content DB to insert new key and migration script will be part of openrap-sunbirded-plugin and it will be executed before the plugin starts for the first time as a first step and migration script will be stored in the plugin with below\
\


| `openrap-sunbirded-plugin -migration     - script.js` |
| ----------------------------------------------------- |

The script will be updated in subsequent include last release script for migration so that unexpected upgrade of the app won't have the issue that is of a user updates app from 1.0.0 to 3.0.0 it contains the 2.0.0 migration script

\


### Schema <a href="#contentdeletion-schema" id="contentdeletion-schema"></a>

delete\_queue

| `{id: String,fileId?: StringfileLocation: String,createdOn: Date,updatedOn: Date}` |
| ---------------------------------------------------------------------------------- |

\


### Telemetry Events   <a href="#contentdeletion-telemetryevents" id="contentdeletion-telemetryevents"></a>

\


Delete button click interact event with content as an object

LOG  event for the delete API call

LOG event for each content delete

ERROR event for error in deleting the content

### Open Question <a href="#contentdeletion-openquestion" id="contentdeletion-openquestion"></a>

Do we need to have content audit DB for content operations?
