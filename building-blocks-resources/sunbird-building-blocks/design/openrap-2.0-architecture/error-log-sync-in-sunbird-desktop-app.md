---
icon: elementor
---

# Error log sync in Sunbird Desktop App

### **Overview:**  <a href="#errorlogsyncinsunbirddesktopapp-overview" id="errorlogsyncinsunbirddesktopapp-overview"></a>

Currently, Deskstop App has a logging system that stores the log in the file system. These logs have the type of log, error message, time-stamp. We can debug the errors locally by accessing the log files.&#x20;

### **Problem  statement:**  <a href="#errorlogsyncinsunbirddesktopapp-problemstatement" id="errorlogsyncinsunbirddesktopapp-problemstatement"></a>

As part of the error log sync to the server, the system should not have the repetitive/duplicate logs, and it should have the required data to make debugging easier. So we should have listed down some possible errors along with there unique `CODE` and `Identifier`

### **Solution:**  <a href="#errorlogsyncinsunbirddesktopapp-solution" id="errorlogsyncinsunbirddesktopapp-solution"></a>

We will list all the possible scenarios where fatal errors might come. Code is a Unique key for error where ID is a combination of the `CODE` and `ID`, where `ID` is an individual attribute for the error such as do\_id, batchId. For better implementation, we can encode `ID` with base64 Encoding.

The following are some Generic errors which may occur during the App lifecycle:

|    | **CODE**                              | **ID**                                  |
| -- | ------------------------------------- | --------------------------------------- |
| 1  | CONTENT\_IMPORT                       | ecar\_filename                          |
| 2  | CONTENT\_IMPORT\_LOW\_DISK\_SPACE     | **`low_disk_space`**                    |
| 3  | CONTENT\_IMPORT\_ECAR\_ADDED\_ALREADY | `ecar_already_added`                    |
| 4  | CONTENT\_EXPORT                       | content\_do\_id                         |
| 5  | CONTENT\_DOWNLOAD                     | content\_do\_id                         |
| 6  | CONTENT\_DOWNLOAD\_LOW\_DISK\_SPACE   | content\_do\_id                         |
| 7  | CONTENT\_DOWNLOAD\_EXTRACT\_FAILED    | content\_do\_id                         |
| 8  | CONTENT\_DELETE                       | content\_do\_id                         |
| 9  | TELEMETRY\_SYNC                       | batchId                                 |
| 10 | TELEMETRY\_IMPORT                     | file\_path                              |
| 11 | TELEMETRY\_EXPORT                     | batch\_ID                               |
| 12 | REPORT\_ISSUE                         | `help_desk_down`                        |
| 13 | FORM\_READ                            | type\_subtype\_action                   |
| 14 | CHANNEL\_READ                         | channel\_id                             |
| 15 | FAQ\_READ                             | language\_code                          |
| 16 | TENANT\_INFO                          | tenant\_id                              |
| 17 | CONTENT\_READ                         | do\_id                                  |
| 18 | COURSE\_HIERARCHY                     | do\_id                                  |
| 19 | DEVICE\_PROFILE                       | device\_profile\_id                     |
| 20 | DIAL\_ASSEMBLE                        | status (online/offline)                 |
| 21 | CONTENT\_SEARCH                       | search\_keyword                         |
| 22 | DESKTOP\_UPDATE                       | `app_update`                            |
| 23 | SYSTEM\_INFO                          | `system_info`                           |
| 24 | CHANGE\_CONTENT\_LOCATION             | `change_content_location`               |
| 25 | USER\_CREATE                          | `user_create`                           |
| 26 | USER\_READ                            | user\_id                                |
| 27 | USER\_UPDATE                          | user\_id                                |
| 28 | LOCATION\_SEARCH                      | location\_keyword                       |
| 29 | LOCATION\_SAVE                        | location\_keyword                       |
| 30 | APP\_START                            | `app_start`                             |
| 31 | APP\_CRASH                            | `app_crash`                             |
| 32 | ELECTRON\_DIALOG                      | req\_id (e.g. '/dialog/content/export') |
| 33 | CRASH\_REPORTER                       | `crash_reporter`                        |
| 34 | UNKNOWN                               | `unknown`                               |
