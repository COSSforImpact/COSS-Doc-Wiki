---
icon: elementor
---

# Sunbird Design : Youtube in ECML

### Introduction <a href="#youtubeinecml-introduction" id="youtubeinecml-introduction"></a>

This page explains the design and implementation to make able to add YouTube videos in between slides while creating content.

### Background <a href="#youtubeinecml-background" id="youtubeinecml-background"></a>

&#x20;When a user is trying to `Add video`, the pop up that contains two tabs – Library and Google Drive shows up where the users can either add videos from their Google drive or from already published Youtube video with CCBY4.0 license.&#x20;



### Problem Statement <a href="#youtubeinecml-problemstatement" id="youtubeinecml-problemstatement"></a>

Currently, in the content editor, a user can add/upload video only from Google drive and Library.

* The process is more complex as the user has to first create a resource with youtube on Generic Editor,
* Get the resource reviewed and published.
* And on Content Editor, search for the desired content and add it to the slides.&#x20;

### Solution 1 - Dedicated API for validation resources at the time of entering Youtube URL <a href="#youtubeinecml-solution1-dedicatedapiforvalidationresourcesatthetimeofenteringyoutubeurl" id="youtubeinecml-solution1-dedicatedapiforvalidationresourcesatthetimeofenteringyoutubeurl"></a>

A dedicated API to validate the license of YouTube video will be used while creating the content.&#x20;

With the help of the video plugin `org.ekstep.video-1.x`, similar to how the upload process of Google Drive videos, a user will be able to add a video through YouTube URLs upon license validation.

When a user gives Youtube URL, it is first validated against the permissible licenses. Based on the validation result, the user is shown a relevant message whether to add/preview or try a different video.

1. On success - Using `org.ekstep.video-1.x`, the user will be able to preview the video and add to the stage
2. On failure - a warning message will be shown.

**API Structure**

```
Request Method: POST
{
"mime-type": "video/x-youtube",
"url": "https://www.youtube.com/watch?v=06atTvwkuJE"
}

Response
{
"licenseType": "",	
"duration":"",
"author": ""
}
```

**Sending for review:**

When the editor sends it for review, the URL validation API is again hit to validate the license of the video and the relevant message is shown.&#x20;

Pros:

1. Content need not be in the review or published state for any sort of validation.
2. A dedicated API will open up the scope to validate any type of content in the future.&#x20;

Cons:

1. There is a limitation in the number of times the GoogleAPI can be accessed.&#x20;
2. Every time the user enters a Youtube URL, a network request happens as many times for license validation

\


### Solution 2 - Dedicated API for validation resources only at the time of reviewing content. <a href="#youtubeinecml-solution2-dedicatedapiforvalidationresourcesonlyatthetimeofreviewingcontent" id="youtubeinecml-solution2-dedicatedapiforvalidationresourcesonlyatthetimeofreviewingcontent"></a>

Once the editor is done creating content and hitting save, then the URL validation happens for all the Youtube videos present in the content.&#x20;

For the Learning Platform to know if the content has to be scanned for Youtube License check, we have to include the meta in the ECML manifest.&#x20;

The meta will include the following:

1. Each Youtube video will be passed as `<media>` tag.
2. `<media>` tag will have `type` set to `youtube`
3. It will also have an attribute called `validate`. -  This will help us validate any content type in the future by just parsing the manifest.&#x20;

**Cons:**

1. If there are many youtube videos inside the content, it will be difficult for the user to identify the invalid video in case of mass validation.
2. The time the editor has taken to create the content will go in vain.&#x20;

### Solution  3- ContentEditor Level API check <a href="#youtubeinecml-solution3-contenteditorlevelapicheck" id="youtubeinecml-solution3-contenteditorlevelapicheck"></a>

In the Content Editor, the GoogleAPI can be directly used as a service to get the license of the entered Youtube URL.&#x20;

1. On success - Using `org.ekstep.video-1.x`, the user will be able to preview the video and add to the stage
2. On failure - a warning message will be shown.

Cons:&#x20;

1. API secret keys will get exposed to public.&#x20;

### Solution  4 - Create a content in the background and mark as flagged.  <a href="#youtubeinecml-solution4-createacontentinthebackgroundandmarkasflagged" id="youtubeinecml-solution4-createacontentinthebackgroundandmarkasflagged"></a>

When the editor is trying to enter YouTube URL, create it as a content in the background and send it for License validation. The created content then will be published and marked as flagged so that it does not show up anywhere else in the platform.

1. On success - Using `org.ekstep.video-1.x`, the user will be able to preview the video and add to the stage
2. On failure - a warning message will be shown.

\


**URL validation from LP team**



**URL validation from LP team**



**Send for review**



\


**Conclusion:**

1. **Create a validate API which internally calls getMetaData API.**
2. **The API will be called at the time when an editor is inputting an URL as well as at the time of Save**
3. **In the ECML Manifest - introduce a new property `youtube` to the attribute `type` in `<media>` tag.**
4. **Create `<media type='youtube'>` while adding YouTube video through via library as well as URL.**
5. **The LP team will have to make sure that any asset of `<media type='youtube'>` is refrained from attempting to download.**

\


\


\


\
