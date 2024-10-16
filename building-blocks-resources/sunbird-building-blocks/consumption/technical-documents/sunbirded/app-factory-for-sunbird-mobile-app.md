---
icon: elementor
---

# App factory for Sunbird Mobile App

### Introduction <a href="#appfactoryforsunbirdmobileapp-introduction" id="appfactoryforsunbirdmobileapp-introduction"></a>

This document talks about the ease of generating Sunbird Mobile app artifacts by the adopters.

### Background: <a href="#appfactoryforsunbirdmobileapp-background" id="appfactoryforsunbirdmobileapp-background"></a>

Current Sunbird Mobile app setup and build generation require multiple frameworks like Ionic, Node, Angular, Java, Gradle for Android, XCode for ios, etc to be installed in the local machine if an adopter who has basic setup configurations ready in the local machine but doesn't have mobile expertise will face difficulties in generating app artifacts.

### Problem Statement: <a href="#appfactoryforsunbirdmobileapp-problemstatement" id="appfactoryforsunbirdmobileapp-problemstatement"></a>

Now to set up Sunbird mobile app on the local machine we have to install the following frameworks

| Package                                                                     | Version | Recommended Version |
| --------------------------------------------------------------------------- | ------- | ------------------- |
| [Node](https://nodejs.org/en/)                                              | 12+     | 12.22.10            |
| [NPM](https://nodejs.org/en/)                                               | 6+      | 6.14.16             |
| [Cordova](https://cordova.apache.org/)                                      | 10+     | 10.1.2              |
| [Ionic](https://ionicframework.com/docs/intro/cli)                          | 5       | 5.7.0               |
| [Java(For Android)](https://www.oracle.com/in/java/technologies/downloads/) | 11+     | 11.0.15.1           |
| [Gradle(For Android)](https://gradle.org/install/)                          | 7+      | 7.0.2               |
| [CocoaPods(For Ios)](https://cocoapods.org/)                                | 1.11.3  |                     |

If an adopter who wants to explore the capabilities of the Sunbird Mobile App, installing all these frameworks can be a cumbersome process.

### Key Design Problems <a href="#appfactoryforsunbirdmobileapp-keydesignproblems" id="appfactoryforsunbirdmobileapp-keydesignproblems"></a>

* Configurable
* Ease of availability of mobile app artifacts

### Design <a href="#appfactoryforsunbirdmobileapp-design" id="appfactoryforsunbirdmobileapp-design"></a>

To eliminate all these problems, a Jenkins job should be there that will take a few configurations as input and provide mobile artifacts as output.

The configurations are as follows

| S No | Config                                                                                                                                           | Description                                                                                                                                                                             |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | build-extras.gradle(only for Android builds)                                                                                                     | Gradle file required to build android app                                                                                                                                               |
| 2    | <p>config</p><ul><li>config.json</li><li>local_notification_config.json</li><li>whitelabel.xml</li></ul>                                         | <ul><li>config.json - Contains all onboarding/tab config</li><li>local_notification_config.json - Contains notification confi</li><li>whitelabel.xml - Contains splash config</li></ul> |
| 3    | google-services.json                                                                                                                             | Google firebase configuraion                                                                                                                                                            |
| 4    | i18n                                                                                                                                             | Localization assets                                                                                                                                                                     |
| 5    | local\_cache\_download\_config.json                                                                                                              | config to download bundles for offline support in app                                                                                                                                   |
| 6    | <p>resources</p><ul><li>ic_launcher.png</li><li>splash (drawable-hdpi-splash.png, drawable-ldpi-splash.png, drawable-xhdpi-splash.png)</li></ul> | <ul><li>ic_launcher.png - App icon</li><li>splash - Splash icons</li></ul>                                                                                                              |
| 7    | <p>signingConfig</p><ul><li>build.json</li><li>sample.jks</li></ul>                                                                              | <ul><li>build.json - certificate config</li><li>sample.jks - sample certificate</li></ul>                                                                                               |
| 8    | sunbird.properties                                                                                                                               | Contains all the properties reuired to configure sunbird app.                                                                                                                           |

* All these configurations will be pushed to the public GitHub so that adopters can take reference.

### Jenkins Job <a href="#appfactoryforsunbirdmobileapp-jenkinsjob" id="appfactoryforsunbirdmobileapp-jenkinsjob"></a>

* The Jenkins job will have two inputs

1. Sunbird mobile app release GitHub tag
2. App factory Github tag

![](../../../../../.gitbook/assets/3346628624.png)

Once “Build“ is clicked the App factory will copy all adopter-specific assets into the Sunbird Mobile app code and start building the app.

### Adoptor flow <a href="#appfactoryforsunbirdmobileapp-adoptorflow" id="appfactoryforsunbirdmobileapp-adoptorflow"></a>

**Design -1**

* The adopters will take the Jenkins instance and host it.

1. The adopters can clone the App factory repo and push their configurations.
2. Run the job

**Design -2**

* Sunbird will host the Jenkins

1. The adapters will have to register themselves in Sunbird.
2. Sunbird team will create one branch in the App factory repo.
3. The adopters will contribute to that specific branch.
4. One entry will be added in the Jenkins flow with the adopter's name.
5. Sunbird team can run the job.
