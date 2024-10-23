---
icon: elementor
---

# Framework Details.

### Background: <a href="#frameworkdetails.-background" id="frameworkdetails.-background"></a>

Presently BMGS is hardcoded for Framework request. If we want to change this label as category1, category2, category3 and category4 then we have to change the framework request.

Jira ticket: [![](https://project-sunbird.atlassian.net/rest/api/2/universal\_avatar/view/type/issuetype/avatar/10316?size=medium)ED-1959](https://project-sunbird.atlassian.net/browse/ED-1959) - Remove BMGS hardcoded from framework selection page -part1 Closed

### **Problem Statement :** <a href="#frameworkdetails.-problemstatement" id="frameworkdetails.-problemstatement"></a>

1.What is the new API request for getFrameworkDetails? (We invoke the getFrameworkDetails api with default framework(BMGS) to get the framework categories as BMGS but to get categorie for multiple framework what API should call?

1.How to handle different categories for multiple frameworks(framework1-board, medium, grade, subject. framework2-department, block)?

2\. Suppose default framework is framework1. so, it’s showing board, medium and grade label in onboarding page. now we select framework2. Then BMG label will change to department, block or what happen??

3\. If user change framework on profile edit page then BMGS label should change?

### **Key Design Problem:** <a href="#frameworkdetails.-keydesignproblem" id="frameworkdetails.-keydesignproblem"></a>

1. Create a form
2. Store multiple frameworks keys as category1, category2
3. Check the label is updating or not for selected framework

### **Design :** <a href="#frameworkdetails.-design" id="frameworkdetails.-design"></a>

#### **Framework-Details Api’s** <a href="#frameworkdetails.-framework-detailsapis" id="frameworkdetails.-framework-detailsapis"></a>

Update framework api request as category\[i] and we have to change the framework details response categories code also in sunbird SDK.

```
export enum FrameworkCategoryCode {
    BOARD = 'board',
    MEDIUM = 'medium',
    GRADE_LEVEL = 'gradeLevel',
    SUBJECT = 'subject',
    TOPIC = 'topic',
    PURPOSE = 'purpose'
}
```

Now change the framework request **BMGS** to **category\[i]**

```
export enum FrameworkCategoryCode1 {
    CATEGORY1 = 'category1',
    CATEGORY2 = 'category2',
    CATEGORY3 = 'category3',
    CATEGORY4 = 'category4',
    TOPIC = 'topic',
    PURPOSE = 'purpose'
}
```

apiRequest.parameters for new request:

```
{categories: "category1,category2,category3,category4"}
```

Categories Response for category1:

```
 {
                    "identifier": "framework1_category1",
                    "code": "category1",
                    "terms": [
                        {
                            "identifier": "framework1_category1_category1term1",
                            "code": "category1term1",
                            "translations": null,
                            "name": "Category1 Term1",
                            "description": "Category1 Term1",
                            "index": 1,
                            "category": "category1",
                            "status": "Live"
                        }
                    ],
                    "translations": null,
                    "name": "Category1",
                    "description": "Category1",
                    "index": 1,
                    "status": "Live"
        }
```

Remove BMGS hardcoded and use category1 for board, category2 for medium, category3 for gradeLevel and category4 for subject in mobile.

1. **Onboarding :** a) Remove BMGS hardcoded and use category1 for board, category2 for medium and category3 for grade in HTML and TS file.

b. we have to use proper methods and variables name for board, medium and grade(onMediumChange, mediumControl, mediumList )&#x20;

c. Update framework API’s request with category\[i].

`DEFAULT_FRAMEWORK_CATEGORIES` should be category1, category2 and category3

```
const getSuggestedFrameworksRequest: GetSuggestedFrameworksRequest = {
      from: CachedItemRequestSourceFrom.SERVER,
      language: this.translate.currentLang,
      requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
    }
this.frameworkUtilService.getActiveChannelSuggestedFrameworkList(getSuggestedFrameworksRequest).toPromise()
```

```
this.framework = await this.frameworkService.getFrameworkDetails({
            from: CachedItemRequestSourceFrom.SERVER,
            frameworkId: value[0],
            requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
          }).toPromise();
```

Change `FrameworkCategoryCode.BOARD` to `FrameworkCategoryCode.CATEGORY1`

```
const boardCategoryTermsRequet: GetFrameworkCategoryTermsRequest = {
            frameworkId: this.framework.identifier,
            requiredCategories: [FrameworkCategoryCode.BOARD],
            currentCategoryCode: FrameworkCategoryCode.BOARD,
            language: this.translate.currentLang
          };

          const boardTerm = (await this.frameworkUtilService.getFrameworkCategoryTerms(boardCategoryTermsRequet).toPromise())
            .find(b => b.name === (this.syllabusList.find((s) => s.code === value[0]).name || 'other'));
```

Change `FrameworkCategoryCode.MEDIUM` to `FrameworkCategoryCode.CATEGORY2`

```
 const nextCategoryTermsRequet: GetFrameworkCategoryTermsRequest = {
            frameworkId: this.framework.identifier,
            requiredCategories: [FrameworkCategoryCode.MEDIUM],
            prevCategoryCode: FrameworkCategoryCode.BOARD,
            currentCategoryCode: FrameworkCategoryCode.MEDIUM,
            language: this.translate.currentLang,
            selectedTermsCodes: this.boardControl.value
          };

          this.mediumList = (await this.frameworkUtilService.getFrameworkCategoryTerms(nextCategoryTermsRequet).toPromise())
            .map(t => ({ name: t.name, code: t.code }));
```

Change `FrameworkCategoryCode.GRADE_LEVEL` to `FrameworkCategoryCode.CATEGORY3`

```
const nextCategoryTermsRequet: GetFrameworkCategoryTermsRequest = {
            frameworkId: this.framework.identifier,
            requiredCategories: [FrameworkCategoryCode.GRADE_LEVEL],
            prevCategoryCode: FrameworkCategoryCode.MEDIUM,
            currentCategoryCode: FrameworkCategoryCode.GRADE_LEVEL,
            language: this.translate.currentLang,
            selectedTermsCodes: this.mediumControl.value
          };

          this.gradeList = (await this.frameworkUtilService.getFrameworkCategoryTerms(nextCategoryTermsRequet).toPromise())
            .map(t => ({ name: t.name, code: t.code }));
```

2\. **Guest Profile :**

a) Remove BMGS hardcoded and use category1 for board, category2 for medium and category3 for grade in HTML and TS file.

b). Update framework API’s request with category\[i].

