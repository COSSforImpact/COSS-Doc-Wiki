---
icon: elementor
---

# Tagging Content with multiple subjects, mediums and grades

We have a challenge from the mobile app i.e. when we enable tagging content with multiple subjects, mediums and grades the apps will crash because it is assuming the data type. After the discussion, we will approach this problem as below.

1. Mobile App and Portal team will make the changes to do not have any assumptions on the datatype of metadata properties - [+Anil Gupta](mailto:anil.gupta@tarento.com) [+Rajeev](mailto:rajeev.sathish@tarento.com)&#x20;
2. Knowledge Platform team will do below changes - [+Amit Priyadarshi](mailto:amitp@ilimi.in)&#x20;
3.
   * Update the datatype to List for the subject, medium and grade properties.
   * Data migration - String to List.
   * Search and Read Content API response to return as a string (To support existing the mobile app). It should be configurable.&#x20;
   *
     * Based on configuration the API response will return either String or List for these properties. Default to String.
     * When most of the mobiles in the field updated to the version with mobile app fix (item 1) this configuration will be updated to send List as value for these properties. - [+Joel Johnson](mailto:joel@ekstep.org) will confirm this.
4. Content-Framework and Sunbird Platform team will make the changes to send List for the subject, medium and grade for Content update APIs - [+Manzarul Haque](mailto:manzarul.haque@tarento.com) [+Kartheek Palla](mailto:kartheekp@ilimi.in)&#x20;
