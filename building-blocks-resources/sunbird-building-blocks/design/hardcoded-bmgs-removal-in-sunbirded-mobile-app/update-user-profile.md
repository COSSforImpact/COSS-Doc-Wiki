---
icon: elementor
---

# Update user profile

### Background: <a href="#updateuserprofile-background" id="updateuserprofile-background"></a>

Jira ticket: [![](https://project-sunbird.atlassian.net/rest/api/2/universal\_avatar/view/type/issuetype/avatar/10316?size=medium)ED-1975](https://project-sunbird.atlassian.net/browse/ED-1975) - Remove hardcoded BMGS from Home page and content consumption Closed

### **Problem Statement :** <a href="#updateuserprofile-problemstatement" id="updateuserprofile-problemstatement"></a>

1. profile should be update by different keys instead of BMGS.
2. how to migrate DB and upgrade local DB insted of BMGS?

Update profile request BMGS to category1, category2, category3 and category4, we are facing some issue from backend.

```
"request": "request": {
  "userId": "155ce3c5-713e-4749-bc1c-95d09c640914",
  "framework": {
    "id": [
      "framework1"
    ],
    "category1": [
      "Category1 Term1"
    ],
    "category2": [
      "Category2 Term1"
    ],
    "category3": [
      "Category3 Term1"
    ]
  }
}
```

**Response:**

```
{
  "id": "api.user.update",
  "ver": "v3",
  "ts": "2023-05-24 11:20:58:043+0000",
  "params": {
    "resmsgid": "8d9f1be63451afa782c6b65a16c409d8",
    "msgid": "8d9f1be63451afa782c6b65a16c409d8",
    "err": "UOS_USRUPD0051",
    "status": "FAILED",
    "errmsg": "Unsupported field framework.category1."
  },
  "responseCode": "CLIENT_ERROR",
  "result": {
    
  }
}
```

Jira ticket: [![](https://project-sunbird.atlassian.net/rest/api/2/universal\_avatar/view/type/issuetype/avatar/10316?size=medium)ED-2124](https://project-sunbird.atlassian.net/browse/ED-2124) - Test update server profile request and response Closed

### **Key Design Problem:** <a href="#updateuserprofile-keydesignproblem" id="updateuserprofile-keydesignproblem"></a>

1. SDK change for DB migration
2. update all request for update profile service in mobile.

**Update Profile:**

**a) Server Profile:**

Now we can use category1, category2, category3 and category4 as update user profile request instead of BMGS.

Example of update profile request.

```
"request": "request": {
  "userId": "155ce3c5-713e-4749-bc1c-95d09c640914",
  "framework": {
    "id": [
      "framework1"
    ],
    "category1": [
      "Category1 Term1"
    ],
    "category2": [
      "Category2 Term1"
    ],
    "category3": [
      "Category3 Term1"
    ]
  }
}
```

**Update Profile for Logged In user:**

Update profile request BMGS to category1, category2, category3 and category4

```
 this.profileService.updateServerProfile(req).toPromise()
```

**Update profile with category\[i] for New Logged in USer:**

Update profile request BMGS to category1, category2, category3 and category4

```
 this.profileService.updateServerProfile(req).toPromise()
```

**Edit Logged In User:**

Update profile request BMGS to category1, category2, category3 and category4

```
 const req: UpdateServerProfileInfoRequest = {
      userId: this.profile.uid,
      framework: {
        id: this.frameworkId,
      }
    };
    req.framework['board'] = [this.boardList.find(board => code === board.code).name];
  req.framework['medium'] = medium;
  req.framework['gradeLevel'] = grade;
  req.framework['subject'] = subjects;
   // req.framework['category1'] = 'categories';
    this.profileService.updateServerProfile(req).toPromise()
```

b) **Local profile DB :**

Update local profile DB keys BMGS to category1, category2, category3 and category4.

The new DB will be created for new user with category1,….category4 but _**for existing user we have to write a migrate code for DB update with category\[i]**_

```
export interface Profile {
    uid: string;
    handle: string;
    createdAt?: number;
    medium?: string[];
    board?: string[];
    subject?: string[];
    profileType: ProfileType;
    grade?: string[];
    syllabus?: string[];
    source: ProfileSource;
    gradeValue?: { [key: string]: any };
    serverProfile?: ServerProfile;
}
```
