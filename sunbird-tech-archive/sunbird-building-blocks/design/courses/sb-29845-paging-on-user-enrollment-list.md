---
icon: elementor
---

# SB-29845: Paging on User Enrollment List

### **Overview:** <a href="#sb-29845-pagingonuserenrollmentlist-overview" id="sb-29845-pagingonuserenrollmentlist-overview"></a>

Currently, user enrollment list API returns a list of fixed size 1000. We are not able to get enrollments records with user enrollments when greater than 1000 . We will need to introduce paging mechanism.

**Pr-requisites:**

1. User is a logged in user and has enrolled into at-least one traceable collection

**Linked Issues:**

[https://project-diksha.atlassian.net/browse/DIK-6248](https://project-diksha.atlassian.net/browse/DIK-6248)

[SB-28497](https://project-sunbird.atlassian.net/browse/SB-28497?src=confmacro)

### **Solutions:** <a href="#sb-29845-pagingonuserenrollmentlist-solutions" id="sb-29845-pagingonuserenrollmentlist-solutions"></a>

1. Paging mechanism in the user enrollment list API .

2\. Batch calls for course composite search API with limit of 1000.

### **Option 1: Paging mechanism in the user enrollment list API.** <a href="#sb-29845-pagingonuserenrollmentlist-option1-pagingmechanismintheuserenrollmentlistapi" id="sb-29845-pagingonuserenrollmentlist-option1-pagingmechanismintheuserenrollmentlistapi"></a>

**Details:**

Introducing paging for user enrollment list API.

Add 2 parameters as offset and limit. Offset is the page state Limit is the number of records

```
request.getContext.get("pageIndex").asInstanceOf[String])
request.getContext.get("size").asInstanceOf[Integer])
```

Steps to follow:

```
New implementation in CassandraOperation as
  
  Response getRecordByIdentifier(RequestContext requestContext, String keyspaceName,
   String tableName, Object key, List<String> fields,
   int size, String pageIndex);
   
   1. Select query has to be modified with limit
        selectStatement.setFetchSize(size);
  
   2. Select query modification with offset
        if (!pageIndex.equals("0")) {
              selectStatement.setPagingState(PagingState.fromString(pageIndex));
          }
   
```

**Pros**:

* Better performance in API due to pagination

**Cons**:

* Portal and back-end implementation required

### **Option 2: Batch calls for course composite search API with limit of 1000.** <a href="#sb-29845-pagingonuserenrollmentlist-option2-batchcallsforcoursecompositesearchapiwithlimitof1000" id="sb-29845-pagingonuserenrollmentlist-option2-batchcallsforcoursecompositesearchapiwithlimitof1000"></a>

**Details:**

**Pros**:

**Cons**:
