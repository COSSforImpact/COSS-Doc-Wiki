---
icon: elementor
---

# Cordova to Capacitor Migration

### Introduction: <a href="#cordovatocapacitormigration-introduction" id="cordovatocapacitormigration-introduction"></a>

This document is about using Capacitor over Cordova plugin for ionic applications, and creating a custom capacitor plugin.&#x20;

### Background: <a href="#cordovatocapacitormigration-background" id="cordovatocapacitormigration-background"></a>

Ionic 5 has a support for both Cordova and Capacitor to Build native-powered app experiences with collection of open source and premium plugins and integrations that make it easy to add native device functionality to any Ionic app with Capacitor or Cordova.&#x20;

These days most of the developers are moving to the Capacitor, as it has more stable plugins than Cordova, and Apache has stopped support for the Cordova platform. &#x20;

### Problem Statement: <a href="#cordovatocapacitormigration-problemstatement" id="cordovatocapacitormigration-problemstatement"></a>

Currently, Sunbird-Ed mobile app is using Ionic 6. Since Cordova is not maintained by the Apache team anymore and now capacitor is default on Ionic framework. as Cordova is not supported by Apache and is maintained under some community member as awesome-cordova-plugin.\
Since Sunbird-Ed is following the Open-Source approach, it is necessary that the codebase should be updated with capacitor for Long-term stability.&#x20;

