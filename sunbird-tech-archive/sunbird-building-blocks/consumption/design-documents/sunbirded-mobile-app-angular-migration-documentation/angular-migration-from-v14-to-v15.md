---
icon: elementor
---

# Angular Migration from V14 to V15

* Migration Steps
*
  * Migrate the Sunbird -ED Library
  * Update Angular Cli/Core
  * Add Angular Material & CDk
* Reference Link

The purpose of this document is to provide a comprehensive guide for migrating the SunbirdEd-mobile-app from Angular v14 to v15

## Migration Steps <a href="#angularmigrationfromv14tov15-migrationsteps" id="angularmigrationfromv14tov15-migrationsteps"></a>

Before upgrade the application, Angular 15 supports Node.js version: 14.20.x/16.13.x and typescript version >=4.8

### Migrate the Sunbird -ED Library <a href="#angularmigrationfromv14tov15-migratethesunbird-edlibrary" id="angularmigrationfromv14tov15-migratethesunbird-edlibrary"></a>

Update the Sunbird Mobile app related libraries to be compatible with Angular version 15. Below is the list of libraries owned by ED that require updating:

1\.      [Sunbird ED Mobile app](https://github.com/Sunbird-Ed/SunbirdEd-mobile-app/tree/release-8.0.0\_v14)

2\.      [@project-sunbird/common-consumption](https://github.com/Sunbird-Ed/SunbirdEd-consumption-ngcomponents/tree/release-7.0.0\_v13\_bmgs)

3\.      [@project-sunbird/common-form-elements](https://github.com/Sunbird-Ed/SunbirdEd-forms/tree/release-6.0.0\_v14)

4\.      [@project-sunbird/sb-dashlet](https://github.com/Sunbird-Ed/sb-dashlets/tree/V14\_Migration)

5\.      [@project-sunbird/sb-notification](https://github.com/Sunbird-Ed/sb-notification/tree/release-6.0.0\_v14)

6\.      [@project-sunbird/sb-svg2pdf](https://github.com/Sunbird-Ed/sb-svg2pdf/tree/release-6.0.0\_v13)

7\.      [@project-sunbird/discussions-ui](https://github.com/Sunbird-Lern/discussions-UI/tree/release-5.3.0\_v14)

### **Update Angular Cli/Core** <a href="#angularmigrationfromv14tov15-updateangularcli-core" id="angularmigrationfromv14tov15-updateangularcli-core"></a>

Update angular core and cli as v15, Repository should be clean before update angular.

```
ng update @angular/core@15 @angular/cli@15
```

Now, SunbirdEd-libraries are available for angular 15. We can upgrade the below libraries version in our mobile package.json after update angular as V15 in mobile.

```
npm i project-sunbird/common-consumption@8.0.1
```

```
npm i @project-sunbird/common-form-elements@8.0.0
```

```
npm i @project-sunbird/discussions-ui@8.0.0
```

```
npm i @project-sunbird/sb-dashlet@8.0.0
```

```
npm i @project-sunbird/sb-notification@8.0.0
```

```
npm i @project-sunbird/sb-styles@0.0.16
```

```
npm i @project-sunbird/sb-svg2pdf@8.0.1
```

### **Add Angular Material & CDk** <a href="#angularmigrationfromv14tov15-addangularmaterial-and-cdk" id="angularmigrationfromv14tov15-addangularmaterial-and-cdk"></a>

1\.      [@project-sunbird/sb-notification](https://github.com/Sunbird-Ed/sb-notification/tree/release-6.0.0\_v14) and [@project-sunbird/common-form-elements](https://github.com/Sunbird-Ed/SunbirdEd-forms/tree/release-6.0.0\_v14) are depends on angular/material and angular/cdk. So, we have to add below dependencies in our mobile app

```
npm i @angular/material@15 @angular/cdk@15
```

2\. Import “`MatIconModule`" in **notification.module.ts & app.module.ts** file

![](file:///C:/Users/chitranshu/AppData/Local/Packages/oice\_16\_974fa576\_32c1d314\_250c/AC/Temp/msohtmlclip1/01/clip\_image001.png)notification.module.ts

```
import { NgModule } from '@angular/core';
```

```
import { CommonModule } from '@angular/common';
```

```
import { FormsModule } from '@angular/forms';
```

```
import { Routes, RouterModule } from '@angular/router';
```

```
 
```

```
import { IonicModule } from '@ionic/angular';
```

```
import { TranslateModule } from '@ngx-translate/core';
```

```
 
```

```
import { NotificationPage } from './notification.page';
```

```
import { ComponentsModule } from '../components/components.module';
```

```
import { SbNotificationModule } from '@project-sunbird/sb-notification';
```

```
import {MatIconModule} from '@angular/material/icon';
```

```
 
```

```
const routes: Routes = [
```

```
  {
```

```
    path: '',
```

```
    component: NotificationPage
```

```
  }
```

```
];
```

```
 
```

```
@NgModule({
```

```
  imports: [
```

```
    CommonModule,
```

```
    FormsModule,
```

```
    IonicModule,
```

```
    TranslateModule,
```

```
    RouterModule.forChild(routes),
```

```
    ComponentsModule,
```

```
    SbNotificationModule,
```

```
   MatIconModule
```

```
  ],
```

```
  declarations: [NotificationPage]
```

```
})
```

```
export class NotificationPageModule {}
```

3\. Add the below style in notification.page.scss file

![](file:///C:/Users/chitranshu/AppData/Local/Packages/oice\_16\_974fa576\_32c1d314\_250c/AC/Temp/msohtmlclip1/01/clip\_image001.png)notification.page.scss

```
 sb-notification{
```

```
    ::ng-deep{
```

```
      .mat-card-notification {
```

```
        display: flex;
```

```
        flex-wrap: wrap;
```

```
        flex-direction: row;
```

```
        align-items: center;
```

```
        border-radius: 0.5rem;
```

```
        background-color: var(--white);
```

```
        box-shadow: 0.3125rem 0.3125rem 0.125rem 0 rgba(0,0,0,.1);
```

```
    
```

```
        mat-card-subtitle {
```

```
            order: 1;
```

```
            display: flex;
```

```
            align-items: center;
```

```
            color: var(--app-dark-gray);
```

```
            font-size: .75rem;
```

```
    
```

```
            .status {
```

```
                height: 0.5rem;
```

```
                width: 0.5rem;
```

```
                background-color: var(--gray-300);
```

```
                border-radius: 0.5rem;
```

```
                display: inline-block;
```

```
                margin-right: 0.5rem;
```

```
            }
```

```
        }
```

```
    
```

```
        mat-card-title {
```

```
            order: 3;
```

```
            color: var(--primary-color);
```

```
            font-size: .875rem;
```

```
            font-weight: 700;
```

```
            overflow: hidden;
```

```
            text-overflow: ellipsis;
```

```
            white-space: nowrap;
```

```
            flex: 1 0 100%;
```

```
        }
```

```
    
```

```
        mat-card-actions {
```

```
            order: 2;
```

```
            margin-left: auto;
```

```
            min-height: auto !important;
```

```
            padding: 0;
```

```
    
```

```
            button {
```

```
                padding: 0;
```

```
                height: auto;
```

```
                width: auto;
```

```
                box-shadow: none !important;
```

```
    
```

```
                mat-icon {
```

```
                    border-radius: 50%;
```

```
                }
```

```
            }
```

```
        }
```

```
    }
```

```
    }
```

```
  }
```

4.Import the below url in style.scss

```
@import url( 'https://fonts.googleapis.com/css?family=Material+Icons');
```

5.Add the below path inside **style in angular.json file.**

```
"./node_modules/@angular/material/prebuilt-themes/indigo-pink.css",
```

After installed the **“angular/material”** and **“angular/cdk”** you can create a build using the below command in mobile.

```
npm run ionic-build
```

If the **“angular/material”** and **“angular/cdk”** are not install properly, you will get the below error.



<figure><img src="../../../../../../.gitbook/assets/Screenshot from 2024-03-18 17-13-00.png" alt=""><figcaption></figcaption></figure>

## Reference Link

Jira ticket: [ED-3607](https://project-sunbird.atlassian.net/browse/ED-3607) - Getting issue details... STATUS

Angular Update Guide: [https://update.angular.io/?v=14.0-15.0](https://update.angular.io/?v=14.0-15.0)