`DEFAULT_FRAMEWORK_CATEGORIES` should be category1, category2, category3 and category4

```
const getSuggestedFrameworksRequest: GetSuggestedFrameworksRequest = {
      language: this.translate.currentLang,
      requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
    };
    this.frameworkUtilService.getActiveChannelSuggestedFrameworkList(getSuggestedFrameworksRequest).toPromise()
```

```
 const frameworkDetailsRequest: FrameworkDetailsRequest = {
      frameworkId: (this.profile && this.profile.syllabus && this.profile.syllabus[0]) ? this.profile.syllabus[0] : '',
      requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
    };
    this.frameworkService.getFrameworkDetails(frameworkDetailsRequest).toPromise()
```

3\. **Guest Edit Profile / Edit logged In profile:**

1. a) Remove BMGS hardcoded and use category1 for board, category2 for medium and category3 for grade in HTML and TS file.

b. we have to use proper methods and variables name for board, medium and grade(onMediumChange, mediumControl, mediumList )&#x20;

c. Update framework API’s request with category\[i].

`DEFAULT_FRAMEWORK_CATEGORIES` should be category1, category2, category3 and category4

```
const getSuggestedFrameworksRequest: GetSuggestedFrameworksRequest = {
      from: CachedItemRequestSourceFrom.SERVER,
      language: this.translate.currentLang,
      requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
    };

    this.frameworkUtilService.getActiveChannelSuggestedFrameworkList(getSuggestedFrameworksRequest).toPromise()
```

