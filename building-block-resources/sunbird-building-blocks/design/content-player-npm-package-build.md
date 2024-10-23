---
icon: elementor
---

# Content-Player: NPM Package build

### Introduction: <a href="#content-player-npmpackagebuild-introduction" id="content-player-npmpackagebuild-introduction"></a>

This document details the content-player npm package build process

### Background <a href="#content-player-npmpackagebuild-background" id="content-player-npmpackagebuild-background"></a>

Content-Player is common module/product used to preview/play the content/question in Portal, Mobile, offline desktop, Editors & Question(editors). The build process of these products to package content-player is different. This process in not automatic for all the application. Because of manual process of sharing the content-player build, some times latest content-player changes are not present in the mobile or portal or offline production build. So we need to stream line the build & packaging process of content-player for Portal, Mobile, offline desktop & editor applications.

### Problem Statement: <a href="#content-player-npmpackagebuild-problemstatement" id="content-player-npmpackagebuild-problemstatement"></a>

1. Automate the build & packaging process of content-player build for all the comsumer applications like Mobile, Portal, Offline desktop, Editors etc..
2. Prodcution build of Mobile, Portal, Offline dekstop & Editors should have always latest version of the content-player specific to release.

### Key Design Problems <a href="#content-player-npmpackagebuild-keydesignproblems" id="content-player-npmpackagebuild-keydesignproblems"></a>

1. How to build content-player which is publicly accessible to all the consumer applications?
2. How to get packaging process of content-player(latest changes specific to release) for all the consumer applications?
3. How to maintain the versioning of content-player specific to each release?

### Design 1: <a href="#content-player-npmpackagebuild-design1" id="content-player-npmpackagebuild-design1"></a>

Use NPM build process for content-player

[https://www.npmjs.com/package/@project-sunbird/content-player](https://www.npmjs.com/package/@project-sunbird/content-player)

\


**Dev:** Any PR is merged to content-player repo, cotent-player npm module will be pushed with the alpha version(prerelease version - **alpha**).

**Staging:** While staging deployment of content-player, content-player npm module will be published with Beta version(release version - **beta**).

**Prod:**  While staging deployment of content-player, content-player npm module will be published with specific release version number(ex: 2.6.0). Any hot-fixes on content-player(prodcution) will get npm publish by updating the patch version (ex: 2.6.1)

\


NPM versioning format: [https://docs.npmjs.com/cli/version](https://docs.npmjs.com/cli/version)

Semantic version format: [://docs.npmjs.com/misc/semver](https://docs.npmjs.com/misc/semver)

\


Note:

1. While pushing the build to prod, all consumption products of content-player has to define the specific version of the content-player npm module in the package.json file. So that any hot-fix deployments of consumption products/modules, will not take the latest version of the content-player.

\


### Design 2: <a href="#content-player-npmpackagebuild-design2" id="content-player-npmpackagebuild-design2"></a>

Pushing latest version of the content-player to CDN/public repo.

\


**Dev**: Taking it from dev preview cdn latest ZIP

**Staging**: Taking it from staging preview cdn latest ZIP

**Pre-prod**: Taking it from pre-prod preview cdn latest ZIP

**Prod**: Taking it from prod preview cdn latest ZIP

\


\


\


\


\
