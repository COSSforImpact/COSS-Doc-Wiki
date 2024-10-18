# Access User private data in masked form in search based on roles

**Problem Statement**

Currently when a user is searched, only the basic data is being returned, User's private data is restricted to user only. However User with certain role would like to access user's private data in masked form when searching for other user.

\


**Solution Approach**

Based on user token, we can fetch user's role who is making a search call. User's role is matched against set of roles stored in properties to allow to extract private data.

In case the role allows, It needs to collect all the userIds in search result and make a second call to ES (type userprofilevisibility) to fetch user's private data and merge it with respective search result.

\


**Changes**

fetch role of the user who is searching

get all the user ids of search result

if user falls in allowed to fetch private data, make additional call to fetch user masked data and merge it with original search result.

\


\
