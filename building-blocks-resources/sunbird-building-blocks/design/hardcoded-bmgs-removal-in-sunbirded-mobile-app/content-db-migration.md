---
icon: elementor
---

# Content DB Migration

### Background: <a href="#contentdbmigration-background" id="contentdbmigration-background"></a>

### **Problem Statement :** <a href="#contentdbmigration-problemstatement" id="contentdbmigration-problemstatement"></a>

For existing users, already content DB is created so, categories filed will not be there and we are using content.category1 so, it will throw undefined error

### **Key Design Problem:** <a href="#contentdbmigration-keydesignproblem" id="contentdbmigration-keydesignproblem"></a>

Update content DB keys BMGS to category1, category2, category3 and category4. The new DB will be created for new user with category1,….category4 but for existing user we have to write a migrate code for DB update with category\[i]

```
export interface Content {
    .....
    subject: string | string[];
    board: string;
    medium: string | string[];
    gradeLevel: string[],
    ......
}
```

```
export interface Content {
    category1: string | string[];
    category2: string | string[];
    category3: string | string[],
    category4: string | string[];
    ..........
}
```
