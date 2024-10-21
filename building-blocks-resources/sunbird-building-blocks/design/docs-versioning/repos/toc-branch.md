---
icon: elementor
---

# toc branch

### TOC branch will contain <a href="#tocbranch-tocbranchwillcontain" id="tocbranch-tocbranchwillcontain"></a>

```
index.html
widgets.json
robots.txt
css/
js/
images/
```

### Widgets <a href="#tocbranch-widgets" id="tocbranch-widgets"></a>

**Types**&#x20;

1. Version Switcher ( versions dropdown )
2. Notification - latest version available on prior versions.

**Widget working**

1. Widgets will consume data from the widgets.json file.
2. widgets.js file generates HTML for widgets and appends them in the empty widget placeholder divs.

### widgets.json <a href="#tocbranch-widgets.json" id="tocbranch-widgets.json"></a>

* It will provide data to the widgets
* Whenever a new version doc is added or removed, this file will have to be updated.&#x20;

\


```
{
   "versions": [

                       {
                            "version": "2.0",
                            "latest": true
                       },
                       {
                            "version": "1.9",
                            "latest": false
                      },
                      {
                            "version": "1.8",
                           "latest": false
                      }
                 ]
}
```

### Note <a href="#tocbranch-note" id="tocbranch-note"></a>

* **robots.txt**  - If any of the version is unpublished, then that directory will have to be disallowed to be indexed in Search engines.

**Related Issues**

### [SB-5499](https://project-sunbird.atlassian.net/browse/SB-5499?src=confmacro) <a href="#tocbranch-systemjirakey-summary-type-created-updated-due-assignee-reporter-priority-status-resolutio" id="tocbranch-systemjirakey-summary-type-created-updated-due-assignee-reporter-priority-status-resolutio"></a>

[SB-5588](https://project-sunbird.atlassian.net/browse/SB-5588?src=confmacro)
