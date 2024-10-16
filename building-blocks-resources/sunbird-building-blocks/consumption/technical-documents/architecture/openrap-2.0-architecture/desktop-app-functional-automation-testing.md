---
icon: elementor
---

# Desktop app functional automation testing

### **Introduction**:  <a href="#introduction" id="introduction"></a>

Desktop App testing should be automated by writing integration tests. The benefits of this are the following:

* Faster Feedback
* Accelerated Results
* Testing Efficiency Improvement
* Higher Overall Test Coverage
* Reusability of Automated Tests
* Earlier Detection of Defects
* Thoroughness in Testing

### **Testing framework:** <a href="#testing-framework" id="testing-framework"></a>

We choose [Spectron](https://github.com/electron-userland/spectron/blob/master/README.md) to automate the test cases since this is created by the electron team and our app is based on the electron. Spectron is nothing but wraps WebdriverIO which shown below picture\
Mocha will be the test runner used and chai will be the assertion library which used in the official documentation and popular libraries for testing BDD or TDD.

&#x20;

Open Functional\_automation\_spectron.jpg![](blob:https://project-sunbird.atlassian.net/f153d61d-ea6d-4f7d-a808-004c2c20478e#media-blob-url=true\&id=22640d79-db4f-480d-9f8d-02a4b03d95cf\&collection=contentId-1359151105\&contextId=1359151105\&mimeType=image%2Fjpeg\&name=Functional\_automation\_spectron.jpg\&size=52388\&width=590\&height=406\&alt=)

<figure><img src="../../../../../../.gitbook/assets/Functional_automation_spectron (2).jpg" alt=""><figcaption></figcaption></figure>

&#x20;

&#x20;

### **Pattern used:** <a href="#pattern-used" id="pattern-used"></a>

**Page Object Model and Page Factory -** Page object is a design pattern that can be implemented as selenium best practices. The functionality classes (PageObjects) in this design represent a logical relationship between the pages of the application.

* The Page Object pattern represents the screens of your web app as a series of objects and encapsulates the features represented by a page.
* It allows us to model the UI in our tests.
* A page object is an object-oriented class that serves as an interface to a page of your AUT.

Some of the advantages of page object pattern as listed below,

* Reduces the duplication of code
* &#x20;Makes tests more readable and robust
* Improves the maintainability of tests, particularly when there is frequent change in the AUT. (Useful in Agile methodology based projects)

&#x20;

### **Folder Structure:** <a href="#folder-structure" id="folder-structure"></a>

&#x20;

`<app_base_dir> /test /data /content_1.ecar /config.json // This file contains data to be passed to the test cases /pages /Page.ts // This is base page for factory implementation /OnboadingPage.ts /ContentDownloadPage.ts /ContentImportPage.ts /ContentDeletePage.ts /ContentPlayPage.ts /TelemetryPage.ts /specs /OnboadingPage.test.ts /ContentDownloadPage.test.ts /ContentImportPage.test.ts /ContentDeletePage.test.ts /ContentPlayPage.test.ts /TelemetryPage.test.ts test.spec.ts utils.ts // which container methods to start and stop the app`

&#x20;

Since we need to execute the tests in a certain order we will export the test files and import them in test.spec.ts in a specific order so that they will execute in that order.