```
 this.framework = await this.frameworkService.getFrameworkDetails({
            from: CachedItemRequestSourceFrom.SERVER,
            frameworkId: value[0],
            requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
          }).toPromise();
```

Update `boardCategoryTermsRequet` as category1TermsRequest, category2TermsRequest for medium . category3TermsRequest for grade

```
this.frameworkUtilService.getFrameworkCategoryTerms(boardCategoryTermsRequet).toPromise()
```

4\. **Logged In Profile :** a) Remove BMGS hardcoded and use category1 for board, category2 for medium, category3 for grade and category4 for subject TS file.

`DEFAULT_FRAMEWORK_CATEGORIES` should be category1, category2, category3 and category4

```
const frameworkDetailsRequest: FrameworkDetailsRequest = {
      frameworkId: id,
      requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
    };
    await this.frameworkService.getFrameworkDetails(frameworkDetailsRequest).toPromise()
```

5.**Help Section (faq-report-issue.page.ts) :**

a) Remove BMGS hardcoded and use category1 for board, category2 for medium, category3 for grade and category4 for subject in HTML and TS file

b. Update framework API’s request with category\[i].

`DEFAULT_FRAMEWORK_CATEGORIES` should be category1, category2, category3 and category4

```
const getSuggestedFrameworksRequest: GetSuggestedFrameworksRequest = {
      from: CachedItemRequestSourceFrom.SERVER,
      language: this.translate.currentLang,
      requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
    };

    this.frameworkUtilService.getActiveChannelSuggestedFrameworkList(getSuggestedFrameworksRequest).toPromise()
```

**6. relevent-content.page.ts:**

a) Remove BMGS hardcoded and use category1 for board, category2 for medium, category3 for grade and category4 for subject TS file

b. Update framework API’s request with category\[i].

`DEFAULT_FRAMEWORK_CATEGORIES` should be category1, category2, category3 and category4

```
const getSuggestedFrameworksRequest: GetSuggestedFrameworksRequest = {
      from: CachedItemRequestSourceFrom.CACHE,
      language: this.translate.currentLang,
      requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
    };

    try {
      const list = await this.frameworkUtilService.getActiveChannelSuggestedFrameworkList(getSuggestedFrameworksRequest).toPromise();
```

**7.search :**

a) Remove BMGS hardcoded and use category1 for board, category2 for medium, category3 for grade and category4 for subject TS file

b. Update framework API’s request with category\[i].

`DEFAULT_FRAMEWORK_CATEGORIES` should be category1, category2, category3 and category4.

```
const getSuggestedFrameworksRequest: GetSuggestedFrameworksRequest = {
        language: this.translate.currentLang,
        requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
      };
      // Auto update the profile if that board/framework is listed in custodian framework list.
      this.frameworkUtilService.getActiveChannelSuggestedFrameworkList(getSuggestedFrameworksRequest).toPromise()
```

**8. Update User Profile (update-profile.service.ts):**

a) Remove BMGS hardcoded and use category1 for board, category2 for medium, category3 for grade and category4 for subject TS file

b. Update framework API’s request with category\[i].

`DEFAULT_FRAMEWORK_CATEGORIES` should be category1, category2, category3 and category4.

```
const getSuggestedFrameworksRequest: GetSuggestedFrameworksRequest = {
                language: this.translate.currentLang,
                requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
            };
            // Auto update the profile if that board/framework is listed in custodian framework list.
            this.frameworkUtilService.getActiveChannelSuggestedFrameworkList(getSuggestedFrameworksRequest).toPromise()
```

`DEFAULT_FRAMEWORK_CATEGORIES` should be category1, category2, category3 and category4.

```
const frameworkDetailsRequest: FrameworkDetailsRequest = {
                                frameworkId: element.identifier,
                                requiredCategories: FrameworkCategoryCodesGroup.DEFAULT_FRAMEWORK_CATEGORIES
                            };
                            this.frameworkService.getFrameworkDetails(frameworkDetailsRequest).toPromise()
```
