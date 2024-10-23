---
icon: folder-open
---

# Capturing usage of features for analysis

### **Introduction** <a href="#capturingusageoffeaturesforanalysis-introduction" id="capturingusageoffeaturesforanalysis-introduction"></a>

In this wiki, we will discuss an approach to compute usage of various features across different components. The usage of features can be captured using telemetry events and then subsequently used for analysis of different feature usage. We will discuss the following computations as part of this wiki

* Approach for computation of feature for existing features.
* Approach for capturing required details for feature usage computation for new features.

### **Solution:** <a href="#capturingusageoffeaturesforanalysis-solution" id="capturingusageoffeaturesforanalysis-solution"></a>

**Description:**  The usage of various features can be directly derived from telemetry events after defining a structure for instrumenting the usage of features. A data product summariser will operate on the telemetry events to compute the feature usage data. The usage data can then be indexed into Druid for further visualisation or analysis.

\


&#x20;  **Event Flow:**    &#x20;

&#x20;   &#x20;

&#x20;     **Event Name:   FEATURE**

&#x20;&#x20;

&#x20;     **Event Data Structure:**

Feature Event Object

```
{
	id:"Feature Identifier", //required
	name:"Editor Undo Redo", // Optional
	description:"", // Optional
    version:"1.0", // Version of the feature
	releasedversion:"15.0", // Required, In which version of product having this featureId
	category:"SunbirdEd" //  Optional, Defined this feature is related to SunbirdEd or SunbirdCore (Ex: SunbirdEd or SunbirdCore)
	duration:"42343", //Optional, Time spent in second 
	
}
```

\


### **Existing features usage computation:** <a href="#capturingusageoffeaturesforanalysis-existingfeaturesusagecomputation" id="capturingusageoffeaturesforanalysis-existingfeaturesusagecomputation"></a>

&#x20;

| <p><br></p> | Feature                                 | Event Name | Properties                                                                                                                                                                                                                                                                                                               |
| ----------- | --------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1           | Youtube video in the ECML Content       | INTERACT   | <p>actor.type='User'</p><p>context.env='contenteditor'</p><p>object.type='content'</p><p>edata.type='select'</p><p>edata.plugin.id='org.ekstep.video'</p>                                                                                                                                                                |
| 2           | Question Plugin                         | INTERACT   | <p>actor.type='User'</p><p>context.env='contenteditor'</p><p>object.type='content'</p><p>edata.type='click'</p><p><a href="http://edata.id">edata.id</a>='button'</p><p>edata.subtype='select'</p><p><a href="http://edata.plugin.id">edata.plugin.id</a>='org.ekstep.questionbank'</p>                                  |
| 3           | Content suggestion in textbook          | INTERACT   | <p>actor.type='User'</p><p>context.env='contenteditor'</p><p>object.type='content'</p><p>edata.type='click'</p><p><a href="http://edata.id">edata.id</a>='button'</p><p>edata.subtype='select'</p><p>edata.plugin.id='org.ekstep.suggestioncontent'</p><p><br></p>                                                       |
| 4           | Math symbol and formula                 | INTERACT   | <p>actor.type='User'</p><p>context.env='contenteditor'</p><p>object.type='content'</p><p>edata.type='TOUCH'</p><p><a href="http://edata.id">edata.id</a>='input'</p><p>edata.pageid='question-creation-mcq-form'</p><p><a href="http://edata.plugin.id">edata.plugin.id</a>='org.ekstep.questionunit.mcq'</p><p><br></p> |
| 5           | Assessment summariser in the mobile app | IMPRESSION | <p>actor.type='User'</p><p>context.env='reports-users-group'</p><p>edata.pageid='user'</p><p>edata.uri='user'</p><p>edata.type='view'</p><p><br></p><p><br></p>                                                                                                                                                          |
| 6           | User Groups in mobile app               | IMPRESSION | <p>actor.type='User'</p><p>context.env='user'</p><p>edata.pageid='users-groups'</p><p>edata.uri='users-groups'</p><p>edata.type='view'</p>                                                                                                                                                                               |

\


\


### Conclusion: <a href="#capturingusageoffeaturesforanalysis-conclusion" id="capturingusageoffeaturesforanalysis-conclusion"></a>

\


\* Instead of generating new `FEATURE` event object from the upstream component, generate a `INREACT` Event with cdata object having featureId with this we can compute the feature usage.

\* For the existing features, Implement data product to compute the feature usage only if the computation is not possible from the druid.

\


\


### &#x20; <a href="#capturingusageoffeaturesforanalysis" id="capturingusageoffeaturesforanalysis"></a>

\


\


\


\
