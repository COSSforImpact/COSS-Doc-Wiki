---
icon: elementor
---

# Offline course progress tracking

Track course progress when the user is offline and sync up with the server when internet is available.

**Current Implementation -**

* The current implementation is completely online, where the content is consumed completely in a course after the content is closed and returned to the Content Details page, handlePageResume() → updateContentProgress() is called, which updates the content state to the server using **updateContentState** api of **courseService**.
* On the success case of **updateContentState** api, a broadcast **COURSE\_STATUS\_UPDATED\_SUCCESSFULLY** is fired, which is subscribed in the **courses** page and this will initiate the call to **getEnrolledCourses(true)** to fetch all the courses from the server, which contains the progress of the course.

**Offline course progress tracking -**

* When the content is consumed completely in a course, after the content is closed and returned to Content Details page

1. onResume of ContentDetails handlePageResume() → updateContentProgress() is called, which updates the content state to the server using **updateContentState** api of **courseService**.
2. But, when offline, in the error case of the above api, we need to store the details in **NoSql** table with all the details required to update it later when the internet is available like **\[contentId, batchId, userId, status, progress]** which are the parameters required by **updateContentState** api.
3. Both in case of success or error of the **updateContentState** api, a broadcast **COURSE\_STATUS\_UPDATED\_SUCCESSFULLY** is fired, which is subscribed in the **courses** page and this will initiate the call to **getEnrolledCourses(true)** to fetch all the courses from the server.
4. But, since the user is in the offline state, **getEnrolledCourses** should check if there are any progress details of a course is available in the NoSql table, then those have to be fetched and checked against each **courseId** from getEnrolledCourses and progress needs to be updated and returned as the response.
5. And when the internet is available, there are two ways the progress of the content of a course can be updated to server
   1. Listen to the network state and when the network is available, check if the progress details are available in the NoSql table, then update them by calling **updateContentState** api of **courseService** and erase all the data from the NoSql table‌**.**
   2. Before calling **getEnrolledCourses()** every time, check if the progress details are available in the NoSql table, then update them by calling **updateContentState** api of **courseService** and then make a call to getEnrolledCourses, \[Caveat - There can be a delay when updating the status of the content and immediately getting the progress of it] and erase all the data from the NoSql table‌**.**

**Comments after design discussion -**

1. Do not rely on the user to come back on the Content Details page after consuming the content, use the END\_EVENT for an alternative to this, to make an API call or storing it to DB locally.
2. Check the timestamp of the getEnrolledCourses fetch time and the timestamp of the content state that is updated locally in the DB, if the local DB content update timestamp is greater than getEnrolledCourses then we need to merge the progress from the getEnrolledCourses and the local DB and give the updated details in the getEnrolledCourses, only during offline state
3. When making a call to getEnrolledCourses during the online state, check if the content update NoSQL table has some data and if it has, then update the content state to server and then do getEnrolledCourses API
   1. IMPORTANT - updateContentState should have bulk update, otherwise user will have the experience problem, as we will want to hit the number of APIs as many as updateContentState
4. We need to check if there is a delay when updating the status of the content and immediately getting the progress of it in getEnrolledCourses

**Scenarios -**

* When the user is offline and is going through course, and the user finishes the content of a course, now the course progress has to be updated on the progress bar on the courses page as well as the course detail page.
* When the user comes online after consuming the course and making some progress, the same has to be updated to the server and the same updated progress has to be got back in the getEnrolledCourses API.
