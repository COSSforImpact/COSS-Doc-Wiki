---
icon: elementor
---

# Background Network Queue Sync Service

## Introduction and Problem Statement <a href="#introduction-and-problem-statement" id="introduction-and-problem-statement"></a>

#### Intro: <a href="#intro" id="intro"></a>

This documents describes the proposed design for tackling data sync over http for mobile client.

#### Problem: <a href="#problem" id="problem"></a>

* Mobile client collects, aggregates and persists data that periodically gets sync’ed to the server. This data has no significance to the UI and is never queried and rendered. The sync is still initiated and resolved on the same main UI thread impacting performance.
* Furthermore, this data is isolated into multiple sync pipelines corresponding to their sources. Some pipelines identified so far would be - telemetry sync, course state sync and assessment state sync. Each pipeline would raise its own coroutine again impacting performance and resources.

## Proposed Solution <a href="#proposed-solution" id="proposed-solution"></a>

* To build and utilise a native Cordova plugin raising its own process for sync pipelines. This would free the Webview process and improve performance.
* To implement an abstract network queue as a priority queue. The only action applied on aggregated data is a network call to sync client data to server, this can be achieved with a single pipeline with single responsibility of data sync irrespective of data type using a priority queue. This unifies existing pipelines and is also extensible for any future pipelines.

## Cordova Plugin Design <a href="#cordova-plugin-design" id="cordova-plugin-design"></a>

* TODO

## Network Queue Design <a href="#network-queue-design" id="network-queue-design"></a>

* In order for the Queue to be extensible. The Queue can hold generic Network Http Requests.
* The Queue needs to retain state, will handle mutations by persisting and querying a DB implementation.

#### Database DDL <a href="#database-ddl" id="database-ddl"></a>

* Proposed DB Schema for persistence -

<figure><img src="../../../../.gitbook/assets/Screenshot 2020-03-11 at 5.39.22 PM.png" alt=""><figcaption></figcaption></figure>

* The Queue would prioritise over the field ‘priority’ and if equal would prioritise over lesser ‘timestamp’

#### Service API <a href="#service-api" id="service-api"></a>

* The Queue API should not be coupled with any specific data-sync-type rather to type Network Request that wrap all data-sync-type(s)
* Sensitive data like tokens should not be persisted, alternatively flags can be used
* Proposed interface -

Open Screenshot 2020-03-11 at 5.42.39 PM.png![](blob:https://project-sunbird.atlassian.net/4b4ab204-5e3c-434e-a5df-c09cbde703b6#media-blob-url=true\&id=c9c7a20d-59b4-4925-9964-402dd15eb085\&collection=contentId-1300889670\&contextId=1300889670\&mimeType=image%2Fpng\&name=Screenshot%202020-03-11%20at%205.42.39%20PM.png\&size=174267\&width=602\&height=361\&alt=)

<figure><img src="../../../../.gitbook/assets/Screenshot 2020-03-11 at 5.42.39 PM.png" alt=""><figcaption></figcaption></figure>

* Following flow diagram represent queue method trigger points and sync flow -

Open Screenshot 2020-03-11 at 2.39.38 PM.png\


<figure><img src="../../../../.gitbook/assets/Screenshot 2020-03-11 at 2.39.38 PM.png" alt=""><figcaption></figcaption></figure>