Capacitor is [backed by Ionic](https://ionicframework.com/), a long-term contributor to Cordova and the larger open source ecosystem. Ionic still uses Cordova heavily and will continue to invest in the platform for a long time to come. It's backward-compatible with Cordova, so you can comfortably switch your existing web apps to it whenever you're ready. Capacitor was designed from the start to support the rich Cordova plugin ecosystem out of the box. Thus, using Cordova plugins in Capacitor is easy.&#x20;

### Design: <a href="#cordovatocapacitormigration-design" id="cordovatocapacitormigration-design"></a>

Add native functionality to your app with Capacitor, a native runtime built by the Ionic team. Install the core packages and easily add them to your project. Capacitor has a wide range of capabilities that developers can use to access features like the device file system, camera, and native location services. All of this is powered by a unified TypeScript API that automatically handles platform differences.&#x20;

**Capacitor — How is it different from Cordova?**&#x20;

This is relevant to application working with Ionic / Cordova. Cordova has been the only choice available for Ionic app developers for quite some time. Cordova helps build an Ionic web app into a device installable app.&#x20;

**Capacitor is very similar to Cordova, but with some key differences in the app workflow**&#x20;

Here are the differences between Cordova and Capacitor &#x20;

* Capacitor considers each platform project a _source asset_ instead of a _build time asset_. That means Capacitor wants you to keep the platform source code in the repository, unlike Cordova which always assumes that you will generate the platform code on build time&#x20;
* Because of the above, Capacitor does not use config.xml or a similar custom configuration for platform settings. Instead, configuration changes are made by editing AndroidManifest.xml for Android and Info.plist for Xcode&#x20;
* Capacitor does not “run on device” or emulate through the command line. Instead, such operations occur through the platform-specific IDE. So you cannot run an Ionic-capacitor app using a command like ionic run ios . You will have to run iOS apps using _Xcode_, and Android apps using _Android studio_&#x20;
* Since platform code is not a _source asset,_ you can directly change the native code using Xcode or Android Studio. This give more flexibility to developers&#x20;

In essence, Capacitor is like a fresh, more flexible version of Cordova.&#x20;

The plugins used in Sunbird-ED mobile app needs to migration from Cordova to Capacitor

* `sb-cordova-plugin-customtabs`
* `sb-cordova-plugin-db`
* `sb-cordova-plugin-sync`
* `sb-cordova-plugin-utility`
* `sb-cordova-plugin-dowloadmanager`
* `jjdltc-cordova-plugin`
* `cordova-plugin-sunbirdsplash`

1.  Install package and platform in capacitor\
    `npm install @capacitor/android` `npx cap add android`

    `npm install @capacitor/ios` `npx cap add ios`
2. On Android, the SDKs also require the following permissions in the `AndroidManifest.xml` \
   On **iOS**, add the `config description` key to the `ios/App/App/Info.plist` file, which tells the user why the app needs to use.
3. Run the app on specific platform\
   `npx ionic cap run android`\
   `npx ionic cap run ios`

### Installing Capacitor in a new Ionic Project[​](https://capacitorjs.com/docs/getting-started/with-ionic#installing-capacitor-in-a-new-ionic-project) <a href="#cordovatocapacitormigration-installingcapacitorinanewionicproject" id="cordovatocapacitormigration-installingcapacitorinanewionicproject"></a>

For new Ionic projects, Capacitor is already installed in new Ionic apps by default! All you have to do is start a new project. To create a new Ionic project, run the following command:\
`ionic start <app_name>`

### Installing Capacitor to an existing Ionic Project[​](https://capacitorjs.com/docs/getting-started/with-ionic#installing-capacitor-to-an-existing-ionic-project) <a href="#cordovatocapacitormigration-installingcapacitortoanexistingionicproject" id="cordovatocapacitormigration-installingcapacitortoanexistingionicproject"></a>

If you have an existing Ionic project that doesn't have Capacitor enabled, you can enable Capacitor by running the following command.\
`ionic integrations enable capacitor`

#### Install Capacitor Plugin Dependencies[​](https://capacitorjs.com/docs/getting-started/with-ionic#install-capacitor-plugin-dependencies) <a href="#cordovatocapacitormigration-installcapacitorplugindependencies" id="cordovatocapacitormigration-installcapacitorplugindependencies"></a>

Ionic Framework makes use of the APIs in the following Capacitor plugins:

* `@capacitor/app`
* `@capacitor/haptics`
* `@capacitor/keyboard`
* `@capacitor/status-bar`

For the best user experience, you should make sure these plugins are installed even if you don't import them in your app. To install these plugins, run the following command in the root of your project:\
`npm i @capacitor/app @capacitor/haptics @capacitor/keyboard @capacitor/status-bar`

#### Add Platforms[​](https://capacitorjs.com/docs/getting-started/with-ionic#add-platforms) <a href="#cordovatocapacitormigration-addplatforms" id="cordovatocapacitormigration-addplatforms"></a>

After Capacitor installed and its plugins are installed, you can add mobile platforms to your app:\
`ionic capacitor add android`\
`ionic capacitor add ios`

This will create a new directory in the root of your project for the native platform. This directory is a native project that should be considered a source artifact.

**Info**

If your Ionic app uses Cordova, we have a guide on how to [migrate from Cordova to Capacitor](https://capacitorjs.com/docs/cordova/migrating-from-cordova-to-capacitor) as well.

### Ionic CLI Capacitor Commands[​](https://capacitorjs.com/docs/getting-started/with-ionic#ionic-cli-capacitor-commands) <a href="#cordovatocapacitormigration-ionicclicapacitorcommands" id="cordovatocapacitormigration-ionicclicapacitorcommands"></a>

The Ionic CLI has a variety of high-level commands that wrap the Capacitor CLI for convenience. See the documentation for each below. Help output is also available by using the `--help` flag after each command.

* `ionic capacitor add`
* `ionic capacitor build`
* `ionic capacitor run`
* `ionic capacitor sync`
* `ionic capacitor open`

**Sample project structure for ionic capacitor project**



Platform Capacitor **ANDROID** structure



Platform Capacitor **IOS** structure



### Reference links: <a href="#cordovatocapacitormigration-referencelinks" id="cordovatocapacitormigration-referencelinks"></a>

[https://ionic.io/blog/a-new-chapter-for-ionic-native](https://ionic.io/blog/a-new-chapter-for-ionic-native)\
[https://ionic.io/blog/capacitor-everything-youve-ever-wanted-to-know](https://ionic.io/blog/capacitor-everything-youve-ever-wanted-to-know)

[https://capacitorjs.com/cordova](https://capacitorjs.com/cordova)\
[https://capacitorjs.com/docs/getting-started/with-ionic](https://capacitorjs.com/docs/getting-started/with-ionic)
