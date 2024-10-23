---
icon: elementor
---

# API throttling

#### Problem statement <a href="#apithrottling-problemstatement" id="apithrottling-problemstatement"></a>

To enhance the better use of resources, the system needs API based throttling for self signup where the signup calls can be restricted based on phone number and throttling needs to be time based which translates to something like for a particular phone number the system should allow only 5 calls in an hour and 30 calls in 24 hour duration.

#### Solution approaches <a href="#apithrottling-solutionapproaches" id="apithrottling-solutionapproaches"></a>

**Points to consider while providing solutions**

1. The throttling should have configurable property and it should be pluggable
2. The throttling solution should be usable for other apis with similar requirement
3. The throttling should be applicable for different targets like phone/email, userId, auth token etc.
4. The throttling cost should be minimal

**approach 1 :**&#x20;

Considering KongHQ as solution for throttling.

Kong works as gateway and provides enhance features and plugin. Kong does provides rate limiting plugin

[Advanced Rate Limit](https://docs.konghq.com/hub/kong-inc/rate-limiting-advanced/) (in enterprise edition)

[Rate Limiting](https://docs.konghq.com/hub/kong-inc/rate-limiting/) (in community edition)

However these rate limits targets consumer, credential and ip only. It does not provide the request payload based limit

**Limitation**

It does not allow rate limiting on the request payload based.

**approach 2 :**&#x20;

Considering nginx rate limiting

nginx rate limiting can be mapped to per request, the basic flow&#x20;

define a rate limiting zone which defines the name of the zone, the target entity and&#x20;

```
limit_req_zone $request zone=one:10m rate=2r/m;
```

above can be read as **create a rate limit zone on **_**target**_** request with **_**name**_** zone and 10mb **_**memory**_**, assign the zone a **_**rate**_** of 2 request per minute**.

this rate limit can be applied on any request proxy as&#x20;

```
location /user/create {
  proxy_pass ;
  limit_req zone=one;
}
```

If there would be more than 2 request in a single minute , It throws _503 Service Temporarily Unavailable_ error

**How it works**

It would be important to understand how nginx rate limiting works, in the given example if we want to limit as 2 request per minute, it divides the time in equal part, which means it will provide 30 second to per request. In other words after accepting a request call it would wait for 30 seconds to accept another one. If in case 2 consecutive calls are received, the second one will be rejected even though that's the only 2 calls in a minute.

**Limitation**

1. &#x20;It works in time division matter, which makes it difficult for scenario like allowing only 5 calls per minute would mean the successive calls should have a difference of 12 seconds or more.
2. It allows only minute(m) or seconds(s) in the rate, which means 60r/h is invalid.
3. It doesn't allow quantitative timing in rates , which means 60r/5m is invalid.
4. for some reason in target $request\_body does not work for payload based throttling however $body\_bytes\_sent does work.

**approach 3:**

This one requires a custom approach to build an application based throttling. This approach would take existing cassandra DB for the backbone of throttling. In this approach we will define a table as below

CREATE TABLE calls\
(

caller TEXT,\
api TEXT,\
time timestamp,\
PRIMARY KEY (caller,api,time)

)

caller -  A caller can be an identifier of multiple type phoneNo, userId, auth token etc.

api - an api is the unique relative url ex. /user/v1/create

time -  it holds on the exact timestamp for the call of api, in CQL NOW() provides the guarantee of a unique timestamp everytime it is invoked, which assures concurrent calls does not update the same entry.

Next we define a function to help in querying this table (it provides the timestamp of unit minutes before)

```
CREATE FUNCTION IF NOT EXISTS toTimestampLast(minutes int) 
 CALLED ON NULL INPUT 
 RETURNS timestamp
  LANGUAGE java AS '
  long now = System.currentTimeMillis();
  if (minutes == null)
    return new Date(now);
  return new Date(now - (minutes.intValue() * 60 * 1000));
';

This function can be used in query as below
```

SELECT caller, api, count(time) as call\_count FROM calls WHERE caller='9111111114' and api='/user/v1/create' and time>=toTimestampLast(1) GROUP BY caller, api; **--last 1 minute**

SELECT caller, api, count(time) as call\_count FROM calls WHERE caller='9111111114' and api='/user/v1/create' and time>=toTimestampLast(60) GROUP BY caller, api; **--last 60 minute**

```

In a nutshell before processing a registered api call, we will query the DB to get the count based on the rule (as only 20 calls in an hour)

We can use system_settings to hold the rule with api rules of throttling with value as

{
 api : {
  "/user/v1/create" : [{
                    caller : "phone",
                    request-count : 20,
                    time : 60
                   },{
                    caller : "phone"
                    request-count : 100,
                    time : 1440
            }]
       }
}
```

These rules can be fetched from memory and can be applied on the request before it is being sent to further processed. in case if any calls violate any of the rule an error "REQUEST\_LIMIT\_REACHED" can be thrown. otherwise an entry is made in the calls table.

\


**Comparison of different approaches**

\


| <p><br></p>                              | Approach 1 (Kong)                                    | Approach 2 (nginx)                                                                     | Approach 3 (Custom)                                 | Remarks     |
| ---------------------------------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------------- | --------------------------------------------------- | ----------- |
| Configurable                             | ![(tick)](../../../../../.gitbook/assets/check.png)  | <img src="../../../../../.gitbook/assets/check.png" alt="(tick)" data-size="original"> | ![(tick)](../../../../../.gitbook/assets/check.png) | <p><br></p> |
| Pluggable                                | ![(tick)](../../../../../.gitbook/assets/check.png)  | ![(tick)](../../../../../.gitbook/assets/check.png)                                    | ![(tick)](../../../../../.gitbook/assets/check.png) | <p><br></p> |
| can be applied for custom time arguments | ![(tick)](../../../../../.gitbook/assets/check.png)  | ![(error)](../../../../../.gitbook/assets/error.png)                                   | ![(tick)](../../../../../.gitbook/assets/check.png) | <p><br></p> |
| can be used for payload (phone)          | ![(error)](../../../../../.gitbook/assets/error.png) | ![(tick)](../../../../../.gitbook/assets/check.png)                                    | ![(tick)](../../../../../.gitbook/assets/check.png) | <p><br></p> |
| can error message be configured          | ![(error)](../../../../../.gitbook/assets/error.png) | ![(error)](../../../../../.gitbook/assets/error.png)                                   | ![(tick)](../../../../../.gitbook/assets/check.png) | <p><br></p> |
| coding effort                            | none                                                 | none                                                                                   | medium to high                                      | <p><br></p> |
| can use DB                               | ![(tick)](../../../../../.gitbook/assets/check.png)  | ![(error)](../../../../../.gitbook/assets/error.png)                                   | ![(tick)](../../../../../.gitbook/assets/check.png) | <p><br></p> |
| performance cost                         | low                                                  | low                                                                                    | high                                                | <p><br></p> |
| <p><br></p>                              | <p><br></p>                                          | <p><br></p>                                                                            | <p><br></p>                                         | <p><br></p> |

\


\


\


\


\


\


\


\
