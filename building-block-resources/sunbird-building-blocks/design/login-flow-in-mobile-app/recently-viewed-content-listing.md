---
icon: elementor
---

# Recently Viewed Content Listing

### Overview:  <a href="#recentlyviewedcontentlisting-overview" id="recentlyviewedcontentlisting-overview"></a>

When user plays any content should list on **Recently Viewed** list.

### Problem statement:  <a href="#recentlyviewedcontentlisting-problemstatement" id="recentlyviewedcontentlisting-problemstatement"></a>

When user plays any content from book then is listing in Recently Viewed list, but when user plays any content by clicking next and previous from player, its not listing.

### Current Implementation: <a href="#recentlyviewedcontentlisting-currentimplementation" id="recentlyviewedcontentlisting-currentimplementation"></a>

* When user clicks on play button in app, calling the SDK API **setContentMarker**. In this API passing the **userid, contentid** and **content metadata** in request body.

### Scenarios: <a href="#recentlyviewedcontentlisting-scenarios" id="recentlyviewedcontentlisting-scenarios"></a>

* Play from content detail page.
* Play from flatten screen after DIAL code scan search.
* Next and previous button click from player.
* Switch user from player.

### Proposed Design: <a href="#recentlyviewedcontentlisting-proposeddesign" id="recentlyviewedcontentlisting-proposeddesign"></a>

**Solution 1:**

* Listen the START event for pid: contentplayer and then call the **setContentMarker** in one common place. And remove from play button click.

**Solution 2:**

* Call the **setContentMarker** as it is from play button click from app.
* Call the same API on next and previous click from player.

### Pros and Cons: <a href="#recentlyviewedcontentlisting-prosandcons" id="recentlyviewedcontentlisting-prosandcons"></a>

| Solution | Pros                                                                                                                   | Cons                                                  |
| -------- | ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| 1        | <ul><li>API call will happen only from one place.</li><li>Switch user scenario from player will be handled. </li></ul> | <p><br></p>                                           |
| 2        | <p><br></p>                                                                                                            | <ul><li>Need to handle from all the places.</li></ul> |

\


\
