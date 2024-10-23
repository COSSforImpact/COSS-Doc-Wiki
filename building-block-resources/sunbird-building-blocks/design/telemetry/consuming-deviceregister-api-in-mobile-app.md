---
icon: elementor
---

# Consuming DeviceRegister API in mobile app

### **Introduction:**  <a href="#consumingdeviceregisterapiinmobileapp-introduction" id="consumingdeviceregisterapiinmobileapp-introduction"></a>

This wiki explains how DeviceRegister API will be consumed in mobile app

### **Background:** <a href="#consumingdeviceregisterapiinmobileapp-background" id="consumingdeviceregisterapiinmobileapp-background"></a>

DeviceRegister API is used for capturing the IP address details and the device specifications on both mobile and web platforms.

### **Problem Statement:** <a href="#consumingdeviceregisterapiinmobileapp-problemstatement" id="consumingdeviceregisterapiinmobileapp-problemstatement"></a>

DeviceRegister API should be called before telemetry sync API every 24 hrs(TTL).

### **Solution :**    <a href="#consumingdeviceregisterapiinmobileapp-solution" id="consumingdeviceregisterapiinmobileapp-solution"></a>

* In GenieSDK Sync api will be invoked after getting success/ failure response from DeviceRegister API.
* In case of success response current epoch timestamp will be stored in the preference, so every time sync API is invoked it will check the time stamp and decide whether to call the DeviceRegister API or not depending on the TTL.
* In case of a failure response, invoke sync API.

\


### **Conclusion** <a href="#consumingdeviceregisterapiinmobileapp-conclusion" id="consumingdeviceregisterapiinmobileapp-conclusion"></a>

* Make the TTL configurable.
* Store epoch time stamp+ttl  so that every time there shouldn't any date conversion to check if its greater than the specified date.

\


&#x20;[Mathew Pallan](https://project-sunbird.atlassian.net/wiki/people/5a0147f1c24efb3c4ed42ac8?ref=confluence)  [Anil Gupta](https://project-sunbird.atlassian.net/wiki/people/557058:4ed203bb-a6b6-40d5-b9a7-25bdb0d6e6b5?ref=confluence)  [Souvik Mondal](https://project-sunbird.atlassian.net/wiki/people/59f6be7a068cd6328f4642f9?ref=confluence) [Shriharsh Saboji](https://project-sunbird.atlassian.net/wiki/people/557058:750d7c92-f316-41dd-8135-77e3e0fa832a?ref=confluence)

\


\
