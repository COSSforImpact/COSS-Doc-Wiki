---
icon: elementor
---

# Notifications PRD

Notifications PRD

### Overview <a href="#pbhh2vme3uex" id="pbhh2vme3uex"></a>

Notifications are a mechanism of informing users of system about various events that might be of interest to them. It is a way of ensuring required workflow steps or change in states are notified to relevant users for them to take required actions. It can also act as reminders to bring users back to the app (mobile/web). They can be used to entice users about new features/content available within the product and to promote the most engaging content to users.

This document details requirements related all notifications provided by the system. Notifications product consists of:

1. Base Infrastructure to send notifications along with supported channels, and its configurability.
2. User Cases where specific events generate specific set of notifications.

### Detailed Features <a href="#id-82ku1ihv7v01" id="id-82ku1ihv7v01"></a>

### Infrastructure <a href="#k2ejl9asi5y5" id="k2ejl9asi5y5"></a>

#### Delivery Channels <a href="#tpxxkxundz4v" id="tpxxkxundz4v"></a>

Notifications can be delivered through following channels (in that order of priority for implementation):

1. Email
2. Mobile App
3. SMS
4. Web App

#### Notification Events <a href="#i0o8x63jqpdy" id="i0o8x63jqpdy"></a>

System provides notifications for a default list of events based on common use cases supported by Sunbird. A specific installation can, if required, configure only a subset of these events for notifications. Any new notifications will have to be created as an extension.

#### Notification Templates <a href="#tnh366ii11h4" id="tnh366ii11h4"></a>

Each event that sends notification will have an associated notification template for each delivery channel that specifies the format of notification. System generates a notification based on the provided template.

Template will have certain information auto-populated from the event related data. These can be specified using a predefined separator (to be designed) within the template.

#### System Configurations <a href="#djjng7n4u9nd" id="djjng7n4u9nd"></a>

Notifications infrastructure provides a set of system configurations that can be configured per instance of sunbird deployment to customize the behaviour of the notifications.

Following are the set of configurations that can be configured:

1. Predefined list of delivery channels through which notifications are sent. Each instance can enable a subset of these delivery channels.
2. A predefined list of events that can generate notifications. Each instance can configure a subset of these events for which notification needs to be sent. Notifications for certain events are mandatory (such as for “Sent for Review”, “Flagging” etc.). Notifications for certain events are optional (such as for Announcements?). Optional notifications can be set on or off by users.
3. Customize Notification Template for each event and notification mechanism. Each combination of notification event and mechanism will have a predefined template to send the notification. Certain parts of the template will be customizable by each instance.

#### User Preferences <a href="#e4in0nm9wxbg" id="e4in0nm9wxbg"></a>

User can also set certain preferences with respect to Notifications. Following are the preferences that user can set or modify:

1. Preferred Delivery Channels - Subset of available delivery channels on which they like to receive notifications. Notifications will be sent to that user only through that channel. There should be atleast one delivery channel set. Email can be set as preferred delivery channel only if email is present in the user profile. SMS can be set as preferred delivery channel only if phone number is present in the profile.
2. Turn off or on notifications to events that are optional.

There may be further user preferences specific to a use case that will be detailed out under each of the use cases separately.

#### Consumption of Notifications <a href="#mjyiio9m70kv" id="mjyiio9m70kv"></a>

**Email**

User receives an email on the registered email id in her profile. If there is no email configured, no notification is delivered through that channel.

The email notification will typically have a link to some page ( on both mobile and web app) clicking on which will take user to corresponding page on mobile or web app (based on the clicked link).

**SMS**

User receives SMS on the registered phone number in her profile. If there is no phone number configured, no notification is delivered through that channel.

The SMS will typically have a link to some page ( on both mobile and web app) clicking on which will take user to corresponding page on mobile or web app (based on the clicked link).

**On Mobile App**

TBD - UI

**On Web App**

TBD - UI

#### Telemetry Requirements <a href="#rq9vd8w975s" id="rq9vd8w975s"></a>

