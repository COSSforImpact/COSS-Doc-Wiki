---
icon: elementor
---

# Search Filter

### Background: <a href="#searchfilter-background" id="searchfilter-background"></a>

BMGS are the request of search filter for searching, filtering and sorting the response data. Now remove the BMGS keys and use category1, category2, category3 and category4.

Jira ticket: [![](https://project-sunbird.atlassian.net/rest/api/2/universal\_avatar/view/type/issuetype/avatar/10316?size=medium)ED-1960](https://project-sunbird.atlassian.net/browse/ED-1960) - Remove BMGS hardcoded from framework selection page(Unit test) Closed

### **Problem Statement :** <a href="#searchfilter-problemstatement" id="searchfilter-problemstatement"></a>

1. How many filter properties should display for multiple frameworks?
2. If user select only board and category1 from other framework then should display all contents or what?

### **Key Design Problem:** <a href="#searchfilter-keydesignproblem" id="searchfilter-keydesignproblem"></a>

1.

**Search API’s:** Search Api’s is using BMGS as Api’s request for searching, filtering and sorting. so removed BMGS and use category1 for board, category2 for medium, category3 for gradeLevel and category4 for subject.

```
export interface ContentRequest {
    uid?: string | string[];
    primaryCategories: string[];
    audience?: string[];
    pragma?: string[];
    exclPragma?: string[];
    attachFeedback?: boolean;
    attachContentAccess?: boolean;
    attachContentMarker?: boolean;
    sortCriteria?: ContentSortCriteria[];
    recentlyViewed?: boolean;
    localOnly?: boolean;
    resourcesOnly?: boolean;
    limit?: number;
    board?: string[];
    medium?: string[];
    grade?: string[];
    dialcodes?: string[];
    childNodes?: string[];
```

convert BMGS to category\[i] for content aggregator.

```
this.contentService.getContents({
                        primaryCategories:
                            (searchCriteria.primaryCategories && searchCriteria.primaryCategories.length
                                && searchCriteria.primaryCategories) ||
                            (searchRequest.filters && searchRequest.filters.primaryCategory) ||
                            [],
                        board: searchCriteria.board,
                        medium: searchCriteria.medium,
                        grade: searchCriteria.grade
```

Remove BMGS from **get content handler** and **search content handler in SDK.**

Change BMGS to category1-4 for content properties in **client service.**

Update the below request BMGS to category1…category4 in mobile and we have to change the request as category1….category4 for search filter and help section in mobile.

```
userPreferences: {
                    board: this.profile.board,
                    medium: this.profile.medium,
                    gradeLevel: this.profile.grade,
                    subject: this.profile.subject,
                  }
```
