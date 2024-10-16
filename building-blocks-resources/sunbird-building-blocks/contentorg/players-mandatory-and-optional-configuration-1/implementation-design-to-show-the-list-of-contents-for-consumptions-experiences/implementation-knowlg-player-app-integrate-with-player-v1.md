---
icon: elementor
---

# Implementation - Knowlg player app integrate with player V1

## Background <a href="#implementation-knowlgplayerappintegratewithplayerv1-background" id="implementation-knowlgplayerappintegratewithplayerv1-background"></a>

Currently, we are showing pdf, epub, and video players in the knowledge player app. To display the interactive, HTML, h5p, and youtube content, we need to integrate the v1 player in the knowledge player app.

## Design <a href="#implementation-knowlgplayerappintegratewithplayerv1-design" id="implementation-knowlgplayerappintegratewithplayerv1-design"></a>

To integrate the v1 player for the knowledge app we need some changes in the following component

### `services/data.ts` <a href="#implementation-knowlgplayerappintegratewithplayerv1-services-data.ts" id="implementation-knowlgplayerappintegratewithplayerv1-services-data.ts"></a>

Old code:

```
playersArray: [{
        name: 'pdf',
        mimeType: 'pdf'}]
```

Changes:

```
playersArray: [{
        name: 'pdf', // Name to display
        mimeType: 'application/pdf', // Actul mimeType for search api call
        playerType: 'pdf', // to get the player info
        playerRedirectURL: "players/pdf" // for routing 
      },
      {
        name: 'epub',
        mimeType: 'application/epub',
        playerType: 'epub',
        playerRedirectURL: "player/pdf"
      },
      {
        name: 'video',
        mimeType: '["video/mp4"]',
        playerType: 'video',
        playerRedirectURL: "player/pdf"
      },
      {
        name: 'ecml',
        mimeType: 'application/vnd.ekstep.ecml-archive',
        playerType: 'ecml',
        playerRedirectURL: "player/ecml"
      },
      {
        name: 'html',
        mimeType: 'application/vnd.ekstep.html-archive',
        playerType: 'html',
        playerRedirectURL: "player/html"
      }
```

### `services/content.service.ts` <a href="#implementation-knowlgplayerappintegratewithplayerv1-services-content.service.ts" id="implementation-knowlgplayerappintegratewithplayerv1-services-content.service.ts"></a>

```
getMimeType(playerType){
      return data.playersArray['playerType'].mimeType;
}
playerRedirectURL(playerType: string){
      return data.playersArray['playerType'].playerRedirectURL;
  }
```

***

### Redirect to the V1 and v2 player <a href="#implementation-knowlgplayerappintegratewithplayerv1-redirecttothev1andv2player" id="implementation-knowlgplayerappintegratewithplayerv1-redirecttothev1andv2player"></a>

#### Solution 1: <a href="#implementation-knowlgplayerappintegratewithplayerv1-solution1" id="implementation-knowlgplayerappintegratewithplayerv1-solution1"></a>

Create the New component for the v1 player

`player-routing.module.ts` (existing routing module change)

```
{
    path: 'player/interactive/:mimeType/:id', component: playerv1Component,
}
```

`v1-player.component.html`

```
<iframe #preview id="contentPlayer" src="/content/preview/preview.html?webview=true"></iframe>
```

`v1-player.component.ts`

```
 @ViewChild('preview', { static: false }) previewElement: ElementRef;
....
ngAfterViewInit() {
    this.previewElement.nativeElement.onload = () => {
        this.previewElement.nativeElement.contentWindow.initializePreview(this.playerConfig);
        this.previewElement.nativeElement.contentWindow.addEventListener('message', resp => {
         ....
         };
    };
  }
  
  ....

ngOnInit(): void {
    // get queryParams.identifier
    // set the content metadata
  }
```

**Pros:**

* Easy to maintain - easy to differentiate the config between the v1 and v2 player
* Easy to redirect and get the action on different types of events

**Cons:**

* Need to maintain a separate component for the v1 player

#### Solution 2: <a href="#implementation-knowlgplayerappintegratewithplayerv1-solution2" id="implementation-knowlgplayerappintegratewithplayerv1-solution2"></a>

Add one more player in the lib-player

`player-routing.module.ts` (existing routing module change)

```
{
    path: 'player/:mimeType/:id', component: playerv1Component,
}
```

### `lib-player` component <a href="#implementation-knowlgplayerappintegratewithplayerv1-lib-playercomponent" id="implementation-knowlgplayerappintegratewithplayerv1-lib-playercomponent"></a>

* `player.component.html`

```
<div *ngSwitchCase="'application/vnd.ekstep.ecml-archive'" class="player">
        ...
        <iframe #preview id="contentPlayer" src="/content/preview/preview.html?webview=true"></iframe>
    </div>
```

* `player.component.ts`

```
  ngAfterViewInit() {
    this.previewElement.nativeElement.onload = () => {
        this.previewElement.nativeElement.contentWindow.initializePreview(this.playerConfig);
        this.previewElement.nativeElement.contentWindow.addEventListener('message', resp => {
         ....
         };
    };
  }
```

**Pros:**

* No need to create the separate component

**Cons:**

* Difficult to maintain - if we need to switch the different versions of the player for the same mimeType

## Conclusion <a href="#implementation-knowlgplayerappintegratewithplayerv1-conclusion" id="implementation-knowlgplayerappintegratewithplayerv1-conclusion"></a>

* Combine the two solutions to create a separate component (v1-player) in the shared module.