Need to have the following measurable:

1. Sending of a notification
2. Receipt of a notification at the client
3. Opening of client via notification

Need to generate following reports (on a delivery means, and daily/weekly level):

1. Number of notifications sent - for each event type
2. Unique user count that notifications were sent to - for each event type
3. Total notifications that were opened - for each event type and delivery channel

#### Non-Functional Requirements <a href="#td36pe8pi7en" id="td36pe8pi7en"></a>

**Latency**:

Notification should be generated after the event completion and not before or during it. So for example if a user gets notification that a content has been published & click on it, it should take the user to content & content should show in published list.

**Localization**

It should be possible to receive emails, push notifications in local Indian languages.

### Use Cases <a href="#j5ljb3wmayi8" id="j5ljb3wmayi8"></a>

| **Use Case**             | **Event**                                                                                | **Users to be notified**                        | **Information to be part of the notification** |
| ------------------------ | ---------------------------------------------------------------------------------------- | ----------------------------------------------- | ---------------------------------------------- |
| Review                   | Content “Sent for Review”                                                                | All reviewers of that channel                   |                                                |
| Review                   | Content sent for “Request Changes”                                                       | Content Author                                  |                                                |
| Review                   | Content is “Published”                                                                   | Content Author                                  |                                                |
| Flagging                 | Content is “Flagged”                                                                     | Content Author, Flag Reviews of that channel    |                                                |
| Flagging                 | Content Flag is “Accepted”                                                               | Content Author                                  |                                                |
| Flagging                 | Content Flag is “Rejected”                                                               | Content Author                                  |                                                |
| Flagging                 | Flagged Content is “Sent for Review”                                                     | All Flag Reviewers of that channel              |                                                |
| Flagging                 | Content sent for “Request Changes”                                                       | Content Author                                  |                                                |
| Flagging                 | Content is “Published”                                                                   | Content Author                                  |                                                |
| Badging                  | Badge is issued to a User                                                                | User to whom the badge is issued                |                                                |
| Content                  | Delete / retire / archive                                                                | Content Author                                  |                                                |
| User Comments on content | User provides comments after playing a content                                           | Content Author                                  |                                                |
| Admin                    | New role assigned                                                                        | User to which the role is assigned              |                                                |
| Course                   | Batch enrolment                                                                          | Mentor                                          | New participant enrolled                       |
| Course                   | Batch enrolment                                                                          | Participant                                     | Enrollment successful                          |
| Course                   | Batch starting                                                                           | Participant & Mentor                            |                                                |
| Course                   | Batch ending                                                                             | Participant & Mentor                            |                                                |
| App (retention)          | Push notifications based on age of users (e.g. D1, D3, D7, gap of 2 days since use etc.) | Any app user                                    |                                                |
| App (local)              | Automated, local rules to show a notification to user (especially offline)               | App users without needing internet connectivity |                                                |
| Announcements            | When an announcement is received on device                                               | Users belonging to an org                       |                                                |
|                          |                                                                                          |                                                 |                                                |

### Release Plan <a href="#id-5ttvzk6c4em0" id="id-5ttvzk6c4em0"></a>

### Miscellaneous <a href="#rcaoptfg0wdh" id="rcaoptfg0wdh"></a>

Admins should be able to see a dashboard of user count of who received the notification, and read it (at least on email).

Ability to see old notifications (and status of read/unread).

Configuration of what a notification contains (only text, text and images, text and images and call-to-action etc.)

Subscription for notifications (specially for reviewers)

Also refer to:

[https://docs.google.com/document/d/1TD0AJSu0rPPePUcVCpjnyz0F\_GtwHIPS\_CxyW8DzdE8/edit#heading=h.qk7vq07zcl5t](https://docs.google.com/document/d/1TD0AJSu0rPPePUcVCpjnyz0F\_GtwHIPS\_CxyW8DzdE8/edit#heading=h.qk7vq07zcl5t)
