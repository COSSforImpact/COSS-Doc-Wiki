---
icon: elementor
---

# Richtext WYSIWYG Design

**Introduction**

The richtext element created on content-editor should be rendered same in content-renderer.

**Background**

**Reference -** [**SB-7213**](https://project-sunbird.atlassian.net/browse/SB-7213?src=confmacro)

Right now Richtext plugin doesn't support WYSIWYG in device as well as portal, preview seen on device is not same as what user created on editor.

There are lot of factor which affect the WYSIWYG of richtext on both device & browser.

\


**Problem Statement**

1. Richtext Editor is using **semantic ui** and in Renderer it is using **ionic framework**, there is conflict on css

&#x20;         For Ex - Semantic is using **H tags** in **EM** but ionic is using it in **PX.**

&#x20;         Because of these css, conflict's are available which is breaking WYSIWYG.

&#x20;        **Solution -** To overcome the css conflict override the ionic css of richtext element to same as semantic css in renderer side.

&#x20;                 Editor will pass the overridden css to renderer as richtext element attributes.

&#x20;     2\. Each device is setting the text zoom level to some percentage which is different that exact percentage(100%) thus resizing the font size.

&#x20;         **Solution -** Using cordova plugin "[**phonegap-plugin-mobile-accessibility**](https://github.com/phonegap/phonegap-mobile-accessibility)" is allowing us to set font zoomlevel to 100%.

&#x20;         **Reference** - [https://github.com/ekstep/Genie-Canvas/issues/1267#issuecomment-315975221](https://github.com/ekstep/Genie-Canvas/issues/1267#issuecomment-315975221)

&#x20;     3\. For Richtext font family is not available in css which is fallbacking the font to either browser fallback or device fallback based on the environment.

&#x20;         **Solution -** Add font family dropdown either in sidebar or in ckeditor from where user can select which font they have added.

\


**Advantages**

1. Using cordova plugin allow to set zoom level to 100% in all devices.
2. Css are overridden based on richtext element only so other element should not be affected with added css

\


**Disadvantages**

1. Adding font-family drop-down in sidebar will limit user to add multiple language in single richtext element.

**Conclusion**

1. Create a common css file for richtext which will work on both editor & renderer.
2. Find a way to fix the text zoom of webview, if nothing is found then use this cordova plugin to set zoom level.
3. Add font family drop down in ckeditor & stop fallback of font family to either device fallback font & browser fallback font.
